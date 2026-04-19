# OpenAI harmony response format

## Source

- URL: https://cookbook.openai.com/articles/openai-harmony
- Author: OpenAI
- Published: 2025-08-18 inferred from local clone git history
- Captured: 2026-04-16
- Raw file: `raw/sources/2025/2025-08-18-openai-harmony-response-format.md`
- Imported from workspace path: `../openai-cookbook/articles/openai-harmony.md`

## Main Claims

- `gpt-oss` should be used with the harmony response format
- roles and channels are part of the model control surface
- `analysis`, `commentary`, and `final` separate internal reasoning, tool use, and user-facing output
- `<|return|>` is a decode-time stop token and should be normalized to `<|end|>` when history is persisted
- a correct renderer or template is required for reliable tool calling and turn continuity

## Why It Matters

Prompt formatting is part of the runtime contract. For long-running agents, the message envelope is one of the places where state, reasoning, and tool use are actually carried forward.

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Codex Workflows](../maps/codex-workflows.md)

## Tensions Or Disagreements

- Self-hosters must handle the format directly, while hosted stacks may hide it behind libraries or platform layers
- Keeping reasoning and tool traces in the envelope improves continuity, but raises UI filtering and debug discipline requirements
- The same message structure may not fit every runtime surface equally well

## Open Questions

- How much of this contract should live in repo docs versus runtime libraries
- Whether other agent stacks should standardize on the same channel split
- How to normalize persisted history without losing the information required for later tool calls

## Merge Candidates

- prompt/template choice is part of the runtime surface
- persisted assistant history should normalize `<|return|>` back to `<|end|>`
- tool calls and reasoning channels are part of the state handoff contract for long-running agents
