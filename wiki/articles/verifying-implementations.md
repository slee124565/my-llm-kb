# Verifying gpt-oss implementations

## Source

- URL: https://cookbook.openai.com/articles/gpt-oss/verifying-implementations
- Author: OpenAI
- Published: 2025-08-11 inferred from local clone git history
- Captured: 2026-04-16
- Raw file: `raw/sources/2025/2025-08-11-verifying-gpt-oss-implementations.md`
- Imported from workspace path: `../openai-cookbook/articles/gpt-oss/verifying-implementations.md`

## Main Claims

- gpt-oss implementations need verification for prompt formatting, reasoning transport, and inference-code differences
- a provider that claims compatibility should test both API shape and tool-calling behavior, not just generation quality
- the recommended smoke test is a compatibility test suite, followed by evals such as AIME, GPQA, and Healthbench
- passing a test harness is useful but not sufficient; verification is a layered process
- raw reasoning and harmony formatting are not optional details, because they affect the correctness of subsequent turns

## Why It Matters

This makes verification part of the runtime contract. For agent stacks, the question is not only whether a model can answer, but whether the whole execution surface can be trusted to preserve structure, reasoning, and tool behavior over time.

## Relation To Existing Concepts

- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md)
- [Externalized Agent State](../concepts/externalized-agent-state.md)
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md)
- [Long-Running Agents](../maps/long-running-agents.md)

## Tensions Or Disagreements

- Compatibility tests are smoke tests, not proof of complete correctness
- Benchmark parity can hide provider-specific regressions in real workflow surfaces
- A harness can verify one API shape while still missing subtle state-preservation bugs across turns

## Open Questions

- What minimal verification bundle should a provider run before claiming gpt-oss support
- How should repos store regression evidence when provider behavior changes
- Which parts of compatibility testing belong in CI versus ad hoc manual validation

## Merge Candidates

- prompt formatting, reasoning transport, and inference code are all part of implementation correctness
- verification should include both API-shape tests and evals
- long-running harnesses should treat runtime compatibility as an ongoing contract, not a one-time check
