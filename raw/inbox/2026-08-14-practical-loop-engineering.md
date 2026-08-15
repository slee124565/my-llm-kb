# Practical Loop Engineering

Subtitle: Goals, loops, and the discipline of not delegating your judgment
Source: https://addyo.substack.com/p/practical-loop-engineering
Requested URL: https://addyo.substack.com/p/practical-loop-engineering?utm_source=share&utm_medium=android&r=6dhj9n
Author: Addy Osmani
Publication: Elevate
Published: 2026-08-14
Captured at: 2026-08-15T09:07:45+08:00
Extraction: rendered Substack article inspection
Import mode: browser extraction with visual review of all article figures
Content status: complete section-by-section paraphrase with complete image context

Note: This inbox source preserves the article's structure, claims, examples, links, and the context of all 13 figures. The prose below is a source-faithful paraphrase rather than a verbatim reproduction. Claims remain the author's framing unless independently verified.

## Article Overview

Addy Osmani describes a daily workflow in which he may run five to ten agents, usually no more than about five concurrently. Some bounded, low-risk tasks can be delegated almost completely when their constraints and stopping conditions are explicit. Complex or sensitive work—especially authentication, security, finance, or systems with real users—requires closer supervision and code review.

The article treats a loop as an agent repeatedly acting, checking its results, incorporating errors, and trying again until a defined stopping condition holds. The key engineering work is therefore not merely making the agent continue; it is specifying a goal that can be checked, choosing the right trigger, bounding the run, and preserving human judgment where the quality bar is subjective.

Two Claude Code primitives anchor the discussion:

- `/goal` advances one bounded task toward a measurable finish line and uses an evaluator to decide whether the stated criteria have been met.
- `/loop` reruns a prompt on a timer or fixed interval, making it useful for polling and recurring checks.
- `/schedule` moves recurring work to a cloud routine when it must outlive the local session.

## Before the Primitives Were Primitives

Before goal and loop behavior became product primitives, practitioners built their own shell loops. Osmani points to Geoff Huntley's Ralph loop as an early pattern people tested mostly on personal projects, where failure was inexpensive.

Modern primitives are more dependable, but they do not eliminate the need for careful babysitting. An underspecified goal, vague constraints, or an unclear end state can leave an unattended loop in a bad condition. The appropriate autonomy differs sharply between a greenfield project with no users and a historically complex brownfield system such as a bank codebase.

## How the Claude Code Team Frames Loops

The article links to the Claude Code team's taxonomy: https://x.com/ClaudeDevs/article/2074208949205881033

It condenses the taxonomy into four levels:

1. **Turn-based / agentic loop** — A human triggers every turn. The agent gathers context, acts, checks its work, and responds; the human inspects the result and supplies the next prompt.
2. **Goal-based loop** — A prompt names an objective and an explicit definition of done. An evaluator checks the transcript after attempted completion and sends the agent back to work until the condition holds or a turn cap is reached.
3. **Time-based loop** — A timer triggers recurring work whose inputs change while the task stays stable, such as checking a pull request for reviews or CI failures.
4. **Proactive loop** — An event or schedule triggers work without a human present in real time. Each task ends at its own goal, while the routine remains active until disabled. Suitable examples include bug intake, issue triage, migrations, and dependency updates.

The article emphasizes starting with the simplest applicable pattern. More autonomy is useful only when its trigger, stopping behavior, and best-fit task are understood.

### Verification Pattern

The Claude Code example makes verification part of the reusable workflow rather than relying on a final manual glance. For a frontend change, the verification skill should require the agent to:

1. Start the application and open the changed page.
2. Interact with the new or edited UI and capture before/after evidence.
3. Confirm that the browser console has no new warnings or errors.
4. Run performance and Core Web Vitals checks.
5. Fix failures and repeat the full verification sequence instead of returning partially verified work.

The important pattern is that “done” is tied to observable checks, not merely to the fact that an edit was made.

## Goal

Osmani uses `/goal` for a specific piece of work that can be pushed until it is demonstrably complete. Better goals name the measurement tool as well as the target—for example, a performance threshold produced by Lighthouse rather than a vague request to make a page faster.

