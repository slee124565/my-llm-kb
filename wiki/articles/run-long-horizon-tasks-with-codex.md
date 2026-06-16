# Run Long Horizon Tasks With Codex

## Source

- URL: https://developers.openai.com/blog/run-long-horizon-tasks-with-codex/
- Author: Derrick Choi
- Publisher: OpenAI Developers
- Published: 2026-02-23
- Captured: 2026-06-16
- Raw file: `raw/sources/2026/2026-04-04-run-long-horizon-tasks-with-codex.md`
- Original workspace path: `myBrainFood/blog/2026-04-04-run-long-horizon-tasks-with-codex/2026-04-04-run-long-horizon-tasks-with-codex.md`

## Main Claims

- 長任務 coding agent 的關鍵能力正在從「單次回答聰明」轉向「可維持時間跨度」。文章用一個約 25 小時、約 13M tokens、約 30k 行程式碼的 Codex 實驗說明：真正有價值的不是 trace 很長，而是 agent 能持續遵守 spec、完成 milestone、跑驗證、修復失敗，並把結果保持在可檢查狀態。
- 長程 coherence 不是只靠大 prompt，而是靠 agent 迴圈（agent loop）和外部化狀態（externalized state）共同支撐。Codex 的 plan、edit、run tools、observe、repair、update docs、repeat 迴圈，讓錯誤、diff、log、測試結果和文件成為 agent 可以反覆利用的回饋面。
- Durable project memory 是這次實驗最重要的技法。作者把 spec、plan、constraints、status 拆成 `prompt.md`、`plans.md`、`implement.md`、`documentation.md`，讓 agent 不必靠單次對話記住所有上下文，而是反覆回讀 repo 中的任務契約、驗證標準與進度紀錄。
- `plans.md` 的價值不只是列待辦，而是把開放式任務切成可驗證 checkpoint。每個 milestone 應有 acceptance criteria、validation commands、失敗先修復再前進的規則，以及避免反覆搖擺的 decision notes。
- `documentation.md` 把進度、決策、run command、demo flow、known issues 變成 audit log。這讓人類可以離開數小時後回來接手，也讓下一個 agent session 不必從聊天記憶裡猜發生過什麼。
- 長程 Codex 工作的成熟模式不是 fire-and-forget，而是 delegation with guardrails：人類定義目標、約束、驗證與中途 steering 點；agent 承接 routine implementation、validation、repair 與 documentation update。

## Why It Matters

這篇把 `my-llm-kb` 既有的 Codex workflow、`/goal`、skills、repo-local system of record 連成一個更具體的長任務操作模型。它的增量不在於「Codex 可以跑 25 小時」這個數字，而在於展示 25 小時要可靠，必須有文件化的任務邊界、milestone 驗證、執行 runbook、可審計狀態，以及人類可以中途 steer 的產品介面。

對工程管理與 AI 導入來說，這篇提供了一個很實用的判準：不要只問模型是否能自己做很久，而要問這個長任務是否有明確的 source of truth、可重跑的 validation、失敗修復規則、progress evidence、handoff artifact 與 review surface。沒有這些，長時間執行只會放大漂移、錯誤和 review 成本。

它也讓 Codex app 的產品 primitives 更容易被理解。Parallel threads、Skills、Automations、worktrees、Plan Mode 不是零散功能，而是把長任務拆成隔離、程序記憶、背景延續、reviewable diff 和可對齊 milestone 的控制面。

## Relation To Existing Concepts

