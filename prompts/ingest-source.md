---
id: ingest-source
purpose: ingest a new source into raw and article layers with repo-aware merge judgment
use_when:
  - a new article, interview, paper note, or transcript should enter the repo
inputs:
  - source content or path
  - why it matters
  - optional topic emphasis
outputs:
  - ingest verdict
  - raw/article action
  - related concepts and maps
  - merge candidates
related_prompts:
  - compare-article-to-existing
  - topic-update
  - ingest-review
tags:
  - ingest
  - source
  - article
---

# Ingest Source

## Use When

當你今天看到一篇新文章、訪談、paper note 或 transcript，想先把它正式收進 repo。

## Goal

把新來源從「剛看到」推進到 `raw/` + `wiki/articles/`，並指出它應該連到哪些既有 concept / map。

## Prompt

```md
幫我 ingest 這篇來源到 repo。

我覺得它重要，因為 ______。

請先檢查 repo 裡是否已有高度重複的 article、concept 或 map。
如果值得保留，請：
- 保存 source 與最小 provenance
- 建立或更新對應 article card
- 指出它最應該連到哪些既有 concept / map
- 明確標出哪些觀察只是 article-level，哪些值得 merge

不要只做摘要。請把重點放在：
1. 這篇的新增價值
2. 它與既有知識庫的關係
3. 是否值得升級成 concept / map 層的更新
```

## Expected Output

- Ingest verdict
- Proposed raw/article action
- Main article-level claims
- Related concepts/maps
- Merge candidates
- Uncertainties

## Notes

- 若來源價值不夠高，可只留在 `raw/inbox/` 或保留 provenance 而不建 article card
- 若來源和既有 article 高度重複，應優先更新既有頁而不是新增近似頁
