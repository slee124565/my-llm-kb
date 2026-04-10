# Effective Harnesses for Long-Running Agents

## Source

- URL: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
- Author: Anthropic Engineering
- Published: 2025-11-26
- Captured: 2026-03-25
- Raw file: `raw/sources/2026/2026-03-25-claude-effective-harnesses-for-long-running-agents.md`

## Main Claims

- 單靠 compaction 不足以支撐多 context window 的長任務；agent 仍需要 initializer、feature list、progress artifact 與明確 session protocol
- 長任務常見失敗模式包括：一次做太多、在中途留下髒狀態、過早宣告完成、沒有做 end-to-end verification
- progress file、git history、init script 與 feature list 這些 artifact，可顯著降低新 session 的重新定向成本
- 把 agent 限制在一次只推進一個 feature，並要求 session 結束前留下乾淨狀態，是長任務穩定性的關鍵

## Why It Matters

這篇把 externalized state 從抽象概念落成具體 harness 設計，對 repo-based agent work 特別重要。它也是 concept layer 裡「外部化記憶」與「長任務治理」之間的橋接來源。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agents](../maps/long-running-agents.md)

## Tensions Or Disagreements

- 文章偏向 coding agent 場景，對 research、ops、knowledge work 等非 coding 代理尚未完整泛化
- 它強調 session artifact，但沒有處理 artifact 本身品質退化與過期治理

## Open Questions

- feature list、progress log、spec 之間的最小 contract 要多嚴格才夠
- context reset 與 continuous session 應如何選擇
- 哪些 artifact 應 machine-readable，哪些保留人類可讀即可

## Merge Candidates

- compaction alone is not enough for long-running agents
- progress artifacts reduce reorientation cost across sessions
- one-feature-at-a-time plus clean state beats broad, under-verified progress
