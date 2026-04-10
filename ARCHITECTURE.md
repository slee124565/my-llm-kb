# ARCHITECTURE.md

這個 repo 以 daily reading knowledge compiler 為核心，採五層結構，外加一層 interaction assets：

- `raw/`
- `wiki/articles/`
- `wiki/concepts/`
- `wiki/maps/` and `wiki/people/`
- `index.md` and `log.md`
- `prompts/` and `tools/`

**1. Raw Layer**

`raw/` 放來源材料，預設不可變：

- web articles
- blog posts
- paper notes
- keynote transcript
- screenshots
- copied threads

`raw/` 的目的是保留 provenance，不是把它整理成最終知識形態。

**2. Article Layer**

`wiki/articles/` 放單篇文章的 compiled card。

每張 article card 應回答：

- 這篇在說什麼
- 主張是什麼
- 哪些觀點值得保留
- 它和既有知識庫有哪些關聯
- 哪些內容應 merge 回 concept pages

這一層是從 source 到 knowledge 的第一層編譯。

**3. Concept Layer**

`wiki/concepts/` 放跨文章的穩定概念頁，例如：

- agent memory
- tool use
- evals
- workflow orchestration
- model context protocol

概念頁不是單篇摘要集合，而是持續被更新的 compiled understanding。

**4. Map and Entity Layer**

`wiki/maps/` 用來維護主題入口頁。
`wiki/people/` 用來維護高頻作者、實驗室、公司、產品或 framework 節點。

這一層的工作是讓 repo 可以回答：

- 從哪裡開始看某個主題
- 這個主題下有哪些重要文章
- 哪些人或組織反覆出現
- 有哪些觀點差異或演化

**5. Navigation and History Layer**

- `index.md` 是 repo 入口圖
- `log.md` 是 append-only maintenance timeline

`index.md` 應維持薄而穩定，只保留少數 entry points。
`log.md` 只記錄 ingest、merge、review、cleanup，不承擔知識本體。

**6. Interaction Assets Layer**

`prompts/` 放 repo-local prompt assets。
`tools/` 放支援這些 prompt assets 或日常互動的小工具。

這一層不承擔知識本體，也不是 source facts。
它的角色是把高頻 human-agent interaction pattern 外部化，降低每次從零描述任務的成本。

**Source of Truth**

- source facts live in `raw/`
- per-article compiled understanding lives in `wiki/articles/`
- cross-article synthesis lives in `wiki/concepts/`
- entry maps live in `wiki/maps/`
- recurring entities live in `wiki/people/`
- navigation lives in `index.md`
- history lives in `log.md`
- reusable interaction patterns live in `prompts/`
- helper lookup utilities live in `tools/`

**Lifecycle**

1. source enters `raw/inbox/`
2. source is normalized into `raw/sources/`
3. article card is created in `wiki/articles/`
4. reusable claims are merged into `wiki/concepts/`
5. topic maps are updated if needed
6. `index.md` and `log.md` are maintained

**Scaling Rule**

- 當某個 topic 只有 1 到 2 篇材料時，先留在 article layer
- 當某個 topic 積累到 3 到 5 篇以上時，建立 concept page
- 當 concept page 已經成為查詢入口時，再建立 map page
