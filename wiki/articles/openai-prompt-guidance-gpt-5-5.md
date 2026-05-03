# OpenAI Prompt Guidance - GPT-5.5

## Source

- URL: https://developers.openai.com/api/docs/guides/prompt-guidance?model=gpt-5.5
- Author: OpenAI
- Published: Unknown
- Captured: 2026-05-03
- Raw file: `raw/sources/2026/2026-05-03-openai-prompt-guidance-gpt-5-5.md`

## Main Claims

- GPT-5.5 prompt migration should start by shortening legacy prompt stacks: define outcome, success criteria, constraints, available context, and final-answer shape instead of over-specifying every process step.
- `low` and `medium` reasoning effort should be re-evaluated before escalating, because GPT-5.5's improved reasoning efficiency can make old high-effort defaults unnecessarily expensive or slow.
- Preambles remain useful in streaming, tool-heavy, or long-running workflows because they improve perceived responsiveness without replacing the actual task work.
- Customer-facing assistants need separate controls for personality and collaboration style; tone instructions should not carry goals, tool rules, success criteria, or stopping conditions.
- Grounding, citations, retrieval budgets, and validation rules should be explicit when evidence quality or high-impact actions matter.
- For Responses workflows, `phase` handling and assistant-item replay are part of the prompt/runtime contract, not only formatting details.

## Why It Matters

This guide shifts prompt design away from dense instruction blobs and toward outcome-first contracts. For this repo, the durable takeaway is that model upgrades should trigger prompt simplification plus better success criteria, not only additive prompt patches.

## Relation To Existing Concepts

- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md)
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)

## Tensions Or Disagreements

- Shorter prompts can improve model latitude, but production systems still need explicit invariants for safety, side effects, output contracts, and missing evidence.
- Preambles improve perceived responsiveness, but they require runtime support to avoid confusing intermediate updates with final answers.
- Reasoning effort tuning should be eval-driven; intuition about "harder task means higher effort" may waste latency and tokens.

## Open Questions

- Which existing repo prompts should be simplified first when moving to GPT-5.5-style prompting?
- How should prompt assets record the difference between true invariants and softer decision rules?
- What minimal eval should prove that an outcome-first prompt has not lost important operational guardrails?

## Merge Candidates

- Newer model prompt migration should remove process-heavy legacy instructions before adding new ones.
- Personality, collaboration style, success criteria, tool rules, and stopping conditions should be separate prompt surfaces.
- Preambles and `phase` fields are part of long-running agent UX and runtime correctness.
- Retrieval budgets and missing-evidence behavior should be explicit in evidence-sensitive tasks.
