# LLM Knowledge Bases

## Source

- URL: https://x.com/karpathy/status/2039805659525644595
- Author: Andrej Karpathy
- Published: 2026-04-06
- Captured: 2026-04-06
- Raw file: `raw/sources/2026/2026-04-06-karpathy-llm-knowledge-bases.md`

## Main Claims

- 個人知識庫的價值，不在 query 時重新從 raw source 拼答案，而在於讓 LLM 持續維護一個 persistent wiki
- `raw/`、compiled wiki、index/log 這種分層，足以在中小規模知識庫中支撐高品質問答，而不必先上複雜 RAG
- 查詢產生的新比較、分析、輸出，也應回寫到知識庫，讓 exploration 本身成為新的資產
- lint / health check 是知識庫維護的一部分，而不是額外整理工作

## Why It Matters

這篇文章定義了這個 repo 的核心 operating model。它把知識庫重心從「存檔」轉成「編譯與維護」，也讓 article card、concept page、topic map 的分工變得合理。

## Relation To Existing Concepts

- [Agent Knowledge Compilation](../concepts/agent-knowledge-compilation.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [LLM Agents](../maps/llm-agents.md)

## Tensions Or Disagreements

- 文章偏向小中型知識庫的 operating pattern，尚未回答更大規模時 metadata、search 與 governance 如何演化
- 對 human review 的介入程度保留彈性，沒有提供明確品質閘門

## Open Questions

- knowledge compilation 何時需要更明確的 metadata schema
- concept page 與 map page 的拆分門檻應如何固定
- lint 週期應按來源數量、主題密度，還是固定節奏運行

## Merge Candidates

- persistent wiki beats repeated rediscovery from raw documents
- query outputs should be filed back into the knowledge base
- linting is part of the knowledge loop, not post-processing
