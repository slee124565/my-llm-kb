# AI Systems Engineering

## Summary

AI systems engineering 指的是：把 classical ML、foundation-model applications、RAG、document intelligence、agentic workflows 與 human governance 視為同一類 decision-producing system 來設計、部署、評估與維護的工程能力。

它不是「會用 LLM API」或「會 prompt」的職稱包裝，而是一種 ownership pattern：負責資料或 context、模型或 prompt、serving、evaluation、monitoring、cost、安全、feedback loop，以及這些部分如何共同產生可被信任的決策或 action。

## Why It Matters

LLM 與 agent 工具降低了 demo 門檻，但沒有降低 production system 的責任。相反地，foundation model app 讓 failure mode、成本模型、evaluation、security、memory 與 action loop 更難觀測。AI systems engineering 的價值，是把注意力從「模型能力」拉回「整個系統是否能在真實工作流裡穩定產生正確、有界、可回溯的結果」。

這個概念也能避免 job-title inflation。MLOps、ML Engineer、AI Engineer、RAG Engineer、LLM Engineer、Agentic AI Engineer 可能各自強調不同 layer，但真正需要被治理的是同一個系統閉環：data / context -> artifact -> inference / action -> evaluation -> monitoring -> feedback。

## Current Framing

- AI Engineering 不是 ML Engineering 的替代品，而是 foundation model 時代的 extension；系統骨架仍需要 pipeline decoupling、versioned artifacts、serving constraints、monitoring 與 feedback loops。
- Feature / Training / Inference（FTI）可以被改寫成 AI system chassis：feature 變成 features、documents、chunks、embeddings、tool registry 或 memory context；training 變成 model training、fine-tuning、prompt registry、model config、eval suite 或 policy config；inference 變成 prediction、generation、retrieval-augmented answer 或 multi-step action loop。
- 對 LLM 系統而言，`artifact pipeline` 往往比狹義 `training pipeline` 更準確。可 version 的 artifact 可能是 prompt、retrieval config、reranker、model route、tool schema、guardrail、eval dataset、policy prompt 或 memory schema。
- RAG 的 engineering boundary 包含 source ingest、parsing、chunking、embedding、hybrid search、reranking、prompt construction、citation validation、freshness、latency、cost 與 hallucination handling。
- Document intelligence 把 source representation 從文字 chunk 擴展到 page image、layout、multimodal embeddings、page-level retrieval 與 grounded answer evidence。
- Agentic AI 的核心增量是 action orchestration：planner、tool calls、reflection、memory writes、multi-agent handoff、安全 gate、trace、budget control 與 task-level eval 都進入 production contract。
- Agentic technical debt repeats the 2015 ML systems pattern: the model call is the small box, while markdown configs, model routing, harness state machines, tool contracts, memory governance, serving infrastructure, traces, evals, guardrails, and human gates form the production system.
- AI gateway makes the model layer governable: model routing、fallback、virtual keys、budgets、cost attribution、trace export、provider adapters 與 MCP/tool routing 應集中成 runtime policy，而不是散落在每個 agent app 的 SDK wrapper 裡。
- Ambient agents extend the decision-producing loop from request / response into event streams. Their system boundary includes the event source, stream bus, cheap filter, LLM reasoner, notification path, alert budget, and escalation policy.
- Prompt files, skills, tool descriptions, policy prompts, model routes, eval suites, and memory schemas should be treated as behavioral artifacts. They need versioning, review, rollout and rollback discipline because they change the decision-producing loop as directly as code.
- AI systems engineering 必須把 evaluation 視為一等 artifact。對 non-deterministic outputs、tool loop、agent traces 與 human approval workflow，只靠單次人工看結果不構成可靠治理。
- Fine-tuning pipelines for agents should be treated as system loops, not isolated ML experiments: scenario generation, trajectory capture, relative judging, reward construction, checkpoint lineage, serving, eval regression, and rollback all affect the decision-producing system.
- Human-supervised agent ops 是 AI systems engineering 的產品化方向之一：agent 擁有 operational loop，人類負責 policy、approval、exception review、taste calibration、evidence audit 與 rollout control。

## Signals From Recent Articles

