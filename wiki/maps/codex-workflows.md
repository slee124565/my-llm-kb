# Codex Workflows

## Scope

這個 map 聚焦於 Codex 作為 coding agent 的主要 workflow：repo guidance、async delegation、execution evidence、planning artifacts、harness design、ticket-level orchestration，以及為重複資料面打造可組合 CLI surface。

## Entry Points

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md)

## Core Concepts

- repository knowledge as system of record
- agent runtime surfaces
- externalized agent state
- human-supervised agent ops
- long-running agent harnesses
- prompt migration and agent steerability
- async delegation with verifiable evidence
- ticket tracker as agent control plane
- CLI-first operability plus companion skills for repeated noisy data surfaces
- OS-enforced local sandboxing for agent command execution

## Key Articles

- [Best Practices For Claude Code](../articles/best-practices-for-claude-code.md)
- [Lessons From Building Claude Code: How We Use Skills](../articles/lessons-from-building-claude-code-how-we-use-skills.md)
- [Using Skills To Accelerate OSS Maintenance](../articles/using-skills-to-accelerate-oss-maintenance.md)
- [Run Long Horizon Tasks With Codex](../articles/run-long-horizon-tasks-with-codex.md)
- [Introducing Codex](../articles/introducing-codex.md)
- [Building a Safe, Effective Sandbox to Enable Codex on Windows](../articles/openai-building-codex-windows-sandbox.md)
- [Building Self-Improving Tax Agents With Codex](../articles/building-self-improving-tax-agents-with-codex.md)
- [Bespoke CLIs for Codex](../articles/bespoke-clis-for-codex.md)
- [Harness Engineering](../articles/harness-engineering-codex-agent-first-world.md)
- [OpenAI Symphony Codex Orchestration](../articles/openai-symphony-codex-orchestration.md)
- [Using PLANS.md for Multi-Hour Problem Solving](../articles/using-plans-md-for-multi-hour-problem-solving.md)
- [Getting The Most Out Of Codex](../articles/getting-the-most-out-of-codex.md)
- [Codex /goal Playbook](../articles/codex-goal-playbook.md)
- [Getting Started With Loops](../articles/2026-07-06-getting-started-with-loops.md)
- [A Field Guide to Fable: Finding Your Unknowns](../articles/2026-07-03-a-field-guide-to-fable-finding-your-unknowns.md)
- [Mastering Codex Mobile For Engineering](../articles/mastering-codex-mobile-for-engineering.md)
- [Unlocking The Codex Harness](../articles/unlocking-the-codex-harness.md)
- [OpenAI Prompt Engineering - GPT-3.5 Era](../articles/openai-prompt-engineering-gpt-3-5-era.md)
- [OpenAI Prompt Guidance - GPT-5.3 Codex](../articles/openai-prompt-guidance-gpt-5-3-codex.md)
- [OpenAI Prompt Guidance - GPT-5.4](../articles/openai-prompt-guidance-gpt-5-4.md)
- [OpenAI Prompt Guidance - GPT-5.5](../articles/openai-prompt-guidance-gpt-5-5.md)
- [OpenClaw Takes Over The Internet](../articles/openclaw-takes-over-the-internet-peter-steinberger.md)
- [OpenClaw: The Viral AI Agent that Broke the Internet](../articles/openclaw-viral-ai-agent-lex-fridman-peter-steinberger.md)
- [Notes From a Marketer Building a Real CLI With Codex](../articles/notes-from-a-marketer-building-a-real-cli-with-codex.md)
- [After Automation](../articles/every-after-automation.md)
- [The Eight Levels of AI Adoption](../articles/every-the-eight-levels-of-ai-adoption.md)

## Key People Or Labs

- OpenAI
- Ryan Lopopolo
- Aaron Friel

## Open Threads

