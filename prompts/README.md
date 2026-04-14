---
id: prompts-index
purpose: index reusable prompt assets for repo-local human-agent collaboration
use_when:
  - choosing a prompt asset for an ingest, review, compare, or maintenance task
inputs:
  - current task intent
  - source type
  - desired output shape
outputs:
  - recommended prompt file
related_prompts:
  - ingest-source
  - markdown-source-ingest
  - ingest-review
  - repo-maintenance-review
tags:
  - prompts
  - index
  - workflow
---

# prompts

這裡放的是可重用的 prompt assets。

用途不是展示「漂亮提示詞」，而是把你和 agent 的高頻互動方式 externalize 成 repo-local interface，讓它們可以被：

- 直接複製使用
- 持續修訂
- 被 agent 讀取與引用
- 跟 repo workflow 一起演化

使用原則：

- 優先選最貼近當前任務的 prompt，不要每次都用萬用 prompt
- prompt 的目標應是驅動 repo-level 判斷，而不只是重做摘要
- 若來源已經是 `.md`，優先使用 markdown-source 類 prompt
- 若任務重點是 merge、結構調整或衝突判斷，優先用 review 類 prompt

frontmatter schema：

- `id`
  prompt 的穩定識別名稱
- `purpose`
  這個 prompt 要驅動什麼判斷
- `use_when`
  什麼情境下最適合使用
- `inputs`
  使用時通常要提供的資訊
- `outputs`
  預期 agent 回傳的結果類型
- `related_prompts`
  常見的下一步 prompt，幫助人類或 agent 繼續往下走
- `tags`
  幫助 agent 或人類快速篩選的分類標籤

設計原則：

- schema 保持薄，先追求可讀與可選用，不先做複雜 registry
- frontmatter 不是替代 prompt 內容，而是讓 agent 更容易判斷「哪個 prompt 最合適」
- 若未來 prompt 變多，再考慮增加 `priority`、`related_prompts` 或 `anti_use_when`

查詢方式：

- repo 入口：[root README](../README.md)
- prompt 導航：[prompts/README.md](README.md)
- machine-readable registry：[index.json](index.json)
- CLI 查詢工具：`tools/list-prompts`

`tools/list-prompts` 常用例子：

- `tools/list-prompts`
- `tools/list-prompts --tag ingest`
- `tools/list-prompts --search markdown`
- `tools/list-prompts --id markdown-source-ingest`
- `tools/list-prompts --related markdown-source-ingest`

建議入口：

- [ingest-source.md](ingest-source.md)
  收一篇新來源，建立或更新 article card
- [markdown-source-ingest.md](markdown-source-ingest.md)
  當來源本身已經是 markdown 檔
- [ingest-review.md](ingest-review.md)
  回顧今天 new ingest 的增量、重複與 merge 建議
- [adoption-follow-up.md](adoption-follow-up.md)
  將高價值 article ingest 轉成 workflow / habit adoption
- [compare-article-to-existing.md](compare-article-to-existing.md)
  比較一篇新文章和 repo 既有內容
- [topic-update.md](topic-update.md)
  以某個主題為中心更新 concept / map
- [conflict-review.md](conflict-review.md)
  專門檢查衝突、不確定性與 revision 壓力
- [repo-maintenance-review.md](repo-maintenance-review.md)
  沒有新來源時，做 repo structure / cleanup review
