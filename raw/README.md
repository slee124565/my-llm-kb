# raw

`raw/` 放 immutable source material。

結構：

- `raw/inbox/`
  剛收進來、尚未正式編譯或尚未判斷的暫存來源
- `raw/sources/`
  已決定保留的 canonical 來源材料

原則：

- 不在原地改寫來源內容
- 保留最小 provenance
- 圖片、截圖、轉錄稿可和來源一起存放
- 從 `raw/inbox/` 正規化到 `raw/sources/YYYY/` 後，確認 canonical source 完整保存，即刪除 inbox 副本
- article card 應引用 `raw/sources/YYYY/` 作為 raw source；inbox path 不應作為已 ingest 文章的長期 metadata

`raw/inbox/` 的 markdown source 建議使用簡易版 frontmatter：

```yaml
---
source_path:
captured:
status: inbox
topic_hint: []
why_it_matters:
---
```

欄位說明：

- `source_path`
  原始 workspace path。這是最重要的 provenance。
- `captured`
  匯入到 inbox 的日期，使用 `YYYY-MM-DD`。
- `status`
  預設固定為 `inbox`。
- `topic_hint`
  給 agent 的初步主題提示，例如 `["codex", "local-agents"]`。
- `why_it_matters`
  你的一句話判斷，說明這份材料為什麼值得進 repo。

範例：

```yaml
---
source_path: /Users/lee/ws/myBrainFood/blog/example/example.md
captured: 2026-04-10
status: inbox
topic_hint: ["codex", "openclaw"]
why_it_matters: 提供 local personal agent 與 Codex workflow 的對照視角
---
```

若要批次處理明確 filename 的 inbox 檔案，可直接用這條短版 prompt：

```md
請批次處理以下 raw/inbox 檔案，依 `prompts/markdown-source-ingest.md` 做 repo-aware ingest judgment，逐檔告訴我保留、升級、merge 或留在 inbox，最後再給我一段今天這批來源的 summary。
```
