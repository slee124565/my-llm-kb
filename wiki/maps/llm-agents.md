# LLM Agents

## Scope

這個 map 聚焦於 `LLM + agent` 主題中的高層入口，特別是 knowledge compilation、externalized state 與 long-running harness design。

## Entry Points

- [Agent Knowledge Compilation](../concepts/agent-knowledge-compilation.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)

## Core Concepts

- agent knowledge compilation
- externalized agent state
- long-running agent harnesses
- repository knowledge as system of record

## Key Articles

- [Deep Dive into LLMs like ChatGPT](../articles/deep-dive-into-llms-like-chatgpt.md)
- [LLM Knowledge Bases](../articles/karpathy-llm-knowledge-bases.md)
- [Shell + Skills + Compaction](../articles/shell-skills-compaction-long-running-agents.md)
- [Effective Harnesses for Long-Running Agents](../articles/effective-harnesses-for-long-running-agents.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [Introducing Codex](../articles/introducing-codex.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)

## Key People Or Labs

- Andrej Karpathy
- OpenAI
- Anthropic
- Peter Steinberger
- Aaron Friel
- Ryan Lopopolo

## Open Threads

- parameter memory、context window 與 externalized repo artifact 應如何分層，而不是互相取代
- 知識型 agent 與 coding agent 是否應共享同一套 state model
- compaction、progress artifact、skill contract 三者的最小組合是什麼
- 更強模型是否會讓 orchestration 複雜度下降，而不是上升
- repo-local knowledge base 與 remote async execution 應如何協同設計
- local personal agents 與 cloud coding agents 應共享哪些設計原則，又該在哪些地方刻意分流
- provider-managed agent infrastructure 會不會把 runtime 與 orchestration 進一步集中到少數平台