- [Codex Workflows](../maps/codex-workflows.md): 本文把 Codex workflow 從「怎麼提示 agent」推進到「怎麼設計 25 小時仍可 review 的 repo-local operating system」。核心是 spec、plan、runbook、documentation、verification loop 與 worktree / thread isolation。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): 文章提供了長任務 harness 的具體 recipe：task contract、milestone acceptance criteria、validation commands、stop-and-fix rule、decision notes、status documentation 與 human steering。
- [Externalized Agent State](../concepts/externalized-agent-state.md): `prompt.md`、`plans.md`、`implement.md`、`documentation.md` 是一組 state surfaces，把目標、進度、決策和驗證證據移出 context window，讓 agent 可以重新載入並維持方向。
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md): 本文強化 repo-local system of record 的工程版本：spec 不只是背景資訊，而是 agent 應遵守的任務合約；documentation 不只是交付說明，而是長任務的可接手記憶。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): Codex app、CLI session、worktrees、skills、automations、Plan Mode 與 repo files 共同構成 runtime surface；它們分別承擔 isolation、tool execution、procedure reuse、background continuation、planning alignment 與 state persistence。
- Related prior sources: [Using PLANS.md for Multi-Hour Problem Solving](using-plans-md-for-multi-hour-problem-solving.md), [Codex /goal Playbook](codex-goal-playbook.md), [Getting The Most Out Of Codex](getting-the-most-out-of-codex.md), [Using Skills To Accelerate OSS Maintenance](using-skills-to-accelerate-oss-maintenance.md), [Best Practices For Claude Code](best-practices-for-claude-code.md)

## Tensions Or Disagreements

- 25 小時 run 很能展示上限，但不能直接代表一般團隊的預設工作法。長時間 autonomy 只有在 spec、validation、rollback、review 和 handoff 都完整時才值得；否則人類 review 可能反而更重。
- 文章強調 durable project memory，但這也會帶來文件治理成本。`prompt.md`、`plans.md`、`implement.md`、`documentation.md` 若沒有人維護，很快會變成過期狀態，讓 agent 讀到錯誤方向。
- Plan Mode 和 milestone planning 適合高不確定、多檔案、多階段的工作；對小改動或已知修復，如果硬套完整長任務儀式，會增加不必要摩擦。
- 實驗中的 design tool 是高複雜、高可視化任務，驗證方式包含 tests、lint、typecheck、build 和 demo flow。其他領域若缺少可重跑驗證，不能直接假設相同長程可靠性。
- 「teammate you can trust」仍需要明確拆分信任邊界。routine implementation 和驗證修復可交給 agent，但產品方向、架構取捨、安全/資料風險、是否真的達到業務目標，仍應有 human supervisor 判斷。

## Open Questions

- 什麼類型的任務值得升級成 `prompt.md` / `plans.md` / `implement.md` / `documentation.md` 這種完整長任務 file stack？
- 對一般 repo 來說，最小可用的 durable project memory 是一份 `PLANS.md`，還是需要拆成 spec、plan、runbook、status 四個文件？
- 長任務 validation 應如何衡量：只看 final demo 成功，還是要保存每個 milestone 的 command transcript、修復紀錄與 decision notes？
- Codex app 的 Automations、Goals、Plan Mode、Skills、worktrees 應如何分層，才不會讓 routine work 變成過度複雜的 orchestration？
- 當非工程使用者也能用 Codex build 時，哪些 guardrails 應由產品內建，哪些仍應由 repo-local 文件和人類 reviewer 承擔？

## Merge Candidates

- Long-horizon Codex work should be judged by sustained spec-following, milestone verification, repair behavior, and reviewable artifacts, not by run length alone.
- Durable project memory turns spec, plan, runbook, progress, decisions, validation commands, and known issues into repo-local state surfaces the agent can reload.
- A long-running Codex task benefits from a file stack: `prompt.md` for target and constraints, `plans.md` for milestones and acceptance criteria, `implement.md` for execution discipline, and `documentation.md` for status and audit history.
- Plan Mode and milestone files are most valuable when the task is open-ended, multi-phase, or high-risk; they should stay lightweight for small, easily verified changes.
- Codex app primitives such as threads, skills, automations, worktrees, and plan mode should be treated as harness controls for continuity, isolation, procedure reuse, background execution, and human steering.
