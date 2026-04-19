# Codex Workflows

## Scope

這個 map 聚焦於 Codex 作為 coding agent 的主要 workflow：repo guidance、async delegation、execution evidence、planning artifacts、harness design，以及為重複資料面打造可組合 CLI surface。

## Entry Points

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)

## Core Concepts

- repository knowledge as system of record
- agent runtime surfaces
- externalized agent state
- long-running agent harnesses
- async delegation with verifiable evidence
- CLI-first operability plus companion skills for repeated noisy data surfaces

## Key Articles

- [Introducing Codex](../articles/introducing-codex.md)
- [Bespoke CLIs for Codex](../articles/bespoke-clis-for-codex.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [Notes From a Marketer Building a Real CLI With Codex](../articles/notes-from-a-marketer-building-a-real-cli-with-codex.md)

## Key People Or Labs

- OpenAI
- Ryan Lopopolo
- Aaron Friel

## Open Threads

- 什麼時候應該用 remote async task，什麼時候應該留在 local interactive loop
- Codex 類 repo-local workflow 和 hosted managed runtime、local personal agent 之間，哪些 state surfaces 可以共享
- `AGENTS.md` 應該保持多薄，才不會又退化成 instruction blob
- plan-heavy workflow 與 lightweight conversation-first workflow 的最佳切換門檻是什麼
- Codex 類 workflow 可以吸收多少 personal-agent pattern，例如 markdown memory ownership、CLI-first tooling 與 conversation-first steerability
- 什麼時候應該直接用 connector / MCP，什麼時候應該再往上編譯成 agent-friendly CLI 與 companion skill
- 在 agent 幫忙做工具時，哪些 product judgment 應該保持在 human loop，而不是被 prompt 或自動化完全吸收
