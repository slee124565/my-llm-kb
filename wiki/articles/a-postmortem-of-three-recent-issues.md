# A Postmortem of Three Recent Issues

## Source

- URL: https://www.anthropic.com/engineering/a-postmortem-of-three-recent-issues
- Author: Anthropic Engineering
- Published: 2025-09-17
- Captured: 2026-04-14
- Raw file: `raw/sources/2026/2026-04-14-a-postmortem-of-three-recent-issues.md`
- Imported from workspace path: `blog/2026-04-14-a-postmortem-of-three-recent-issues/2026-04-14-a-postmortem-of-three-recent-issues.md`

## Main Claims

- Claude's intermittent quality regressions in August and September 2025 were caused by three overlapping infrastructure bugs rather than demand, time of day, or intentional degradation
- serving one model across multiple hardware platforms and partner surfaces requires strict output-equivalence expectations, but that same heterogeneity expands the space where routing, compiler, and inference bugs can hide
- noisy benchmark-heavy validation was not sufficient to distinguish these regressions from normal variance; production-quality monitoring and user-reported signal were required to isolate the failures
- privacy-preserving access controls made debugging harder because engineers could not freely inspect problematic interactions, so better tooling is needed to connect community reports to specific recent changes without weakening privacy
- model-serving reliability is not just a deployment concern; eval sensitivity, canary design, debugging tooling, and rollback discipline are part of the quality harness

## Why It Matters

這篇的新增價值不只是 Anthropic 的事故說明，而是把 `production inference reliability` 正式拉進 agent / model workflow 討論。先前 repo 較多聚焦在 repo-local harness、long-running execution 與 workflow orchestration；這篇補上 provider-side runtime 的另一面：如果 serving、routing、sampling、eval 與 debugging loops 不可靠，再好的 agent workflow 也可能建立在不穩定地基上。

## Relation To Existing Concepts

- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)

## Tensions Or Disagreements

- 這篇主要是 provider-internal postmortem，不是通用 agent team 都能直接複製的操作手冊；許多修正依賴 Anthropic 對 serving stack、compiler path 與 deployment pipeline 的控制權
- 文章強調 user feedback 的重要性，但沒有完整回答如何在強隱私約束下建立足夠細的 debug signal，而不滑向過度觀測
- 它聚焦的是 quality regression detection，不等於已證明所有 model-quality 問題都應優先靠 production eval 解決；有些問題仍更適合在離線 eval 或 product instrumentation 層處理

## Open Questions

- provider-managed runtime 的最小 quality harness 應包含哪些 production eval、canary、rollback 與 user-feedback correlation surfaces
- 當 privacy controls 限制工程師直接檢查真實對話時，什麼樣的 debugging artifact 才足夠支撐快速根因分析
- repo-local agent teams 能否借用這個 framing，把自己的 app logs、quality checks、community reports 與 recent changes 串成更可檢查的 postmortem loop
- cross-platform equivalence 應被視為單純 infra 問題，還是 hosted agent runtime contract 的一部分

## Merge Candidates

- production model quality depends on a broader harness than offline evals alone: routing correctness, serving equivalence, sensitive production checks, rollback discipline, and debugging tooling all matter
- noisy evaluations can miss real regressions, especially when models recover from isolated mistakes and overlapping bugs create contradictory reports
- user feedback is part of the quality-control loop, but privacy constraints mean teams need purpose-built tooling to connect reports to recent infra changes without exposing raw interactions broadly
- hosted runtime reliability should be treated as a first-class agent surface, not an invisible implementation detail beneath the product

## Adoption Follow-Up

### Knowledge Delta

- 這篇真正新增的不是「大模型 infra 很複雜」，而是 quality regression 也應被視為一種 harness failure，而不是單純 deployment accident
- `runtime surface` 不只決定 agent 在哪裡跑，也決定品質問題會以什麼形式暴露給使用者，以及 team 是否有足夠 artifact 能把問題連回最近的變更
- user feedback 不是最後才看的雜訊；當 eval 對真實 degradation 不夠敏感時，它本身就是 production quality loop 的核心輸入之一

### Workflow Delta

- 當你自己在用 agent 或觀察 workflow 品質時，不要只用「好像今天比較差」這種印象來判斷；應嘗試把異常回應連回具體的 runtime、tool、prompt、資料面或最近變更
- 對自己的 agent workflow review，不應只檢查 prompt 與輸出，也應補一層最小 postmortem 問題集：異常發生在哪個 surface、是否可重現、最近改了什麼、缺了哪種 debug artifact
- 當你做新 workflow、prompt、skill 或 CLI 的實驗時，除了定義成功標準，也應先想好退化時要看什麼 signal，避免失敗後只能靠印象回想

### Habit Delta

- 開始做：當某個 agent workflow 連續出現 2 到 3 次「怪怪的但說不清」的退化時，立刻記下具體症狀、觸發條件、最近變更與可疑 surface，不要等它自己消失
- 開始做：對高價值 workflow experiment，固定補一個小型 regression note 區塊，至少記 `what changed`、`what broke`、`how detected`
- 開始做：把使用者／自己在真實任務中的異常回饋，視為 eval 補充，而不是低可信抱怨
- 停止做：不要把 workflow 品質波動先直覺歸因成模型隨機性或「今天狀態不好」
- 停止做：不要只記成功案例，卻沒有留下失敗時的觀測 artifact

### Next Adoption Experiment

- 下一次你在真實任務中發現某個 agent workflow、prompt、skill 或 CLI surface 出現連續異常時，不要直接修；先做一版極小 postmortem note
- 最小格式：
  - issue surface：問題出現在 prompt、tooling、runtime、資料面或 handoff 的哪一層
  - symptom：具體退化表現是什麼
  - recent change：最近改了哪些規則、prompt、腳本或流程
  - detection signal：你是靠什麼發現它不對
  - next check：還缺哪個 artifact 才能更快定位
- 這個實驗最適合落在下一次你明顯感覺「不是完全壞掉，但品質持續不穩」的工作流上

### Stop Doing

- 停止把間歇性品質退化直接當成不可避免的模型波動
- 停止在 workflow 改版後只看成功路徑，而沒有留意 regression 是怎麼被發現的
- 停止把 user-side anomaly report 視為太主觀而不值得保留；真正的問題常常就是先從模糊回饋浮出來

### Success Criteria

- 你至少在一個真實 workflow 異常案例中，留下可回查的 postmortem note，而不是只在對話裡口頭描述
- 你能把一次退化明確拆成 symptom、可能 surface、最近變更與缺少的 debug artifact，而不是籠統說「效果變差」
- 下一次類似問題再出現時，你能更快縮小排查範圍，而不是從零回想
- 若這種 postmortem note 連續出現於同一類 workflow，你能指出它應升級成哪個 prompt、checklist 或 rule

### Recommended Writeback Target

- 目前先留在 article level，因為這個 adoption 比較像一個跨 workflow 的觀測習慣，還沒有收斂成單一固定流程
- 如果你後續真的累積 2 到 3 次可比較的 regression note，下一步應回寫成 prompt、checklist 或 review rule，而不是只留在單篇文章裡

### Issue Follow-Up Decision

- 目前不建議建立 GitHub adoption issue
- 原因：
  - 這篇有明確 workflow value，但下一次實驗觸發點是「下次遇到間歇性退化時」，不是已知短期內一定會發生的固定任務
  - success criteria 可以定義，但沒有足夠明確的近期承接場景，現在開 issue 很容易變成抽象提醒
  - 更好的做法是先等第一個真實 regression note 出現，再決定是否把它升級成 prompt / checklist / issue 追蹤
