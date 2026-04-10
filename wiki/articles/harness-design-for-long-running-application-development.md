# Harness Design for Long-Running Application Development

## Source

- URL: https://www.anthropic.com/engineering/harness-design-long-running-apps
- Author: Prithvi Rajasekaran
- Published: 2026-03-24
- Captured: 2026-03-25
- Raw file: `raw/sources/2026/2026-03-25-claude-harness-design-long-running-apps.md`
- Imported from workspace path: `blog/2026-03-25-claude-harness-design-long-running-apps/2026-03-25-claude-harness-design-long-running-apps.md`

## Main Claims

- 對主觀品質與長任務 coding 這兩類問題，將 generator 與 evaluator 分離，是比讓單一 agent 自評更有效的結構化解法
- 對長時間 autonomous coding 而言，context reset 與 compaction 不是等價替代；前者提供 clean slate，後者保留 continuity，但未必能解決 context anxiety
- planner、generator、evaluator 三代理架構，可以把高層產品規格展開、逐步實作、再用可執行 QA 驗證回圈收斂品質
- 隨模型升級，部分 scaffolding 可以移除，但 evaluator 或 planner 是否仍有價值，要看任務是否仍位在模型單獨能力邊界之外
- harness complexity 不應固定不變，而應隨模型能力與任務性質持續做 load-bearing analysis

## Why It Matters

這篇把 long-running harness 的設計又往前推了一步：不只是保持 session coherence，而是進一步把「主觀品質評分」和「產品深度驗證」納入 agent loop。對 `my-llm-kb` 來說，它補強了 `long-running-agent-harnesses` 裡對 evaluator 角色與 context reset/compaction 取捨的理解。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agents](../maps/long-running-agents.md)

## Tensions Or Disagreements

- 這套 harness 成本高，文章中的 run 成本與時長都不低，對多數日常軟體任務未必划算
- planner / evaluator 的收益明顯依賴模型當前能力邊界，未必是穩定不變的 architecture choice
- 文章主要基於 Claude Agent SDK 與 Playwright MCP；對其他 agent/runtime 的移植性還需要實測

## Open Questions

- evaluator 在主觀品質任務與可驗證 engineering 任務中的最佳 prompt 與 grading contract 是否相同
- context reset 與 automatic compaction 的切換門檻，應如何以任務或模型能力來決定
- 哪些 harness 組件應固定存在，哪些應視模型升級而定期刪減

## Merge Candidates

- separate generator and evaluator when self-evaluation is a bottleneck
- context reset and compaction solve different long-task failure modes
- harness components should be stress-tested as models improve, not treated as permanent
