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

**編譯步驟**

1. 讀 `raw/` 原始來源
2. 查 `index.md` 找既有 topic 入口
3. 讀相關 `wiki/concepts/` 與 `wiki/maps/`
4. 建立或更新 `wiki/articles/*.md`
5. 將可重用內容 merge 回對應 concept pages
6. 若此來源改變某個 topic 的入口結構，再更新 map page

**判斷規則**

- 單篇內容只屬於自身脈絡：停留在 article card
- 可跨 2 篇以上文章重用：寫進 concept page
- 已成為查詢入口：寫進 map page

**避免事項**

- 不要把 article card 寫成 raw source 的改寫版
- 不要把 concept page 寫成 article list
- 不要讓 `index.md` 承擔詳細知識內容
