---
title: "The Eight Levels of AI Adoption"
source_id: every-the-eight-levels-of-ai-adoption
source_kind: external-case-study
source_url: "https://every.to/guides/the-eight-levels-of-ai-adoption"
source_markdown_url: "https://every.to/guides/the-eight-levels-of-ai-adoption.md"
source_title: "The Eight Levels of AI Adoption"
host_author: "Mike Taylor, Laura Entis, Claude / Every"
publication: "Guides"
publication_slug: guides
published_at: "2026-06-02T22:00:00Z"
published_date: 2026-06-02
captured_date: 2026-06-13
status: archived
raw_file: "raw/sources/2026/2026-06-02-every-the-eight-levels-of-ai-adoption.md"
content_type: "external-case-study / ai-adoption / delegation-boundary / agent-workflow / workflow-redesign"
audience: everyone
slug: the-eight-levels-of-ai-adoption
canonical_url: "https://every.to/guides/the-eight-levels-of-ai-adoption"
---

# The Eight Levels of AI Adoption

All it takes is one viral post to make you feel like you’re using AI all wrong. Someone is running 12 Claude Code sessions in parallel. Someone else’s agent is answering emails while they sleep. Meanwhile, you’re still arguing with ChatGPT.

But here’s the thing: Keeping up with every power user isn’t the point. The best way to find value in AI is to use it in a way that fits your work—and to regularly check in to see if you could be getting more from it than you already are. (I was using [Steve Yegge’s “Gas Town”](https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04) post about directing dozens of coding agents to illustrate this in client presentations, but it didn’t quite match with my experience, and I needed to modify it.)

This guide maps eight levels of AI adoption, from basic chatbot use to full agent orchestration. With each new level, you delegate more of your work to—and place more trust in—the AI. The following sections explain how each level works in practice, complete with sample prompts, so you can figure out which levels match your current needs and workflows, what’s possible at each stage, and when it’s time to move to the next one.

| Level | Description |
| --- | --- |
| **1—Chatbot** | You give it a task, it provides a response. (ChatGPT, Claude, Gemini) |
| **2—Copilot** | The AI exists inside your files and completes work alongside you. (Cursor, Claude in Excel, Gemini in Google Docs) |
| **3—Agent** | You describe a task, and the agent executes it step by step, asking for your approval before moving on. (Cowork, Codex) |
| **4—Autopilot** | You skip approvals and let an agent complete a task on its own, then review the results. (Lovable, Codex, Claude Code) |
| **5—Workflows** | You build a system that professionalizes the agent’s output. (Compound engineering, Claude Workflows, Copilot AI Studio) |
| **6—Assistant** | The agent works proactively in the background without being prompted. (OpenClaw, Hermes Agent, Claude Managed Agents) |
| **7—Multi-agent** | You’re managing multiple long-running agents at the same time. (Claude Managed Agents, OpenClaw, or Codex Goals) |
| **8—Orchestrator** | A manager agent runs a team of sub-agents on your behalf. (Gas Town, Paperclip, Symphony) |

A higher level isn’t necessarily better. The most sophisticated AI users I know operate at several levels at once, identifying the best level to work within based on the specific challenge in front of them. The right level for a task is generally determined by how much you trust the AI to do a good job without intervention—and how big a deal it’ll be if it does mess up. For high-stakes tasks, you should either stay at a lower level so you can supervise the AI, or be prepared to invest the time, engineering resources, and tokens necessary to get that same quality at a higher level with less human oversight.

Most people I talk to who are struggling to adopt AI have good reasons: The output quality is either too low for the work they do or it’s too expensive to achieve. Safely moving up to the next level requires effort and experimentation—or a jump in model capability.

The right level match for most of your tasks may also depend on your role. Broadly speaking, the sweet spot for knowledge workers right now falls somewhere between Levels 1 and 4. Engineers are more often in Levels 5 through 8, partly because they can build the scaffolding that makes newer, less stable systems usable before they’re ready for everyone else.

