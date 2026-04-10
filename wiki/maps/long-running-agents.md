# Long-Running Agents

## Scope

這個 map 聚焦於跨 session、跨 context window 的長任務 agent 系統設計。

## Entry Points

- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)

## Core Concepts

- progress artifacts
- task contracts
- compaction and continuity
- verification loops

## Key Articles

- [Shell + Skills + Compaction](../articles/shell-skills-compaction-long-running-agents.md)
- [Effective Harnesses for Long-Running Agents](../articles/effective-harnesses-for-long-running-agents.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [Harness Design for Long-Running Application Development](../articles/harness-design-for-long-running-application-development.md)
- [Claude Managed Agents](../articles/claude-managed-agents.md)

## Key People Or Labs

- OpenAI
- Anthropic
- Peter Steinberger
- Aaron Friel
- Ryan Lopopolo
- Prithvi Rajasekaran

## Open Threads

- artifact handoff 與 model-native memory 的邊界
- hosted runtime 與 local runtime 在 harness design 上的取捨
- 更好的模型是否能把「重型 harness」收斂成「文件 + 對話 + 少量規則」
- 長任務是否應統一採 plan-first，還是讓不同 repo 採不同 planning contract
- generator / evaluator 分離在什麼類型的任務上最划算
- provider-managed runtime 若成為主流，哪些 state artifact 仍必須由使用者自己持有
