# Question-Answer Packets for RAG

## Source

- URL: https://x.com/akshay_pachaar/status/2052743644411765230
- Author: Akshay @akshay_pachaar
- Published: 2026-05-08
- Captured: 2026-06-21
- Raw file: `raw/sources/2026/2026-05-08-question-answer-packets-for-rag.md`
- Extraction: `myAgentTools/xcom-article-import`

## Main Claims

- 這篇的核心主張是：很多 RAG 失敗不是因為 retriever、reranker 或 embedding model 不夠好，而是因為一開始把「文字 chunk」當成知識單位。chunk 只是切割方便的容器，不知道 idea 邊界、版本狀態或 access rule；下游再怎麼調 top-k、threshold 或 prompt，都只是在修補上游 representation 的問題。
- 作者提出的替代單位是問題答案封包（question-answer packet）：一個問題、一個經驗證的答案，再加上 typed governance fields，例如 clearance level、version state、source。這讓 retrieval 的單位從「可能包含答案的一段文字」變成「可被查詢直接命中的 atomic claim」。
- Blockify / IdeaBlock 的設計把這個想法做成 preprocessing layer，放在 parser 和 vector store 之間。它不是改變應用層的查詢方式，而是改變進入 index 的資料形狀：先把文件轉成一組可治理、可去重、可追蹤來源的 IdeaBlocks，再送進 vector DB。
- 文章引用 Blockify 內部 benchmark，主張 IdeaBlocks 相比 naive chunks 有更低的 query-to-block cosine distance，並且經過 80-85% similarity 的 iterative deduplication 後，資料量下降但 vector accuracy 反而提高。這裡的重要直覺是：向量資料庫不是越滿越好，近似重複的 vectors 會在同一片 embedding space 裡彼此競爭，降低 canonical answer 的訊號。
- 對 enterprise RAG 來說，version 與 access control 不是外掛邏輯，而應靠近 knowledge unit 本身。若同一個規格文件有 current、deprecated、draft 多個版本，或不同角色可看不同 clearance level，這些欄位應和 claim 一起流過 ingestion、dedup、validation、export，而不是最後才靠 orchestrator 補 filter。

## Why It Matters

這篇補上 repo 裡 RAG / memory 討論的一個缺口：我們已經有「vector RAG 不等於長期記憶」和「temporal graph 適合動態關係」的 framing，但還需要更細地看 static corpus 內部的 representation。即使只是企業文件問答，文字 chunk 也可能不是最好的 retrieval unit。

對 AI systems engineering 來說，這把 RAG engineering boundary 往前推。系統可靠性不只取決於 embedding model、reranker、prompt construction 和 citation validation，也取決於 ingest-time 的語意蒸餾（semantic distillation）、去重、版本欄位、權限欄位與人工驗證。換句話說，RAG pipeline 應該有一層「knowledge unit compiler」，而不是 parser 之後直接進 vector store。

對 agent memory 來說，這篇的價值不是說 IdeaBlock 可以取代 temporal graph，而是讓「static document memory」也有更好的單位設計。若資料仍然是相對靜態的文件集合，question-answer packets 可能比 raw chunks 更適合承擔 provenance、version、access 與 update propagation；若資料是會演化的人事物關係，才需要 graph / temporal memory。

## Relation To Existing Concepts

- [AI Systems Engineering](../concepts/ai-systems-engineering.md)：這篇把 RAG 的系統責任從 query-time tuning 推到 ingest-time representation。document parser、LLM-based claim extraction、semantic deduplication、governance tagging、SME validation 和 vector export 都應被視為同一個 decision-producing loop 的 artifact pipeline。
- [Agent Memory Architecture](../concepts/agent-memory-architecture.md)：文章強化「vector RAG 適合 static corpus，但需要資料單位治理」這個分層。question-answer packets 可改善 static document retrieval 的 idea boundary、version 與 access control，但不等於解決 long-term personal / customer memory 的 temporal truth 問題。
- [Building Agent Memory with Knowledge Graphs](building-agent-memory-with-knowledge.md)：兩篇都反對把所有 memory 問題塞進 naive vector chunks。差別是知識圖譜那篇強調 dynamic relationships and valid time；本文則強調 static enterprise corpus 也應先把 claim 結構化。
- [LLM Agents](../maps/llm-agents.md)：這篇可作為 RAG data representation 的補充入口，連到 agent knowledge、memory、AI systems engineering 與 enterprise governance。

## Tensions Or Disagreements

- 文章引用的數字來自 Blockify 內部 benchmark，且樣本範圍是 17 documents / 298 pages；它足以形成值得追蹤的 pattern，但不能直接當成所有 enterprise RAG 場景的普遍效果。
- 把 chunks 轉成 question-answer packets 需要 LLM extraction、deduplication、canonicalization 與 validation。這會把成本從 query time 移到 ingest time，也會引入 extraction error、over-compression 和 lost nuance 的風險。
- 「一個 fact per unit」對規格、FAQ、政策文件很有吸引力，但對論證型文章、研究報告或需要長上下文的判斷題，過度 atomic 化可能讓模型失去脈絡。實務上仍可能需要 packet-level retrieval 搭配 source passage 或 document-level citation。
- Governance fields 放進 block schema 會讓權限與版本更靠近資料，但不能取代 runtime enforcement。系統仍需要確保 export、vector store filter、API path、audit log 和 UI disclosure 都遵守同一套 policy。

## Open Questions

- Question-answer packet 適合哪些 corpus：FAQ、SOP、產品規格、合約條款、客服知識庫、研究報告，還是需要不同 granularity？
- LLM extraction 產生的 answer packet 應如何保存 source span、confidence、validation owner 與 last-reviewed timestamp，才不會把錯誤 claim 結構化成更有權威感的資料？
- 若 canonical IdeaBlock 更新，舊 block 的 deprecation、redirect、audit history 與 evaluation regression 應如何管理？
- Retrieval 評估應如何同時衡量 answer hit rate、citation faithfulness、access-control correctness、version freshness 與 token/cost reduction？
- 對 long-running agents 而言，static corpus 的 question-answer packets、temporal graph memory、repo knowledge base 與 procedural skills 應如何分工？

## Merge Candidates

- RAG failure should be reviewed at the knowledge-unit layer before tuning retrievers, rerankers, thresholds, or prompts.
- Text chunks are parsing conveniences, not necessarily reliable retrieval units; they lack idea boundaries, version context, and access state.
- Question-answer packets / IdeaBlocks turn static documents into atomic claims with typed governance metadata, making retrieval more structural and easier to validate.
- Semantic deduplication can improve retrieval quality by collapsing near-duplicate vectors into canonical claims, reducing embedding-space competition.
- RAG pipelines need an ingest-time knowledge-unit compiler between parser and vector store when enterprise governance, versioning, and update propagation matter.
