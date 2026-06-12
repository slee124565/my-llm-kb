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
4. 確認 `raw/sources/YYYY/` 已完整保存 canonical source 後，刪除原本 `raw/inbox/` 副本
5. 在 `wiki/articles/` 建立對應 article card
6. 更新相關 `wiki/concepts/` 或 `wiki/maps/`
7. 在 `log.md` append 一條簡短紀錄

**Inbox Retention Rule**

- `raw/inbox/` 是暫存與判斷區，不是長期備份區。
- 一篇文章一旦被正式 ingest，canonical raw source 應只保留在 `raw/sources/YYYY/`。
- article card 的 `Source` 區塊應指向 canonical `raw/sources/YYYY/` 檔案，不再引用已刪除的 inbox path。
- 只有尚未判斷、尚未正規化，或正規化失敗需要重試的來源，才留在 `raw/inbox/`。
- 若來源來自 workspace 其他 repo 或外部路徑，保留原始 path 作為 provenance metadata；不要用 `raw/inbox/` 複製品來承擔 provenance。

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
