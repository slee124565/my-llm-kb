# Compile Workflow

**目標**

把單篇 source 編譯成可重用知識，而不是停在摘要。

**Article Card 應包含**

- source metadata
- main claims
- why it matters
- relation to existing concepts
- tensions or disagreements
- open questions
- merge candidates

**Article Card Rendering Contract**

- Article card 的 section headings 維持英文，並優先沿用 `wiki/_templates/article.md`：
  `Source`、`Main Claims`、`Why It Matters`、`Relation To Existing Concepts`、
  `Tensions Or Disagreements`、`Open Questions`、`Merge Candidates`。
- `Source` 區塊保留 metadata 原樣；URL、檔名、日期、作者、產品名與專有名詞不要為了中文化而改寫。
- 除 metadata、link target、code、檔名、產品名與必要原文術語外，article card 的說明內容預設使用繁體中文。
- 說明內容採「導讀式編譯」風格，不做逐字翻譯，也不要只列英文摘要。
- 每個 claim 應先讓非工程讀者理解直覺意思，再保留必要技術含義與管理、產品、工程意義。
- 重要英文術語第一次出現時，使用 `中文意思（English）` 格式，例如：評估套件（eval suite）、評分器（grader）、執行紀錄（transcript）、agent 執行框架（agent harness）。
- `Main Claims` 的 bullet 不應只是短句翻譯；每個 bullet 應說清楚這個主張對 agent、產品品質、workflow 或工程管理的意義。
- `Merge Candidates` 也使用繁體中文表述，但保留必要英文術語，方便未來 merge 到 concept / map。

**編譯步驟**

1. 讀 `raw/` 原始來源
2. 查 `index.md` 找既有 topic 入口
3. 讀相關 `wiki/concepts/` 與 `wiki/maps/`
4. 將 source claims 轉成 article card rendering：
   - section headings 使用英文 template
   - body 使用繁體中文導讀式編譯
   - 技術詞以 `中文（English）` 保留
   - 避免逐字翻譯與英文摘要堆疊
5. 建立或更新 `wiki/articles/*.md`
6. 將可重用內容 merge 回對應 concept pages
7. 若此來源改變某個 topic 的入口結構，再更新 map page

**判斷規則**

- 單篇內容只屬於自身脈絡：停留在 article card
- 可跨 2 篇以上文章重用：寫進 concept page
- 已成為查詢入口：寫進 map page

**Article Card Style Check**

- `##` section headings 是否仍為英文 template 標題
- `Main Claims` 是否為繁體中文導讀式 bullet，而不是英文 claim list
- 是否保留必要英文術語與專有名詞
- 是否避免把 raw source 改寫成逐段翻譯
- 是否仍有明確 merge candidates，而不是只做閱讀心得

**避免事項**

- 不要把 article card 寫成 raw source 的改寫版
- 不要把 concept page 寫成 article list
- 不要讓 `index.md` 承擔詳細知識內容
