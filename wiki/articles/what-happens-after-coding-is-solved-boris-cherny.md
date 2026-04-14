# What Happens After Coding Is Solved

## Source

- URL: https://www.youtube.com/watch?v=We7BZVKbCVw
- Author: Boris Cherny interview; workspace source is a rewritten zh-Hant article based on the transcript
- Published: 2026-04-12 (inferred from workspace folder name)
- Captured: 2026-04-12
- Raw file: `raw/sources/2026/2026-04-12-head-of-claude-code-what-happens-after-coding-is-solved-boris-cherny.md`
- Imported from workspace path: `podcast/2026-04-12-head-of-claude-code-what-happens-after-coding-is-solved-boris-cherny/2026-04-012-head-of-claude-code-what-happens-after-coding-is-solved-boris-cherny.article.zh-Hant.md`
- Source note: imported filename used the invalid date fragment `2026-04-012`; the raw copy was normalized to `2026-04-12` while preserving the original workspace path for provenance
- Source note: this is a transcript-based rewrite, not a verbatim transcript

## Main Claims

- 對 frontier coding agent 而言，最劇烈被壓縮的環節是手動輸入程式碼；真正稀缺的能力正往 problem framing、prioritization、feedback triage、review 與 orchestration 上移
- Claude Code 不應只被視為 coding tool，而是從 coding 到 tool use、computer use、再到一般 knowledge work 的能力外溢窗口
- 當 agent 可以直接讀取 bug reports、Slack thread 與 telemetry 並提出下一步建議時，implementation 與 product shaping 之間的邊界會開始模糊
- 團隊在模型高速進步期應優先追求 experiment velocity，而不是太早最佳化 form factor、流程或 token 成本
- coding skill 不會立刻消失，但長期價值會更偏向能跨 PM、design、engineering 整合訊號並驅動 agent 持續前進的 `builder`

## Why It Matters

這篇補上了現有 repo 較少明講的一層：`coding 被解掉之後，工作單位如何上移`。如果說 [Harness Engineering](harness-engineering-codex-agent-first-world.md) 比較像 repo-local engineering system 的 view，這篇則提供了 product workflow 與職能重組的 view，說明為什麼 feedback loop、工作分流、multi-agent 並行與人類驗收會變成更核心的 control surface。

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [LLM Agents](../maps/llm-agents.md)
- [Codex Workflows](../maps/codex-workflows.md)

## Tensions Or Disagreements

- `coding is solved`、`software engineer 會淡化成 builder` 這類說法更像 frontier framing，不適合直接當成通用現況描述
- 訪談多以 Anthropic / Claude Code 團隊的內部工作法為背景；對受治理約束較高的企業、legacy codebase 或低信任環境，遷移速度未必相同
- Boris 強調 experiment speed 與 unlimited tokens，這對探索期合理，但在高成本或高風險場景仍需要額外治理層
- 來源本身是 transcript-based rewrite，不是逐字稿；較適合保留觀點輪廓與 workflow framing，而不是做細節級引文依據

## Open Questions

- coding agent 吸收 feedback triage、bug prioritization 與 PR drafting 之後，哪些 PM / design responsibility 會真的被重畫，哪些仍需要專職深度判斷
- `builder` 這個角色在小團隊與大組織中，會對應到同一種能力結構嗎
- frontier workflow 裡的 multi-agent parallelism，何時會提升 throughput，何時會反而增加 review 與 coordination 負擔
- 如果 bottleneck 上移到方向與驗收，repo-local artifact 應如何更好地承接 acceptance criteria、feedback summaries 與 prioritization rationale

## Merge Candidates

- coding automation shifts bottlenecks upward into direction-setting, prioritization, and acceptance
- feedback triage and telemetry interpretation are becoming part of the coding-agent control loop, not purely upstream human work
- frontier teams may prefer speed of experimentation over early workflow or token optimization
- `builder` is a useful framing for role convergence across PM, design, and engineering, but still requires explicit human review and responsibility

## Adoption Follow-Up

### Knowledge Delta

- 這篇真正新增的不是「AI 會寫更多 code」，而是 bottleneck migration 的 framing：一旦 implementation 被壓縮，最值錢的工作會上移到方向設定、訊號整理、優先順序與驗收
- coding agent 的工作面不再只限於 repo 內實作，它可以開始吸收 bug triage、feedback summarization、PR drafting 與初步建議形成
- `builder` 的價值不在 title，而在能否把 PM、design、engineering 與 agent orchestration 連成同一條交付回路

### Workflow Delta

- 下次遇到 feature request、bug cluster 或零散使用者回饋時，不要先把自己預設成「人工整理需求的人」；先判斷能否讓 agent 先做第一輪 triage、摘要與候選優先順序
- 對 agent 任務的輸入，不應只給 implementation ask；應更常提供回饋來源、目標結果與 acceptance lens，讓 agent 從較上游的工作單位開始推進
- 人類在 loop 裡的主要工作應更偏向設定方向、挑選要做的事、驗收結果與調整 control surface，而不是搶先把所有中間整理手工做完

### Habit Delta

- 開始做：當你蒐集到一串 Slack 討論、issue、回饋或觀察時，先問「這次是否該先讓 agent 做 triage，再由我驗收」
- 開始做：在派任務時，固定補上 `該解哪個問題`、`憑什麼算完成`、`有哪些訊號可用來判斷優先順序`
- 停止做：不要把 agent 只當成最後一哩的 code writer，自己先把上游整理與取捨全部做完
- 停止做：不要過早把 token、form factor 或流程最佳化當成主要目標，尤其在你還沒找到有效工作模式之前

### Next Adoption Experiment

- 下一次你遇到需要根據多條回饋決定「先做哪個問題」的情境時，刻意把原始材料直接交給 agent 做第一輪整理
- 最小實驗格式：
  - input: 一串 issue / Slack thread / 使用者回饋摘要 / telemetry 線索
  - ask: 請 agent 先分群問題、提出前 3 個應優先處理的項目、說明理由，並起草其中一項的 implementation plan 或 PR brief
  - human role: 只負責驗證 prioritization 是否合理、補充漏掉的上下文、批准真正開始做的項目
- 這個實驗最適合發生在下一次你已經感覺「整理這些訊號很花時間，但還沒真正進到做事」的任務上

### Stop Doing

- 停止把每次多來源回饋整理都當成只能由你手工完成的前置工
- 停止在 workflow 還沒成熟前，就急著用成本或界面偏好否決更上游的 agent 使用方式

### Success Criteria

- 你至少在一個真實任務裡，讓 agent 先做過回饋 triage 或優先順序建議，而不是只讓它從已決定的 spec 開始寫
- agent 的輸出能明確區分問題分群、優先順序理由與下一步建議，而不是重新敘述原始材料
- 你能指出這種做法是否真的減少了前置整理時間，或提升了你對「先做什麼」的決策清晰度
- 若 agent 的第一輪排序不夠好，你能明確說出缺的是哪一類 context 或 acceptance criteria，而不是籠統歸因成模型不行

### Recommended Writeback Target

- 目前先留在 article level，因為這還是單篇觸發的 adoption experiment
- 如果後續有更多文章或真實任務都支持同一模式，下一步應回寫成 prompt、checklist 或 `_todos/` task intake rule，讓「先 triage 再 implementation」變成可重複工作法
