# Agent Knowledge Compilation

## Summary

Agent knowledge compilation 指的是：先把來源保存為 raw material，再由 agent 將單篇內容編譯成 article cards，並持續 merge 到 concept pages 與 topic maps，形成會隨新來源增長而更新的 persistent knowledge layer。

## Why It Matters

如果每次 query 都回到原始來源重新拼裝答案，知識不會累積，只會重複勞動。knowledge compilation 把維護工作前置，讓後續查詢、比較與回寫都更便宜。

## Current Framing

- `raw/` 保存來源與 provenance
- `wiki/articles/` 保存單篇編譯理解
- `wiki/concepts/` 保存跨來源穩定理解
- `wiki/maps/` 保存導航入口
- `index.md` 與 `log.md` 分別承接導航與歷史
- 可重用的知識頁面本身也應該好掃讀：takeaway 要前置，標題要具體，段落要短，這樣下一輪 agent 才能快速判斷哪些內容該 merge、哪些內容只留在 article card

## Signals From Recent Articles

- [LLM Knowledge Bases](../articles/karpathy-llm-knowledge-bases.md)
- [What Makes Documentation Good](../articles/what-makes-documentation-good.md)

## Open Questions

- concept page 的拆分粒度應如何控制
- query 產出的 reusable artifact 應如何分類回寫
- 何時需要從 index-first 升級到 search-first
- knowledge page 是否也應明確區分 skim layer 與 detail layer

## Related Pages

- [Externalized Agent State](externalized-agent-state.md)
- [LLM Agents](../maps/llm-agents.md)
