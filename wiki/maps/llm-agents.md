# LLM Agents

## Scope

這個 map 聚焦於 `LLM + agent` 主題中的高層入口，特別是 knowledge compilation、externalized state 與 long-running harness design。

## Entry Points

- [Agent Knowledge Compilation](../concepts/agent-knowledge-compilation.md)
- [Agent Evaluations](../concepts/agent-evaluations.md)
- [Agent Memory Architecture](../concepts/agent-memory-architecture.md)
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [AI Compute Infrastructure](../concepts/ai-compute-infrastructure.md)
- [AI Systems Engineering](../concepts/ai-systems-engineering.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)

## Core Concepts

- agent knowledge compilation
- agent evaluations
- agent memory architecture
- agent runtime surfaces
- AI compute infrastructure
- AI systems engineering
- externalized agent state
- human-supervised agent ops
- long-running agent harnesses
- prompt migration and agent steerability
- repository knowledge as system of record

## Key Articles

- [Building Agent Memory with Knowledge Graphs](../articles/building-agent-memory-with-knowledge.md)
- [Welcome to The AI Systems Engineer Journey](../articles/welcome-to-the-ai-systems-engineer.md)
- [Hidden Technical Debt in Agentic Systems](../articles/hidden-technical-debt-in-agentic-systems.md)
- [Don't Marry Your LLM Provider](../articles/dont-marry-your-llm-provider.md)
- [Building a Local Ambient Agent That Never Sleeps](../articles/building-a-local-ambient-agent-that-never-sleeps.md)
- [Question-Answer Packets for RAG](../articles/2026-05-08-question-answer-packets-for-rag.md)
- [Vibe Coding is a Ticking Time Bomb](../articles/2026-06-18-vibe-coding-runtime-safety-boundary.md)
- [Best Practices For Claude Code](../articles/best-practices-for-claude-code.md)
- [Lessons From Building Claude Code: How We Use Skills](../articles/lessons-from-building-claude-code-how-we-use-skills.md)
- [Deep Dive into LLMs like ChatGPT](../articles/deep-dive-into-llms-like-chatgpt.md)
- [Demis Hassabis: Agents, AGI & The Next Big Scientific Breakthrough](../articles/demis-hassabis-agents-agi-next-big-scientific-breakthrough.md)
- [LLM Knowledge Bases](../articles/karpathy-llm-knowledge-bases.md)
- [Shell + Skills + Compaction](../articles/shell-skills-compaction-long-running-agents.md)
- [Effective Harnesses for Long-Running Agents](../articles/effective-harnesses-for-long-running-agents.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [OpenClaw: The Viral AI Agent that Broke the Internet](../articles/openclaw-viral-ai-agent-lex-fridman-peter-steinberger.md)
- [Hermes Agent Masterclass](../articles/hermes-agent-masterclass.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [OpenAI Symphony Codex Orchestration](../articles/openai-symphony-codex-orchestration.md)
- [Building Self-Improving Tax Agents With Codex](../articles/building-self-improving-tax-agents-with-codex.md)
- [How to Fine-Tune LLMs in 2026](../articles/how-to-fine-tune-llms-in-2026.md)
- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [What Happens After Coding Is Solved](../articles/what-happens-after-coding-is-solved-boris-cherny.md)
- [A Postmortem of Three Recent Issues](../articles/a-postmortem-of-three-recent-issues.md)
- [Jensen Huang - TPU Competition, China Chips, and Nvidia's Supply Chain Moat](../articles/jensen-huang-tpu-china-chips-nvidia-supply-chain-moat.md)
- [Introducing Codex](../articles/introducing-codex.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [OpenAI Prompt Engineering - GPT-3.5 Era](../articles/openai-prompt-engineering-gpt-3-5-era.md)
- [OpenAI Prompt Guidance - GPT-5.5](../articles/openai-prompt-guidance-gpt-5-5.md)
- [OpenAI Prompt Guidance - GPT-5.4](../articles/openai-prompt-guidance-gpt-5-4.md)
- [OpenAI Prompt Guidance - GPT-5.3 Codex](../articles/openai-prompt-guidance-gpt-5-3-codex.md)
- [The Founder's Playbook: Building an AI-Native Startup](../articles/claude-the-founders-playbook.md)
- [After Automation](../articles/every-after-automation.md)
- [The Eight Levels of AI Adoption](../articles/every-the-eight-levels-of-ai-adoption.md)
- [Demystifying Evals For AI Agents](../articles/demystifying-evals-for-ai-agents.md)
- [Collapse Your CRM Pipeline Into One Table](../articles/collapse-your-crm-pipeline-into-one-table.md)

## Key People Or Labs

- Andrej Karpathy
- OpenAI
- Anthropic
- Nvidia
- Google DeepMind
- Demis Hassabis
- Boris Cherny
- Peter Steinberger
- Aaron Friel
- Ryan Lopopolo
- Akshay Pachaar
- Nous Research

## Open Threads

- parameter memory、context window 與 externalized repo artifact 應如何分層，而不是互相取代
- hosted runtime、repo-local runtime 與 local personal runtime 的 design principles，哪些應共享，哪些必須分流
- 知識型 agent 與 coding agent 是否應共享同一套 state model
- compaction、progress artifact、skill contract 三者的最小組合是什麼
- 更強模型是否會讓 orchestration 複雜度下降，而不是上升
- repo-local knowledge base 與 remote async execution 應如何協同設計
- issue tracker 作為 agent control plane 時，哪些 team process 應該被版本化成 repo-local workflow contract
- local personal agents 與 cloud coding agents 應共享哪些設計原則，又該在哪些地方刻意分流
- provider-managed agent infrastructure 會不會把 runtime 與 orchestration 進一步集中到少數平台
- AI gateway 會成為多模型、多 tool、多 MCP server agent stack 的必要 reverse proxy，還是只適合多 provider / 多 team / 高流量 production apps
- 如果 coding 不再是主要瓶頸，agent-era builder 的最小能力組合應如何定義，哪些 specialist review 仍然不可壓縮
- 當 hosted model quality regressions 只在特定 routing path 或硬體平台上出現時，使用者可見的 agent reliability 應如何被觀測、解釋與治理
- AI compute stack 的分裂或集中，會如何影響 hosted agent 的成本、可用性、可靠性與 developer ecosystem lock-in
- context window, externalized memory, and learned continual memory should be composed how if agents are expected to adapt to a user's or task's long-term context
- future general agents should absorb specialized capabilities into one model, or orchestrate separate expert systems as tools
- local personal agents with browser/app control should expose which security and agent-facing API contracts before becoming mainstream consumer software
- model upgrades should trigger prompt simplification, eval-backed reasoning-effort choices, and stricter runtime contracts rather than unbounded prompt accumulation
- AI-native application design should be judged by whether agents own operational loops under human governance, not merely whether AI assists a human-operated UI
- AI-native startup design should preserve stage-specific evidence gates: faster research, coding, and automation only help if validation, scope, security, metrics, and handoff state stay ahead of execution speed
- self-improving agent claims should be evaluated by whether production feedback becomes structured, replayable, eval-backed improvement work rather than informal prompt tweaking
- automation cheapens already-framed competence and pushes the scarce human role toward framing, taste, review, harness design, and deciding what should matter now
- AI adoption level should be chosen by task stakes, trust calibration, setup / review economics, and available scaffolding rather than by the highest autonomy the tool can demo
- agent eval reports should separate the model, scaffold, task spec, environment, transcript, outcome, grader, aggregation metric, and production-monitoring layer instead of collapsing them into one score
- self-evolving personal-agent runtimes should be judged by whether memory, skills, traces, evals, curator decisions, and rollback paths form an auditable improvement loop
- coding agent adoption should distinguish user habits from runtime guarantees: context hygiene, verifier-first task contracts, thin instruction files, hooks, skills, subagents, and sandbox / permission controls each solve different parts of reliability
- team skill catalogs should be judged as shared procedural memory: routing descriptions, gotchas, progressive disclosure, verification scripts, setup state, usage logging, ownership, and deprecation policy determine whether skills improve agent behavior or become context noise
- agent memory architecture should distinguish static document retrieval, temporal relationship memory, procedural skills, session history, task artifacts, and platform memory instead of treating all persistence as one store
- table-native agent workflows should be judged by whether rows, columns, triggers, approval gates, and logs form an auditable runtime rather than merely hiding webhook glue behind a familiar spreadsheet UI
- AI systems engineering should be treated as a system-ownership pattern across ML, RAG, document intelligence, and agentic AI: the durable skill is owning the decision-producing loop, not adopting whichever role title is current.
- agentic technical debt should be reviewed by surface, not only by model choice: markdown configs, model routing, harness state machines, tool contracts, memory, serving, traces, evals, guardrails, and human gates each carry separate failure modes.
- vibe-coded internal tools should be reviewed by runtime boundary, not only app code: generated UI that performs business writes needs identity, permissions, approval, audit logs, scoped resources, and rollback before production use.
- ambient agents should be treated as event-driven systems with model reasoning inserted after a cheap filter; the durable pattern is stream -> filter -> LLM judgment -> human escalation, not chat UI plus background polling.
- agent fine-tuning should be treated as a governed improvement loop over trajectories, relative judging, rewards, checkpoints, eval gates, and rollback paths rather than as a standalone model-training trick.
- RAG reliability should be reviewed at the knowledge-unit layer: chunks, question-answer packets, graph triples, page units, and governance-tagged claims create different retrieval and memory failure modes.
