# After Automation

## Source

- URL: https://every.to/p/after-automation
- Author: Dan Shipper
- Publisher: Every
- Published: 2026-05-21
- Captured: 2026-05-27
- Raw file: `raw/sources/2026/2026-05-21-every-after-automation.md`
- Workspace provenance: copied from `refs/my-blog-kb/raw/inbox/every-after-automation.md`

## Main Claims

- AI automation does not simply remove human work in expert knowledge work; it makes yesterday's framed competence cheap and creates more demand for current human judgment, taste, review, and system design.
- Work with agents is splitting into two modes: `agent employees` that can be delegated bounded jobs, and human-agent collaboration surfaces such as Codex / Claude Code / Claude Cowork that act more like operating systems for complex work.
- Employee-style agents still require ownership, maintenance, calibration, and team-level stewardship. Personal or team agents go stale when no human keeps their context, skills, workflows, and quality loop alive.
- The scarce human role moves to framing: deciding what matters, setting the task boundary, judging output, converting results into real decisions, and building review queues, evals, harnesses, repo rules, CI, permissions, and workflows.
- Benchmarks measure model performance inside a frame. When a benchmark saturates, the frame can be changed to expose a new edge, so benchmark progress should not be confused with the model replacing the human framer.
- Cheap model competence stimulates demand: if codebase rewrites become easy, many more people will attempt rewrites, which increases the need for senior judgment about scope, invariants, migration, rollback, data, and review.
- Even a strong AGI-like always-on agent would still operate under goals, reward signals, or progress definitions supplied by a framer. The article argues that the frame is not the framer.
- Current AI agents have autonomy in task execution but not agency in the human sense of having their own ends; they act on behalf of human operators rather than independently choosing what should matter.

## Why It Matters

This article strengthens a recurring thesis in this repo: AI shifts the bottleneck upward. Earlier sources framed this around coding, startup operation, and self-improving production loops. Shipper adds a more general mechanism: automation cheapens work that has already been framed, which floods the system with acceptable-but-generic output and increases demand for expert judgment at the next boundary.

For `my-llm-kb`, the most reusable contribution is the distinction between `frame` and `framer`. It explains why better agent benchmarks and stronger task execution do not remove human-supervised harness design. Instead, they make framing, evaluation, permissioning, rollback, and taste more valuable because more people can now act inside the old frame.

## Relation To Existing Concepts

- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): humans become framers, supervisors, reviewers, and system designers rather than step-by-step operators.
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): broader automation increases the need for review queues, evals, CI, permissions, workflows, and rollback surfaces.
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): the article distinguishes delegated `agent employee` surfaces from collaborative work OS surfaces where humans and multiple agents share tools and context.
- [Prompt Migration And Agent Steerability](../concepts/prompt-migration-and-agent-steerability.md): benchmark and prompt performance depends on framing; changing the prompt changes what is being measured.
- [Codex Workflows](../maps/codex-workflows.md): Codex is framed as a work operating system, not only a code generator.
- [LLM Agents](../maps/llm-agents.md): the article adds a broad theory of why agent progress creates more expert work at the current edge.

## Tensions Or Disagreements

- The article is based heavily on Every's internal early-adopter experience, so it is strongest for expert knowledge work and may not generalize cleanly to all labor markets.
- The `frame is not the framer` thesis is useful, but it can understate the possibility that future systems will better propose, compare, and revise frames under human goals.
- The article rejects a simple job-replacement tipping point, but it does not prove that all affected roles will benefit equally; increased demand for experts can coexist with disruption to less differentiated work.
- Its AGI definition, `when it makes economic sense to keep your agent running continuously`, is operationally useful but narrower than many research or policy definitions.

## Open Questions

- What minimum artifacts let human framers stay ahead of agent execution: problem brief, invariants, evidence threshold, eval target, rollback plan, and review rubric?
- When does an `agent employee` need a named owner, maintenance budget, skills repository, or team-level quality harness?
- How should benchmark reports separate model capability from the intelligence embedded in prompt, harness, data selection, verifier, and scoring frame?
- Which parts of expert judgment can be reliably externalized into repo rules, evals, workflows, and supervisor planes, and which must remain live human taste?
- How should organizations measure whether automation is producing differentiated work rather than merely increasing output volume?

## Merge Candidates

- automation cheapens framed competence, then raises the value of human framing, taste, review, and system design
- agents as employees and collaborative agent workspaces are different runtime modes with different ownership and maintenance needs
- benchmark saturation should trigger frame analysis, not only model-capability extrapolation
- expert review demand grows when lower-cost agents let more non-experts attempt previously scarce work
- the frame is not the framer: agent autonomy inside a task does not equal human agency over what should matter
- review queues, evals, harnesses, repo rules, CI, permissions, and workflows are the expert response to abundant AI-generated work
