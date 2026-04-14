---
id: adoption-follow-up
purpose: turn a newly ingested article into workflow changes habit changes and a concrete next adoption step
use_when:
  - a high-value article card was just added or updated
  - the user wants to turn understanding into practice
inputs:
  - target article card
  - related concept or map pages if relevant
  - optional current workflow or habit to compare against
outputs:
  - knowledge delta
  - workflow delta
  - habit delta
  - next adoption experiment
  - recommended repo writeback target
  - issue follow-up decision
related_prompts:
  - ingest-source
  - markdown-source-ingest
  - topic-update
tags:
  - adoption
  - workflow
  - habit
  - follow-up
---

# Adoption Follow-Up

## Use When

當一篇文章已經完成 ingest，但你不要停在理解，而是要把它轉成新的做法、習慣或下一次真實任務中的實驗。

## Goal

辨認這篇文章真正帶來的增量，並把它編譯成可採用的 workflow / habit change，而不是只留下「這篇很重要」的印象。

## Prompt

```md
這篇文章已經 ingest 完成。請不要重做摘要，而是幫我做 adoption follow-up。

目標 article：
______。

如果有需要，先讀相關 concept / map，但重點放在：
1. 這篇真正新增的 knowledge delta 是什麼
2. 它要求我改變哪個 workflow
3. 它要求我開始養成什麼新習慣，或停止什麼舊習慣
4. 下一次在哪個具體情境，我最值得刻意練習這個新做法
5. 什麼證據算 adoption 成功
6. 這個結果應該只留在 article level，還是要回寫成 concept / map / prompt / checklist / rule
7. 是否值得建立 GitHub adoption issue 來承接短期實驗追蹤；若不值得，也請明說原因

請把輸出分成：
- knowledge delta
- workflow delta
- habit delta
- next adoption experiment
- stop doing
- success criteria
- recommended writeback target
- issue follow-up decision

不要給空泛建議。請盡量讓每一點都能在下一次真實工作中被執行或驗證。
```

## Expected Output

- Knowledge delta
- Workflow delta
- Habit delta
- Next adoption experiment
- Stop-doing recommendation
- Success criteria
- Recommended writeback target
- Issue follow-up decision

## Notes

- governance、writeback target 與 GitHub issue 建立門檻，遵循 `docs/adoption.md`
- adoption 的重點是「下一次怎麼做得不同」，不是重述文章內容
- 若文章只有知識增量，沒有明確 workflow / habit value，可以明說不建議做 adoption
