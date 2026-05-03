# OpenAI Prompt Guidance - GPT-5.4

## Source

- URL: https://developers.openai.com/api/docs/guides/prompt-guidance?model=gpt-5.4
- Author: OpenAI
- Published: Unknown
- Captured: 2026-05-03
- Raw file: `raw/sources/2026/2026-05-03-openai-prompt-guidance-gpt-5-4.md`

## Main Claims

- GPT-5.4 is positioned for production assistants and agents that need reliable multi-step execution, evidence-rich synthesis, long-context work, style control, and structured output contracts.
- The model benefits from explicit output contracts, compact verbosity controls, default follow-through policies, and clear instruction priority when users change task, tone, or format mid-conversation.
- Tool use should be persistent when correctness depends on it, especially early in a session or when retrieval, terminal work, or coding validation can fail silently.
- Long-horizon tasks need explicit completeness checks, verification loops before high-impact actions, and research/citation rules that bind final claims to retrieved evidence.
- Coding and terminal agents need clear tool boundaries, brief user updates, validation expectations, and explicit treatment of intermediate updates versus final answers.
- Prompt migration to GPT-5.4 should happen one change at a time and treat reasoning effort as a last-mile tuning knob.

## Why It Matters

This guide is a production prompt contract checklist. It connects prompt design to runtime correctness: output shape, tool persistence, citations, validation, phase handling, and reasoning effort all become control surfaces for reliable agent behavior.

## Relation To Existing Concepts

- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Repository Knowledge As System Of Record](../concepts/repository-knowledge-as-system-of-record.md)

## Tensions Or Disagreements

- The guide asks for explicit contracts, but also says to start with the smallest prompt that passes evals. That creates a useful migration discipline: add blocks only for measured failure modes.
- Persistent tool use improves correctness but can increase cost, latency, and UI noise if the harness lacks good progress updates.
- Structured output contracts reduce ambiguity, but over-structuring can make answers feel mechanical or too heavy for simple user requests.

## Open Questions

- Which prompt assets in this repo should adopt explicit default follow-through and high-impact verification policies?
- Should coding-agent user updates be standardized as a reusable repo-local prompt block?
- How should the KB record reasoning-effort decisions when they are workload-specific rather than model-global?

## Merge Candidates

- GPT-5.4-style prompting treats output contracts, tool persistence, evidence rules, and verification loops as production control surfaces.
- Prompt migrations should be incremental and eval-backed.
- Reasoning effort is a tuning knob, not a default proxy for quality.
- Coding-agent prompts should define shell/tool boundaries and validation behavior explicitly.
