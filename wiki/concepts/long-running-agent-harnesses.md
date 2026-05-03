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
- gpt-oss verification guidance 顯示 harness 的驗證邊界應涵蓋 API shape、reasoning transport 與 eval bundle，而不只是單一 smoke test
- gpt-oss-safeguard guide 進一步表明，harness 還要把 policy prompt structure、reasoning effort 與 output format 當成可驗證的 control surfaces
- full fire-and-forget agents likely require continual learning and task-context adaptation; patching together current stateless models can help with subtasks but is not yet a complete long-task harness
- OpenClaw's agentic-engineering workflow treats the agent like a capable engineer with a partial codebase view: guide it to relevant context, discuss intent, let it build, then ask what should be refactored while the session context is still warm
- self-aware harnesses can let an agent inspect and modify its own runtime, but that pushes review, rollback, permissioning, and security audit into the harness contract

## Signals From Recent Articles

- [Effective Harnesses for Long-Running Agents](../articles/effective-harnesses-for-long-running-agents.md)
- [Shell + Skills + Compaction](../articles/shell-skills-compaction-long-running-agents.md)
- [Shipping at Inference-Speed](../articles/shipping-at-inference-speed-peter-steinberger.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [OpenAI Symphony Codex Orchestration](../articles/openai-symphony-codex-orchestration.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [Harness Design for Long-Running Application Development](../articles/harness-design-for-long-running-application-development.md)
- [Claude Managed Agents](../articles/claude-managed-agents.md)
- [Demis Hassabis: Agents, AGI & The Next Big Scientific Breakthrough](../articles/demis-hassabis-agents-agi-next-big-scientific-breakthrough.md)
- [OpenClaw: The Viral AI Agent that Broke the Internet](../articles/openclaw-viral-ai-agent-lex-fridman-peter-steinberger.md)
- [A Postmortem of Three Recent Issues](../articles/a-postmortem-of-three-recent-issues.md)
- [OpenAI harmony response format](../articles/openai-harmony.md)
- [How to handle the raw chain of thought in gpt-oss](../articles/handle-raw-cot.md)
- [Verifying gpt-oss implementations](../articles/verifying-implementations.md)
- [User Guide For Gpt-Oss-Safeguard](../articles/gpt-oss-safeguard-guide.md)

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
- self-modifying agent runtimes need which minimum review, rollback, and local security evidence before they are safe for non-expert users

## Related Pages

- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Externalized Agent State](externalized-agent-state.md)
- [Repository Knowledge As System Of Record](repository-knowledge-as-system-of-record.md)
- [Long-Running Agents](../maps/long-running-agents.md)
