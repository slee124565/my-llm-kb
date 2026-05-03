# Human-Supervised Agent Ops

## Summary

Human-supervised agent ops 指的是：agent 擁有 operational loop，人類轉為 supervisor、policy owner、exception reviewer 與 taste calibrator 的 AI-native application pattern。

這和 `AI-enhanced human ops` 不同。AI-enhanced human ops 是人類仍然看狀態、判斷下一步、操作工具、檢查結果，只是 AI 幫忙摘要、搜尋、建議或加速。Human-supervised agent ops 則是 agent 觀測狀態、建立 job、查 KB、做決策、執行低風險 action、驗證結果、記錄 evidence，並在不確定時升級給人。

## Why It Matters

AI-native 應用的核心不只是「有 AI 功能」，而是 operational loop 的擁有者是否從人類轉移到 agent。若這一點沒有明確改寫，產品很容易退化成「AI-enhanced human ops」：看起來有 AI，實際上仍然是人類在逐步操作，只是旁邊多了一個建議器。

更強的 framing 是：

> AI-native application is not software with AI assistance; it is software whose operational loop is owned by agents and governed by humans.

## Current Framing

- 核心判準不是 AI 功能多少，而是誰擁有 operational loop
- 如果主要 UI 是給人類連續操作的，它大概率只是 AI-enhanced；如果主要 runtime 是給 agent 連續操作的，而 human UI 是 supervision surface，才開始接近 AI-native
- human role 會從 operator 轉成 policy owner、risk boundary designer、exception reviewer、evidence auditor、KB maintainer 與 rollout governor
- agent role 會從 assistant 轉成 operator：觀測、判斷、執行、驗證、記錄、升級
- AI-native 產品真正重要的 artifacts 會變成 state machine、policy gate、action API、KB / memory、confidence model、escalation protocol、audit log、eval / replay、rollback / freeze、supervisor console
- 對客服、ops、coding、data maintenance 這類 workflow 來說，產品設計問題應該從「如何把 AI 放進 UI」改成「哪些 loop 可以交給 agent 關閉，哪些 loop 必須保留 human approval，哪些 evidence 足以支撐下一層授權」
- long-running harness 的價值測試也應改寫：不是 agent trace 有多長，而是 agent 是否能在可審計、可恢復、可回滾的邊界內擁有更多 operational loop
- Slack、issue tracker、admin console 這類 human-facing surface，在 AI-native ops 中通常應被設計成 supervisor plane，而不是 primary operator UI
- 與 coding agent 共同開發 human-supervised agent ops 系統時，開發流程本身也需要 supervisor discipline：每個 milestone 要問 agent 多擁有哪一小段 loop、需要哪些 evidence、哪個 gate 沒過就停，而不是讓 `PLANS.md` 無限延伸成 design/implement loop
- Karpathy 對 future agents 的 human-to-agent ratio framing，補強了這個概念的需求來源：更長的 autonomous run 會把人推向 supervisor role，但 supervision 必須靠 evidence、approval、rollback 與 risk boundary 實作，而不是只靠人「看著」agent

## Working Thesis

一個應用若只是讓人類更快操作既有流程，仍然屬於 AI-enhanced human ops。AI-native 應用應該把業務流程重新塑造成 agent-legible、agent-actionable、human-auditable 的 runtime。

這意味著產品與工程的主要工作會上移：

- 人類不再逐步執行每個 case，而是定義允許 agent 關閉哪些 loop
- policy 不再只寫在人類 SOP 裡，而要落成可執行 gate
- knowledge 不再只是人查的 FAQ，而要成為 agent 可檢索、可引用、可回寫的 memory
- review 不再是人手逐條看所有輸出，而是抽查、例外審核、品質校準與 rollback
- UI 不再是所有操作的主入口，而是 evidence、approval、override、handoff 與 observability surface

## Example: Shopee Customer Service Harness

Shopee 客服 harness 的設計錯位可以這樣分辨：

- 人類客服工作台：human ops
- AI 推薦回覆：AI-enhanced human ops
- agent 自己追蹤問題、查 KB、決定是否低風險自動回覆、低信心才問 Slack：human-supervised agent ops

在第三種設計裡，Shopee webchat browser 是 agent 的 hands，repo KB / policy / queue / canary ledger 是 memory 與 control layer，Slack `/shopee-cs` 是 supervisor plane。人類不逐筆操作 webchat，而是在低信心、高風險、source gap、browser uncertainty 或 rollout decision 時介入。

## Development Practice: Avoiding PLANS Loop Drift

這個概念不只描述產品 runtime，也描述與 coding agent 共同開發 AI-native 系統時的工作法。

案例：`/Users/lee/ws/wsFLH/flh-shopeecs-agent-harness` 從 M0 到 M33 建立了 contracts、queue/state machine、KB、Slack supervisor plane、guarded Shopee sender、canary ledger、LLM draft gate、duty loop、scheduler、overnight readiness 與 unread-safe tracking。這些 milestones 大多遵守了「先 evidence，再擴權」的節奏；但累積到 M34 前後，`PLANS.md` 也開始有退化成設計/實作循環的風險：每次討論都可能再新增一個 plan section，而不是關閉一段 operational loop。

