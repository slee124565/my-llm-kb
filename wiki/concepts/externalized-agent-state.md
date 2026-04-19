# Externalized Agent State

## Summary

Externalized agent state 指的是：把 agent 執行所需的關鍵狀態從單次對話中抽離，落在 repo 或其他持久層 artifact 中，讓後續 session 或其他 agent 可以正確接手。

## Why It Matters

長任務失敗常不是因為模型不夠聰明，而是因為任務狀態只存在於 context window 或操作者腦中。沒有外部化狀態，任務一旦跨 session，就容易重複摸索、遺漏驗證，甚至把錯誤延續下去。

## Current Framing

- progress file 讓後續 session 能快速定向
- feature list / task list 提供可驗證的未完成工作視圖
- skill、workflow docs、templates 把 procedure 外部化
- Karpathy 對 `weights = vague recollection`、`context window = working memory` 的 framing，說明了為什麼 repo artifact 有價值：它讓 agent 能把正確狀態重新載入 working memory，而不是只靠模型參數中的模糊回憶
- raw/article/concept/map 四層結構把知識與操作記憶穩定放在 repo 中
- 維護中的 `docs/` 與 `AGENTS` 規則，也是一種可被 agent 回讀的長期狀態表面
- `PLANS.md` 這類 self-contained execution document，則把長任務的目標、決策、驗證與進度整合成可接手 artifact
- 完整的 execution plan 不只保存目標與進度，還應把 repository context、interfaces、dependencies、idempotence 與 recovery 條件一起外部化
- sprint contracts、planner-generated specs、evaluator feedback files 這類中介 artifact，也能承接跨代理 handoff 所需的局部狀態
- personal agent 的 local markdown memory、hosted agent 的 session log、repo-local docs / plans，都是 externalized state，但它們分屬不同 runtime surface，治理責任也不同
- 把 context storage 與 context management 分開，是 externalized state 的治理原則：先確保歷史不丟，再讓摘要、裁剪與檢索策略隨模型演化調整
- memory ownership 與 runtime surface 的差異，應與 state externalization 分開理解；前者決定誰持有與管理狀態，後者決定狀態是否脫離單次對話存在
- living document 的修訂紀律本身也是 state contract 的一部分；若 plan 更新時沒有同步回寫 progress、decision log 與 retrospective，externalized state 很快就會腐化
- raw reasoning / analysis messages 是一種外部化狀態：它們必須能跨 turn 被保留與重新載入，但不應直接暴露成 user-facing content
- harmony format 裡的 `analysis` / `commentary` / `final` 分工，說明外部化狀態不只是「存下來」，還包含如何在下一輪正確放回 context
- gpt-oss 的 reasoning fields 與 reasoning-text events，提供了把內部 trace 以結構化方式外部化的例子
- 當 AI 對話需要成為後續可重用的工作 artifact 時，匯出成 markdown、PDF 或 repo file 就不只是備份，而是把 state 從聊天 UI 外部化
- policy taxonomy、decision label 與 output schema 也是外部化狀態；若它們只留在 prompt 裡而沒有版本化，就很難做後續審計或回放

## Signals From Recent Articles

- [Effective Harnesses for Long-Running Agents](../articles/effective-harnesses-for-long-running-agents.md)
- [Shell + Skills + Compaction](../articles/shell-skills-compaction-long-running-agents.md)
- [LLM Knowledge Bases](../articles/karpathy-llm-knowledge-bases.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [Introducing Codex](../articles/introducing-codex.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [Harness Design for Long-Running Application Development](../articles/harness-design-for-long-running-application-development.md)
- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [Deep Dive into LLMs like ChatGPT](../articles/deep-dive-into-llms-like-chatgpt.md)
- [Notes From a Marketer Building a Real CLI With Codex](../articles/notes-from-a-marketer-building-a-real-cli-with-codex.md)
- [How to handle the raw chain of thought in gpt-oss](../articles/handle-raw-cot.md)
- [Verifying gpt-oss implementations](../articles/verifying-implementations.md)
- [User Guide For Gpt-Oss-Safeguard](../articles/gpt-oss-safeguard-guide.md)

## Open Questions

- 哪些 state 必須 machine-readable，哪些只要 human-readable 即可
- compaction 與 explicit artifact handoff 的責任邊界如何切分
- artifact 變多之後如何防止 state 腐化與過期
- `docs/` 與 progress artifact 在不同任務型別下應如何分工
- execution plan 與 lightweight task contract 的切換門檻應如何判斷
- planner / evaluator 之間交換的中介文件，應如何設計才不會快速陳舊
- hosted session logs、repo-local docs 與 user-owned memory 之間，應如何協同，而不是互相取代
- 對探索型任務而言，prototype artifact 應併入單一 plan，還是拆成獨立 spike / validation doc
- raw reasoning 應以什麼粒度保存，才能同時支援 tool calling、debug 與 user privacy
- reasoning summary、raw reasoning 與 persisted turn history 的責任邊界應如何切分
- 當 conversation 本身成為工作 artifact 時，export format 應如何和後續檢索、重用、審計對齊
- policy prompt 的版本化與 replayable evidence 應如何保存

## Related Pages

- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Agent Knowledge Compilation](agent-knowledge-compilation.md)
- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [Long-Running Agents](../maps/long-running-agents.md)