Examples include processing a fixed number of GitHub issues, improving a page by a stated percentage, or refactoring until both a Lighthouse score and an LCP threshold are achieved. A robust goal also states invariants, progress expectations, a no-progress abort rule, and a maximum turn count.

The evaluator behind `/goal` is narrower than a human reviewer. It checks the conversation transcript against the hard conditions in the goal. It does not judge whether the implementation is tasteful, maintainable, or strategically worthwhile.

## Loop

`/loop` behaves more like a scheduler or an agent attached to a cron job. It is best used to watch something, poll logs, monitor external state, or repeat a stable task at a suitable cadence.

The cadence should match how quickly the underlying system changes. Polling a repository every minute when it receives one pull request per day wastes attention and compute. The article notes these operational details:

- The minimum recurring-loop cadence is one minute.
- A loop is scoped to its conversation session.
- Starting a new conversation stops it, although resuming the original session can restore an unexpired recurring task.
- Recurring loops expire after seven days, not three as Osmani had previously stated.
- Work that must outlive the session should use `/schedule` in the cloud.

## What I Delegate, and What I Watch

Low-risk work such as drafting documentation or checking test coverage can often run with broad delegation. Complex tasks, uncertain specifications, and security- or finance-adjacent changes receive closer supervision.

The article recommends separating the maker from the checker. One agent drafts the change; another receives fresh context, reviews the diff, and tries to refute the maker's confidence. A performance change judged only on desktop can look successful while failing the actual mobile requirement, so the verifier's prompt must name every relevant dimension and compare the work against the specification or issue.

Osmani recounts asking agents to research competitors and prepare local implementations for perceived product gaps. He almost pushed the changes after reading the research but before reviewing the code closely. The implementations added considerable complexity for little user benefit. His lesson is to delegate execution without delegating taste and judgment.

Parallel agents also need isolation. Each run should work in its own checkout or worktree and branch. Without isolation, multiple agents edit the same tree and collide; with separate worktrees, their changes remain reviewable and independently mergeable.

## The Workflow I Run Every Day

Osmani applies recurring checks to his Agent Skills repository: https://github.com/addyosmani/agent-skills

The repository can receive roughly 80–90 pull requests in a day. A recurring pass can identify new issues, summarize urgency, provide a first review, and filter obviously unsuitable work. The loop does not replace his review; it reduces the size and disorder of the queue that requires human judgment.

## Combining Loops and Goals

The two primitives compose cleanly when their responsibilities stay distinct:

- The loop is the heartbeat: wake on a cadence, inspect the external system, and decide whether work exists.
- The goal is the hands: start only when a match exists, solve one bounded problem, and stop when a measurable exit condition holds.

An example pattern checks GitHub daily for issues labeled as bugs and, when one exists, launches a bounded goal to implement a fix until the local test suite passes. The article warns against packing several unrelated outcomes into one goal because the evaluator then has no sharp condition to check.

The linked Claude Code composition extends this pattern with scheduled routines, verification skills, dynamic workflows, separate agents exploring solutions, adversarial review, and an auto mode for unattended execution.

## What the Triage System Actually Does

In pull-request triage, the system cross-references incoming work against the repository's current goals and contribution rules. It can summarize what is new, identify urgency, and remove items that clearly do not fit.

One concrete stopping rule comes from the contribution guideline that the project does not accept translations it cannot maintain. Turning that written policy into a routine check shrinks the human review batch. The larger benefit is cross-referencing: when an area is being reworked, the system can identify superseded issues and flag changes that would conflict with someone else's work.

The broader principle is that a concise, explicit constraint can be enforced by an agent repeatedly, while ambiguous policy continues to demand human interpretation.

## What Loops Do Not Buy You

Loops are a poor fit when “done” cannot be stated or checked. Requests such as making a design good, improving taste, or conducting open-ended creative exploration lack a stable machine-verifiable finish line.

Good candidates include:

- Greenfield work with a clear specification.
- Well-fenced modules covered by tests.
- Triage and label hygiene.
- Dependency updates, codemods, and mechanical migrations.
- Performance work with a numeric target.
- A recurring check already performed manually every morning.

Work that should remain closely supervised includes:

- Fuzzy goals that could run indefinitely.
- Deep architectural judgment and data-model design.
- Brownfield systems whose constraints have not yet been mapped.
- Outcomes whose correctness depends on taste.
- Changes affecting real users without a safe rollback.
- The first unattended run of a new workflow.