## The levels

### Level 1—Chatbot

![Level 1 - Chatbot](https://d24ovhgu8s7341.cloudfront.net/uploads/editor/posts/4283/optimized_95d80989-6191-4ae0-b82f-9b84d15a92e6.png)

**What it is:** You ask, it answers. This is the classic chatbot experience: ChatGPT, Claude, Gemini, or any other model that’s not embedded in your files or your systems. You give it a task, and it returns a response.

**What changes at this level:** You move from doing everything yourself to drafting and synthesizing with an always-available AI generalist.

**What you can use it for:** Writing from rough notes, summarizing documents, or answering questions about uploaded files

#### Try it:

```text
I need to send a post-meeting follow-up email to a client. Here are my rough notes, the decisions we made, and two risks we need to flag. Draft the email in a calm, confident tone and end with three clear next steps. Tell me if anything sounds unclear or unsupported before you start writing.
```

**Input:** Meeting notes

**Output:** A polished email draft that identifies if there’s any missing information that still needs to be filled in

**Human judgment:** Confirm that the tone and facts are right, and the email’s content is something you stand behind.

* * *

```text
I am uploading a 20-page PDF on our new benefits policy. Summarize the five changes employees will care about the most, and then answer these three questions: Who is affected, what specific policies does the new timeline impact, and what would likely confuse someone who is reading this quickly?
```

**Input:** A PDF or set of documents

**Output:** A summary and direct answers to your questions grounded in the source material

**Human judgment:** Verify the summary is factual, and that the model recognizes when the material is ambiguous.

* * *

**When to move up:** Chatbots can assist with a wide variety of tasks, but each session requires manual setup: You have to explain what you want, provide the necessary context, and transfer the chatbot’s response to wherever you’re getting work done. Consider moving to the next level if you get a lot of value from chatbot exchanges but are tired of copy and pasting.

### Level 2—Copilot

![Level 2 - Copilot](https://d24ovhgu8s7341.cloudfront.net/uploads/editor/posts/4283/optimized_943babb7-2e8e-41e7-b187-f404d05d89b1.png)

**What it is:** The model is embedded inside the place where you’re already doing work and has access to everything in your document, spreadsheet, presentation, notes app, or code editor.

**What changes at this level:** AI stops being a separate tab and becomes an in-place collaborator that can extend, revise, and interpret the work you’re doing as you do it.

**What you can use it for:** Revising drafts, understanding a document set or workspace without manually pasting everything into a chat window, and making changes to a live spreadsheet without leaving the file

#### Try it:

```text
Using the draft already in this doc, write the next two sections in the same voice. Keep the tone consistent with the existing text, preserve existing structure, and flag any areas where you need examples or evidence from me before you get started.
```

**Input:** An unfinished document, memo, or social media post

**Output:** A continuation of your draft that matches the existing material

**Human judgment:** Decide whether the new sections sound like you wrote them, and then determine whether they successfully advanced your argument.

* * *

```text
Here is our cash flow projection for Q2. Update the monthly totals with these new numbers, flag any months where we are projected to go negative, and add a summary row at the bottom with the full-quarter picture.
```

**Input:** A spreadsheet with your existing cash flow data. The new figures you want incorporated can be pasted directly into the prompt or provided as a second file.

**Output:** Updated monthly cash flow figures, a list of months where the cash flow is projected to be negative, and a summary of projected cash flow for the entire quarter

**Human judgment:** Verify the formulas are correct, check that the summary is accurate, and determine what strategies you’d like to take for addressing months with a projected negative cash flow.

* * *

**When to move up:** Copilot removes the need to manually provide context, but it can only reliably access information from a single file. Consider moving to the next level if you need to pull, compile, or analyze information across multiple sources.

### Level 3—Agent

![Level 3 - Agent](https://d24ovhgu8s7341.cloudfront.net/uploads/editor/posts/4283/optimized_82509d33-0272-448e-82e0-b515d33f0233.png)

**What it is:** You describe a task, and the agent works step by step to complete it, checking in with you for approval along the way. It can access your files and systems, perform actions on your computer, and compile information from multiple sources.

One key distinction worth keeping in mind: An agent in this context is reactive. It waits for you to initiate and will not start a task unless you explicitly tell it to.

**What changes at this level:** AI becomes a true operator capable of executing multi-step tasks with supervision.

**What you can use it for:** Using figures from one file to update another, or building something new—like a dashboard—from a set of source documents

#### Try it:

```text
Take the Q4 revenue numbers from this spreadsheet and update the board deck with the new figures, charts, and commentary. Show me the proposed edits slide by slide before you apply them, and call out anywhere the source data seems inconsistent.
```

**Input:** A spreadsheet and a presentation deck

**Output:** Proposed slide updates tied to specific data

**Human judgment:** Confirm that the interpretation of the data is how you’d like to present it, correct any factual or contextual issues the agent might have missed, and approve the changes.

* * *

```text
Using the NPS data in this file, build a simple dashboard I can open in a browser. I want to track overall score, key themes in the comments, and how responses break down by segment. Before you build it, tell me how you plan to structure it and what assumptions you are making about the data.
```

**Input:** A data file and a dedicated folder the agent can work within

**Output:** A working dashboard, along with a detailed plan for how it built it plus a summary of the assumptions it made about the data

**Human judgment:** Approve the plan, confirm the dashboard works the way you want it to, and determine whether any assumptions the agent made about the data need to be revised.

* * *

**When to move up:** With an agent, the process is iterative—the agent completes a step, you review and refine, wash, repeat. Consider moving to the next step when you want to relinquish control in exchange for speed or the ability to one-shot a prototype without writing any code.

### Level 4—Autopilot

![Level 4 - Autopilot](https://d24ovhgu8s7341.cloudfront.net/uploads/editor/posts/4283/optimized_3088f1c9-89df-4e7b-97cd-026e933a6d03.png)

**What it is:** You skip permissions and let an agent complete a task on its own, then review the results. With an agent, you stay involved in the process because you care how each step gets done. On autopilot, which is often called [vibe coding](https://every.to/working-overtime/it-s-me-hi-i-m-the-vibe-coder), you describe what you want, let the system run, and evaluate what comes back. At this stage, you’re typically building something other users will interact with, such as a prototype or landing page.

Determining which tasks can be done on autopilot depends on how capable the model is, a calculation that changes with every release. For example, I’ll happily produce a landing page on autopilot, because the models are good enough to make one that meets my standards. I can’t do the same with a complex slide deck, at least not yet—the result is so far from what I want correcting it takes longer than doing it myself. As the models improve, you can get away with doing more of your work on autopilot.

**What changes at this level:** You hand over the entire task to the model and review the end result instead of revising along the way.

**What you can use it for:** Building prototypes, internal tools, and first-pass products. Autopilot is the first level that allows you to build something other people can use without having to write a line of code yourself. It can also usually cover routine tasks, such as filling out recurring forms or drafting weekly status reports.

#### Try it:

```text
Build me a lightweight internal lead-scoring tool for our sales team. It should let us paste in account notes, assign a score from 1 to 5, and show which factors drove the score. Use dummy data for now and make the interface clean enough that I can demo it tomorrow.
```

**Input:** A plain-English description of what the tool should do, who will use it, and any constraints, such as whether it needs to work in a browser or stay local

**Output:** A functioning prototype

**Human judgment:** Test the output and decide if it’s demo-ready. A prototype doesn’t need to be perfect, but it’s worth noting where you’d need to invest in reliability before putting it in front of users.

* * *

```text
Build a landing page for our new feature. It should explain what the feature does, include a clear call to action, and match the tone and brand colors of our existing site. Make it responsive.
```

**Input:** A product brief, brand guidelines, and the existing site as a reference. Brand guidelines can be as simple as a color palette and a few sentences about tone; if you don’t have a formal document, describing your existing site in a sentence or two is enough to get started.

**Output:** A working landing page

**Human judgment:** Read the copy, test the page on mobile, and decide whether it’s ready to share more widely.

* * *

**When to move up:** Autopilot is fast, but it often produces uneven or unreliable results. That might be fine for a prototype, but for higher-stakes work, you’ll want to build a repeatable system around the agent that structures its thinking and execution. Consider moving to the next level if you want the speed and versatility of autopilot with more structured quality control.

### Level 5—Workflows

![Level 5 - Workflows](https://d24ovhgu8s7341.cloudfront.net/uploads/editor/posts/4283/optimized_50985b3b-17a4-4072-a6df-9e0572270492.png)

**What it is:** You build a system, or harness, around your agent that professionalizes its output. Instead of a one-shot run, your agent plans, reviews, performs confidence checks, and runs code through other safeguards to make the results more reliable. This is a transition from vibe coding to agentic engineering. The pace is still fast, but because you have structured the process and included guardrails that catch and fix mistakes, the output is of a higher quality.

This level is primarily the domain of engineers. Reviewing a plan, evaluating which tests need to be done, and designing the harness that keeps the agent from going off the rails all require an understanding of what’s happening under the hood. The [compound engineering guide](https://every.to/source-code/compound-engineering-the-definitive-guide) covers this in detail. Much of this discipline will be baked into platforms over the next six to 12 months; for now, it requires technical judgment to implement.

**What changes at this level:** You stop treating the agent as a one-shot performer. By designing a repeatable process for the agent to follow—and encoding your standards into that process—you can trust the agent with work you’d otherwise want to do by hand.

**What you can use it for:** Shipping features with a plan-review-implement loop, turning a vibe coded prototype into something stable enough for production, or building a process other engineers on the team can follow

#### Try it:

```text
Run `/plan` (plan mode in Claude Code, or `/ce-plan` in compound engineering) before writing any code.

`/ce-plan` Inspect this repo and propose a plan for adding a customer support inbox view. Include the files you expect to touch, edge cases, and how you will verify the behavior. Wait for my approval before implementing.
```

**Input:** A codebase the agent has access to, and a written feature request or specification. The more context you can give upfront—existing architecture patterns, relevant files, known constraints—the better the plan will be.

**Output:** A plan for building a feature that you can review before the agent implements anything

**Human judgment:** Evaluate the plan and make any necessary improvements before having your agent implement it.

* * *

```text
After the agent finishes a change, run `/ce-code-review` (or ask it to review its own work).

Review this change like a skeptical teammate would. Tell me how confident you are from 1 to 100, list the weakest parts of the implementation, and make another pass until you are above 90 or can clearly explain why you are not.
```

**Input:** The completed change—a diff, a set of modified files, or a pull request—plus the original spec or plan the agent was working from, so the review can check whether the implementation matches the instructions

**Output:** A self-review, confidence score, and an improved version of the feature

**Human judgment:** Decide whether the confidence score is justified and whether you agree with the review. If the agent rates itself highly but you identify issues it didn’t flag, name them and have it do another pass.

* * *

**When to move up:** Even the most sophisticated workflows require you to activate them, which, for certain tasks, becomes a bottleneck. Consider moving to the next level if there are areas of your life or work you’d trust an agent to handle without checking in with you first. (At this stage of model development, that’s more often lower-stakes administrative or household tasks.)

### Level 6—Assistant

![Level 6 - Assistant](https://d24ovhgu8s7341.cloudfront.net/uploads/editor/posts/4283/optimized_aedc1a8d-12f9-4e2c-8832-c97a2a02d24a.png)

**What it is:** Unlike an agent—which waits for you to tell it to do something—an assistant acts on your behalf without being prompted. It can monitor a domain, do recurring work, and surface relevant information around the clock. For example, OpenClaw’s heartbeat.md file triggers every half an hour with instructions around priorities, and the agent takes action automatically. No need to prompt.

**What changes at this level:** AI moves from providing reactive help to proactive, ongoing support.

**What you can use it for:** Recurring research, monitoring a topic you care about, or personal administrative work that would otherwise fall through the cracks

This level still requires either technical knowledge or access to someone who can walk you through the onboarding process and fix your assistant when it breaks. On the consulting team, we have an AI assistant that handles all project management and sales pipeline-related tasks, but it only [reliably functions](https://every.to/p/what-i-learned-onboarding-our-ai-project-manager) because it’s maintained by Every senior engineer **[Nityesh Agarwal](https://every.to/@nityesh)**.

OpenClaw is the most popular platform for personal AI assistants, but it’s inherently unstable and time-intensive to set up. Is memory problem hasn’t been solved yet, so it can struggle to retain context between sessions.

Lower-stakes personal uses, such as monitoring your inbox for emails from your child’s school or tracking household purchases, are more accessible with the current state of available models than giving an assistant access to your work systems, which requires engineering and IT support to do safely. Risk tolerance matters here more than at any earlier level.

#### Try it:

```text
Every 30 minutes, check my calendar and flag events taking place within the next two hours that require preparation. If there is a meeting with no agenda, draft a short suggested one based on its title and attendees.
```

**Input:** Calendar access and your preferences about what events qualify as requiring prep—for example, whether you want to be flagged for one-on-ones, external calls, or anything over 30 minutes. Output is typically delivered to a messaging app like Slack, although the specific setup depends on which platform you’re using.

**Output:** A recurring brief delivered to your message app of choice

**Human judgment:** Decide what is urgent, and refine the rules based on the results.

* * *

```text
Monitor my inbox for emails from my child’s school. Each morning, give me a short summary of anything I need to know or act on. Also keep a running log of recent grocery purchases and let me know when we are running low on staples.
```

**Input:** Access to your calendar, inbox, and receipts

**Output:** A daily brief and a running household inventory

**Human judgment:** Verify that the summary captures the most important information and the agent is accurately identifying grocery items that need to be restocked.

* * *

**When to move up:** When set up correctly, an always-on assistant can proactively handle a wide variety of tasks. Consider moving to the next level if you want your assistant to accomplish even more for you, but don’t want to interrupt its existing workflow or are worried about overburdening its memory.

### Level 7—Multi-agent

![Level 7 - Multi-agent](https://d24ovhgu8s7341.cloudfront.net/uploads/editor/posts/4283/optimized_8acad988-d418-40d4-96b7-63e1918f0b2f.png)

**What it is:** You are managing multiple long-running agents or assistants at the same time. Each one has a role, a task, or an area of responsibility, and your work starts to look more like leading a small team. This level is firmly in senior engineering territory—it is rare for knowledge workers to be running multiple parallel agent sessions.

**What changes at this level:** Your productivity multiplies when you move from one agent doing a task to having several agents working on tasks in parallel.

**What you can use it for:** Running implementation and planning simultaneously, or automating recurring investigation work so it no longer requires your direct attention

#### Try it:

```text
You already have one always-on agent—perhaps a custom Claude agent that runs on its own Mac Mini—that handles your editorial work. Rather than interrupt its workflow to have it complete an unrelated task, you set up a second agent that is responsible for a different job function: _“You’re responsible for our customer support inbox. Triage new tickets as they come in, draft replies for the routine ones, and flag anything that needs a human.”_
```

**Input:** A custom long-running agent with its own scope, tools, and memory, kept separate from the first so their contexts don’t bleed together

**Output:** Two agents working in parallel with distinct job functions, skills, and memory

* * *

```text
Systematically review each agent’s work to determine whether it’s executing at the level you need it to and its job description is focused enough that its memory isn’t getting overburdened.
```

**Input:** A bug-reporting system connected to an agent trigger

**Output:** A steady stream of pull requests, each tied to a specific reported issue

**Human judgment:** Review each pull request, merge the approved ones, and identify cases where the agent misdiagnosed the problem.

* * *

**When to move up:** Long-running agents are valuable because they can largely work independently, but you still need to set their goals and evaluate their progress. Consider moving to the next level when you have so many of these agents that you lose track of which one is responsible for what.

### Level 8—Orchestrator

![Level 8 - Orchestrator](https://d24ovhgu8s7341.cloudfront.net/uploads/editor/posts/4283/optimized_73dabd59-1756-4842-9a90-1df893c9e224.png)

**What it is:** An orchestrator agent manages a team of agents. It plans, delegates, monitors progress, and consolidates outputs so you can focus on bigger-picture tasks, such as setting overall goals or reviewing major decisions. Tools like [Gas Town](https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04), [Paperclip](https://github.com/paperclipai/paperclip), and [Symphony](https://github.com/openai/symphony) (from OpenAI) are early examples of this model.

It’s critical to note that this level is highly experimental. Even engineers operating at the frontier still largely fill the role of orchestrator themselves rather than trusting an orchestrator agent to handle complex coordination work.

**What changes at this level:** You stop managing each individual agent and instead focus on setting goals, establishing constraints, and implementing approval thresholds.

**What you can use it for:** Projects where the economics only make sense if you remove yourself as the bottleneck—building a system for keeping track of who’s doing what, sequencing work across multiple agents, and making sure the right issues are escalated without you

#### Try it:

```text
An always-on agent takes the next ticket in the queue from your project management software. _“Your job is to design a landing page for this SEO keyword [insert keyword]. Break the research up into parallel search queries related to the topic, search our company documents for unique insights, then write up a full page using the /brand-style skill. ”_ Agents continue to take and complete tickets until the board is clear, and the fully completed project is ready for human review.
```

**Input:** A high-level objective, defined agent roles, and rules for what requires human review

**Output:** A managed project where you receive critical updates instead of raw output from every agent that’s running in parallel

**Human judgment:** Determine whether the orchestrator is doing a good job triaging issues or if too many—or too few—are being handed over for you to review.

* * *

```text
Set up a pipeline that reviews each code submission against our codebase standards, runs the tests, checks for common issues, and escalates issues to me only when they require a judgment call.
```

**Input:** A repository, contribution guidelines, and a test suite

**Output:** A short queue of escalated items that need your input, instead of hundreds of raw submissions that require manual triage

**Human judgment:** Establish the threshold for what qualifies as something that needs your attention, and raise or lower the bar as needed. The agent can flag those tasks for human review, or it can work on the entire project autonomously until all tests pass and the agent has recorded a video of the software working end to end.

## What the levels measure

There is no value judgment baked into these levels. The vast majority of people should not pursue orchestration, for example, because the models aren’t reliable enough for most use cases. That said, as the technology improves, it can be worth revisiting a level that was previously inaccessible to you or your company. Model releases can pull everyone up, making tools and systems more reliable and easier to use.

If you take anything away from this guide, let it be this: AI use is not a competition. You wouldn’t brag that you had eight interns working overnight on a key project, and you hadn’t checked their output. Instead, you’d work closely with them for months until you were confident they had enough training to be able to work autonomously. Expect to put in a similar amount of effort with your agents before you can trust them to get reliable results at the next level of autonomy. Determining which levels fit your specific needs—rather than seeing how far you can ascend for the sake of it—is the most important thing you can do if you want to make better use of the technology.

* * *

**_[Mike Taylor](https://every.to/@mike_2114)_** _is the head of [tech consulting](https://every.to/consulting) at Every and a co-author of_ [Prompt Engineering for Generative AI](https://www.oreilly.com/library/view/prompt-engineering-for/9781098153427/) (O’Reilly)_. Learn more about how Every’s consulting team can [bring AI into your organization](https://every.to/consulting?utm_source=emailfooter)._

**_[Laura Entis](https://every.to/@laura_27bbaf_1)_** _is a staff writer at Every. You can follow her on [LinkedIn](https://www.linkedin.com/in/lauraentis/)._
