# Long-Running Agents

## Scope

這個 map 聚焦於跨 session、跨 context window 的長任務 agent 系統設計。

## Entry Points

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)

## Core Concepts

- progress artifacts
- hosted vs local runtime surfaces
- task contracts
- compaction and continuity
- verification loops
- tracker-backed orchestration
- human supervisor plane
- human-to-agent ratio

## Key Articles

- [Deep Dive into LLMs like ChatGPT](../articles/deep-dive-into-llms-like-chatgpt.md)
- [Shell + Skills + Compaction](../articles/shell-skills-compaction-long-running-agents.md)
- [Effective Harnesses for Long-Running Agents](../articles/effective-harnesses-for-long-running-agents.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [OpenAI Symphony Codex Orchestration](../articles/openai-symphony-codex-orchestration.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [Harness Design for Long-Running Application Development](../articles/harness-design-for-long-running-application-development.md)
- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [Demis Hassabis: Agents, AGI & The Next Big Scientific Breakthrough](../articles/demis-hassabis-agents-agi-next-big-scientific-breakthrough.md)
- [A Postmortem of Three Recent Issues](../articles/a-postmortem-of-three-recent-issues.md)

## Key People Or Labs

- OpenAI
- Anthropic
- Andrej Karpathy
- Peter Steinberger
- Aaron Friel
- Ryan Lopopolo
- Prithvi Rajasekaran
- Demis Hassabis

## Open Threads

- artifact handoff 與 model-native memory 的邊界
- hosted runtime 與 local runtime 在 harness design 上的取捨
- provider-managed runtime 能吸收哪些 orchestration complexity，哪些 state 仍必須由使用者自己持有
- 更好的模型是否能把「重型 harness」收斂成「文件 + 對話 + 少量規則」
- 長任務是否應統一採 plan-first，還是讓不同 repo 採不同 planning contract
- issue tracker state、blocker graph 與 per-issue workspace 是否可以成為長任務 agent 的預設外部狀態骨架
- generator / evaluator 分離在什麼類型的任務上最划算
- provider-managed runtime 若成為主流，哪些 state artifact 仍必須由使用者自己持有
- provider-managed long-running agent 若因 serving bug 導致品質退化，production eval、user feedback 與 rollback loop 應算哪一層的 harness contract
- multi-agent swarms and long autonomous runs should be judged by output value per agent-hour, not only by trace length or autonomy level
- longer context windows do not by themselves solve long-running multimodal task memory; harnesses still need relevance selection, evidence, supervision, and recovery
- 哪些 operational loops 可以交給 agent 關閉，哪些必須保留 human supervisor approval，應成為 AI-native harness 的核心設計問題
