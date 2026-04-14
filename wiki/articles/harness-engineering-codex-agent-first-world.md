# Harness Engineering

## Source

- URL: https://openai.com/index/harness-engineering/
- Author: Ryan Lopopolo
- Published: 2026-02-11
- Captured: 2026-03-08
- Raw file: `raw/sources/2026/2026-02-11-openai-harness-engineering.md`
- Imported from workspace path: `_todos/2026-03-08-ai-native-engineer-capability-checklist/refs/01-openai-harness-engineering.md`

## Main Claims

- 在 agent-first engineering 中，人類的主要工作會從直接寫 code 轉向設計環境、規範 intent、建立 feedback loops
- `AGENTS.md` 不應是冗長百科，而應是 table of contents；真正的 system of record 應放在結構化 `docs/` knowledge base
- 讓 app、logs、metrics、traces、quality grades 與 execution plans 都對 agent 可見，是提升 agent legibility 與長任務穩定性的關鍵
- 高吞吐 agent workflow 會改變 merge philosophy、review 分工與 codebase governance；重點變成機械式 enforcement，而不是人手逐行把關
- fully agent-generated repo 若要維持長期可維護性，必須持續把 taste、architecture 與 cleanup 規則編碼進 repo 本身

## Why It Matters

這篇不是只在談 Codex 產品，而是在談一整套 agent-first repository operating model。它把 `externalized state`、`long-running harnesses` 與 `repo-local knowledge base` 三件事連成一個更高層的設計語言。

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Codex Workflows](../maps/codex-workflows.md)

## Tensions Or Disagreements

- 這篇假設 team 能投入大量基礎設施與 custom linting；對較小團隊或輕量 repo 是否划算，仍需看上下文
- 「minimal blocking merge gates」在高吞吐 agent 團隊可能合理，但在高風險產品或多人協作環境未必適用

## Open Questions

- 哪些 observability 與 quality artifacts 是大多數 repo 都應該具備的最小集合
- agent-first repo 的機械式治理，何時會開始過度投資
- `AGENTS.md` 作為 table of contents 的做法，應如何對應不同 agent 的入口需求

## Merge Candidates

- short AGENTS plus structured docs beats one giant instruction manual
- repository-local knowledge should be the system of record for agent work
- agent legibility requires making UI, logs, metrics, plans, and architecture visible in-repo
