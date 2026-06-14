# Hidden Technical Debt in Agentic Systems

## Source

- URL: https://theneuralmaze.substack.com/p/hidden-technical-debt-in-agentic
- Author: Miguel Otero Pedrido
- Publisher: The Neural Maze
- Published: 2026-05-06
- Captured: 2026-06-12
- Raw file: `raw/sources/2026/2026-05-06-hidden-technical-debt-in-agentic.md`
- Guided reading note: `raw/sources/2026/2026-05-06-hidden-technical-debt-in-agentic-guided-reading-note.md`
- Subtitle: Issue #02 — Eleven years later, the same diagram is being redrawn
- Source note: Second article in `The AI Systems Engineer Journey`; adapts the 2015 hidden-technical-debt framing from ML systems to production agentic AI systems.

## Main Claims

- Agentic AI 的「模型呼叫」正在變成 2015 年 ML 系統圖裡的小盒子：真正的工程風險、成本與技術債，集中在模型周圍的 runtime、tool layer、memory、serving、tracing、eval 與 guardrails。若 team 只優化模型能力，會錯過 production 失敗實際發生的位置。
- Markdown configs、prompts、skills、sub-agent definitions 與 slash commands 應被視為 agent 的行為原始碼（source code）。它們需要 version control、diff review、rollback、eval-gated merges 與 feature flag，而不是被當成散落在程式裡的字串或 notes。
- Model layer 的第一個問題不是「用哪個模型」，而是「哪些任務該由哪個模型處理」。Production agent 需要 model routing、model fleet、fallback chain 與 provider-agnostic abstraction，否則成本、品質與 vendor lock-in 都會被第一版 demo 的選擇鎖住。
- Agent harness 本質上是狀態機（state machine）。ReAct、Plan-and-Execute、Reflexion 不是互斥流派，而是不同控制流程元件；真正危險的是 team 無法畫出 agent 狀態、轉移、步數上限、重試策略與成本 circuit breaker。
- Tool layer 的高槓桿點不只在 implementation，而在 schema、contract 與自然語言 description。Agent 不是直接「看見」工具，而是透過 tool description 決定何時呼叫；描述不清、工具過多、失敗模式沒寫清楚，都會變成 loop、誤選工具與 API 成本債。
- Memory 不是把所有東西丟進 vector DB。短期 scratchpad、session memory、long-term memory、semantic memory、episodic memory 與 procedural memory 是不同子系統；其中 session summarization 與 raw history 的漂移，往往比長期記憶 backend 更早造成 production bug。
- Agent serving 的單位不是 request，而是 session。Agent run 可能長時間、stateful、異質、等待工具或人工 approval，這讓 invocation model、state location、scaling pattern、observability boundary 與 idle-time cost 成為 serving design 的核心問題。
- Agent observability 需要 replay 多步 trace，而不只是看 final answer、latency 或 error code。每次 model call、tool call、reflection、retry、token 與 cost 都應進 trace tree；monitoring 則應聚焦 task success rate、cost per successful task、P95 latency、tool error rate 與 average steps per task。
- Eval harness 不是上線後補的 QA，而是 agent product 的交付物之一。Reference-based eval、LLM-as-judge、trajectory eval 與 online / shadow eval 各自覆蓋不同 failure mode；沒有 eval，prompt、model routing 或 tool description 的修改只能靠 48 小時 vibe check。
- Guardrails 不能只寫在 system prompt。Prompt injection through tool output、PII memory leak、runaway cost、off-policy assistance 與 irreversible actions 都需要 code-level enforcement、human approval gate、audit log 與 defense-in-depth 的 runtime design。

## Why It Matters

這篇是 `The AI Systems Engineer Journey` 的關鍵中間節點：第一篇先定義 `AI Systems Engineer` 是負責整個 decision-producing system 的角色；這篇則把 agentic system 的 production surface 一格一格畫出來，說明這個角色到底要管哪些元件。

對 `my-llm-kb` 來說，它把 repo 裡幾條已存在的線收斂成一張更完整的 agent technical-debt map：prompt / skills 是可版本化 artifact，model choice 是 routing 與成本策略，harness 是狀態機，tools 是公共 API，memory 是多層治理問題，serving 是 session infrastructure，tracing / eval / guardrails 是授權 agent 行動前的可靠性底座。

最重要的管理含義是：agent demo 越容易，production debt 越容易被延後。早期看起來只是「加一個 tool」、「改一段 prompt」、「換個模型」的決策，會在流量、成本、稽核、資安、使用者資料與 human approval workflow 進來後變成系統級債務。這正是 AI systems engineering 要提前命名與治理的責任面。

