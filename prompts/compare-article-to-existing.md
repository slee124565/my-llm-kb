---
id: compare-article-to-existing
purpose: compare a new article against existing repo pages and decide whether it is net-new duplicate or revision pressure
use_when:
  - a new source looks similar to existing articles or concepts
inputs:
  - new article or source
  - closest relevant pages in the repo
outputs:
  - difference analysis
  - recommended write target
  - duplicate versus net-new judgment
related_prompts:
  - ingest-source
  - markdown-source-ingest
  - topic-update
  - conflict-review
tags:
  - compare
  - article
  - deduplication
---

# Compare Article To Existing

## Use When

當你看到一篇新文章，但不確定它對 repo 來說到底是增量、重複，還是 revision trigger。

## Goal

把單一新來源和 repo 現有頁面做差異比對，避免重複 ingest 或重複建 card。

## Prompt

```md
幫我比較這篇新文章和 repo 裡既有相關頁面。

請先找出最相關的 article、concept、map，再回答：
1. 哪些內容是重複
2. 哪些是新增 framing 或新增 evidence
3. 哪些會改變既有理解
4. 這篇最適合更新哪一頁
5. 是否值得新增 article card，還是只更新現有頁

請不要只做摘要。我要的是差異判斷與回寫建議。
```

## Expected Output

- Closest existing pages
- Repeated ideas
- Net-new ideas
- Revision pressure
- Recommended write target

## Notes

- 若新文章只是提供相同主張的另一個例子，可保留為來源，但不一定要新增 article card
