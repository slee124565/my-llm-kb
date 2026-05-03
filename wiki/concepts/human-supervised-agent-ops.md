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

## Signals From Recent Articles

- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
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

## Related Pages

- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Externalized Agent State](externalized-agent-state.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [Prompt Migration And Agent Steerability](prompt-migration-and-agent-steerability.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
- [Codex Workflows](../maps/codex-workflows.md)
