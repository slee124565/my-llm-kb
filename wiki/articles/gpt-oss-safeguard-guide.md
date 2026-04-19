# User Guide For Gpt-Oss-Safeguard

## Source

- URL: https://cookbook.openai.com/articles/gpt-oss-safeguard-guide
- Author: ROOST and OpenAI
- Published: 2026-03-24 inferred from local clone git history
- Captured: 2026-04-16
- Raw file: `raw/sources/2026/2026-03-24-gpt-oss-safeguard-guide.md`
- Imported from workspace path: `../openai-cookbook/articles/gpt-oss-safeguard-guide.md`

## Main Claims

- gpt-oss-safeguard is a policy-following safety model for Trust & Safety workflows
- it should be paired with the harmony response format so reasoning stays structured and recoverable
- policy prompts work best when they are explicit, compact, and broken into instruction, definitions, criteria, and examples
- output instructions should be literal and reinforced, not implied
- policy length and reasoning effort are practical controls over quality and latency

## Why It Matters

This article extends the runtime-surface discussion beyond generic reasoning and into policy-driven classification. It shows that the execution surface now includes policy text, reasoning depth, and output contract, not just the model call itself.

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)

## Tensions Or Disagreements

- A compact policy prompt is easier to reason about, but some safety domains will still require longer context
- The harmony format improves recoverability, but it also raises the bar for correct implementation and persistence
- Safety workflows need explicit outputs, but over-specifying the output can reduce flexibility for borderline cases

## Open Questions

- How much of a safety policy should live in repo-local docs versus runtime code
- Which parts of policy prompting should be standardized across repos and which should remain domain-specific
- Where should reasoning effort defaults be set and reviewed

## Merge Candidates

- policy prompt structure is part of the runtime contract
- reasoning effort and prompt length are control surfaces, not afterthoughts
- explicit output formats are required for safety workflows that need auditability and repeatable downstream handling
