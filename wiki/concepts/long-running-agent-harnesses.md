# Long-Running Agent Harnesses

## Summary

Long-running agent harnesses 是讓 agent 能在多輪、多 session、長時間工作中持續推進的執行框架。它通常由任務 contract、artifact handoff、verification rules、execution environment 與 context continuity primitives 組成。

## Why It Matters

真正困難的不是讓 agent 完成單步操作，而是讓它跨時間維持方向、在失敗點停下修復、並把進度留給下一輪。沒有 harness，長任務通常會退化成高成本試錯。

## Current Framing

- incremental progress beats broad one-shot execution
- verification must be part of the loop, not a final afterthought
- initializer / planner / coding-session protocol 可以降低 session drift
- shell、skills、compaction 這類 primitive 是 harness 的底層能力，不是完整解法本身
- 對更成熟的模型而言，部分顯式 harness 步驟可能退化為較輕量的 conversation-first planning 與 doc-driven steering
- 對 Codex 類 workflow 而言，isolated sandboxes、verifiable evidence、async delegation 與 plan artifacts 是同一套 harness 的不同面向
- planner / generator / evaluator 的角色分離，是另一種可把主觀評估與功能驗證納入 loop 的 harness pattern
- context reset 與 compaction 應視為不同控制手段，而不是單純新舊替代
- 在 local personal-agent workflow 中，conversation-first UX 也可以是一種 harness 選擇：把 session、folder 與 model management 隱藏起來，換取更高 steerability
- CLI-first tooling 與 protocol-light integration，可能是另一種 harness 極簡主義，前提是本地 operability 比 protocol purity 更重要
- hosted agent platforms 把部分 harness complexity 產品化：使用者不再自己維運 sandbox、state recovery、credential routing，而是消費 provider-managed runtime primitives
- 對 hosted long-running agents 而言，brain / hands / memory 分離可同時支撐 lazy execution、故障隔離、credential isolation 與多 agent handoff
- 隨模型能力升級，某些 hand-tuned orchestration patch 會迅速失去必要性；由模型供應商維護的 harness，理論上能比每個客戶各自重寫更快跟上
- runtime surface 會改變 harness 責任分工：repo-local coding agent、provider-managed hosted agent、local personal agent，不會共享完全相同的 control surfaces
- 對 provider-managed runtime 而言，quality harness 不能只看離線 eval；routing correctness、cross-platform equivalence、production-side sensitive eval、rollback discipline 與 privacy-aware debugging tooling 都是 load-bearing parts
- 當多個小型 infra bug 疊加且症狀互相干擾時，community feedback 與 postmortem loop 也應被視為 harness 的一部分，而不是事後公關附屬品

## Signals From Recent Articles

- [Effective Harnesses for Long-Running Agents](../articles/effective-harnesses-for-long-running-agents.md)
- [Shell + Skills + Compaction](../articles/shell-skills-compaction-long-running-agents.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [Harness Design for Long-Running Application Development](../articles/harness-design-for-long-running-application-development.md)
- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [A Postmortem of Three Recent Issues](../articles/a-postmortem-of-three-recent-issues.md)

## Open Questions

- 最小可用 harness contract 是什麼
- reinforcement、compaction、subagent handoff 應如何組合
- coding 與 non-coding workload 是否應共用同一種 harness 骨架
- 隨模型能力提升，哪些 harness 元件可被簡化，哪些不能
- async remote execution 與 repo-local long session 各自應由哪些 control surfaces 承擔
- evaluator 在主觀品質任務中的 role，是否能穩定遷移到一般產品 QA
- hosted managed runtime 與 repo-local harness 之間，最小可攜 contract 應如何定義，才能降低平台綁定
- provider-managed runtime 要如何在不放寬隱私邊界的前提下，維持足夠敏感的 regression detection 與 root-cause debugging 能力

## Related Pages

- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Externalized Agent State](externalized-agent-state.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [Long-Running Agents](../maps/long-running-agents.md)
