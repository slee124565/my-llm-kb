# Shell + Skills + Compaction

## Source

- URL: https://developers.openai.com/blog/skills-shell-tips
- Author: Charlie Guo
- Published: 2026-02-11
- Captured: 2026-02-11
- Raw file: `raw/sources/2026/2026-02-11-shell-skills-compaction-tips-for-long-running-agents-openai.md`

## Main Claims

- 長任務 agent 需要的不是單一 prompt，而是一組可重用 procedure、可執行環境與可延續上下文的 primitives
- skill description 實際上是 routing logic，應該明確描述何時用、何時不用、輸出與成功標準
- shell 與 compaction 一起使用時，才能讓 multi-step workflow 在同一執行脈絡中持續推進
- skills 搭配 networking 有資料外洩風險，設計時要預設 containment 與 allowlist

## Why It Matters

這篇把「long-running agent 要怎麼穩定運作」拆成可以工程化的原件，而不是只談抽象 agent intelligence。對你的 repo 來說，它提供了 workflow doc 與 `CLAUDE.md` 背後的 practical design language。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agents](../maps/long-running-agents.md)

## Tensions Or Disagreements

- 它主要談 OpenAI Responses API 下的 primitives，對非同平台環境的可移植性需要再驗證
- compaction 被描述為 continuity primitive，但沒有深入處理 compact 後的 state drift 風險

## Open Questions

- skill routing 何時應交給模型自主判斷，何時應外部強制指定
- 哪些 workflow 適合用 hosted shell，哪些應保留在 local runtime
- compaction 與 explicit artifact handoff 應如何組合

## Merge Candidates

- skill descriptions are decision boundaries, not marketing copy
- long-running agents need reusable procedures plus execution plus continuity
- open network plus powerful procedures requires strict containment
