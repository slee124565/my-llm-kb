---
id: repo-maintenance-review
purpose: review repo structure for cleanup merge opportunities and navigation improvements without ingesting new sources
use_when:
  - there is no new source to ingest
  - the user wants to improve repo structure and navigability
inputs:
  - index
  - maps
  - concepts
  - recent article cards
outputs:
  - structure issues
  - cleanup suggestions
  - top next actions
related_prompts:
  - topic-update
  - compare-article-to-existing
  - ingest-review
tags:
  - review
  - maintenance
  - structure
---

# Repo Maintenance Review

## Use When

當天沒有新來源要 ingest，但你想讓 repo 結構更清楚、更可導航、更不重複。

## Goal

做一次結構層面的 maintenance review，找出該 merge、拆分、升級或收斂的地方。

## Prompt

```md
今天不 ingest 新文章。請直接對 repo 做一次 maintenance review。

請先讀 index、相關 maps、concepts、最近新增的 article cards，再判斷：
1. 哪些 article page 太厚，應把內容 merge 回 concept
2. 哪些 concept 開始變成查詢入口，值得升級成 map
3. 哪些 map 已經過薄、過厚，或入口不清楚
4. 哪些 recurring entity 值得開始寫進 wiki/people
5. 哪些地方有重複、命名漂移、或 provenance 不清

最後請輸出：
- Structure issues
- Merge opportunities
- Map / people candidates
- Cleanup suggestions
- Top 3 next actions
```

## Expected Output

- Structure issues
- Merge opportunities
- Map / people candidates
- Cleanup suggestions
- Top 3 next actions

## Notes

- maintenance review 應聚焦結構，不要退化成全文巡覽摘要
