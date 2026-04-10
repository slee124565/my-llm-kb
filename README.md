# my-llm-kb

一個專門用來承接我每日閱讀 `LLM + agent` 文章、並持續編譯成可查詢知識庫的 repo。

這個 repo 基於 [llm-wiki-kb](https://github.com/slee124565/llm-wiki-kb) 的 knowledge-base operating model，並進一步收斂成個人的 daily reading workflow for LLM and agent articles。

它以 Karpathy 式 `llm-wiki` / `llm knowledge base` 的設計理念為原型，但不是要做成自動收集器，而是要把「人的判斷」與「agent 的編譯能力」拆成兩層，讓 repo 成為長期可累積的 externalized knowledge layer。

**兩層協作模型**

- `Human Layer`
  負責選題、判斷訊號強弱、指出這篇為什麼值得看、定義今天想回答的問題，以及決定哪些主題值得持續追。
- `Agent Layer`
  負責 ingest 來源、抽 metadata、整理 claims、比對既有 article / concept / map、標示不確定性、提出 merge 建議，並把結果回寫成可查詢結構。

這代表你平常不需要自己維護完整知識樹；你比較像 editor / curator，agent 比較像 compiler / librarian。人的角色是提供方向、脈絡與品味，agent 的角色是把閱讀結果穩定編譯進 repo。

**日常最佳互動情境**

你每天可以直接挑一種情境和 agent 協作：

1. `快速收錄一篇`
   你今天看到一篇文章，先告訴 agent「這篇值得收，原因是什麼」。agent 負責放入 `raw/`、建立 article card，並指出應該連到哪些既有 concept。
2. `帶著問題讀一篇`
   你不是單純想存文章，而是想回答一個問題，例如「這篇對 long-running agents 有什麼新東西？」agent 會用該問題重組 article card，並把可重用觀察 merge 回 concept page。
3. `比較新文章與舊知識`
   你看到相似主題的新文章，請 agent 比對它和 repo 內既有頁面的差異。agent 應回答哪些是重複、哪些是增量、哪些會改變既有理解。
4. `追一個主題，不追單篇`
   你今天想整理一個主題，例如 tool use、memory、evals、MCP、agent workflow。agent 應先從 `wiki/maps/` 和 `wiki/concepts/` 回顧現況，再吸收新來源，把單篇輸入轉成主題層的更新。
5. `整理一個人或組織的觀點`
   你連續看到同一位作者、lab、公司或產品反覆出現。agent 應把分散在 article cards 裡的觀點收斂到 `wiki/people/`，讓 repo 不只記文章，也記「誰在推動什麼觀點」。
6. `做一次衝突與不確定性檢查`
   當新文章和既有理解不一致時，你可以要求 agent 專門檢查衝突。agent 應明確標出哪些 claim 仍不確定、哪些只是語境不同、哪些值得升級成 concept revision。
7. `做一次 repo maintenance review`
   當你沒有新文章要收，但想讓 repo 更好用時，可以請 agent 找出過厚的 article page、該 merge 的 concepts、該建立的 maps，以及過時或重複的入口。

如果你不知道今天該怎麼開始，最低摩擦的互動方式是：

1. 你丟一篇今天看到的文章
2. 你補一句「我覺得它重要，因為...」
3. agent 回收錄、比較、merge 建議
4. 你只需要決定哪些主題值得升級成長期知識

**Prompt Starters**

若你想直接引用可維護的 prompt asset，請看 [prompts/README.md](prompts/README.md)。

若你想讓 script 或 agent 直接選 prompt，請看 [prompts/index.json](prompts/index.json)。

若你忘了該用哪個 prompt，可用 `tools/list-prompts` 查詢。
常用例子：

- `tools/list-prompts`
- `tools/list-prompts --tag ingest`
- `tools/list-prompts --related markdown-source-ingest`

最常用的入口：

- 新來源 ingest：`prompts/ingest-source.md`
- `.md` 來源 ingest：`prompts/markdown-source-ingest.md`
- 今天新 ingest 回顧：`prompts/ingest-review.md`
- 單篇比對既有內容：`prompts/compare-article-to-existing.md`
- 主題更新：`prompts/topic-update.md`
- 結構維護：`prompts/repo-maintenance-review.md`

這個 repo 不是一般閱讀筆記區，也不是書摘堆放區。

它的用途是：

1. 保存原始文章與來源資訊
2. 把單篇文章編譯成可重用的 article card
3. 把跨文章概念沉澱成 concept page
4. 維護少量可導航的 topic map

核心操作模型是：

- capture raw source
- compile article brief
- merge into concepts and maps
- maintain index and log

如果你每天都在讀 LLM、agents、tool use、memory、eval、MCP、AI product workflow 相關文章，這個 repo 的目的是讓那些閱讀結果不要停在一次性摘要，而是逐步長成可回查、可比較、可被 agent 利用的知識結構。

**建議閱讀順序**

- 若你用 Codex：先讀 [AGENTS.md](AGENTS.md)
- 若你用 Claude：先讀 [CLAUDE.md](CLAUDE.md)
- [README.md](README.md)
- [ARCHITECTURE.md](ARCHITECTURE.md)
- [docs/README.md](docs/README.md)
- [docs/ingest.md](docs/ingest.md)
- [docs/compile.md](docs/compile.md)
- [docs/review.md](docs/review.md)
- [docs/query.md](docs/query.md)
- [prompts/README.md](prompts/README.md)
- [prompts/index.json](prompts/index.json)
- [raw/README.md](raw/README.md)
- [wiki/README.md](wiki/README.md)

**Repo Structure**

- `raw/`
  放 immutable source material
- `wiki/articles/`
  放單篇文章的 compiled card
- `wiki/concepts/`
  放跨文章穩定概念頁
- `wiki/maps/`
  放主題導覽頁與 topic map
- `wiki/people/`
  放高頻作者、lab、公司或產品節點
- `index.md`
  放少量 stable entry points
- `log.md`
  記錄 ingest、merge、review、cleanup
- `docs/`
  放穩定 workflow 與維護規則
- `prompts/`
  放可重用的 prompt assets 與 agent interaction starters
  `prompts/index.json` 提供 machine-readable prompt registry
- `tools/`
  放 repo-local tools；`tools/list-prompts` 可查詢 prompt registry

**Agent Entry Files**

- `AGENTS.md`
  給 OpenAI Codex 的 repo operating rules
- `CLAUDE.md`
  給 Claude 的最小操作規則

**你做什麼，Agent 做什麼**

- 你負責挑文章、保存來源、判斷值得長期保留的主題
- Agent 負責抽 metadata、整理 claims、比較舊內容、回寫 article/concept/map pages
- 你定期 review 結構是否仍然清楚

**這個 Repo 的邊界**

這個 repo 應聚焦在：

- `LLM + agent` 閱讀輸入
- 可重用知識頁的編譯
- 主題地圖與知識導航
- 後續 query / synthesis / maintenance

這個 repo 不應長期承擔：

- 原始全文收藏系統
- 全域 PKM inbox
- 任務管理
- 對外發表草稿
- workspace 級 workflow 說明

如果內容還只是瞬時想法，應留在 `_ideas/`。
如果是進行中的任務材料，應留在 `_todos/`。

**最小日更流程**

1. 把文章或材料放進 `raw/inbox/` 或 `raw/sources/`
2. 建立或更新對應的 `wiki/articles/*.md`
3. 把可重用觀察 merge 回 `wiki/concepts/*.md`
4. 必要時更新 `wiki/maps/*.md`
5. 更新 `index.md` 與 `log.md`

**設計原則**

- `raw/` 只保存來源，不在原地改寫
- 單篇摘要不等於知識頁；知識頁應帶有比較、定位與連結
- `index.md` 應保持很薄，只保留入口
- `log.md` 只記 maintenance history，不承擔知識內容
- 當某個主題累積到 3 到 5 篇以上時，應考慮升級成 `wiki/maps/` 導覽頁
