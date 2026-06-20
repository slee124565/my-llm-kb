# Agent Evaluations

## Summary

Agent evaluations are the discipline of measuring a model-harness system across tasks, trials, transcripts, tool use, environment state, outcomes, and graders. For agents, the question is rarely only whether a final answer looks good. The more durable question is whether the agent can repeatedly complete the right task under realistic runtime constraints, with enough evidence that humans can trust the score.

## Why It Matters

As agents move from demos into production workflows, quality failures become harder to reason about. A weak agent may fail the task, a weak task spec may make success ambiguous, a brittle grader may reject valid behavior, a harness may constrain the model unfairly, or production monitoring may catch issues the offline suite misses. Without explicit eval structure, teams collapse all of these into vague claims that the agent is better or worse.

For this repo, evals are part of harness design. They define success, preserve evidence, make model upgrades safer, convert production failures into regression tests, and give human supervisors a concrete way to delegate more work without losing control.

## Current Framing

- An agent eval measures the model and scaffold together: prompts, tools, permissions, environment, state reset, transcripts, outcomes, graders, and result aggregation all affect the score.
- Useful vocabulary separates `task`, `trial`, `grader`, `transcript`, `outcome`, `evaluation harness`, `agent harness`, and `suite`; this prevents teams from mistaking one example run for a reliable evaluation.
- Capability evals ask what an agent can newly do and should leave room for improvement; regression evals ask whether old behavior still works and should have high expected pass rates.
- Code-based graders should be preferred where the outcome is deterministic, model-based graders where judgment is open-ended, and human graders for calibration, expert judgment, and gold-standard checks.
- Outcome verification is usually more robust than enforcing exact tool-call sequences, but tool-use grading remains appropriate when the path is itself a policy, safety, or business requirement.
- Non-determinism should be measured explicitly. `pass@k` rewards at least one successful attempt, while `pass^k` measures consistency across repeated attempts.
- Good eval suites start from real failures, manual release checks, support queues, and observed workflow breaks; they need unambiguous task specs, reference solutions, balanced positive and negative cases, and clean environment isolation.
- Transcript review is not optional maintenance. It is how teams detect ambiguous tasks, unfair graders, harness constraints, valid alternate solutions, reward hacking, and saturation.
- Automated evals are one layer in a broader quality system with production monitoring, A/B tests, user feedback, manual transcript review, and systematic human studies.
- Production self-improvement loops work only when traces, corrections, reviewed findings, targeted evals, and regression suites are connected into a durable evidence chain.
- Benchmark scores should be read as performance inside a frame: model weights, prompt, scaffold, task distribution, environment, verifier, scoring policy, and human judgment all contribute.
- GEPA-style skill optimization extends agent evals into procedural memory: execution traces identify failure points, candidate skill variants are evaluated with rubric-based judges, constraint gates prevent drift, and winning changes move through PRs rather than direct runtime mutation.
- Self-evaluation by the same agent that wrote the skill is weak evidence. The stronger pattern is to separate the runtime that generated experience from the offline harness that reviews traces, constructs eval data, scores variants, enforces constraints, and records the change.
- Production agent evals need trajectory and cost-aware signals, not only final-answer scoring. The eval surface should check tool order when policy-relevant, loop counts, retries, trace completeness, cost per successful task, and whether human approval gates fire for irreversible actions.
- Time-horizon evaluations translate agent capability into a delegation boundary: they ask what human-task duration a `model + scaffold + task suite + grader` can complete at a target reliability level, so the result should be read as benchmarked task difficulty rather than literal AI runtime or a claim about whole-job replacement.
- Eval suites themselves rot. They should be refreshed from sampled production traces, support queues, manual release checks, user feedback, and expert review so prompt, model-routing, tool-description, or memory changes are judged against current failure modes.
- Example and integration validation in OSS agent SDKs should preserve per-example logs, rerun files, install/runtime evidence, and source intent. A passing exit code is evidence, but the stronger check is whether observed stdout/stderr matches the intended example flow across supported runtimes.

## Signals From Recent Articles

- [Demystifying Evals For AI Agents](../articles/demystifying-evals-for-ai-agents.md): provides the anchor vocabulary for task / trial / grader / transcript / outcome / harness / suite, plus the practical zero-to-one roadmap.
- [METR - Measuring AI Ability to Complete Long Tasks](../articles/metr-measuring-ai-ability-to-complete-long-tasks.md): anchors time-horizon evaluation as a task-duration / reliability curve for long-running agents, with clear caveats about scaffold, task distribution, and real-world messiness.
- [Building Self-Improving Tax Agents With Codex](../articles/building-self-improving-tax-agents-with-codex.md): shows how practitioner corrections can become targeted evals and regression gates when production evidence is structured.
- [A Postmortem of Three Recent Issues](../articles/a-postmortem-of-three-recent-issues.md): shows that noisy benchmark-heavy validation can miss real regressions, so production quality signals and rollback loops are part of the eval system.
- [After Automation](../articles/every-after-automation.md): frames benchmarks and evals as artifacts inside a chosen task frame, not neutral proof of capability outside that frame.
- [Verifying gpt-oss implementations](../articles/verifying-implementations.md): treats smoke tests, API-shape checks, and eval bundles as layered verification rather than a single pass/fail event.
- [OpenAI Prompt Guidance - GPT-5.5](../articles/openai-prompt-guidance-gpt-5-5.md): pushes prompt migration and reasoning-effort choices toward eval-backed decisions.
- [Hermes Agent Masterclass](../articles/hermes-agent-masterclass.md): frames GEPA as an offline trace-based optimizer for agent-authored skills, with eval data, rubric scoring, constraint gates, and PR-based change flow.
- [Hidden Technical Debt in Agentic Systems](../articles/hidden-technical-debt-in-agentic-systems.md): argues that an agent without an eval harness is still a demo; adds reference-based, reference-free, trajectory, and online evals to the production debt map.
- [Using Skills To Accelerate OSS Maintenance](../articles/using-skills-to-accelerate-oss-maintenance.md): shows example auto-run, integration tests, release review, and PR review as repeatable OSS maintenance eval surfaces.

## Open Questions

- What is the minimum eval evidence bundle a repo-local agent should preserve after a meaningful failure: task spec, transcript, tool calls, environment diff, expected outcome, grader output, or all of these?
- How should product teams decide when a capability eval has saturated and should graduate into a regression suite?
- Which agent surfaces need consistency metrics like `pass^k` instead of success-opportunity metrics like `pass@k`?
- How should teams calibrate LLM-as-judge graders without making human review the bottleneck for every iteration?
- What anti-gaming checks should be standard in agent evals where the agent can inspect files, environment state, or grader-adjacent artifacts?
- How can benchmark reports clearly separate model capability from prompt framing, scaffold design, verifier choices, and task distribution?
- When a skill is improved from session traces, what evidence proves the new variant generalizes instead of overfitting to one user's recent failures?

## Related Pages

- [Long-Running Agent Harnesses](long-running-agent-harnesses.md)
- [Agent Runtime Surfaces](agent-runtime-surfaces.md)
- [Human-Supervised Agent Ops](human-supervised-agent-ops.md)
- [Prompt Migration And Agent Steerability](prompt-migration-and-agent-steerability.md)
- [LLM Agents](../maps/llm-agents.md)
- [Long-Running Agents](../maps/long-running-agents.md)
