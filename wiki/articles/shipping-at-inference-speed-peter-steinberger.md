# Shipping at Inference-Speed

## Source

- URL: https://steipete.me/posts/2025/shipping-at-inference-speed
- Author: Peter Steinberger
- Published: 2025
- Captured: 2026-03-04
- Raw file: `raw/sources/2026/2026-03-04-shipping-at-inference-speed-peter-steinberger.md`
- Imported from workspace path: `curated/2026-03-04-shipping-at-inference-speed-peter-steinberger/2026-03-04-shipping-at-inference-speed-peter-steinberger.md`

## Main Claims

- 對高品質 coding agent 使用者而言，軟體開發速度的主要瓶頸，正在從寫碼速度轉向 inference time 與高品質系統思考
- 更強的模型會改變 workflow 本身，例如減少對 plan mode、頻繁重啟 session、checkpointing 與 worktree 的依賴
- 持續維護 `docs/` 與全域 `AGENTS` 規則，比回看舊 session 更能提供穩定上下文
- 跨專案對照、把 pattern 寫進 docs、讓 agent 自己選檔名回寫 `docs/*.md`，是比 elaborate prompts 更高效的 context engineering
- 對 solo builder 而言，queueing、多專案併行與直接 commit to main 可以形成一種低協調成本的 agentic shipping 模式

## Why It Matters

這篇提供了一種和典型多-agent orchestration 不同的實戰路線：不是先堆更多控制層，而是先提升模型能力、文件品質與 repo 可導航性，讓單一 agent session 在更長時間內保持有效。它補強了 `externalized agent state` 與 `long-running harnesses` 兩個概念頁的人類工作流面向。

## Relation To Existing Concepts

- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Long-Running Agents](../maps/long-running-agents.md)
- [LLM Agents](../maps/llm-agents.md)

## Tensions Or Disagreements

- 文章偏強烈的 solo builder 立場，像是 `commit to main`、少用 worktree、少用 issue tracker，未必適合團隊或受治理約束的環境
- 對更強模型降低 scaffolding 需求的判斷，可能會隨模型與任務類型而變；不是所有長任務都能靠更長 session 解決
- queueing 與多專案並行在高上下文污染風險場景下可能反而帶來 drift

## Open Questions

- 哪些 harness 元件會隨模型進步而被淘汰，哪些仍然是長期穩定的 infrastructure
- `docs/` 與 `AGENTS` 這類靜態 artifact，何時比 progress log 或 task contract 更有價值
- solo workflow 中有效的策略，如何轉譯到小團隊或多 contributor 場景

## Merge Candidates

- better models can reduce the need for heavy scaffolding, but not the need for durable artifacts
- docs folders and agent instructions can outperform session recall as context surfaces
- conversation-first planning can replace explicit plan mode in some mature model workflows
