# Your KV Caching Is Broken

## Source

- URL: https://x.com/akshay_pachaar/status/2074502882812952666
- Author: Akshay @akshay_pachaar
- Published: 2026-07-07
- Captured: 2026-07-08T07:22:50+08:00
- Raw file: `raw/sources/2026/2026-07-07-your-kv-caching-is-broken.md`
- Source note: X.com long-form post about KV cache management, prompt / prefix caching limits, LMCache's disaggregated cache architecture, and CacheBlend for multi-document reuse.

## Main Claims

- 這篇的核心主張是：agent 成本問題不只來自模型「思考」本身，也來自每一步都把相同 system prompt、tool definitions、documents 和歷史脈絡重新送進模型。若 agent loop 每次都從頭讀同一包 context，即使單價下降，總 token volume 仍會把成本推高。
- KV cache 是模型在處理輸入 token 時產生的 key / value attention state。穩定的 system prompt 或固定文件理論上不該每次重算；如果無法保存與重用這些 state，長上下文 agent 就像每次問第七章問題都要求人從第一頁重讀教科書。
- Provider 的 prompt caching / prefix caching 是有用但有限的最佳化：它適合長而穩定的開頭，能讓 cached input token 大幅降價；但只要文件順序改變、RAG query 需要組合多份已分別 cached 的文件，或對話歷史持續成長，exact prefix rule 就會讓 cache hit 率受限。
- 文章把「cache management 放在 inference engine 內部」視為另一個瓶頸。cache I/O 是搬運大量 tensor 的 I/O-heavy 工作，inference 是 GPU matrix multiplication 的 compute-heavy 工作；兩者擠在同一 process，會互相阻塞，讓原本省下的計算被同步與搬運成本吃掉。
- LMCache 的增量在於把 KV cache 管理拆成獨立 process，透過 shared GPU memory 與 inference engine 協作。直覺意思是：模型服務不再一邊做菜一邊跑倉庫，而是讓 cache layer 專門處理 GPU / CPU / SSD / remote storage 之間的搬運與查找。
- CacheBlend 則處理 prefix caching 的組合問題：多份文件各自 cached 後，直接拼接會缺少跨文件 attention；CacheBlend 選擇性重算少數跨邊界關鍵 token，其餘 state 重用，讓多文件 RAG / agent context 可以從「必須重算」變成「局部補算」。
- 對 production self-hosted inference 來說，KV cache 不只是 performance trick，而是成本結構與 runtime architecture 決策。當 agent workload 會反覆使用穩定 prompt、tool schema、文件、memory 或長歷史時，cache 命中率、跨 GPU 共享、多層 storage、fault tolerance 和 observability 都會變成服務可靠性的組成部分。

## Why It Matters

這篇值得收進 `my-llm-kb`，因為它補上 repo 目前較少明確寫出的「agent inference economics」層。既有頁面已經有 AI compute infrastructure、runtime surfaces、RAG representation、agent memory 與 long-running harness；這篇把它們接到一個很實際的問題：長上下文 agent 的成本不只取決於模型價格，也取決於 context 是否被重送、重算、重排與重用。

對管理者與產品負責人而言，這篇的提醒是：不要只問「哪個模型每百萬 token 最便宜」。更該問的是 agent workflow 反覆送出的 token 裡，有多少其實是穩定上下文；這些上下文能否被 prompt cache、KV cache、document cache、memory layer 或更好的 prompt construction 重用。否則價格下降會被 agent step count、tool schema、RAG documents 和 multi-turn context 的膨脹抵消。

對工程實作而言，這篇把 serving 架構從 model API 旁邊拉回系統設計：inference engine、cache process、GPU memory、CPU RAM、SSD、remote storage、observability、crash downgrade mode 都是同一個 runtime surface。當 workload 進入 agent / RAG / long-context production，不做 cache architecture review，就等於默認每次都用最貴方式重新理解同一批材料。

## Relation To Existing Concepts

