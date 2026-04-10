# AGENTS.md

## Repo Purpose

這是一個用來承接每日 `LLM + agent` 閱讀輸入、並由 OpenAI Codex 持續編譯與維護的知識庫 repo。

它的核心不是收集文章，而是把來源逐步編譯成：

- article cards
- concept pages
- topic maps

## Start Here

1. 先讀 `AGENTS.md`
2. 再讀 `README.md`
3. 再讀 `ARCHITECTURE.md`
4. 再讀 `docs/README.md`
5. 開始工作前，先看 `index.md`

若任務是 ingest 新文章，再讀：

- `docs/ingest.md`
- `docs/compile.md`

若任務是整理結構或做維護，再讀：

- `docs/review.md`
- `docs/query.md`

## Top-Level Map

- `raw/`
  immutable source material
- `wiki/articles/`
  單篇來源的 compiled card
- `wiki/concepts/`
  跨文章穩定概念頁
- `wiki/maps/`
  主題入口與 topic map
- `wiki/people/`
  高頻作者、lab、公司或產品節點
- `index.md`
  repo-level navigation
- `log.md`
  append-only maintenance timeline
- `docs/`
  穩定 workflow 與 operating rules
- `prompts/`
  repo-local prompt assets，承接高頻 human-agent interaction patterns
- `tools/`
  repo-local helper tools，例如 prompt registry lookup

## Source-of-Truth Rules

- 來源事實以 `raw/` 為準。
- 單篇編譯理解以 `wiki/articles/` 為準。
- 跨來源穩定理解以 `wiki/concepts/` 為準。
- 導航入口以 `wiki/maps/` 與 `index.md` 為準。
- 維護歷史只寫進 `log.md`，不要把知識內容塞進 log。

## Shared Operating Rules

- 預設先更新既有頁面，不要急著新增近似重複頁。
- 不要把 raw source 大段改寫後直接搬進 wiki。
- 單篇摘要不等於知識編譯；應補上定位、比較、衝突與 merge candidates。
- 若某個觀察可跨兩篇以上文章重用，應優先 merge 到 `wiki/concepts/`。
- 若某個主題已經成為查詢入口，應更新或建立 `wiki/maps/`。
- `index.md` 應保持薄，只列 stable entry points。
- `log.md` 每次只 append 簡短 maintenance note，不回寫長段分析。
- 若 claim 不確定，明確標示不確定性，並指回對應 `raw/` 檔案。

## Default Codex Workflow

1. 讀 `index.md`，找現有入口與相關概念
2. 讀相關 `wiki/maps/`、`wiki/concepts/`、`wiki/articles/`
3. 必要時回看對應 `raw/` 來源
4. 先決定是更新既有頁，還是新增頁面
5. 更新 article page
6. 將可重用內容 merge 回 concept 或 map page
7. 視需要調整 `index.md`
8. append 一條 `log.md`

## Ingest Rule

當新來源進 repo 時：

1. 先放到 `raw/inbox/` 或 `raw/sources/YYYY/`
2. 補最小 metadata
3. 建立或更新對應 article card
4. 把可重用觀察 merge 到 concepts
5. 必要時更新 maps、index、log

若來源是從 workspace 其他位置匯入：

- 將內容複製到 `raw/sources/YYYY/`，讓 `raw/` 成為此 repo 的 source of truth
- 在 article card 的 source metadata 裡保留原始 workspace path，避免 provenance 斷裂

## Query Rule

回答問題時，優先使用：

1. `wiki/maps/`
2. `wiki/concepts/`
3. `wiki/articles/`
4. `raw/`

若查詢結果具有可重用性，應回寫為：

- concept update
- map update
- 新 article-level synthesis

## File Responsibilities

- `README.md`
  repo overview 與邊界
- `ARCHITECTURE.md`
  結構分層與 source-of-truth
- `docs/README.md`
  workflow doc 入口
- `docs/ingest.md`
  新來源進 repo 的規則
- `docs/compile.md`
  article -> concept/map 的編譯規則
- `docs/review.md`
  review / cleanup 規則
- `docs/query.md`
  查詢與回寫規則
- `prompts/README.md`
  prompt assets 的人類可讀入口與使用原則
- `prompts/index.json`
  prompt assets 的 machine-readable registry
- `tools/list-prompts`
  prompt registry 的最小查詢工具

## Biases

- prefer synthesis over accumulation
- prefer merge over duplication
- prefer durable navigation over exhaustive indexing
- prefer explicit provenance over confident guessing
