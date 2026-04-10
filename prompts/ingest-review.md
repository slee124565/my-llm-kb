---
id: ingest-review
purpose: review today's newly ingested articles for net-new signal merge pressure and structural impact
use_when:
  - one or more new article cards were added or updated today
inputs:
  - today's new or updated article cards
  - existing concepts maps and index
outputs:
  - daily ingest synthesis review
  - article verdicts
  - concept and map update suggestions
related_prompts:
  - topic-update
  - conflict-review
  - repo-maintenance-review
tags:
  - review
  - ingest
  - synthesis
---

# Ingest Review

## Use When

當天已經有一批 new ingest article，想做一次 daily synthesis review，而不是逐篇重看摘要。

## Goal

判斷今天這批新增來源對 repo 的實際增量、重複度、merge 壓力與結構影響。

## Prompt

```md
請針對今天 new ingest 的 article 做一次 repo-aware daily ingest review。

先讀今天新增或更新的 article cards，再對照現有 concepts、maps、index。
不要重做摘要，請專注在知識庫層級的判斷。

請回答：
1. 今天新增了哪些真正有增量的觀察
2. 哪些內容只是重複既有理解
3. 哪些 article 應該只停留在 article layer
4. 哪些觀察應該 merge 到既有 concept pages
5. 哪些主題已經接近需要建立或更新 map page
6. 今天的 ingest 是否改變了 repo 對某些主題的理解
7. 哪些 claim、framing、source metadata 仍然不確定，需要後續補查

對每篇 article，請給我一句話 verdict：保留、merge、觀察中、或可能重複。

最後請輸出：
- Today’s signal
- Article-by-article verdict
- Merge candidates
- Concept/map updates to consider
- Uncertainties / follow-ups
- Recommended next action
```

## Expected Output

- Today’s signal
- Article-by-article verdict
- Merge candidates
- Concept/map updates to consider
- Uncertainties / follow-ups
- Recommended next action

## Notes

- review 的目標是 repo synthesis，不是二次摘要
- 如果當天實際上只有 1 篇新來源，也應明確說明「今天的 signal 很窄」
