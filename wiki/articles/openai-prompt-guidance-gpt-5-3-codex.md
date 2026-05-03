# OpenAI Prompt Guidance - GPT-5.3 Codex

## Source

- URL: https://developers.openai.com/api/docs/guides/prompt-guidance?model=gpt-5.3-codex
- Author: OpenAI
- Published: Unknown
- Captured: 2026-05-03
- Raw file: `raw/sources/2026/2026-05-03-openai-prompt-guidance-gpt-5-3-codex.md`

## Main Claims

- GPT-5.3 Codex prompting is presented as a full coding-agent operating contract: autonomy, implementation discipline, editing constraints, repo exploration, planning, frontend behavior, tool rules, and final reporting.
- `AGENTS.md` is a first-class repo-local steering surface; it should orient the agent to local rules, scope, validation, and handoff expectations.
- Mid-rollout user updates are part of the interaction contract, especially for long-running or tool-heavy work.
- Tool definitions are not just API plumbing. `apply_patch`, shell execution, update-plan, image inspection, custom search, and parallel tool calling all shape what work the agent can safely and efficiently perform.
- Coding-agent prompts should explicitly guard user work: inspect before editing, avoid reverting unrelated changes, prefer targeted validation, and report unrun checks.
- Preambles, `phase`, personality, and metaprompting are runtime/prompt surfaces that affect how Codex communicates, recovers, and debugs its own failures.

## Why It Matters

This guide is the strongest bridge between prompt guidance and repo-local agent workflow. It treats a coding agent prompt as operational infrastructure: the prompt tells the model how to read a repo, edit files, protect user work, use tools, validate, and hand off.

## Relation To Existing Concepts

- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Codex Workflows](../maps/codex-workflows.md)

## Tensions Or Disagreements

- A comprehensive Codex prompt reduces ambiguity but can become too large if repo-specific rules are duplicated instead of delegated to `AGENTS.md` and local docs.
- More autonomy improves momentum, but the prompt still needs crisp boundaries for destructive commands, external side effects, and user-owned dirty worktrees.
- Parallel tool calling and subagent delegation can speed exploration, but only when subtasks are independent and write scopes are clear.

## Open Questions

- Which parts of the Codex starter prompt should live in global agent instructions versus repo-local `AGENTS.md`?
- How thin can `AGENTS.md` remain while still protecting user work and preserving validation discipline?
- Should this repo's prompt assets borrow the Codex guide's explicit sections for autonomy, editing constraints, and final handoff?

## Merge Candidates

- Codex prompting is a repo workflow contract, not only a tone or response-style prompt.
- `AGENTS.md` is a durable steering surface for repo-local agent behavior.
- Tool affordances and tool response limits should be reflected in prompt design.
- User updates, validation reporting, and non-destructive editing are core coding-agent prompt requirements.