避免開發迷航的核心方法是：不要再問「下一個 milestone 要怎麼設計」，而要問：

> 下一個 slice 要讓 agent 多擁有哪一小段 operational loop？需要哪些 evidence 才能授權？如果 evidence 不足，停在哪個 supervisor gate？

固定節奏：

1. `Outcome first`
   每個 milestone 只能有一個主要 outcome，例如「hosted agent 能處理一筆低信心 case 到 Slack review」或「operator edit 後只送 approved answer」。
2. `Authority delta`
   先寫清楚本 slice 是否擴大 agent 權限。若沒有擴權，只能是 reliability、evidence 或 UX slice；若有擴權，必須同時有新增 gate、rollback、duplicate-send proof。
3. `One-plane rule`
   一次只改一個主要平面：KB quality、Slack supervisor、browser hands、scheduler reliability、policy gate、LLM draft 或 live-send rollout。不要同時改 prompt、DOM sender、KB schema 與 Slack command。
4. `Proof before next milestone`
   每個 slice 結尾必須有 proof command、job/event evidence、Slack 或 browser proof、fail-closed case。沒有 proof，不開下一個 milestone。
5. `Plan closure rule`
   一次 planning 最後必須落到「本輪要改哪些檔、跑哪些測試、什麼情況算 blocked」。如果結尾只是「下一步再設計」，就沒有完成。
6. `Kill design-only milestones`
   新 milestone 必須交付 runtime capability、verification bundle、operator workflow，或明確刪除/收斂舊風險。純整理想法應留在 docs section，不應升級成新的 milestone。

把 GPT-5.5 outcome-first prompt checklist 套到這個開發案例：

1. 這個 agent 最後要交付什麼？
   一個 hosted Shopee CS agent-operator runtime：agent 觀測 unread-safe tracking、建立 job、查 reviewed KB、產生 answer proposal、套 policy、在需要時升級 Slack，並在 approved gate 後透過 guarded browser sender 執行與記錄 evidence。
2. 什麼條件下算成功？
   最小成功不是全自動客服，而是 hosted preflight 可檢查 DB、Slack、KB、Chrome/CDP、read-state boundary、freeze/cap/duplicate-send；低信心 case 可進 `waiting_review`；operator edit 後只送 approved answer；高信心低風險 approved-source case 也必須通過 explicit rollout/live-send gates。
3. 哪些限制不可違反？
   不把 dry-run scheduler reliability 當成 live-send 授權；不讓 Slack 變成任意 executor；不讓 low confidence、source gap、high risk、context drift 或 browser uncertainty 自動送出；不提交 secrets、runtime DB、Chrome profile 或 raw browser evidence。
4. 哪些資訊或證據是必要的？
   tracking artifact checksum、read-state classification、job event chain、KB source trace、review status、confidence reason、risk labels、policy decision、Slack supervisor action refs、browser preview/send proof、KB writeback path、failure taxonomy 與 next safe command。
5. 什麼情況應該停止、標記 blocked 或問問題？
   缺 approved source、source conflict、Chrome/CDP 不可用、selector/context drift、read-state boundary 不安全、freeze/cap/duplicate-send gate 擋住、Slack review 無法 audit，或 coding agent 找不到最小有效驗證。
6. 最終輸出要讓人或系統如何接續使用？
   人應能在 Slack 上看到 evidence packet 與 safe commands；下一個 agent 應能從 repo artifacts 接手，跑 preflight、bounded iteration、status/evidence command、tests，並知道哪些 gate 沒過。

## Signals From Recent Articles

- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [Deep Dive into LLMs like ChatGPT](../articles/deep-dive-into-llms-like-chatgpt.md)
- [OpenAI Symphony Codex Orchestration](../articles/openai-symphony-codex-orchestration.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [Harness Design for Long-Running Application Development](../articles/harness-design-for-long-running-application-development.md)
- [Introducing Codex](../articles/introducing-codex.md)

## Open Questions

- 哪些 business workflows 真的適合把 operational loop 交給 agent，哪些仍應保持 human-operated
- confidence、risk、source lineage 與 action reversibility 應如何共同決定 agent 授權層級
- supervisor plane 的最小可用 evidence packet 應包含哪些欄位
- AI-native application 的 product analytics 應如何衡量 agent loop closure，而不只是回覆速度或自動化比例
- 當 agent 擁有 operational loop 時，policy、KB、eval、rollback 與 audit 應如何分層，才不會讓 human supervisor 失去真實控制
- human supervisor 與 coding agent 共同推進 AI-native 系統時，哪些 planning artifacts 應成為 durable operating contract，哪些只是暫時探索，應避免升級成新的 milestone

## Related Pages

- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Externalized Agent State](externalized-agent-state.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [Prompt Migration And Agent Steerability](prompt-migration-and-agent-steerability.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
- [Codex Workflows](../maps/codex-workflows.md)
