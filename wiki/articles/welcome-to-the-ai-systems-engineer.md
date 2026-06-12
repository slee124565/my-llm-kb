# Welcome to The AI Systems Engineer Journey

## Source

- URL: https://theneuralmaze.substack.com/p/welcome-to-the-ai-systems-engineer
- Author: Miguel Otero Pedrido
- Publisher: The Neural Maze
- Published: 2026-04-29
- Captured: 2026-06-12
- Raw inbox file: `raw/inbox/2026-04-29-welcome-to-the-ai-systems-engineer.md`
- Raw source file: `raw/sources/2026/2026-04-29-welcome-to-the-ai-systems-engineer.md`
- Subtitle: Issue #01 - One single role behind a dozen titles
- Source note: Opening article for `The AI Systems Engineer Journey`; frames AI systems engineering as the system-level role behind ML, MLOps, LLM, RAG, and agentic AI job-title fragmentation.

## Main Claims

- 產業裡的 AI job title 很混亂，但底層其實集中在少數系統責任：把資料、模型或 foundation model、serving、evaluation、monitoring 與 feedback loop 串成能在真實使用者面前運作的系統。作者用 `AI Systems Engineer` 命名這個已存在但常被分散在多個職稱裡的角色。
- `AI Engineering` 不是取代 `ML Engineering`，而是把 ML engineering 的系統骨架擴展到 foundation model 時代。Feature / Training / Inference（FTI）仍然是可重用 chassis，只是 feature 可能變成 context、chunks、embeddings 或 tool registry，training 可能變成 prompt / config / eval suite，inference 可能變成 RAG pipeline、multimodal document intelligence 或 agent orchestrator。
- 古典 ML 系統與 LLM 系統共享工程判準：需要 decoupled pipeline、versioned artifacts、latency / throughput / cost budgets、monitoring、feedback loops 與 business-facing routing decision。差異不是「有沒有模型 API」，而是哪一層 artifact、成本模型、失敗模式與 evaluation 變了。
- RAG、document intelligence 與 agentic AI system 都不是 demo script。真正困難的是 chunking / retrieval / reranking / citation / guardrail / latency / cost / freshness、multimodal retrieval、tool calling、memory、observability、security 與 task-level evaluation 這些系統面問題。
- Agentic AI 的新風險在於 action loop。當 LLM 不只產生文字，而是規劃、呼叫工具、反思、寫入記憶、協調其他 agent 時，失敗率會連乘，成本會因 loop 放大，trace 與 eval 會變成獨立產品級問題，security 也從 prompt hygiene 變成實際漏洞邊界。
- `AI Systems Engineer` 的核心不是某個工具棧，而是對「產生決策的整個系統」負責：不管是 XGBoost、forecaster、recommender、RAG 或 agent，都要關心資料、模型或 prompt、serving、evaluation、monitoring 與迭代閉環。

## Why It Matters

這篇是 `The AI Systems Engineer Journey` 的定位文章，價值不在新技術細節，而在把 repo 裡已經分散出現的幾條線收斂成一個角色與能力模型：agent 時代的工程師不是只會 prompt，也不是只會調模型，而是要能設計、觀測、驗證並治理整個 AI decision system。

對 `my-llm-kb` 來說，這補上 `agent runtime surfaces`、`agent evaluations`、`long-running harnesses` 與 `human-supervised agent ops` 之間的上位 frame。先前文章多從 coding agent、memory backend、eval harness 或 runtime surface 切入；本文則把 classical ML、foundation-model apps、RAG、document intelligence 與 agents 放在同一個 FTI 系統框架下比較，讓「AI-native system」不再只指 agent product，而是指一套可被工程化的 decision loop。

它也校正一個常見誤讀：AI Engineering 不是「呼叫 LLM API 的應用工程」。如果一個系統會影響使用者、成本、風險或業務決策，就需要 artifact versioning、observability、eval、guardrails、feedback loops 與 ownership boundary。這些能力比單一模型或 prompt 更接近長期可遷移的工程核心。

## Relation To Existing Concepts

- [AI Systems Engineering](../concepts/ai-systems-engineering.md): 本文是此概念的 primary anchor，定義 role、FTI chassis 與 ML / AI engineering 的延續關係。
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): 文章把 tool registry、memory store、prompt registry、model config、guardrails、tracing 與 cost controls 都放進 runtime surface 的責任邊界。
- [Agent Evaluations](../concepts/agent-evaluations.md): Agentic AI 的 task-level success、multi-step trace 與 non-deterministic output 讓 evaluation 從 textbook procedure 變成系統設計問題。
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): 多步 tool loop、reflection、memory writes、budget guard 與 security gate 都是 long-running harness 的基本部件。
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): AI Systems Engineer 的責任面包含 agent action loop 與 human governance，不只是模型或平台 layer。
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
- Related prior source: [Building Agent Memory with Knowledge Graphs](building-agent-memory-with-knowledge.md)

## Tensions Or Disagreements

- `AI Systems Engineer` 是有用的 framing，但仍可能變成另一個職稱包裝。真正可檢查的不是 title，而是這個人或 team 是否真的擁有 data / model or prompt / serving / eval / monitoring / feedback loop 的閉環責任。
- FTI 是很強的抽象，但 agentic systems 會讓 `Training Pipeline` 這個詞有點拉伸：很多團隊沒有 training，只有 prompt registry、model routing、tool schema、eval suite 與 policy config。對 LLM 系統而言，`artifact production pipeline` 可能比 `training pipeline` 更精確。
- 作者強調 AI Engineering 是 ML Engineering 的 superset，這對系統骨架成立；但在組織分工上，classical ML、LLM product engineering、security、data governance 與 domain operations 仍可能需要不同專長與責任切分。
- Agent failure 的連乘估算提醒很重要，但真實可靠性不只由 tool-call success rate 決定。planner quality、recovery strategy、idempotent tools、human approval gate、retry policy 與 task decomposition 都會改變有效成功率。

## Open Questions

- 在實際 team 裡，`AI Systems Engineer` 應該是一個 role、一組能力模型，還是跨 MLE / MLOps / backend / product / security 的 operating contract？
- 對 LLM / agent 系統來說，FTI 的 `Training Pipeline` 應如何重命名或拆分，才能同時容納 prompt registry、model routing、eval suite、fine-tuning、tool schema 與 policy config？
- 如果 AI 系統的核心 artifact 是 prompt + retrieval + model config + tool registry，versioning、rollback、diff review 與 audit 應該落在哪個 repo 或 runtime surface？
- Agentic AI 的 evaluation 若仍是研究級問題，production team 應先建立哪些最小可用 eval harness，才足以支持逐步授權 agent action loop？
- 這個 role framing 如何落到 hiring rubric 或 team capability map，避免再次變成 title inflation？

## Merge Candidates

- `AI Engineering is a superset of ML Engineering` 可被整理成 repo 的上位能力模型：old system skeleton remains; components, artifacts, cost model, evaluation, and action risk change.
- FTI for AI systems: feature/context pipeline、artifact pipeline（prompt / model config / eval / fine-tune / registry）、inference/action pipeline，外加 monitoring、feedback、security 與 cost guard。
- Agentic AI 的關鍵差異不是多一次 LLM call，而是 LLM 變成 action orchestrator；可靠性、observability、cost、security 與 eval 都必須按 multi-step loop 設計。
- `AI Systems Engineer` 應被定義為 system ownership pattern，而不是新職稱：own the decision-producing loop across data, model/prompt, serving, eval, monitoring, and feedback.
