# Repository Knowledge As System Of Record

## Summary

Repository knowledge as system of record 指的是：讓 agent 所需的長期上下文、設計規則、計畫、品質標準與關鍵決策，都以 repo-local、versioned、可交叉連結的 artifact 形式存在，而不是散落在 chat、文件雲端或人腦中。

## Why It Matters

對 agent 來說，看不到的知識幾乎等於不存在。若重要規則、架構思路、驗證方式與執行計畫不在 repo 中，後續 session 或其他 agent 就很難可靠接手。

## Current Framing

- `AGENTS.md` 應作為入口與 table of contents，而不是冗長百科
- 結構化 `docs/`、execution plans、quality docs 與 references 應承擔 deeper source-of-truth
- `PLANS.md` 這類 self-contained living document 可把長任務脈絡固定下來
- 若 execution plan 要成為真正的 repo-local system of record，它還必須明確寫出 paths、interfaces、dependencies、驗證方式與 recovery path，而不是只寫高層意圖
- repository-local artifacts 的價值，不只是保存知識，而是讓 agent 可以讀、驗證、修改、延續
- `WORKFLOW.md` 代表 repo system of record 往 process layer 延伸：不只保存技術規則，也保存 agent 應如何接 issue、操作 tracker、交付 review packet 與回報 evidence
- 修訂 execution plan 時同步更新 living sections，並在底部留下變更原因，是避免 repo-local knowledge drift 的必要紀律
- system of record 不只是「有文件」，還要「文件可以被快速掃讀」；標題、takeaway、段落長度與一致術語都是讓後續 agent 接手的基礎設施
- OpenAI GPT-5.3 Codex prompt guidance reinforces that `AGENTS.md` should be a repo-local steering surface: it should route the agent to deeper docs, protect user work, define validation expectations, and keep global prompts from absorbing all repo-specific workflow detail

## Signals From Recent Articles

- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [OpenAI Symphony Codex Orchestration](../articles/openai-symphony-codex-orchestration.md)
- [Introducing Codex](../articles/introducing-codex.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [What Makes Documentation Good](../articles/what-makes-documentation-good.md)
- [OpenAI Prompt Guidance - GPT-5.3 Codex](../articles/openai-prompt-guidance-gpt-5-3-codex.md)

## Open Questions

- `AGENTS.md`、`docs/`、`PLANS.md` 的最佳切分邊界是什麼
- 哪些 repo 需要完整 knowledge base，哪些只需要最小入口
- 如何防止 repo-local knowledge 自身發生 drift 與過期
- 哪些文件應該用更嚴格的 skim-first 標準，哪些可以保留較厚的敘述層
- 當 process contract 同時被 issue tracker 和 repo 持有時，哪一邊才是狀態轉移與交付規則的 source of truth
- 哪些 Codex behavior 應該留在 global prompt，哪些應該下沉到 repo-local `AGENTS.md`、`docs/`、prompt asset 或 task plan

## Related Pages

- [Externalized Agent State](externalized-agent-state.md)
- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Prompt Migration And Agent Steerability](prompt-migration-and-agent-steerability.md)
- [Codex Workflows](../maps/codex-workflows.md)