The safe autonomy level rises with the strength and affordability of the verifier, not with the apparent simplicity or size of the task.

## The Fine Print

A classic no-progress signal is the agent repeating the same command without changing the result. If a third attempt produces no meaningful difference from the second, the loop should probably stop.

The easiest first loop is a check already performed manually every morning. Osmani's was the pull-request queue. The disciplined sequence is to choose a stable recurring task, state the end condition, add independent verification, set bounds, watch early runs, and retain human judgment over irreversible or subjective decisions.

## Image Context

The original article does not provide useful alt text for its figures. The descriptions below were added after visual inspection so the diagrams remain searchable and understandable in a text-first knowledge base.

### Figure 1 — Trigger.dev sponsor: a durable machine per conversation

![Trigger.dev graphic showing a TypeScript chat agent and the message “Every conversation gets its own machine”](https://substack-post-media.s3.amazonaws.com/public/images/760f67b2-a638-4d9a-972a-d8364be73651_1270x760.jpeg)

Advertisement context: Trigger.dev presents each chat conversation as a durable task that can survive refreshes, redeployments, idle periods, and crashes, while retaining a human-approval boundary for irreversible actions.

### Figure 2 — Anatomy of a loop

![Diagram of goal, act, evaluate, stop, and error feedback](https://substack-post-media.s3.amazonaws.com/public/images/84591717-7aa7-4119-817a-54065151635d_1456x855.webp)

The diagram shows a four-part flow: state a machine-checkable goal, let the agent act, evaluate with compilers, linters, tests, or a separate model, and stop only when the condition holds. Failed checks become the next input. It highlights the evaluator as the decisive part of the system and recommends deterministic, fast, independent checks.

### Figure 3 — Four kinds of loops

![Table comparing turn-based, goal-based, time-based, and proactive loops](https://substack-post-media.s3.amazonaws.com/public/images/a5545307-6cad-40cc-b08f-52a093cf50c8_3200x1996.png)

The table compares each loop type by trigger, stopping condition, and best-fit work. Turn-based loops depend on the user's next prompt; goal-based loops stop at a verifiable objective or turn cap; time-based loops watch recurring external work; proactive loops handle continuing streams without a human present at trigger time.

### Figure 4 — `/goal` drives one task to a finish line

![Goal diagram contrasting machine-checkable and subjective completion criteria](https://substack-post-media.s3.amazonaws.com/public/images/85bdc2cf-ca2a-4bd8-bc48-f283b3d0a6c5_3200x1880.png)

The figure breaks a goal into the command, a condition a machine can evaluate, and a mandatory bound. Passing tests, clean lint, numeric latency, Lighthouse scores, and type-check results are shown as checkable; requests for cleaner code, better UX, more engaging copy, or a proper refactor are shown as too subjective for an unattended goal.

### Figure 5 — `/loop` is a cron with an agent on the far end

![Loop scheduling diagram showing interval syntax, session lifetime, and seven-day expiry](https://substack-post-media.s3.amazonaws.com/public/images/b7e56709-7f67-4f14-84a4-5d34561e68f2_3200x1910.png)

The figure illustrates interval-first and interval-last syntax, supported time units, the one-minute minimum cadence, session scope, and automatic expiry after seven days. It warns that cadence should reflect how quickly the monitored system actually changes.

### Figure 6 — Split the maker from the checker

![Maker-checker workflow with a drafting agent, independent review agent, and feedback loop](https://substack-post-media.s3.amazonaws.com/public/images/0a538d8b-09db-4ee0-a5db-2c3100f15eb6_1456x851.webp)

The maker drafts the change and passes a diff to a checker with fresh context. The checker tries to disprove correctness; failures return to the maker with a specific reason. The prompt should name all important dimensions and tell the checker to default toward finding flaws rather than validating the maker's confidence.

### Figure 7 — One clean checkout per parallel run

![Comparison of agents colliding in one tree versus separate worktrees and branches](https://substack-post-media.s3.amazonaws.com/public/images/eda9894c-b06f-4cf5-94cf-609391812e6a_3200x1760.png)

The left side shows several agents editing one working tree and branch, producing collisions. The right side assigns each agent a separate worktree and branch—for API, documentation, or performance work—so parallel runs remain isolated. It also notes that temporary worktrees are automatically removed only when the sub-agent made no changes.

### Figure 8 — Loop schedules the check; goal solves the problem

![Composition diagram in which a recurring loop detects work and a bounded goal finishes it](https://substack-post-media.s3.amazonaws.com/public/images/4597394f-0385-47ac-b4c4-84ce52c7a030_3200x1880.png)

The loop wakes periodically and cheaply decides whether anything needs attention. When it finds work, it launches a goal that runs until tests or another real exit condition pass. The figure reinforces one clear objective and one measurable exit per goal.

### Figure 9 — What the triage system actually does

![PR triage diagram reducing an 80–90 item daily queue using scheduled policy checks](https://substack-post-media.s3.amazonaws.com/public/images/0133fdd6-a421-4c8d-a608-f38cb22a6542_1456x846.webp)

The workflow changes a manual review of 80–90 pull requests into a scheduled first pass that summarizes new items, assesses urgency, removes clearly unsuitable contributions, and leaves a smaller pile for a person. Written contribution rules become repeatable machine checks; cross-referencing active rework against incoming changes is presented as the larger win.

### Figure 10 — Where to point a loop

![Decision guide comparing loop-friendly tasks with tasks that need human control](https://substack-post-media.s3.amazonaws.com/public/images/7dd891d6-13ec-4818-8d23-208a74915c2c_3200x1880.png)

The diagram contrasts bounded, testable, repetitive work with fuzzy, judgment-heavy, high-impact, or first-time workflows. Its rule of thumb is to grant only as much autonomy as can be verified cheaply.

### Figure 11 — Trigger.dev sponsor: conversations survive refreshes and crashes

![Trigger.dev graphic showing a conversation continuing after the app window is closed](https://substack-post-media.s3.amazonaws.com/public/images/fba6f2b6-b8d1-4662-b4ca-83e841310bfb_1270x760.jpeg)

Advertisement context: the graphic illustrates a multi-turn conversation continuing as a durable background task through browser refreshes, application closes, redeployments, and crashes.

### Figure 12 — Choosing between goal, loop, and schedule

![Comparison table for goal, loop, and schedule primitives](https://substack-post-media.s3.amazonaws.com/public/images/91307c12-4fc6-48ed-99ef-2672210998d2_3200x1940.png)

The comparison says `/goal` is for one task ending at a condition, `/loop` is for session-scoped cadence-based watching with a seven-day expiry, and `/schedule` is for cloud routines that must outlive the local session. The rule of thumb is finish line versus heartbeat versus a heartbeat that continues after the laptop closes.

### Figure 13 — Article title card

![Black title card reading “Practical Loop Engineering”](https://substack-post-media.s3.amazonaws.com/public/images/4a351633-8c64-479d-b066-811f8d0ec3fb_1376x768.png)

Closing title graphic for the article.

## Source Links

- Canonical article: https://addyo.substack.com/p/practical-loop-engineering
- Author profile: https://substack.com/@addyosmani
- Claude Code goal documentation: https://code.claude.com/docs/en/goal
- Claude Code scheduled-task / loop documentation: https://code.claude.com/docs/en/scheduled-tasks
- Claude Code routines / schedule documentation: https://code.claude.com/docs/en/routines
- Claude Code auto mode documentation: https://code.claude.com/docs/en/auto-mode-config
- Claude Code dynamic workflows documentation: https://code.claude.com/docs/en/workflows
- Claude Code team's loop write-up: https://x.com/ClaudeDevs/article/2074208949205881033
- Geoff Huntley's Ralph loop: https://ghuntley.com/loop/
- Addy Osmani's Agent Skills repository: https://github.com/addyosmani/agent-skills
- Sponsor link used in the article: https://fandf.co/4pVPWbQ

## Source Notes

- The rendered article was publicly accessible without a paywall at capture time.
- The article metadata showed publication on August 14, 2026.
- The extraction excluded comments, subscription UI, share controls, and Substack navigation.
- All 13 in-article figures were loaded and visually inspected; the source supplied empty alt text for them.
- Sponsor sections and their two images are retained and clearly labeled as advertisements.
- No image binaries were copied into this repository; Markdown embeds the original Substack-hosted image URLs.
