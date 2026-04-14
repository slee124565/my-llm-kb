# Introducing Codex

## Source

- URL: https://openai.com/index/introducing-codex/
- Author: OpenAI
- Published: 2025-05-16
- Captured: 2026-03-08
- Raw file: `raw/sources/2025/2025-05-16-openai-introducing-codex.md`
- Imported from workspace path: `_todos/2026-03-08-ai-native-engineer-capability-checklist/refs/02-openai-introducing-codex.md`

## Main Claims

- Codex 的核心形態是 cloud-based、isolated、parallel task execution 的 software engineering agent
- `AGENTS.md` 是引導 agent 理解 repo、測試命令與工程慣例的重要入口，雖然不是唯一前提，但能明顯提高表現
- verifiable evidence 是 Codex workflow 的核心；agent 應回傳 terminal logs、test outputs 與可檢查的執行軌跡
- remote asynchronous delegation 與 local interactive pairing 會逐漸收斂成統一 workflow，而不是彼此取代
- well-scoped tasks、多 agent 並行與可 review 的 sandbox execution，是 Codex product model 的基本使用假設

## Why It Matters

這篇定義了 `Codex` 作為 async coding agent 的產品操作面，也補上了 `AGENTS.md` 在 Codex workflow 中的地位。它對 `my-llm-kb` 很重要，因為這個 repo 本身就是在把文章讀法轉成可被 Codex 重複使用的 repo contract。

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Codex Workflows](../maps/codex-workflows.md)

## Tensions Or Disagreements

- 文章偏產品宣告與使用模式說明，對長時間 repo governance、artifact decay、knowledge drift 沒有深挖
- 它強調 isolated cloud sandbox，但對需要更強 steerability 的本地長任務工作流沒有深入比較

## Open Questions

- 在 Codex workflow 中，哪些資訊應放在 `AGENTS.md`，哪些應下沉到 `docs/`
- remote task sandbox 與 repo-local long-running session 各自的最佳使用邊界是什麼
- verifiable evidence 是否應進一步標準化為 repo-level output contract

## Merge Candidates

- AGENTS.md materially improves Codex performance in real repositories
- codex workflows depend on isolated execution plus verifiable evidence
- async delegation and interactive pairing are converging workflow modes