- [Welcome to The AI Systems Engineer Journey](../articles/welcome-to-the-ai-systems-engineer.md): primary framing for AI Systems Engineer as the role that owns the decision-producing system across ML and AI engineering.
- [Hidden Technical Debt in Agentic Systems](../articles/hidden-technical-debt-in-agentic-systems.md): maps the agentic production debt surface around the model: configs, routing, harness, tools, memory, serving, tracing, evals, and guardrails.
- [Don't Marry Your LLM Provider](../articles/dont-marry-your-llm-provider.md): turns provider-agnostic model routing into the AI gateway pattern, where auth, budgets, fallbacks, observability, cost attribution, provider adapters, and MCP/tool routing become centralized runtime policy.
- [Building a Local Ambient Agent That Never Sleeps](../articles/building-a-local-ambient-agent-that-never-sleeps.md): frames ambient agents as event-driven systems with a cheap deterministic filter before an LLM reasoner and a notify-first human escalation path.
- [Building Agent Memory with Knowledge Graphs](../articles/building-agent-memory-with-knowledge.md): memory backend choice becomes a systems-engineering decision about representation, freshness, latency, provenance, correction, and retrieval.
- [Demystifying Evals For AI Agents](../articles/demystifying-evals-for-ai-agents.md): evaluation harness design is not optional QA; it is part of the system's reliability surface.
- [After Automation](../articles/every-after-automation.md): cheap automation raises the value of framing, review, harnesses, and taste rather than eliminating system ownership.
- [Building Self-Improving Tax Agents With Codex](../articles/building-self-improving-tax-agents-with-codex.md): production corrections can become structured findings, eval targets, and bounded improvement loops.
- [How to Fine-Tune LLMs in 2026](../articles/how-to-fine-tune-llms-in-2026.md): connects agent trajectories, GRPO/RULER-style relative rewards, LoRA checkpoints, and MCP tool-use training into a model-weight improvement loop that still needs systems governance.

## Working Thesis

AI systems engineering should be judged by system ownership rather than by model choice.

Useful questions:

- What decision or action does this system produce?
- What data, context, memory, tools, and policies influence that output?
- Which artifacts are versioned and reviewable?
- How is correctness measured, and what evidence supports it?
- What happens when the model, retrieval corpus, tool, vendor, prompt, or user context changes?
- Where are the human approval gates, rollback paths, and audit logs?
- Which costs scale with usage, context length, retries, tool loops, or model routing?

If these questions are unanswered, the system is still a demo or assisted workflow, even if it uses a powerful model.

## Organization-Level AI Core Capabilities

在 AI 時代，組織的 AI 核心能力不應被定義成「會用哪個模型」或「有多少 AI 功能」，而應定義成：能否持續把重要工作流改造成可被 AI 系統理解、執行、評估、監督與改善的 decision-producing loop。

最低限度應包含：

- `workflow framing`: 能把業務問題切成明確任務、輸入、輸出、限制、成功條件與停止條件，而不是只要求 AI 自由發揮。
- `context and knowledge operations`: 能把 domain knowledge、SOP、案例、資料來源、例外規則與歷史決策整理成 agent 可檢索、可引用、可回寫、可更新的 knowledge layer。
- `AI systems engineering`: 能管理 prompt、model route、retrieval config、tool schema、policy、eval suite、memory schema、traces、cost 與 serving constraints 等 behavioral artifacts。
- `evaluation and evidence discipline`: 能把人工 review、production failure、support queue、agent transcript、grader、regression suite 與 monitoring 串成品質閉環。
- `human-supervised delegation`: 能判斷哪些 operational loops 可交給 agent 關閉，哪些需要 human approval、exception review、rollback、audit log 或 freeze gate。
- `tool and runtime design`: 能把內部系統、資料表、issue tracker、browser、CLI、API 與 approval surface 變成 agent-legible / agent-actionable 的 runtime，而不是只在既有 UI 上加聊天框。
- `feedback-to-improvement loop`: 能把人類修正轉成 structured finding、eval target、scoped engineering task、validated fix 與 rollout / rollback decision。
- `organizational taste and governance`: 能保留人類在 framing、taste、policy、risk boundary、customer promise 與 final accountability 上的責任，而不是把責任外包給模型輸出。

因此，AI-era organization capability 的成熟度可用一個問題檢查：這個組織是否能把 AI 從零散 productivity tool，升級成可治理、可評估、可迭代的 operating layer？

## Open Questions

- 應如何把 AI systems engineering 轉成 hiring rubric、team charter 或 architecture review checklist？
- LLM / agent product 的 artifact registry 最小集合是什麼：prompt、model config、tool schema、retrieval config、eval dataset、policy、memory schema 是否都要進同一個 versioning surface？
- FTI 在 agentic workflow 中是否應擴展成 feature/context pipeline、artifact pipeline、action pipeline、feedback/eval pipeline？
- 哪些 systems-engineering responsibilities 應由 platform team 承擔，哪些必須由 product/domain team 擁有？
- Human supervisor 的 evidence packet 應包含哪些欄位，才能讓 AI systems engineering 從「模型測試」升級成「可治理的 operational loop」？
- 組織應如何把 AI 核心能力拆成 team charter、能力盤點、adoption ladder、review checklist 與 operating metrics，而不是停在工具採購或培訓課程？
- 當 agent traces 被用來 fine-tune 模型權重時，哪些 artifact 必須進 registry：trajectory、judge prompt、reward output、training config、checkpoint、eval report、rollback decision？

## Related Pages

- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Agent Evaluations](agent-evaluations.md)
- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Human-Supervised Agent Ops](human-supervised-agent-ops.md)
- [Externalized Agent State](externalized-agent-state.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
