# Demystifying Evals For AI Agents

## Source

- URL: https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
- Author: Anthropic Engineering
- Published: 2026-01-09
- Captured: 2026-04-14
- Raw file: `raw/sources/2026/2026-04-14-demystifying-evals-for-ai-agents.md`
- Workspace provenance: copied from `refs/my-blog-kb/raw/sources/2026/2026-04-14-demystifying-evals-for-ai-agents/2026-04-14-demystifying-evals-for-ai-agents.md`

## Main Claims

- Agent evals are harder than single-turn LLM evals because the evaluated object is the model plus the agent harness: tools, environment state, intermediate reasoning, transcripts, outcomes, and grading infrastructure all affect the result.
- A useful eval suite distinguishes tasks, trials, graders, transcripts, outcomes, evaluation harnesses, agent harnesses, and suites instead of treating an eval as only prompt plus answer plus score.
- Evals pay off when teams move beyond early dogfooding: they turn user complaints and manual checks into baselines, regression tests, model-upgrade evidence, and product-research communication artifacts.
- Agent evals need a portfolio of graders. Code-based graders are fast and objective, model-based graders handle subjective or open-ended judgment, and human graders remain necessary for calibration and gold-standard review.
- Capability evals and regression evals serve different jobs. Capability evals should expose room to climb; regression evals should stay near 100% and catch backsliding. Mature capability evals can graduate into regression suites.
- Eval design should match the agent type: coding agents lean on deterministic tests and static checks; conversational agents need state checks plus interaction rubrics; research agents need groundedness, coverage, and source-quality checks; computer-use agents need sandboxed UI environments and outcome verification.
- Non-deterministic agent behavior requires repeated trials and product-specific metrics. `pass@k` measures whether one of many attempts succeeds, while `pass^k` measures consistent success across all attempts.
- The zero-to-one roadmap is practical: start with 20-50 real or manual-test tasks, write unambiguous specs with reference solutions, build balanced problem sets, isolate trial environments, choose robust graders, read transcripts, monitor saturation, and give eval maintenance clear ownership.
- Automated evals are only one layer. Production monitoring, A/B tests, user feedback, manual transcript review, and systematic human studies are complementary signals that catch failures synthetic evals miss.

## Why It Matters

This article turns `evals` from a generic quality word into a concrete harness discipline. The strongest contribution for `my-llm-kb` is the separation between the agent being evaluated and the evaluation harness that observes it. A team is not just asking whether a model answered correctly; it is asking whether a task spec, environment, tool surface, transcript, outcome check, grader, and aggregation process jointly measure the behavior that matters.

That bridges several existing repo threads. `A Postmortem of Three Recent Issues` showed that weak production-quality signals can miss real regressions. `Building Self-Improving Tax Agents With Codex` showed how production corrections become targeted evals. `After Automation` framed benchmarks as artifacts inside a chosen frame. This Anthropic article supplies the operating vocabulary for building and maintaining those eval artifacts.

## Relation To Existing Concepts

- [Agent Evaluations](../concepts/agent-evaluations.md): this is the anchor article for treating eval suites, graders, transcripts, outcomes, and trial environments as first-class knowledge objects.
- [Long-Running Agent Harnesses](../concepts/long-running-agent-harnesses.md): evals are part of the harness contract, especially for multi-turn tasks where state, tool calls, and environment outcomes matter.
- [Agent Runtime Surfaces](../concepts/agent-runtime-surfaces.md): the runtime being evaluated must resemble production closely enough that results are meaningful, while each trial still starts from isolated state.
- [Human-Supervised Agent Ops](../concepts/human-supervised-agent-ops.md): product teams and domain experts should own task definitions, calibrate LLM judges, and keep suites healthy over time.
- [LLM Agents](../maps/llm-agents.md): the article adds a reusable framework for evaluating coding, conversational, research, and computer-use agents.
- [Long-Running Agents](../maps/long-running-agents.md): multi-turn evals, transcript review, pass-rate consistency, and environment isolation all matter more as task horizons lengthen.

## Tensions Or Disagreements

- The article recommends grading outcomes over rigid tool paths, but some production systems still need policy or compliance checks over tool use. The practical rule is not `never grade tool calls`; it is to avoid path checks that reject valid solutions unless the path itself is part of the safety or business requirement.
- LLM-as-judge graders are framed as scalable and flexible, but they introduce their own calibration burden. Without human spot checks, an eval suite can become a second model system with opaque failure modes.
- The article says 20-50 tasks can be enough early on. That is useful pragmatism, but mature products with small expected deltas still need larger, harder, and better stratified suites.
- Evaluation frameworks are helpful infrastructure, but the appendix is careful that framework choice cannot compensate for ambiguous tasks, brittle graders, or unrepresentative examples.

## Open Questions

- What minimum transcript and outcome schema should a repo-local agent harness preserve so future evals can be built from real failures?
- When should a task grade tool-call path explicitly, and when should it only grade final environment state?
- How should a team decide whether to optimize for `pass@k`, `pass^k`, or another reliability metric for a given product surface?
- What is the smallest calibration loop that keeps LLM-as-judge graders trustworthy without turning every eval run into a human review project?
- How should eval suites expose saturation, ambiguity, and grader bugs so benchmark reports do not overstate model or agent capability?

## Merge Candidates

- agent evals measure the model, scaffold, task spec, environment, graders, and aggregation loop together
- task, trial, grader, transcript, outcome, eval harness, agent harness, and suite should be separate vocabulary in agent evaluation work
- capability evals and regression evals should be designed, interpreted, and maintained differently
- repeated trials need metrics that distinguish occasional success from reliable success, especially `pass@k` versus `pass^k`
- good eval suites start from real failures and manual checks, then require unambiguous specs, reference solutions, balanced cases, isolated environments, and transcript review
- outcome grading should be preferred over brittle path grading unless tool-use path is itself a requirement
- automated evals should be combined with production monitoring, A/B tests, user feedback, manual transcript review, and human studies
