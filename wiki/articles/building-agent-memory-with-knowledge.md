# Building Agent Memory with Knowledge Graphs

## Source

- URL: https://theneuralmaze.substack.com/p/building-agent-memory-with-knowledge
- Author: Miguel Otero Pedrido
- Publisher: The Neural Maze
- Published: 2026-06-04
- Captured: 2026-06-08
- Raw file: `raw/sources/2026/2026-06-04-building-agent-memory-with-knowledge.md`
- Imported from workspace path: `my-blog-kb/raw/inbox/2026-06-04-building-agent-memory-with-knowledge.md`
- Subtitle: Issue #04 — The theory, the trade-offs, and a Graphiti + Neo4j assistant you can run today
- Source note: Substack article from `The AI Systems Engineer Journey`; includes a conceptual comparison of RAG and temporal knowledge graphs plus a Graphiti / Neo4j personal assistant example.

## Main Claims

- 單純把每個 user turn embed 進向量資料庫，不等於真正的 agent 記憶（agent memory）。它可以找相似片段，但沒有身份（identity）、關係（relationship）與時間（time）的明確欄位，所以遇到同名人物、過期事實或多跳問題時，很容易把舊資訊和新資訊混在一起。
- RAG 仍然適合大規模、相對靜態的文件問答：文件切塊、embedding、向量搜尋、BM25 / hybrid search 與 reranker 都是成熟且便宜的 retrieval 技術。問題不是 RAG 沒用，而是把 RAG 當成長期記憶時，representation 無法表達「誰和誰有什麼關係」以及「這件事什麼時候有效」。
- 知識圖譜（knowledge graph）把事實表示成節點與邊，例如人、地點、組織與它們之間的關係。這讓 explainable reasoning、multi-hop reasoning、entity resolution 與 schema flexibility 變成資料結構本身的能力，而不是只靠 prompt 要模型猜。
- 對 agent memory 來說，時間是關鍵增量。時間型知識圖譜（temporal knowledge graph）不只是保存目前快照，而是讓邊帶有有效時間：使用者搬家後，舊居住地不應和新居住地同時被當成 current truth，而應變成 history。
- Graphiti 的定位是把圖譜記憶做成可增量更新的 runtime memory layer。它把 message、document、event 當成 episode ingest，抽取 entity / relationship，和既有圖譜 reconcile，並用 bi-temporal model 區分事件發生時間與系統得知時間。
- Graphiti-style retrieval 不是拋棄 RAG，而是把向量語意搜尋、BM25 關鍵字搜尋與 graph traversal 組合起來。對長期個人助理、客服 agent 或企業知識演化系統，這種 hybrid memory 比純相似度檢索更能處理 current facts、關係鏈與可解釋答案。
- 記憶架構的選擇應依 workload 決定：靜態文件查詢用 vector RAG；長期、動態、關係密集、需要追蹤事實演化的 agent 才值得付出圖譜抽取的成本。

## Why It Matters

這篇對 `my-llm-kb` 的價值，是把 repo 裡一直分散在 `externalized state`、`personal-agent memory`、`long-running harness` 與 `RAG / knowledge base` 的討論，收斂成一個更精確的問題：agent memory 不是「多存一點上下文」，而是要選擇能表示 identity、relationship、freshness、history 與 retrieval path 的 state model。

它也補上 Hermes / OpenClaw / Codex memory 討論中比較缺的一層資料結構判斷。先前來源常談 user-owned files、MEMORY.md、skills、session history、repo artifacts 與 durable threads；本文則明確指出，當記憶需要處理人、事件、偏好、地點、職務、時間變化與多跳推理時，純文字或向量 chunk 會把「過期但相似」的事實和「目前有效」的事實放在同一層。這會直接影響 personal agents、customer-support agents 與 enterprise workflow agents 的可信度。

## Relation To Existing Concepts

- [Agent Memory Architecture](../concepts/agent-memory-architecture.md): 本文是 temporal knowledge graph / Graphiti memory 的主要 anchor，補上 RAG、graph 與 hybrid retrieval 的取捨。
- [Externalized Agent State](../concepts/externalized-agent-state.md): article 將外部化狀態進一步拆成 static document memory、dynamic episodic memory、temporal fact memory 與 procedural memory。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): Graphiti / Neo4j 成為 personal assistant runtime 的 memory backend，和模型、chat loop、user namespace、Docker deployment 共同構成 runtime surface。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): 長任務與長期 assistant 不能只依賴 context window；harness 需要 episode ingest、fact reconciliation、retrieval policy、freshness handling 與可審計 trace。
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md): repo/wiki 適合穩定知識與 source provenance；temporal graph 更適合 live、relationship-rich、會更新的 user / customer / enterprise memory。
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
- Related prior sources: [Hermes Agent Masterclass](hermes-agent-masterclass.md), [Getting The Most Out Of Codex](getting-the-most-out-of-codex.md), [OpenClaw: The Viral AI Agent that Broke the Internet](openclaw-viral-ai-agent-lex-fridman-peter-steinberger.md), [LLM Knowledge Bases](karpathy-llm-knowledge-bases.md)

## Tensions Or Disagreements

- 文章用很清楚的方式批評「vector store as memory」，但這不代表所有 memory 都該上圖譜。每個 episode 都做 LLM entity / relationship extraction 會增加 latency、成本與抽取錯誤，對大量靜態文件搜尋反而不划算。
- Temporal graph 能處理 fact supersession，但仍需要高品質 ingestion policy。若時間戳、entity resolution 或 contradiction detection 錯了，圖譜會把錯誤結構化，後續 retrieval 反而更有權威感。
- Graphiti 避免 query-time LLM call 以換取低延遲 retrieval，但把成本移到 ingest-time extraction 與 reconciliation。這適合長期記憶，不一定適合一次性查詢或高寫入量事件流。
- Knowledge graph 的可解釋 path 很有價值，但不等於答案必然正確。path 只能展示系統如何連到某個答案，仍需要 source provenance、confidence、更新策略與使用者修正機制。

## Open Questions

- 對 personal agent 來說，哪些 facts 應進 temporal graph，哪些應留在 markdown memory、repo KB、session transcript 或平台 memory？
- Graphiti 這類 episode ingest 的最小 human review / correction loop 應長什麼樣，才不會讓錯誤 entity resolution 長期污染記憶？
- Temporal graph、RAG corpus、repo knowledge base 與 skill catalog 應如何分工，才能同時保留 freshness、provenance、procedural memory 與 auditability？
- 對客服或企業 agent，fact expiration、user correction、privacy deletion 與 legal retention policy 應該落在 graph schema、memory service 還是上層 harness？
- 當 graph retrieval 回傳一條關係路徑時，agent 應如何把 path、source episode、valid time 與不確定性一起呈現給使用者或 reviewer？

## Merge Candidates

- Agent memory architecture 應依資料形態分層：static document knowledge 用 RAG / KB；dynamic relationship-rich facts 用 temporal graph；procedures 用 skills；任務進度用 repo / tracker artifacts。
- Vector similarity is not memory governance. 長期記憶需要 identity resolution、relationship modeling、valid time、supersession 與 correction path。
- Temporal knowledge graphs are most valuable when current truth and historical truth must coexist without contradiction.
- Graphiti-style hybrid retrieval keeps vector and BM25 search but adds graph traversal and temporal reconciliation; the real shift is representation, not abandoning retrieval.
- Memory backend selection is a runtime-surface decision: latency, ingest cost, privacy, update frequency, explainability, deletion policy, and user ownership all matter.
