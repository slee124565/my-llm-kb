# Long-Running Agent Harnesses

## Summary

Long-running agent harnesses 是讓 agent 能在多輪、多 session、長時間工作中持續推進的執行框架。它通常由任務 contract、artifact handoff、verification rules、execution environment 與 context continuity primitives 組成。

## Why It Matters

真正困難的不是讓 agent 完成單步操作，而是讓它跨時間維持方向、在失敗點停下修復、並把進度留給下一輪。沒有 harness，長任務通常會退化成高成本試錯。

## Current Framing

- incremental progress beats broad one-shot execution
- verification must be part of the loop, not a final afterthought
- initializer / planner / coding-session protocol 可以降低 session drift
- shell、skills、compaction 這類 primitive 是 harness 的底層能力，不是完整解法本身
- 對更成熟的模型而言，部分顯式 harness 步驟可能退化為較輕量的 conversation-first planning 與 doc-driven steering
- 對 Codex 類 workflow 而言，isolated sandboxes、verifiable evidence、async delegation 與 plan artifacts 是同一套 harness 的不同面向
- ticket-level orchestration 把長任務 harness 從「單一 agent session 如何持續」推進到「issue tracker 如何分派、阻塞、重試、恢復與觀測多個 agent run」
- always-on coding agents 需要 bounded concurrency、retry/backoff、per-issue workspace isolation、terminal-state cleanup 與 structured observability，否則只是把多個互動 session 包成更難 debug 的背景程序
- 對高不確定性的長任務，prototyping milestones 與 parallel implementations 也應被視為 harness 技法：先以可驗證的小路徑降風險，再決定是否納入主實作
- Hassabis's agent critique is a useful value test: long autonomous runs and swarms need output that justifies their agent-hours, not only impressive traces or demos
- planner / generator / evaluator 的角色分離，是另一種可把主觀評估與功能驗證納入 loop 的 harness pattern
- context reset 與 compaction 應視為不同控制手段，而不是單純新舊替代
- 在 local personal-agent workflow 中，conversation-first UX 也可以是一種 harness 選擇：把 session、folder 與 model management 隱藏起來，換取更高 steerability
- CLI-first tooling 與 protocol-light integration，可能是另一種 harness 極簡主義，前提是本地 operability 比 protocol purity 更重要
- hosted agent platforms 把部分 harness complexity 產品化：使用者不再自己維運 sandbox、state recovery、credential routing，而是消費 provider-managed runtime primitives
- 對 hosted long-running agents 而言，brain / hands / memory 分離可同時支撐 lazy execution、故障隔離、credential isolation 與多 agent handoff
- 隨模型能力升級，某些 hand-tuned orchestration patch 會迅速失去必要性；由模型供應商維護的 harness，理論上能比每個客戶各自重寫更快跟上
- runtime surface 會改變 harness 責任分工：repo-local coding agent、provider-managed hosted agent、local personal agent，不會共享完全相同的 control surfaces
- 對 provider-managed runtime 而言，quality harness 不能只看離線 eval；routing correctness、cross-platform equivalence、production-side sensitive eval、rollback discipline 與 privacy-aware debugging tooling 都是 load-bearing parts
- 當多個小型 infra bug 疊加且症狀互相干擾時，community feedback 與 postmortem loop 也應被視為 harness 的一部分，而不是事後公關附屬品
- harmony format 把 reasoning、tool calls 與 final answers 排進同一條可恢復的 turn chain，說明 harness 必須同時處理狀態保留與 user-facing normalization
- raw CoT handling 讓「internal trace 必須跨 turn 保留，但不能直接展示」成為 harness 的明確責任，而不是 UI 的臨時細節
- GPT-5.4 / GPT-5.5 prompt guidance makes preambles, phase-preserving assistant replay, validation loops, retrieval budgets, and stop rules part of the long-running harness contract
- GPT-5.5 outcome-first prompting reframes prompt text as a declarative control layer over the harness: prompt defines success, constraints, evidence, permission boundaries, output shape, and stop conditions, while the harness supplies tools, state, observability, recovery, and verification evidence
- gpt-oss verification guidance 顯示 harness 的驗證邊界應涵蓋 API shape、reasoning transport 與 eval bundle，而不只是單一 smoke test
- gpt-oss-safeguard guide 進一步表明，harness 還要把 policy prompt structure、reasoning effort 與 output format 當成可驗證的 control surfaces
- full fire-and-forget agents likely require continual learning and task-context adaptation; patching together current stateless models can help with subtasks but is not yet a complete long-task harness
- Karpathy's long-context warning is a harness constraint: making the token window bigger does not by itself solve long-running multimodal tasks, because the system still needs relevance selection, memory management, verification, and human supervision over longer autonomous runs
- OpenClaw's agentic-engineering workflow treats the agent like a capable engineer with a partial codebase view: guide it to relevant context, discuss intent, let it build, then ask what should be refactored while the session context is still warm
- self-aware harnesses can let an agent inspect and modify its own runtime, but that pushes review, rollback, permissioning, and security audit into the harness contract
- AI-native harnesses should be evaluated by operational loop ownership: whether agents can observe, decide, act, verify, record evidence, and escalate under human governance, rather than merely assisting a human-operated UI
- Codex's Windows sandbox adds a local-machine harness pattern: practical agent safety may require composing OS primitives, dedicated users, firewall rules, restricted tokens, ACLs, setup binaries, and command runners because no single primitive maps cleanly to autonomous coding-agent work
- Codex app primitives split long-running work into three productized harness modes: durable pinned threads for continuity, thread automations for periodic wakeups inside the same context, and Goals for tasks with a measurable verifier and stopping condition.
- Codex `/goal` becomes more reliable when its persistent objective is backed by a concrete local artifact: a small status checklist for batch work, or a design doc with phases, acceptance criteria, tests, and commit gates for refactors.
- Codex Mobile makes several harness controls portable: worktree / branch / environment setup define task isolation before the first prompt, side chat keeps understanding questions out of the execution transcript, and mobile review / steering lets a human unblock long-running work without returning to the desktop.
- Tax AI shows a production self-improvement harness pattern: practitioner corrections are captured as structured review rows, grouped into recurring findings, converted into targeted evals, and then handed to Codex inside a bounded repo / trace / eval / skill environment.
- `After Automation` reframes benchmarks and evals as frame-dependent harness artifacts: a model's score measures performance inside a chosen prompt, verifier, and task boundary, so benchmark saturation should lead to frame analysis rather than simple replacement conclusions.
- abundant AI output makes harness design more valuable, not less: review queues, evals, repo rules, CI, permissions, rollback paths, and workflow gates are how experts absorb the flood of cheap first attempts.
- agent eval harnesses must be treated as part of the long-running harness: tasks, trials, graders, transcripts, outcomes, environment isolation, repeated-run metrics, and transcript review determine whether the system is actually improving.
- Hermes Agent shows a local personal-agent version of the long-running harness: a bounded ReAct loop, turn caps, interruptible tool calls, layered memory, self-authored skills, background skill curation, offline GEPA optimization, isolated profiles, messaging gateways, and cron jobs.
- Self-evolving skill loops are harnesses only if they include reviewable artifacts: skill diffs, execution traces, eval datasets, rubric scores, constraint gates, snapshots, PR flow, and rollback. Without those, skill writing can become unbounded prompt drift.
- Claude Code best practices frame context as a scarce harness resource: long sessions should actively manage file reads, command output, compaction, `/clear`, subagent investigation, and fresh reviewer sessions instead of assuming one growing conversation remains reliable.
- Verifier-first prompting is a user-level harness pattern. Tests, screenshots, expected outputs, lint/build commands, and root-cause acceptance criteria let the agent close a smaller loop before asking the human to judge.
- Plan Mode is a risk-management primitive, not a universal ritual: use it when scope is uncertain, multi-file, or unfamiliar; skip it when the desired diff can be described directly and verified cheaply.
- Verification skills are a reusable harness primitive. When product flows, checkout paths, CLI interactions, CI/CD steps, runbooks, or infra operations recur, a skill can package the driver script, assertions, transcript/video evidence, gotchas, and escalation policy so the agent verifies through the same route every time.
- OSS maintenance skills are harness primitives for recurring repository work: code-change verification, docs sync, example auto-runs, integration tests, release review, OpenAI docs lookup, and PR draft handoff each bind commands, evidence, model judgment, and maintainer-facing output into a repeatable loop.
- Long-running assistants need memory harnesses, not only memory stores: episode ingest, entity resolution, relationship extraction, temporal supersession, retrieval explanation, correction/deletion policy, and namespace isolation all become part of the reliability contract.
- AI systems engineering treats long-running agent reliability as a whole-system problem: planner quality, tool-call reliability, traceability, eval suites, cost budgets, security gates, rollback, and human supervision must be designed together.
- Production agent harnesses should be reviewed as explicit state machines. ReAct, Plan-and-Execute, and Reflexion can be composed, but the harness still needs named states, legal transitions, step limits, retry / recovery policy, budget circuit breakers, trace spans, terminal states, and escalation paths.
- Anthropic's effective-harness pattern makes the minimum cross-session contract concrete: an initializer agent should create runnable setup, structured feature requirements, progress notes, and an initial git baseline; each coding session should pick one feature, verify through the real user path, leave a clean state, commit, and update progress.
- Machine-readable task state is a drift-control surface. A JSON feature list with immutable test descriptions and a narrow mutable `passes` field is safer than a free-form Markdown checklist when agents repeatedly read and update completion state.
- The serving primitive for long-running agents is a session, not a request. Harness design must account for pause/resume, filesystem or external state, idle waiting on tools or humans, heterogeneous run length, and cost models that do not quietly bill idle time as active work.
- Every's `The Eight Levels of AI Adoption` makes Level 5 `Workflows` the adoption threshold where harness design becomes load-bearing: moving beyond autopilot requires explicit planning, review, confidence checks, tests, guardrails, and repeatable output professionalization.
- Long-horizon Codex experiments make durable project memory concrete: `prompt.md` freezes goals and constraints, `plans.md` defines milestones and validation, `implement.md` gives the runbook, and `documentation.md` records status, decisions, demo flow, known issues, and audit evidence.
- Ambient-agent harnesses are long-running by default. They need backpressure control, cheap first-stage filters, bounded LLM wakeups, notification rate limits, replayable event windows, and a clear escalation tier before any irreversible action is allowed.
- Codex App Server shows the harness protocol layer directly: thread persistence, turn lifecycle, item lifecycle, streamed deltas, tool approval pauses, diff artifacts, and client reconnect support are not UI details; they are runtime primitives for long-running coding-agent work.