- 什麼時候應該用 remote async task，什麼時候應該留在 local interactive loop
- Codex 類 repo-local workflow 和 hosted managed runtime、local personal agent 之間，哪些 state surfaces 可以共享
- `AGENTS.md` 應該保持多薄，才不會又退化成 instruction blob
- plan-heavy workflow 與 lightweight conversation-first workflow 的最佳切換門檻是什麼
- ticket-level orchestration 應該接 routine implementation、migration、investigation，還是也能承接高 judgment 的產品決策工作
- Codex 類 workflow 可以吸收多少 personal-agent pattern，例如 markdown memory ownership、CLI-first tooling 與 conversation-first steerability
- 什麼時候應該直接用 connector / MCP，什麼時候應該再往上編譯成 agent-friendly CLI 與 companion skill
- 在 agent 幫忙做工具時，哪些 product judgment 應該保持在 human loop，而不是被 prompt 或自動化完全吸收
- OpenClaw-style agentic engineering can transfer which habits to Codex: short conversational prompts, guiding the agent's codebase view, post-build refactor prompts, and designing codebases for fresh-session navigation
- Codex prompt design should be split across global operating rules, repo-local `AGENTS.md`, task prompts, tool affordances, and validation evidence rather than one ever-growing instruction blob
- agent-first product work should distinguish building AI-assisted tools for human operators from building agent-operated systems with human supervisor surfaces
- local Codex workflows need a visible sandbox health contract: setup, firewall policy, writable roots, network mode, and command-runner evidence are part of the workflow surface, not background implementation detail
- Codex app workflow now has a broader operating pattern: durable pinned threads carry continuity, side panel carries artifact review, browser/Chrome/computer-use/MCP/connectors carry reach, thread automations/Goals carry continuation, and vault/repo memory carries cross-thread state
- production systems can manufacture high-quality Codex tasks when they preserve traces, review human corrections, group repeated failures, and convert them into targeted evals with explicit regression gates
- Codex as a work OS shifts the human role toward sandwiching agent work: set the frame, let agents collapse the task, then judge, redirect, and turn the result into the next useful slice
- `/goal` work should be paired with a visible execution artifact: checklist for batch work, design doc plus phases for refactors, acceptance criteria for each phase, and commit/test gates after verified progress
- Claude Code best practices add a comparable local-terminal workflow lens: verifier-first prompts, scoped context, thin persistent instructions, Plan Mode only when uncertainty warrants it, and fresh-context reviewer sessions should be treated as workflow control surfaces rather than generic prompt tips
- Claude Code skill practice adds a companion-skill design lens for Codex: reusable workflow knowledge should be packaged with routing descriptions, gotchas, scripts, setup state, verification evidence, and owner / promotion rules rather than only as long task prompts
- OpenAI Agents SDK maintenance adds an OSS-scale Codex workflow lens: keep mandatory triggers in `AGENTS.md`, put repeatable procedure in repo-local skills, push deterministic mechanics into scripts, preserve evidence in logs / rerun files / release diffs, and reserve human review for high-judgment API, architecture, migration, and release decisions.
- Codex adoption should not be measured by reaching maximum autonomy; chatbot, copilot, agent, autopilot, workflow, Goal, and orchestration modes each fit different task stakes and review economics
- Codex Mobile should be treated as a supervisor/control plane over connected engineering hosts: it is strongest when it lets humans select task boundaries, capture mobile context, steer runs, add review comments, and unblock bounded decisions without pretending the phone is the execution environment
- Long-horizon Codex delegation needs a durable file stack, not just a long prompt: spec, milestone plan, implementation runbook, documentation/status, validation commands, and worktree isolation together define what the agent should keep doing and how humans can review it.
- Codex App Server turns the Codex harness into an embeddable product runtime: clients integrate through thread / turn / item events, streamed assistant deltas, tool approvals, diff artifacts, and reconnectable session state rather than a flat request/response API.
- Claude Code's loop taxonomy is useful for Codex workflow design too: interactive prompts, Goals, automations, skills, and scheduled routines should be chosen by trigger and stop condition, then bounded with verification artifacts and usage evidence.
- Before a Codex Goal or long-horizon implementation run, ambiguous work should often start with unknown discovery: ask for blindspot passes, architecture-changing questions, throwaway prototypes, source-code references, and implementation-note discipline so the agent does not efficiently execute the wrong map.