- [AI Compute Infrastructure](../concepts/ai-compute-infrastructure.md): 本文把 compute 討論從 chips / provider / accelerator stack 延伸到 inference-time KV cache layer；便宜 token 不等於便宜 agent，因為 context 重算和 cache I/O 也會成為成本與 latency 主因。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): KV cache、prompt cache、LMCache process、multi-tier storage 和 CacheBlend 都是 runtime surfaces；它們決定 agent loop 的 context reuse、latency、failure downgrade 和 observability。
- [AI Systems Engineering](../concepts/ai-systems-engineering.md): 文章把 RAG / agent serving 的成本、latency、cache hit、fault tolerance 與 monitoring 放進同一個 decision-producing loop，符合「不是 demo script，而是可營運系統」的 framing。
- [Agent Memory Architecture](../concepts/agent-memory-architecture.md): KV cache 不是長期記憶，但它是「短期重用已理解上下文」的 serving layer；它應和 static corpus retrieval、temporal graph memory、repo artifacts、session history 分清責任。
- [Question-Answer Packets for RAG](2026-05-08-question-answer-packets-for-rag.md): 前者處理 RAG 的 knowledge-unit representation；本文處理多文件 context 進入模型後能否重用 computation。兩者分別位於 retrieval representation layer 與 inference cache layer。
- [Don't Marry Your LLM Provider](dont-marry-your-llm-provider.md): AI gateway 可以處理 provider routing 和 cost attribution，但若底層 self-hosted inference 沒有 cache architecture，gateway 只能在 provider / model 間換路，無法消除重算穩定 context 的浪費。

## Tensions Or Disagreements

- 文中的成本、速度與預測數字來自該 X.com 文章的整理，應作為待追蹤 signals，而不是 repo 內已獨立驗證的普遍事實。尤其 Gartner / Uber / Stanford / LMCache benchmark 的原始上下文需要 primary source 才能升級成強 claim。
- Prompt caching、KV caching、RAG representation 和 long-term memory 容易被混成同一件事。本文最可保留的增量是 inference-time computation reuse；它不能取代 knowledge governance、source provenance、versioning 或 dynamic memory correction。
- Disaggregated cache architecture 對自架 inference 和高吞吐 RAG / agent workload 很有價值，但對純 API 使用者或低頻內部工具，最先該做的可能仍是 prompt construction、tool definition trimming、context budgeting、model routing 和 eval-backed cost attribution。
- CacheBlend 的「局部重算跨文件 token」很有吸引力，但實務上還需要看模型相容性、quality regression、cache invalidation、security isolation 與 observability。不能只因為多文件 RAG 常見，就假設所有 production stack 都應立即採用。

## Open Questions

- 在 agent workload 裡，哪些 context 應被設計成穩定 prefix，哪些應外部化為 retrieval / memory，哪些才應進入當次 prompt？
- 對 API-only team 而言，能用哪些可見指標近似評估 cache benefit：cached input token 比例、prefix stability、tool schema size、document reorder rate、conversation growth rate？
- 對 self-hosted inference team 而言，LMCache 這類 disaggregated cache layer 應該在哪個規模門檻後導入：QPS、context length、GPU count、cache hit rate、還是 cost per successful task？
- RAG pipeline 是否應在 retrieval 排序時同時考慮 semantic relevance 和 cache locality，避免每次都組出語意正確但 cache-hostile 的 context？
- KV cache、session memory、repo knowledge base、vector store 和 graph memory 之間，應如何暴露給 agent planner，才能讓它知道「重用計算」和「重用知識」是不同層次？

## Merge Candidates

- Agent cost review 應從 price per token 升級成 cost per successful task，並拆出 repeated context、step count、tool schema size、RAG document volume、cache hit rate 和 latency。
- Prefix caching 適合穩定開頭，但 document order、multi-document RAG 與 growing conversation history 會造成 hard ceiling。
- KV cache management 是 inference runtime surface，不只是模型內部細節；cache I/O、GPU memory sharing、multi-tier storage、fault tolerance 和 observability 都會影響 production agent reliability。
- 對 self-hosted agent / RAG inference，disaggregated cache layer 可以把 I/O-heavy cache movement 與 compute-heavy inference 分離，避免兩者在同一 process 爭資源。
- CacheBlend 類技術代表 RAG caching 的下一個問題：不是只 cache 單份文件，而是讓多份已 cached 的知識單位在新組合中仍能保留必要跨文件理解。
