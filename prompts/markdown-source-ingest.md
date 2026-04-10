---
id: markdown-source-ingest
purpose: classify and ingest a markdown source while preserving provenance and naming accuracy
use_when:
  - the source already exists as a markdown file
  - the source comes from another workspace folder
inputs:
  - source path
  - why it should enter the repo
  - desired emphasis such as ingest compare merge or review
outputs:
  - source classification
  - provenance decision
  - raw/article/concept action
  - naming recommendation
related_prompts:
  - compare-article-to-existing
  - topic-update
  - ingest-review
tags:
  - ingest
  - markdown
  - provenance
---

# Markdown Source Ingest

## Use When

當來源本身已經是 `.md` 檔，例如 transcript、整理稿、workspace 其他位置匯出的文章或筆記。

## Goal

把 markdown source 當成候選來源處理，同時保留 provenance，並判斷它應該落在 article、concept，還是只停在 raw layer。

## Prompt

```md
這個 markdown 檔請當成 source ingest 候選：

- source path: ______
- 我想收它的原因：______
- 這次我想偏重：ingest / compare / merge / review

請先讀這個 md 檔，再對照 repo 裡既有 article、concept、map，幫我判斷：
1. 它應該被視為單一 source、概念增量，還是只是工作草稿
2. 是否值得正式複製進 raw/sources/
3. 是否應新增 article card，或只更新既有頁面
4. 哪些 provenance 必須保留

如果外部檔名、標題、正文內容彼此不一致，請明確標示，不要直接沿用錯誤命名。
```

## Expected Output

- Source classification
- Provenance decision
- Raw/article/concept action
- Naming recommendation
- Merge candidates
- Uncertainties

## Notes

- 不要因為來源已是 markdown 就跳過 source-of-truth 判斷
- 若它本身是跨多篇綜合整理，先判斷是否更像 concept 素材，而不是直接做 article card
