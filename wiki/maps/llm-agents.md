# LLM Agents

## Scope

這個 map 聚焦於 `LLM + agent` 主題中的高層入口，特別是 knowledge compilation、externalized state 與 long-running harness design。

## Entry Points

- [Agent Knowledge Compilation](../concepts/agent-knowledge-compilation.md)
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)

## Core Concepts

- agent knowledge compilation
- agent runtime surfaces
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
- [OpenAI Symphony Codex Orchestration](../articles/openai-symphony-codex-orchestration.md)
- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [What Happens After Coding Is Solved](../articles/what-happens-after-coding-is-solved-boris-cherny.md)
- [A Postmortem of Three Recent Issues](../articles/a-postmortem-of-three-recent-issues.md)
- [Introducing Codex](../articles/introducing-codex.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)

## Key People Or Labs

- Andrej Karpathy
- OpenAI
- Anthropic
- Boris Cherny
- Peter Steinberger
- Aaron Friel
- Ryan Lopopolo

## Open Threads

- parameter memory、context window 與 externalized repo artifact 應如何分層，而不是互相取代
- hosted runtime、repo-local runtime 與 local personal runtime 的 design principles，哪些應共享，哪些必須分流
- 知識型 agent 與 coding agent 是否應共享同一套 state model
- compaction、progress artifact、skill contract 三者的最小組合是什麼
- 更強模型是否會讓 orchestration 複雜度下降，而不是上升
- repo-local knowledge base 與 remote async execution 應如何協同設計
- issue tracker 作為 agent control plane 時，哪些 team process 應該被版本化成 repo-local workflow contract
- local personal agents 與 cloud coding agents 應共享哪些設計原則，又該在哪些地方刻意分流
- provider-managed agent infrastructure 會不會把 runtime 與 orchestration 進一步集中到少數平台
- 如果 coding 不再是主要瓶頸，agent-era builder 的最小能力組合應如何定義，哪些 specialist review 仍然不可壓縮
- 當 hosted model quality regressions 只在特定 routing path 或硬體平台上出現時，使用者可見的 agent reliability 應如何被觀測、解釋與治理
