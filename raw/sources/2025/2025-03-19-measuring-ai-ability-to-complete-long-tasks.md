# Measuring AI Ability to Complete Long Tasks

Source: https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/
Publisher: METR
Author: METR; Thomas Kwa, Ben West, Joel Becker, Amy Deng, Katharyn Garcia, Max Hasin, Sami Jawhar, Megan Kinniment, Nate Rush, Sydney Von Arx, Ryan Bloom, Thomas Broadley, Haoxing Du, Brian Goodrich, Nikola Jurkovic, Luke Harold Miles, Seraphina Nix, Tao Lin, Neev Parikh, David Rein, Lucas Jun Koba Sato, Hjalmar Wijk, Daniel M. Ziegler, Elizabeth Barnes, Lawrence Chan
Published: 2025-03-19
Captured: 2026-06-20
Related dashboard: https://metr.org/time-horizons/
Related paper: https://arxiv.org/abs/2503.14499
Tags: METR, agent evaluations, time horizon, long-running agents, AI autonomy, software tasks

Markdown Content:

## Summary

METR proposes measuring AI performance in terms of the length of tasks AI agents can complete. The core metric is the task duration, measured by how long human professionals take, that a model-agent system can complete autonomously with a given reliability threshold.

The post reports that the length of tasks generalist frontier model agents can complete autonomously with 50% reliability has been doubling approximately every seven months over the previous six years. METR frames this as useful for forecasting future AI capabilities and for resolving a tension: frontier models score extremely well on many knowledge and exam-style tasks, but still struggle to reliably substitute for human labor in substantive projects.

METR argues that task length is a helpful lens because agents often fail less from missing single-step knowledge and more from difficulty stringing together longer sequences of actions without drift or accumulated error.

## Core Measurement Approach

METR records the time needed for humans with appropriate expertise to complete a diverse set of multi-step software and reasoning tasks.

The post reports a strong relationship between human task duration and model success:

- Current models have near-100% success on tasks taking humans less than four minutes.
- Current models succeed less than 10% of the time on tasks taking more than around four hours.

This lets METR characterize a model by the length, in human task-duration terms, of tasks it can successfully complete with a fixed probability.

For each model, METR fits a logistic curve to predict model success probability from human task length. Once a target success probability is fixed, such as 50%, the model's time horizon is the human task duration where the fitted curve intersects that success threshold.

The accompanying dashboard defines the task-completion time horizon as the task duration, measured by human expert completion time, at which an AI agent is predicted to succeed with a given level of reliability. The 50%-time horizon is the duration at which an agent is predicted to succeed half the time; the 80%-time horizon is the analogous duration for 80% reliability.

## Why This Metric Exists

METR argues that traditional benchmark scores are often hard to translate into real-world usefulness. Many benchmarks measure static question-answering or narrow skills, while real work requires multi-step coherence, tool use, error recovery, and persistence.

Time horizon is intended to make benchmark performance more interpretable in absolute terms: not only "model A scored higher than model B," but "this agent setup can handle tasks that low-context human experts usually need roughly this much time to complete, at this reliability level."

METR also notes that measuring longer tasks can support forecasts: if the trend continued, generalist autonomous agents could eventually handle week-long or month-long projects, which would carry large benefits and risks.

## Important Scope And Limitations

The dashboard emphasizes that time horizon does not mean the literal length of time an AI can act autonomously. It measures task difficulty using human expert completion time. AI agents may complete successful tasks faster than humans, and METR does not report exact AI elapsed time because it depends heavily on provider and scaffold.

The task distribution is primarily software engineering, machine learning, and cybersecurity tasks. These tasks are self-contained and well-specified, with clear success criteria that can often be automatically evaluated.

METR cautions against interpreting an eight-hour time horizon as meaning that AI can do all intellectual work a low-context human can do in eight hours. Most jobs involve tacit context, other people, ambiguous success metrics, and messy economic constraints. METR says its tasks are cleaner than most real work and that AI agents do worse on messier tasks.

METR also notes that human task-duration estimates likely overestimate how long real professionals would take in familiar day-to-day contexts, because both humans and AI agents receive much less prior project context than incumbent workers.

## Operational Details From The Dashboard

The current time-horizon dashboard follows the same methodology as the initial paper, but uses a larger task suite. It includes over a hundred diverse software tasks.

To run a time-horizon evaluation, METR combines a model with a scaffold that gives it tools and manages the interaction loop. METR first elicits capabilities on a small dev set, chooses or adjusts a scaffold such as ReAct, Triframe, Claude Code, or Codex, then scales to a separate larger test set.

METR launches multiple independent runs per task, checks for reward hacks, checks whether the model had enough token budget, and reviews flagged runs both automatically and manually. The dashboard says this process often takes at least one to two weeks of calendar time.

The dashboard also warns that measurements above 16 hours are unreliable with the current task suite.

## Citation

```text
@misc{metr-2025-measuring-ai-ability-to-complete-long-tasks,
    title = {Measuring AI Ability to Complete Long Tasks},
    author = {METR},
    howpublished = {\url{https://metr.org/blog/2025-03-19-measuring-ai-ability-to-complete-long-tasks/}},
    year = {2025},
    month = {03},
}
```
