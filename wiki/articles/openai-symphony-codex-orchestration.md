# OpenAI Symphony Codex Orchestration

## Source

- URL: https://openai.com/index/open-source-codex-orchestration-symphony/
- Author: Alex Kotliarskyi, Victor Zhu, and Zach Brock
- Published: 2026-04-27
- Captured: 2026-04-28
- Raw file: `raw/sources/2026/2026-04-27-openai-symphony-codex-orchestration.md`
- Imported from workspace path: `/Users/lee/ws/myBrainFood/blog/2026-04-28-an-open-source-spec-for-codex-orchestration-symphony/2026-04-28-an-open-source-spec-for-codex-orchestration-symphony.md`

## Main Claims

- Interactive coding agents hit a human-attention ceiling: engineers can supervise only a few live sessions before context switching becomes the bottleneck.
- Symphony reframes coding-agent work around deliverables in an issue tracker, not around sessions or pull requests.
- In the Symphony model, each eligible Linear issue maps to an isolated workspace and a continuously managed Codex run; the issue board becomes the control plane.
- Ticket state, blockers, retries, per-issue workspaces, structured logs, runtime metrics, and `WORKFLOW.md` together form the orchestration contract.
- The article reports a 500% increase in landed pull requests on some OpenAI teams, but its deeper claim is behavioral: lower coordination cost makes speculative implementation and exploration cheap.
- The open-source artifact is intentionally a spec plus reference implementation, not a product; teams are expected to adapt the pattern to their own tracker, repo, and trust posture.

## Why It Matters

This article is the follow-up to OpenAI's `Harness Engineering` post. The earlier post framed how to make a repo legible and operable for Codex; Symphony moves the bottleneck up one level, from single-agent execution to multi-task work management. Its durable contribution is the idea that an issue tracker plus repo-owned workflow contract can become an always-on agent orchestrator.

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Codex Workflows](../maps/codex-workflows.md)
- [Long-Running Agents](../maps/long-running-agents.md)

## Article-Level Claims

- Issue trackers can act as state machines for agent work, where active states dispatch agents, blocker relationships define dependency order, and terminal states drive cleanup.
- A task can legitimately produce multiple PRs, no PR, an investigation packet, or new child issues; tying orchestration too tightly to PRs loses this flexibility.
- Failures are treated as harness feedback: instead of manually patching missed work, the team adds guardrails, skills, documentation, QA smoke tests, or app-driving capabilities.
- `WORKFLOW.md` turns previously implicit team process into a versioned prompt and runtime contract that agents can follow and teams can revise.
- Codex App Server gives an orchestration layer a cleaner integration point than driving terminal sessions directly, because it exposes headless thread and turn control.
- Dynamic tool calls can expose constrained tracker operations to agents without leaking full credentials into subagent containers.

## Merge Candidates

- ticket-level orchestration shifts agent management from session supervision to deliverable management
- issue trackers can become agent control planes when their states, blockers, and comments are treated as runtime state
- `WORKFLOW.md` is a repo-owned process contract, not just a prompt file
- always-on coding agents need bounded concurrency, retry semantics, workspace isolation, and operator-visible logs
- cheaper speculative work changes team behavior, broadening who can initiate implementation and exploration tasks

## Tensions Or Disagreements

- Symphony fits routine implementation, migration, cleanup, and investigation work better than tasks that require frequent mid-flight judgment.
- A tracker-as-control-plane model increases leverage only if the tracker states, issue quality, repo docs, and validation loops are already disciplined enough for agents to consume.
- The article's throughput numbers are OpenAI-internal signals; they should be treated as directional evidence, not a guaranteed outcome for smaller teams or less agent-ready repos.
- The spec deliberately avoids prescribing a single sandbox or approval posture, so adopters must still design their own trust boundary.

## Open Questions

- When should a team keep work in an interactive Codex session instead of filing it into an always-on orchestrator?
- What is the minimum issue quality bar before an agent can safely pull work without human pre-triage?
- How should `WORKFLOW.md`, `AGENTS.md`, and project docs divide responsibility in a repo that uses ticket-level orchestration?
- Which Symphony concepts should remain tracker-specific, and which should become a portable coding-agent orchestration contract?
