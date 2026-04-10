# Ingest Workflow

**目標**

把新文章穩定地從「剛讀到」推進到「已納入知識庫」。

**日更流程**

1. 把新來源先放到 `raw/inbox/`
2. 補最小 metadata
   - title
   - source URL
   - author
   - published date if known
   - captured date
3. 若確定值得保留，將來源整理到 `raw/sources/YYYY/`
4. 在 `wiki/articles/` 建立對應 article card
5. 更新相關 `wiki/concepts/` 或 `wiki/maps/`
6. 在 `log.md` append 一條簡短紀錄

**命名建議**

- raw source:
  `raw/sources/2026/2026-04-10-title-slug.md`
- article card:
  `wiki/articles/title-slug.md`

**保留標準**

以下情況值得 ingest：

- 提出新的 agent pattern
- 對既有概念有更清楚的 framing
- 有可與其他來源比較的主張
- 對你自己的工作流有直接影響

以下情況可先留在 inbox，不急著編譯：

- 純新聞轉述
- 內容重複度很高
- 暫時看不出對你的知識結構有何影響
