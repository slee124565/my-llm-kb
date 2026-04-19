# How to handle the raw chain of thought in gpt-oss

## Source

- URL: https://cookbook.openai.com/articles/gpt-oss/handle-raw-cot
- Author: OpenAI
- Published: 2025-08-05 inferred from local clone git history
- Captured: 2026-04-16
- Raw file: `raw/sources/2025/2025-08-05-how-to-handle-the-raw-chain-of-thought-in-gpt-oss.md`
- Imported from workspace path: `../openai-cookbook/articles/gpt-oss/handle-raw-cot.md`

## Main Claims

- raw chain-of-thought is intended for implementors and should not be shown to end users
- in the harmony format, raw reasoning is carried in the `analysis` channel
- subsequent turns must preserve reasoning until the model has produced a final response, especially when tool calls are involved
- Responses API and Chat Completions implementations need explicit reasoning fields or reasoning-text events so the raw CoT can be handed back safely
- raw reasoning is part of the execution state that makes tool calling work across turns

## Why It Matters

This is a direct statement about externalized state: the useful internal trace must survive turn boundaries, but the user-facing surface must not expose it raw.

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)

## Tensions Or Disagreements

- Keeping raw CoT available improves tool-use continuity, but also raises safety, privacy, and disclosure risk
- API providers may expose the same underlying behavior through different field names or event shapes
- A UI can summarize reasoning safely, but that summary is not a substitute for the raw trace when the next turn depends on it

## Open Questions

- Where should repo-local workflows store raw reasoning versus user-facing summaries
- How to hide raw reasoning from end users without losing debug usefulness
- Which provider-level conventions are stable enough to become shared workflow assumptions

## Merge Candidates

- raw reasoning is internal state, not user-facing content
- tool-call loops should retain analysis until a final response closes the turn
- reasoning should be represented as a structured, recoverable field when subsequent turns need it
