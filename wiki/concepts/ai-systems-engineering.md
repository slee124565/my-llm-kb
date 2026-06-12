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
- Prompt files, skills, tool descriptions, policy prompts, model routes, eval suites, and memory schemas should be treated as behavioral artifacts. They need versioning, review, rollout and rollback discipline because they change the decision-producing loop as directly as code.
- AI systems engineering 必須把 evaluation 視為一等 artifact。對 non-deterministic outputs、tool loop、agent traces 與 human approval workflow，只靠單次人工看結果不構成可靠治理。
- Human-supervised agent ops 是 AI systems engineering 的產品化方向之一：agent 擁有 operational loop，人類負責 policy、approval、exception review、taste calibration、evidence audit 與 rollout control。

## Signals From Recent Articles

- [Welcome to The AI Systems Engineer Journey](../articles/welcome-to-the-ai-systems-engineer.md): primary framing for AI Systems Engineer as the role that owns the decision-producing system across ML and AI engineering.
- [Hidden Technical Debt in Agentic Systems](../articles/hidden-technical-debt-in-agentic-systems.md): maps the agentic production debt surface around the model: configs, routing, harness, tools, memory, serving, tracing, evals, and guardrails.
- [Building Agent Memory with Knowledge Graphs](../articles/building-agent-memory-with-knowledge.md): memory backend choice becomes a systems-engineering decision about representation, freshness, latency, provenance, correction, and retrieval.
- [Demystifying Evals For AI Agents](../articles/demystifying-evals-for-ai-agents.md): evaluation harness design is not optional QA; it is part of the system's reliability surface.
- [After Automation](../articles/every-after-automation.md): cheap automation raises the value of framing, review, harnesses, and taste rather than eliminating system ownership.
- [Building Self-Improving Tax Agents With Codex](../articles/building-self-improving-tax-agents-with-codex.md): production corrections can become structured findings, eval targets, and bounded improvement loops.

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

## Open Questions

- 應如何把 AI systems engineering 轉成 hiring rubric、team charter 或 architecture review checklist？
- LLM / agent product 的 artifact registry 最小集合是什麼：prompt、model config、tool schema、retrieval config、eval dataset、policy、memory schema 是否都要進同一個 versioning surface？
- FTI 在 agentic workflow 中是否應擴展成 feature/context pipeline、artifact pipeline、action pipeline、feedback/eval pipeline？
- 哪些 systems-engineering responsibilities 應由 platform team 承擔，哪些必須由 product/domain team 擁有？
- Human supervisor 的 evidence packet 應包含哪些欄位，才能讓 AI systems engineering 從「模型測試」升級成「可治理的 operational loop」？

## Related Pages

- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Agent Evaluations](agent-evaluations.md)
- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Human-Supervised Agent Ops](human-supervised-agent-ops.md)
- [Externalized Agent State](externalized-agent-state.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
