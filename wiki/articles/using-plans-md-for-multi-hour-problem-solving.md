# Using PLANS.md for Multi-Hour Problem Solving

## Source

- URL: https://developers.openai.com/cookbook/articles/codex_exec_plans
- Author: Aaron Friel
- Published: 2025-10-07
- Captured: 2026-03-08
- Raw file: `raw/sources/2025/2025-10-07-openai-using-plans-md-for-multi-hour-problem-solving.md`
- Imported from workspace path: `_todos/2026-03-08-ai-native-engineer-capability-checklist/refs/04-openai-cookbook-codex-exec-plans.md`

## Main Claims

- 對 multi-hour 任務而言，`PLANS.md` / ExecPlan 應是 fully self-contained 的 living document，而不是一次性的設計備忘
- `AGENTS.md` 應定義何時使用 `PLANS.md`，讓 planning contract 成為 repo workflow 的一部分
- 長任務若要讓 novice agent 也能正確接手，計畫文件必須內含目的、脈絡、步驟、驗證、progress、decision log 與 retrospective
- observable outcomes 與 validation instructions 不是附加項，而是 execution plan 的必要部分
- 對高不確定性任務而言，plan 內可顯式納入 prototyping milestones 與 parallel implementations，先降風險再收斂主路徑
- 好的 ExecPlan 不只描述工作項目，還必須明確列出 repository context、interfaces、dependencies、idempotence 與 recovery
- long-running Codex success 的重點不只是思考更久，而是把可恢復、可接手、可驗證的工作脈絡寫回 repo
- revision discipline 也是 contract 本身的一部分：更新 plan 時，必須同步更新 living sections，並留下變更原因

## Why It Matters

這篇補上了 `AGENTS.md -> PLANS.md -> implementation` 之間的 contract，對長任務治理很重要。它讓 `externalized state` 不再只是 progress file，而是進一步變成可執行規格。這次 raw source 補完整後，也讓文章從「plan 要完整」更進一步走到「plan 要如何承接探索、介面定義、修訂紀律與可恢復實作」。

## Relation To Existing Concepts

- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Codex Workflows](../maps/codex-workflows.md)

## Tensions Or Disagreements

- 這套 plan discipline 對 repo 使用者的寫作負擔較高，並非所有任務都值得採用這種完整 ExecPlan
- 若 plan 與實作節奏脫節，living document 反而可能成為新的陳舊 artifact
- 把 prototyping、parallel path、interfaces、recovery 全塞進單一計畫文件，雖然提高可接手性，但也可能讓計畫過厚、維護成本過高

## Open Questions

- ExecPlan 適用的最小任務門檻應如何判斷
- `PLANS.md` 與較輕量的 task contract / progress file 如何分工
- 哪些 repo 應採全文 self-contained plan，哪些只需輕量引用式規格
- prototyping milestone 應在什麼時點升格為正式 implementation path，而不是長期並行存在
- 「單一 self-contained plan」與「拆成多份專門 artifact」之間的最佳切分邊界是什麼

## Merge Candidates

- PLANS.md should be a self-contained living execution document for multi-hour tasks
- AGENTS.md should define when plans are required
- validation, progress, decision logs, and retrospectives are core plan elements, not optional extras
- prototyping milestones and parallel implementations can be first-class parts of a long-running agent harness
- an execution plan should specify repository context, interfaces, dependencies, idempotence, recovery, and revision discipline
