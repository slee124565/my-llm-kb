# Getting Started With Loops

## Source

- URL: https://x.com/i/status/2074208949205881033
- Author: ClaudeDevs @ClaudeDevs
- Published: 2026-07-06
- Captured: 2026-07-07T19:09:15+08:00
- Raw file: `raw/sources/2026/2026-07-06-getting-started-with-loops.md`
- Source note: X.com long-form post / article by the Claude Code team explaining loop types, stop conditions, verification practices, and token-management boundaries for coding-agent work.

## Main Claims

- 這篇把「設計 loops」從模糊口號改成可操作分類：loop 是 agent 重複執行工作循環，直到某個停止條件（stop condition）成立。真正要設計的不是單一句 prompt，而是誰觸發 loop、它如何停止、用哪個 Claude Code primitive、適合哪種任務。
- `Turn-based loops` 是最基本的手動互動 loop：使用者給 prompt，Claude 讀 context、修改、檢查、必要時再試，最後回報。它適合短任務或非固定流程；若要降低來回成本，重點不是把 prompt 寫得更長，而是把驗證步驟（verification）編成 skill，讓 agent 能自己看見、測量或互動結果。
- `Goal-based loop` 把「何時停止」外部化成明確完成條件。對比較複雜的任務，agent 不應只憑自己覺得完成就停；若成功標準能被 evaluator 或 deterministic check 判斷，例如測試通過、分數達標、Lighthouse 超過門檻，`/goal` 這類 primitive 才有穩定價值。
- `Time-based loop` 用時間間隔觸發，適合 recurring work 或需要觀察外部系統變化的任務，例如定期整理 Slack、檢查 PR review 或 CI。這類 loop 的風險是頻率和成本失控，所以應該讓 interval 配合外部狀態變化，而不是預設高頻輪詢。
- `Proactive loops` 則把 schedule、goal、skills、dynamic workflows 和 auto mode 組合起來，用於 bug report、issue triage、migration、dependency upgrade 等可重複且邊界清楚的工作流。這代表 agent loop 從「我叫它做一次」升級成「系統有事件或排程時自動喚醒並完成一段工作」。
- 程式品質取決於 loop 周圍的系統，而不只是模型能力。乾淨的 codebase、可到達的 docs、可執行的 verification skill、第二個 agent code review，以及把失敗經驗編回系統，都是 loop 能否長期變好的控制面。
- token 管理也應成為 loop design 的一部分：選對 primitive 和 model、定義清楚 success / stop criteria、先小規模 pilot、用 script 承接 deterministic work、避免過度頻繁的 routine，並用 usage reporting 回看技能、subagent、workflow 的成本。

## Why It Matters

這篇值得收進 `my-llm-kb`，因為它把 coding-agent workflow 的一個關鍵語彙「loop」具體化。repo 內已經有 Codex Goals、thread automation、long-running harness、skills、agent org chart、ambient agent、workflow adoption level 等材料；這篇的增量是提供一個簡潔分類軸：trigger、stop condition、primitive、task fit。

對實務最有用的讀法是：不要一開始就追求複雜 proactive automation。先問這件事到底是短互動、可驗收長任務、定時檢查，還是 recurring event stream。不同答案會導向不同控制面：turn-based 需要 prompt 與 verification skill，goal-based 需要明確完成條件，time-based 需要 interval 和外部狀態邊界，proactive loop 需要更完整的 workflow / routing / review / cost governance。

這也補強了 repo 一直追蹤的 human-supervised agent ops：人類的工作不是每一步都手動推 agent，而是決定哪種 loop 能交給 agent 關閉、哪些 evidence 足以讓它繼續、什麼條件要停止、何時升級給人。loop taxonomy 讓 supervisor discipline 變得更具體。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): 本文把 loop 設計拆成 trigger、stop condition、primitive 與 task fit，補上 long-running harness 在「何時醒來、何時停止」上的分類語言。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): turn-based、goal-based、time-based、proactive loops 對應不同 human role：直接提示者、完成條件設計者、routine owner、以及 supervisor / exception reviewer。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): `/goal`、`/loop`、`/schedule`、skills、dynamic workflows、auto mode 與 usage reporting 都是不同 runtime control surfaces；它們決定 agent 是被手動呼叫、定期喚醒，還是能在更完整 workflow 裡主動處理事件。
- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md): 本文延續「不要只靠更長 prompt」的方向；重複驗證應升級成 skill，完成條件應升級成 goal，固定 routine 應升級成 loop / schedule。
- [Agent Evaluations](../concepts/agent-evaluations.md): goal-based loop 特別依賴 deterministic criteria 或 evaluator model；這把 eval 從離線評測拉進日常 agent execution loop。
- [Codex Workflows](../maps/codex-workflows.md): 雖然本文來自 Claude Code，但對 Codex Goals、thread automation、skills 與 repo-local verification workflow 有直接可比性。

## Tensions Or Disagreements

- 文章以 Claude Code primitives 為主，不能直接假設每個平台都有相同 `/goal`、`/loop`、`/schedule` 或 dynamic workflow 語義；可保留的是 loop 設計分類，而不是特定 CLI 命令的可攜性。
- Goal-based loop 對「可衡量完成條件」很有效，但許多產品、架構、研究或寫作任務的完成標準混有主觀 judgment。這類任務若只交給 evaluator model，仍可能過早停止或追錯 proxy metric。
- Proactive loops 很容易把 automation 包裝成 autonomy。若缺少 permission boundary、cost cap、trace、review queue、rollback 與 human escalation，schedule + auto mode 可能只是把錯誤移到背景發生。
- 將 manual verification 編成 skill 很有價值，但 skill 也會腐化。若產品 UI、CLI、依賴或 quality bar 變了，verification skill 需要 owner、更新節奏與失敗回報，否則會給 agent 錯誤信心。

## Open Questions

- 對 coding-agent work 而言，哪些任務應停留在 turn-based loop，哪些應升級到 goal-based loop？
- 一個 goal 的停止條件何時可以交給 deterministic check，何時需要 human review 或第二個 agent reviewer？
- Time-based loop 的最佳 interval 應由人設定，還是由外部事件、queue depth、CI 狀態、Slack activity 或成本預算動態決定？
- Proactive loop 的最小 evidence packet 應包含哪些欄位，才足以讓 human supervisor 審計：trigger、input snapshot、plan、actions、tests、diff、usage、review status、rollback path？
- Verification skills 應該如何版本化和測試，避免它們本身變成過期的品質假象？

## Merge Candidates

- Agent loop 應按 trigger、stop condition、runtime primitive 與 task fit 設計，而不是只按「prompt 寫多細」設計。
- Turn-based loop 適合短任務；若同一種檢查反覆出現，應把 manual verification 升級成 skill。
- Goal-based loop 需要明確可判斷的停止條件；沒有 verifier 的 goal 容易退化成長 prompt。
- Time-based loop 適合 recurring work 或外部系統觀測，但 interval、成本與取消條件應明確。
- Proactive loop 是 schedule、goal、skills、workflow routing、auto mode 與 review governance 的組合，不應只靠背景執行來定義。
- Token budget 是 loop design 的一部分；先 pilot、用 scripts 處理 deterministic work、用 usage evidence 調整 model、頻率與 subagent fanout。
