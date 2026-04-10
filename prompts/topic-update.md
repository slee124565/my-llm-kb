---
id: topic-update
purpose: update a concept or map from a topic-first perspective rather than a single-article perspective
use_when:
  - the user wants to advance a topic such as tool use memory evals or agent workflow
inputs:
  - target topic
  - new source or batch of sources
  - existing concept and map pages
outputs:
  - topic state before
  - concept updates
  - map updates
  - open threads
related_prompts:
  - compare-article-to-existing
  - conflict-review
  - repo-maintenance-review
tags:
  - topic
  - concept
  - map
  - synthesis
---

# Topic Update

## Use When

當你今天想追一個主題，不想被單篇文章牽著走。

## Goal

以主題為中心更新 repo，讓新來源被吸收到 concept / map，而不是只停在 article layer。

## Prompt

```md
我今天想更新 ______ 這個主題。

請先讀現有 concept / map，再吸收這個新來源或這批新來源。
不要把工作停在 article summary，請直接判斷：
1. 現有主題理解的核心是什麼
2. 新來源帶來了什麼新增 framing、例外、或衝突
3. 哪些內容應回寫 concept
4. map 是否需要補入口、重組，或增加 recurring entities

最後請給我：
- Topic state before
- New signal
- Required concept updates
- Required map updates
- Open threads
```

## Expected Output

- Topic state before
- New signal
- Required concept updates
- Required map updates
- Open threads

## Notes

- 若主題材料仍太少，應誠實停留在 article layer，不要過早膨脹 concept / map
