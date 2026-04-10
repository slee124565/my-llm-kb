---
id: conflict-review
purpose: separate real conflicts from framing differences uncertainty and revision pressure
use_when:
  - a new source appears to disagree with existing repo understanding
  - the user wants a conflict-focused review
inputs:
  - new source
  - relevant article concept and map pages
outputs:
  - real conflicts
  - contextual differences
  - recommended revisions
  - follow-up verification needs
related_prompts:
  - compare-article-to-existing
  - topic-update
  - repo-maintenance-review
tags:
  - review
  - conflict
  - uncertainty
---

# Conflict Review

## Use When

當新來源和你對 repo 現有理解的印象不一致，或你懷疑某些 claim 彼此衝突。

## Goal

把衝突、不確定性、語境差異與需要 revision 的地方分開處理。

## Prompt

```md
這篇內容和 repo 既有理解可能不同。請幫我做一次 conflict review。

請先找出最相關的 article、concept、map，再判斷：
1. 哪些是真正的 claim 衝突
2. 哪些只是 framing 不同或適用語境不同
3. 哪些 source metadata 或表述仍然不夠確定
4. 哪些 concept page 應該修文，而不是只新增一條 observation

最後請輸出：
- Real conflicts
- Contextual differences
- Uncertainties
- Recommended revisions
- What to verify next
```

## Expected Output

- Real conflicts
- Contextual differences
- Uncertainties
- Recommended revisions
- What to verify next

## Notes

- 不要把所有差異都判成衝突
- 若資訊不足，應明確指出需要回到 raw source 補查
