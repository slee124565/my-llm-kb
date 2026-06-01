# Codex /goal Playbook

## Source

- URL: https://github.com/openai/openai-cookbook/tree/main/examples/codex
- Related official docs: https://developers.openai.com/codex/prompting#goal-mode
- Author: Unknown
- Published: Unknown
- Captured: 2026-06-01
- Raw file: `raw/sources/2026/2026-06-01-codex-goal-playbook.md`
- Original path: `/Users/lee230917/Downloads/Codex_Goal_Playbook.md`

## Main Claims

- Codex `/goal` 不應只是一句「請一直做完」的長 prompt，而應搭配外部任務清單、設計文件、phase、驗收條件與 commit 節點，讓 agent 的長任務推進有可檢查的軌道。
- Checklist 分批處理法適合逆向程式碼、批次分析與大量資料整理：每個 item 有 `todo` / `doing` / `done` 這類狀態，Codex 每次只處理一小批，完成後更新狀態、測試、commit。
- Design Doc + Phases 執行法適合重構與架構改造：先產生施工圖，再把大任務拆成 phase，每個 phase 都有明確驗收條件，未通過就不能進入下一階段。
- 對長任務而言，commit 不是單純版本管理動作，而是進度邊界與交接點；它把「這一批已完成且驗證過」變成後續 session 能信任的 state。
- 核心原則是把 workflow 寫進可追蹤文件，而不是期待 Codex 在 context 或模型記憶裡穩定記住流程；`Design Doc`、`Checklist`、`Task JSON`、`Acceptance Criteria` 才是可恢復的控制面。
- 官方 Codex goal mode 的定位是讓 Codex 追蹤一個持久目標與可判斷的完成條件；這份 playbook 的增量，是把完成條件落成更細的 local artifacts 與 phase gates。

## Why It Matters

這份 playbook 把 `/goal` 從產品功能轉成一套可操作的長任務治理方法。它提醒使用者：Goal mode 本身提供持久目標，但真正讓長任務穩定的是外部化的進度、驗收與提交節奏。對 coding agent 來說，最危險的不是任務大，而是「大任務沒有分批證據」；Checklist 與 Phases 讓 Codex 可以小步完成、留下紀錄、在驗證失敗時停住。

對 `my-llm-kb` 這類 repo-local workflow 也有直接價值：當 ingest、review、批次修正或跨 repo 掃描變長時，不應只靠聊天上下文推進，而應把 batch list、phase contract 與驗證結果寫回 repo artifact。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): 這份 playbook 是輕量版 harness recipe，把長任務拆成 batch / phase / acceptance criteria / test / commit。
- [Externalized Agent State](../concepts/externalized-agent-state.md): `analysis_tasks.json`、`auth_refactor_plan.md` 與 phase 驗收條件都是把進度和決策放出 context window 的 state surface。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): 人類的角色從逐步操作轉成定義 batch size、驗收條件、停損規則與何時 commit。
- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md): `/goal` prompt 應該描述 outcome、約束、驗收與 stop gate，而不是只堆疊「努力完成」式指令。
- [Codex Workflows](../maps/codex-workflows.md): 這份 playbook 可作為使用 `/goal` 執行長任務的入口範例，補在 PLANS.md 與 Codex app Goals 之間。

## Tensions Or Disagreements

- Checklist 法很適合可列舉的批次任務，但對探索型架構問題可能太機械；這類任務更需要 design doc、prototype phase 與明確風險回復方式。
- 每批完成後 commit 可以提高可恢復性，但如果驗證不足或 commit message 太粗，反而會把不完整的狀態包裝成「已完成」。
- 把 workflow 寫進文件能降低 drift，但文件本身也會腐化；若 Codex 更新 task JSON 或 plan 時沒有同步記錄原因，後續 session 仍可能誤讀狀態。
- `/goal` 的完成條件若太抽象，Codex 可能過早宣布完成；若太細碎，則可能讓目標退化成僵硬流程而失去中途調整能力。

## Open Questions

- 哪些任務應使用 Checklist，哪些應升級成 Design Doc + Phases？
- `/goal` 的 goal text、task JSON、plan doc 與 repo `AGENTS.md` 之間，責任邊界應如何切？
- commit gate 應該要求哪些最低驗證，才足以支撐下一批或下一個 phase？
- 對跨 repo 或跨工具長任務，phase progress 應該留在單一 repo、workspace-level plan，還是 issue tracker？

## Merge Candidates

- Codex `/goal` should be paired with external artifacts such as checklists, task JSON, design docs, phases, acceptance criteria, tests, and commits.
- For batch analysis work, use a small `todo` / `doing` / `done` list and require Codex to update it after each verified batch.
- For refactors or architecture changes, start with a design document, split work into phases, and gate each phase on explicit acceptance criteria.
- Commit boundaries are long-running-agent state boundaries: they mark verified progress that future sessions can trust.
- The durable rule is: do not ask Codex to remember the workflow; ask Codex to read and maintain the workflow artifact.