## Relation To Existing Concepts

- [AI Systems Engineering](../concepts/ai-systems-engineering.md): 本文是 `AI Systems Engineer` 角色的 production component map，將 2015 ML technical-debt 圖轉譯成 agentic system surface。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): 文章把 markdown config、model fleet、tool registry、memory store、serving layer、trace store、eval harness 與 guardrails 都放進 runtime surface。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): Agent harness 被明確定義為可畫出的狀態機，需要步數上限、成本 circuit breaker、retry / recovery policy 與 human gate。
- [Agent Evaluations](../concepts/agent-evaluations.md): Eval harness 被放在 agent product 的核心，尤其包含 trajectory eval、online eval、eval set refresh 與 LLM-as-judge 校準。
- [Agent Memory Architecture](../concepts/agent-memory-architecture.md): 本文預告後續 memory issue，先把 memory 拆成 short-term、session、long-term、semantic、episodic、procedural 幾個治理層。
- [Externalized Agent State](../concepts/externalized-agent-state.md): Markdown configs、tool schemas、eval suites、traces、memory schemas 與 audit logs 都是 agent 行為外部化後可 review 的 state surface。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): Guardrails 與 irreversible actions 的 human-in-the-loop 規則，直接支持 agent operational loop 的授權分層。
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
- Related prior sources: [Welcome to The AI Systems Engineer Journey](welcome-to-the-ai-systems-engineer.md), [Demystifying Evals For AI Agents](demystifying-evals-for-ai-agents.md), [Building Agent Memory with Knowledge Graphs](building-agent-memory-with-knowledge.md), [Effective Harnesses for Long-Running Agents](effective-harnesses-for-long-running-agents.md)

## Tensions Or Disagreements

- 文章強調 agentic infrastructure 的 debt surface 很完整，但不同產品階段不一定需要一次建滿所有元件。早期 team 的判斷不是「是否要 trace / eval / guardrail」，而是哪些 action risk、cost risk、privacy risk 已經足以要求 production-grade surface。
- `Markdown configs are source code` 是很好的工程直覺，但仍需要區分穩定 prompt contract、暫時 experiment prompt、personal instruction 與 generated skill。全部一律套 code review，可能降低迭代速度；完全不 review，則會讓行為改變不可追溯。
- Provider-agnostic abstraction 可以降低 model lock-in，但也可能遮蔽不同模型的 prompt format、tool semantics、reasoning visibility 與 safety behavior 差異。抽象層要服務 routing 與 fallback，不應把 eval 需要看到的模型差異抹平。
- Tool 數量與 tool selection accuracy 的關係很重要，但不是單純越少越好。真正要管理的是 overlapping semantics、ambiguous descriptions、side-effect boundary、schema validation 與 task-specific tool routing。
- 文章主張 eval harness 是 product 的 deliverable，這對 production agent 正確；但 eval set 本身也會腐化。若沒有從 production traces、user feedback 與 expert review 回補，eval 也會變成另一個讓 team 產生假安全感的 artifact。

## Open Questions

- 對一個剛從 prototype 進入 early production 的 agent product，哪些 technical-debt surfaces 是最低限度必須先建立的：trace、eval、cost budget、human gate、tool schema、prompt versioning，還是 model routing？
- Markdown configs、skills、tool descriptions 與 policy prompts 應該共用同一套 review / release / rollback 流程，還是依 action risk 分層？
- Agent serving 若以 session 為單位，平台應如何區分 active compute、idle wait、human approval wait 與 external webhook wait，才能讓成本模型可預測？
- Tool-output prompt injection 與 memory privacy leak 應如何被寫進 trajectory eval 或 security eval，而不是只靠紅隊測試？
- 當 eval harness 成為 agent product 的核心 deliverable，product manager、domain expert、engineer 與 security reviewer 的 ownership 應如何切分？

## Merge Candidates

- `The model is the small box` 可作為 AI systems engineering 的核心檢查句：agent reliability 主要取決於 prompt/config versioning、tool contracts、memory governance、serving state、traceability、evals、guardrails 與 feedback loops。
- Markdown configs should be governed as behavioral source code: versioned files, diff review, eval-gated changes, rollout flags, rollback path, and provenance.
- Agent harnesses should be drawn as state machines before production: states, transitions, step limits, retry rules, budget circuit breakers, escalation, and terminal states.
- Agent serving is session infrastructure, not request infrastructure; cost, state migration, observability and scaling decisions should be made around long-lived sessions.
- Agent evals should include trajectory and online signals, not only final-answer grading; trace replay and cost-per-success are part of the quality contract.
