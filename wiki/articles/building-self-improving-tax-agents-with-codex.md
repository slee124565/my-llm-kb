# Building Self-Improving Tax Agents With Codex

## Source

- URL: https://openai.com/index/building-self-improving-tax-agents-with-codex/
- Author: Aravind Srinivasan and Samay Shamdasani (Thrive Holdings), Arthur Fernandes Araujo and John de Wasseige (OpenAI)
- Publisher: OpenAI
- Published: 2026-05-27
- Captured: 2026-05-27
- Raw file: `raw/sources/2026/2026-05-27-building-self-improving-tax-agents-with-codex.md`

## Main Claims

- Tax AI is presented as a production agent system that improves because practitioner corrections are captured as structured evidence, not because the model passively learns from usage.
- The self-improvement loop has three pillars: stay close to domain practitioners, preserve production traces from source files through filed-return corrections, and convert recurring reviewed failures into tailored evals plus scoped Codex engineering tasks.
- Product traces matter because a changed tax field may mean an extraction miss, mapper gap, unsupported product behavior, practitioner preference, carried-forward prior-year value, or ordinary workflow noise.
- Codex becomes useful when the failure has already been packaged into a bounded task: representative source packages, expected outputs, product scaffold, eval commands, regression suites, and read-only production evidence.
- The article reports concrete product outcomes from the Crete pilot: 7,000 processed returns, roughly one-third tax-prep time savings, up to 97% draft accuracy, about 50% throughput increase, and a rise from one quarter to 86% of returns reaching 75% correct field completion within six weeks.
- The pattern is not tax-specific. It generalizes to domains where expert operators generate valuable corrections and the product can preserve enough evidence to turn those corrections into eval-backed engineering work.

## Why It Matters

This article makes `self-improving agent` concrete by grounding it in a human-supervised production loop. The important claim is not that Codex autonomously improves a deployed product end to end. The stronger and more reusable pattern is that production evidence can be shaped into agent-legible engineering tasks: human experts correct real work, the system turns repeated corrections into eval targets, and Codex operates inside a repo / trace / eval / skill scaffold with explicit validation gates.

For `my-llm-kb`, this is a missing bridge between earlier `Harness Engineering` and `Symphony` notes. `Harness Engineering` explains how to make a repo legible to Codex; `Symphony` explains how issue-level orchestration can scale Codex work; this article shows how a live product can manufacture the right tasks for Codex from operational traces.

## Relation To Existing Concepts

- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): practitioners steer the improvement loop through review and correction, while Codex acts only after the evidence is structured.
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): production traces, targeted evals, regression suites, and task environments form the harness that makes self-improvement bounded.
- [Externalized Agent State](../concepts/externalized-agent-state.md): source packages, predicted fields, practitioner edits, filed-return values, findings, eval datasets, and task results become reusable state outside any single chat or agent run.
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): the system separates writable repo surfaces from read-only production context and scoped tools.
- [Codex Workflows](../maps/codex-workflows.md): Codex is used as an investigation and implementation agent over a pre-scoped engineering task, not as an unbounded autonomous product owner.
- [Long-Running Agents](../maps/long-running-agents.md): the article offers a concrete production feedback loop for improving agents over weeks and months.

## Tensions Or Disagreements

- The article uses strong `self-improving` language, but the durable mechanism is still heavily engineered and human-governed: practitioners label reality, engineers define the scaffold, and Codex works inside eval gates.
- The reported improvements are compelling but domain-specific. Tax workflows have structured final outputs and practitioner corrections that can be compared against filed returns; messier domains may not yield equally clean eval targets.
- Turning corrections into evals requires careful filtering. If expected workflow noise is counted as failure, Codex may optimize the wrong layer.
- The loop depends on sensitive production traces and source documents, so privacy, access control, and read-only evidence boundaries are not optional implementation details.

## Open Questions

- What minimum trace schema is needed before practitioner corrections can reliably become eval targets?
- Which parts of this loop should be product infrastructure, which should be repo-local task packaging, and which should remain manual product judgment?
- How should teams decide when a recurring correction is actionable enough for Codex versus when it should route back to product or domain experts?
- Can this pattern work in workflows where final correctness is subjective, delayed, or only partially observable?

## Merge Candidates

- self-improving agents require structured production evidence, not only deployment plus user feedback
- practitioner corrections become useful to Codex only after they are reviewed, grouped, and converted into bounded eval targets
- production traces should preserve the full path from source material to intermediate extraction, downstream mapping, expert correction, and final output
- Codex task environments should separate writable repo surfaces from read-only production evidence and scoped domain tools
- ambiguous production differences should route back to humans instead of being forced into an automated improvement loop