## Signals From Recent Articles

- [Building a Safe, Effective Sandbox to Enable Codex on Windows](../articles/openai-building-codex-windows-sandbox.md)
- [Building Self-Improving Tax Agents With Codex](../articles/building-self-improving-tax-agents-with-codex.md)
- [Effective Harnesses for Long-Running Agents](../articles/effective-harnesses-for-long-running-agents.md)
- [Shell + Skills + Compaction](../articles/shell-skills-compaction-long-running-agents.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [OpenAI Symphony Codex Orchestration](../articles/openai-symphony-codex-orchestration.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [Harness Design for Long-Running Application Development](../articles/harness-design-for-long-running-application-development.md)
- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [Deep Dive into LLMs like ChatGPT](../articles/deep-dive-into-llms-like-chatgpt.md)
- [Demis Hassabis: Agents, AGI & The Next Big Scientific Breakthrough](../articles/demis-hassabis-agents-agi-next-big-scientific-breakthrough.md)
- [OpenClaw: The Viral AI Agent that Broke the Internet](../articles/openclaw-viral-ai-agent-lex-fridman-peter-steinberger.md)
- [A Postmortem of Three Recent Issues](../articles/a-postmortem-of-three-recent-issues.md)
- [OpenAI harmony response format](../articles/openai-harmony.md)
- [How to handle the raw chain of thought in gpt-oss](../articles/handle-raw-cot.md)
- [Verifying gpt-oss implementations](../articles/verifying-implementations.md)
- [User Guide For Gpt-Oss-Safeguard](../articles/gpt-oss-safeguard-guide.md)
- [OpenAI Prompt Guidance - GPT-5.5](../articles/openai-prompt-guidance-gpt-5-5.md)
- [OpenAI Prompt Guidance - GPT-5.4](../articles/openai-prompt-guidance-gpt-5-4.md)
- [OpenAI Prompt Guidance - GPT-5.3 Codex](../articles/openai-prompt-guidance-gpt-5-3-codex.md)
- [Getting The Most Out Of Codex](../articles/getting-the-most-out-of-codex.md)
- [Codex /goal Playbook](../articles/codex-goal-playbook.md)
- [After Automation](../articles/every-after-automation.md)
- [Demystifying Evals For AI Agents](../articles/demystifying-evals-for-ai-agents.md)
- [Hermes Agent Masterclass](../articles/hermes-agent-masterclass.md)
- [Best Practices For Claude Code](../articles/best-practices-for-claude-code.md)
- [Lessons From Building Claude Code: How We Use Skills](../articles/lessons-from-building-claude-code-how-we-use-skills.md)
- [Using Skills To Accelerate OSS Maintenance](../articles/using-skills-to-accelerate-oss-maintenance.md)
- [Building Agent Memory with Knowledge Graphs](../articles/building-agent-memory-with-knowledge.md)
- [Welcome to The AI Systems Engineer Journey](../articles/welcome-to-the-ai-systems-engineer.md)
- [Hidden Technical Debt in Agentic Systems](../articles/hidden-technical-debt-in-agentic-systems.md)
- [Building a Local Ambient Agent That Never Sleeps](../articles/building-a-local-ambient-agent-that-never-sleeps.md)
- [The Eight Levels of AI Adoption](../articles/every-the-eight-levels-of-ai-adoption.md)
- [Mastering Codex Mobile For Engineering](../articles/mastering-codex-mobile-for-engineering.md)
- [Run Long Horizon Tasks With Codex](../articles/run-long-horizon-tasks-with-codex.md)
- [Unlocking The Codex Harness](../articles/unlocking-the-codex-harness.md)

## Open Questions

- 最小可用 harness contract 是什麼
- what evidence threshold should prove that a multi-hour agent run is worth its compute, coordination, and review cost
- reinforcement、compaction、subagent handoff 應如何組合
- coding 與 non-coding workload 是否應共用同一種 harness 骨架
- 隨模型能力提升，哪些 harness 元件可被簡化，哪些不能
- async remote execution 與 repo-local long session 各自應由哪些 control surfaces 承擔
- ticket state machine、blocker graph、workspace lifecycle 與 workflow prompt 應如何拆分責任，才不會把 orchestration policy 寫死在 runner 裡
- evaluator 在主觀品質任務中的 role，是否能穩定遷移到一般產品 QA
- hosted managed runtime 與 repo-local harness 之間，最小可攜 contract 應如何定義，才能降低平台綁定
- provider-managed runtime 要如何在不放寬隱私邊界的前提下，維持足夠敏感的 regression detection 與 root-cause debugging 能力
- plan 內的 prototype path 與正式 path 應如何分流，才不會讓 living document 過厚又失去可執行性
- raw reasoning persistence 和 user-facing safety 之間，應如何設計最小可用的 state handoff contract
- verification bundle 的最小組合應如何分層，才不會把 smoke test 和 production-grade eval 混為一談
- safety prompt 的驗證應否成為 harness 的標準步驟，而不是額外手工檢查
- preamble / phase / final-answer separation 應作為所有 long-running Responses workflow 的基礎 contract，還是只在 tool-heavy agent 中使用
- self-modifying agent runtimes need which minimum review, rollback, and local security evidence before they are safe for non-expert users
- 哪些 loops 應由 agent 擁有，哪些應由 human supervisor approval 保留，應如何用 confidence、risk、source lineage 與 reversibility 分層
- when sandbox setup modifies host security state, which receipts, health checks, and rollback paths should the harness expose before users trust long-running local agent work
- scheduled automations、thread automations 與 Goals 應如何分層，才能同時保留 continuity、bounded execution、evidence 與 human approval
- production trace schema、review taxonomy、targeted evals 與 regression suites 的最小組合是什麼，才能讓 Codex safely close an improvement loop
- benchmark reports should expose which parts of apparent capability come from model weights, prompt framing, harness scaffolding, verifier design, and human scoring judgment
- agent reliability metrics should distinguish `pass@k` style opportunity for one success from `pass^k` style consistency across repeated runs
- always-on personal agents need profile isolation, schedule visibility, secret boundaries, skill versioning, and curator / optimizer audit logs before cron-driven autonomy is safe
- verification skills should be built first for which workflows: highest frequency, highest failure cost, easiest programmatic assertions, or largest human review bottleneck
- temporal graph memory should be tested with what fixtures: stale fact replacement, same-name entity disambiguation, multi-hop recall, deletion/correction requests, and source-episode attribution
- what minimum workflow harness is required before a team moves a task from supervised agent use to autopilot, always-on assistant, multi-agent, or orchestrator mode
- which long-running task types need a full spec / plan / runbook / documentation file stack, and which can safely rely on a lighter checklist plus validation commands
- when an initializer agent expands a vague product prompt into hundreds of feature checks, what review gate prevents the long-running harness from faithfully executing the wrong spec

## Related Pages

- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Agent Memory Architecture](agent-memory-architecture.md)
- [Agent Evaluations](agent-evaluations.md)
- [AI Systems Engineering](ai-systems-engineering.md)
- [Externalized Agent State](externalized-agent-state.md)
- [Human-Supervised Agent Ops](human-supervised-agent-ops.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [Prompt Migration And Agent Steerability](prompt-migration-and-agent-steerability.md)
- [Long-Running Agents](../maps/long-running-agents.md)
