# Building a Local Ambient Agent That Never Sleeps

## Source

- URL: https://theneuralmaze.substack.com/p/building-a-local-ambient-agent-that
- Author: Miguel Otero Pedrido
- Publisher: The Neural Maze
- Published: 2026-06-13
- Captured: 2026-06-19
- Raw file: `raw/sources/2026/2026-06-13-building-a-local-ambient-agent-that.md`
- Subtitle: Issue #05 - The theory, the design trade-offs, and a Kafka + Ollama agent you can run today
- Source note: Imported with `myAgentTools/neural-maze-ase-journey-import`; Substack metadata marked the post as `only_paid`, and the captured body ends at the start of the code-build section.

## Main Claims

- Ambient agent 的核心不是更聰明的 chat bot，而是把主動權從人轉給環境。Reactive agent 等人輸入才回應；ambient agent 常駐在事件流上，持續觀測、判斷、只在需要人類注意時升級。這讓時間模型、成本模型與安全邊界都和一般聊天介面不同。
- Ambient agent 可以被理解成「event-driven architecture with a model in the loop」。傳統事件系統是 source -> bus -> consumer；這篇把 consumer 裡的硬編碼規則換成 LLM reasoner。也就是說，重點不是發明新架構，而是把模型放進既有 stream / queue / consumer pattern 裡。
- 安全的第一版 ambient agent 應先停在通知（notify）層級。文章把 human-in-the-loop 分成 notify、question、review 三個 trust tier；對 always-on agent 來說，越接近不可逆 action，越需要 runtime gate、approval path 與 audit discipline。本文示範的是只觀測與回報，不下單、不自動執行不可逆行為。
- 本地 ambient agent 的最小骨架可拆成 senses、nervous system、brain：外部事件來源把世界轉成訊號，Kafka 這類 bus 承接可靠事件流，Ollama 本地模型負責在候選事件上做判斷。這個拆法讓 agent 可以換不同 senses，例如 crypto trades、email、logs、papers 或 filings，而不必重寫整個 reasoning layer。
- 文章最重要的工程決策是兩階段漏斗（two-stage funnel）：便宜的 deterministic filter 先跑在所有 window 上，只把異常或有意義的事件交給 LLM；LLM 只處理通過 threshold 的候選。這把 ambient agent 從「每個 tick 都問模型」改成「只有值得判斷時才喚醒模型」，否則 token、延遲與 backlog 會讓 always-on agent 失去實用性。
- Structured output 與本地模型讓 ambient agent 從研究玩具變成週末可做的系統，但真正能否 productionize，仍取決於 event stream、filter threshold、reasoning output contract、human escalation path 與可觀測性，而不只是模型能不能生成一段好看的分析。

## Why It Matters

這篇把 `The AI Systems Engineer Journey` 從「production agent technical debt」推進到「always-on agent runtime」：agent 不再只是被使用者召喚的 request / response loop，而是常駐在事件流上的 operator。

對 `my-llm-kb` 來說，增量在兩個地方。第一，它把 ambient agent 拆回大家熟悉的 event-driven architecture，避免把 proactivity 神秘化。第二，它把 LLM 成本與延遲放到架構中心：always-on agent 的核心不是「能不能每秒都想」，而是「能不能用便宜、可解釋、可調整的前置 filter，讓模型只在必要時介入」。

這也補強 human-supervised agent ops 的授權梯度。Notify-only agent 看起來權限很小，但它是可治理 proactivity 的起點：先讓 agent 觀測、篩選、解釋、通知；等 evidence、eval、audit log 與 rollback 成熟後，才逐步升級到 question 或 review。

## Relation To Existing Concepts

- [AI Systems Engineering](../concepts/ai-systems-engineering.md): ambient agent 是 decision-producing loop 的一種具體型態；系統責任落在 stream、filter、reasoner、notification、cost 與 safety gates 的組合，而不是單一模型呼叫。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): Kafka topic、local Ollama model、threshold filter、Telegram / terminal notification 都是 runtime surface；它們共同決定 agent 的觀測範圍、延遲、成本、權限與可審計性。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): ambient agent 是 long-running harness 的 always-on 分支，需要處理 stream backpressure、bounded reasoning、filter gates、human escalation 與 terminal/non-terminal event state。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): notify / question / review 提供了 agent 授權層級；本文保守停在 notify，符合先建立 supervisor evidence plane 再擴權的路徑。
- [Agent Evaluations](../concepts/agent-evaluations.md): threshold filter 與 LLM 判斷都需要 eval；否則 system 只能靠主觀感覺調參，容易在 false positive、false negative、cost 與 alert fatigue 之間失衡。
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
- Related prior sources: [Welcome to The AI Systems Engineer Journey](welcome-to-the-ai-systems-engineer.md), [Hidden Technical Debt in Agentic Systems](hidden-technical-debt-in-agentic-systems.md), [Building Agent Memory with Knowledge Graphs](building-agent-memory-with-knowledge.md)

## Tensions Or Disagreements

- 把 consumer 的 hard-coded rule 換成 LLM reasoner 是清楚的 framing，但 production system 不能因此放棄 rule-based guardrails。便宜 filter、schema validation、rate limit、approval gate 與 alert budget 仍應在 code-level enforcement 裡，而不是只靠 prompt。
- 本地模型降低 API 成本與資料外流風險，但不自動解決 reliability。Ambient agent 的錯誤通常不是單次回答錯，而是長時間漏報、誤報、重複打擾或在 stream backlog 中失去時效性。
- Crypto trade feed 適合展示 high-volume stream 與 threshold filter，但它不是最安全的產品範例。文章有明確聲明不自動下單；若未來改成交易、寄信、修改 CRM 或執行維運操作，授權層級必須從 notify 重新評估到 review 或 explicit approval。
- 目前 captured raw source 在 `Let's build it` heading 後停止，沒有保存後續 code walkthrough。這張卡只編譯已捕捉到的理論、架構與設計取捨，不驗證 Kafka / Ollama 實作細節。

## Open Questions

- Ambient agent 的 threshold filter 應如何被 eval：用 historical stream replay、human-labeled incidents、synthetic spike fixtures，還是 production alert feedback？
- Notify-only agent 何時可以升級到 question 或 review？需要哪些 evidence packet、approval log、rollback path 與 false-positive/false-negative 指標？
- 對高頻事件流，LLM reasoner 的 output contract 應該是 human-readable read、structured incident object、priority score，還是 action proposal？
- Kafka 這類 durable bus 對個人本地 ambient agent 是否必要，還是某些低風險場景用 SQLite queue、filesystem inbox 或 lightweight stream 就足夠？
- 如果 ambient agent 常駐本機並連到 Telegram / terminal notification，它的 credential boundary、schedule visibility、log retention 與 disable switch 應如何設計？

## Merge Candidates

- Ambient agent = event-driven architecture plus model reasoner: source / stream / cheap filter / LLM judgment / human escalation path.
- Always-on agent 的核心 constraint 是 efficiency 與 bounded attention；LLM 應只處理通過 cheap deterministic filter 的候選事件。
- Notify / question / review 可以作為 human-supervised agent ops 的授權梯度；第一版 proactivity 應先停在 notify-only，避免不可逆 action。
- Ambient runtime 的最小 evidence packet 應包含 source event window、filter metrics、reasoner output、confidence / severity、notification channel、human action taken 與 follow-up feedback。
