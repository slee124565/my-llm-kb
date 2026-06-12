# Welcome to The AI Systems Engineer Journey

Source: https://theneuralmaze.substack.com/p/welcome-to-the-ai-systems-engineer
Author: Miguel Otero Pedrido
Publisher: The Neural Maze
Published: 2026-04-29
Captured: 2026-06-12
Tags: AI Systems Engineer Journey
Subtitle: Issue #01 — One single role behind a dozen titles

Markdown Content:

![](https://substackcdn.com/image/fetch/$s_!PKlD!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0b4bc5e6-2315-485e-9574-44b3b445671e_1200x1100.png)

Hey friends! 👋

Welcome to Issue #1 of [The AI Systems Engineer Journey](https://theneuralmaze.substack.com/i/194592195/the-ai-systems-engineering-journey), the series I announced a few weeks back. So, what is this thing?

It's a Substack series. Not a course. Not a cohort. Not a "get-started-in-5-minutes" thing. Just a long, slow, careful walk through what it actually means to do system design and systems engineering for AI. New issues all year long, right here in your inbox.

And honestly? You're the ones who pushed me toward this. The comments, the DMs, the polls, the office hours — over and over, the same signal kept showing up:

> "There's so much content out there about building demos. There's almost nothing about building systems."

And you're right. The industry is drowning in "build this in 5 minutes" content. What's actually missing is the engineering layer underneath — the architectures, the trade-offs, the boring-but-critical pieces that decide whether your AI thing survives contact with real users or quietly dies on a Friday afternoon.

That's the gap, and that's what this series is here to fill.

Ready? Let's begin!

![](https://substackcdn.com/image/fetch/$s_!u_S1!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F45c14036-8d52-4a40-a398-847d1de8c3b2_1200x650.png)

> If you want to see systems engineering applied to a real-world agentic system, [Agents in Production](https://theneuralmaze.substack.com/p/my-new-course-with-luis-serrano) is exactly that — 6 weeks, end of May, Luis on theory, me on production, GCP throughout.
> 🎁 And one more thing — just for you, my beloved subscribers ❤️
> Because you're here, you already have free access to something special. On May 7th, Luis and I are running a live masterclass — [Why Your LLM Is Not Enough — A Practical Intro to AI Agents](https://tinyurl.com/agentsmasterclass) — and you don't pay a cent.
> Foundations and engineering. Theory (Luis) and production (me). Two hours of the good stuff, completely on the house 🥂
> Consider it a sneak peek of the course — and a small thank you for being part of The Neural Maze 🫶
> 👉 [Save your spot here](https://tinyurl.com/agentsmasterclass)

# A normal scroll through LinkedIn

Let's do something.

Open LinkedIn. Scroll for forty-five seconds. Count the AI-flavored job titles.

I'll wait …

Done? Cool. Here are the ones I screenshotted this week, in the order they showed up on my feed:

- MLOps Engineer
- ML Engineer
- AI Engineer
- Generative AI Engineer
- Agentic AI Engineer
- LLM Engineer
- RAG Engineer
- Prompt Engineer (apparently they're back)
- Vibecoding Engineer (no comment)
- Applied AI Scientist
- Applied AI Engineer
- AI Solutions Architect

12 titles. Three jobs. Maybe four if I'm being generous.

If you've been in this industry more than ten minutes, you already know what's happening. Every six to nine months the field invents a new title to describe roughly the same work, the underlying tech shifts by 15%, somebody at a Series B writes a job description that reads like a ransom note … and we all nod along like this is normal.

It's exhausting, confusing for newcomers, and it's especially confusing for hiring managers, who at this point are pasting buzzwords like they're being graded on coverage.

So today, I want to do something simple.

> I want to cut through the noise and tell you what I actually do.

And I want to argue — slowly, with examples — that the real role behind all twelve of those titles already has a name, even if it's the one I just made up.

> The AI Systems Engineer.

Yes, I know. I literally just complained about people inventing titles, and now I'm inventing one. I'll defend that move at the end of the post. Stay with me 😉

# The two books that frame everything

![mlops #machinelearning #datascience #llm | Miguel Otero Pedrido | 50 comments](https://substackcdn.com/image/fetch/$s_!u6v3!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F32ef8eaa-6688-49c2-9925-cd431c94436c_800x533.jpeg)

If you took everything I have to say in this newsletter and removed it, you'd still be 80% of the way there if you read these two books back to back:

- 📕 [Designing Machine Learning Systems](https://www.oreilly.com/library/view/designing-machine-learning/9781098107956/) (2022) — by Chip Huyen. The book that finally taught a generation of practitioners that "the model" is maybe 10% of the project.
- 📕 [AI Engineering](https://www.oreilly.com/library/view/ai-engineering/9781098166298/) (2024) — also by Chip. The spiritual sequel, written for the post-foundation-model world, where you don’t necessarily train anything, but you absolutely still have to engineer the system around it.

Read them in order. Pay attention to the moments where she says the same thing twice using different vocabulary. Because the punchline I want to land in this issue is exactly that:

> AI Engineering isn't a replacement for ML Engineering. It’s a superset.

Same skeleton. New organs. The discipline didn't change — the components did.

And the easiest way to feel that in your bones is to draw the systems side by side. So that's what we're going to do.

# The chassis: FTI

![](https://substackcdn.com/image/fetch/$s_!seE7!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbcb98f49-56da-4b60-adfb-b58f55f75e17_1080x1080.png)

Before we go anywhere near specific systems, let me lay down the one mental model that ties everything in this newsletter together:

> FTI — Feature, Training, Inference.

If you've been around The Neural Maze for a while, you're probably familiar with this architecture / design. It's the chassis of every ML system I've ever built — and, as you'll see in a minute, of every AI system too.

Three pipelines. Decoupled. Independently deployable. Independently monitored.

- The Feature Pipeline turns raw data into features (or context, or chunks, depending on the era), and writes them somewhere your training and serving code can both read from.
- The Training Pipeline reads features, fits a model — or fine-tunes one, or assembles a prompt + retrieval setup, depending on the era — and writes a versioned artifact to a registry.
- The Inference Pipeline reads features at request time, plus the latest registered artifact, and produces a prediction (or a generation, or an action) within whatever latency and cost budget the business actually cares about.

That's it. That's the chassis.

Every single example below — classical ML or LLM-powered — is just a different body bolted onto this exact same chassis. Once you see it, you can't unsee it.

Let's prove it 👇

# What "ML Engineering" actually looks like

Before LLMs ate the conversation, this is what we built. And — let me be clear — this is what most companies are still building today. It's just that nobody's tweeting about it because it doesn’t have an "AI" sticker on the front.

Three (and a half) archetypes I've seen at every single company I've worked at.

## Classification Systems

![](https://substackcdn.com/image/fetch/$s_!7Z7D!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F73c16649-2381-4099-a211-9c2a07015293_1774x887.png)

The setup. You've got a binary or multi-class label. Fraud or not fraud. Churn or not churn. Spam or ham. Hot lead, warm lead, cold lead. You've got historical examples. You want a model that scores incoming events in real time and routes them somewhere useful.

Why everyone builds this. Because the business value is embarrassingly easy to compute. "We blocked $X of fraud last quarter" is a slide that writes itself.

The system, mapped onto the chassis:

- Feature Pipeline → events from the transactional DB / Kafka stream get aggregated into per-user, per-merchant, per-time-window features. Lands in a feature store.
- Training Pipeline → XGBoost or LightGBM (because it works and your CTO doesn't want to pay for GPUs you don't need 🙃). Versioned artifact goes to the model registry.
- Inference Pipeline → real-time API, single-digit ms latency, pulls features from the store at request time, scores the event, returns a probability + a routing decision.
- Wrapped around all three → drift monitoring, performance monitoring against eventually-arriving labels, and the world's most-ignored Slack channel, `#fraud-model-alerts` (sorry for that, but come on, I'm sure you have already experienced that ).

## Regression & Time-Series

I'm putting these together on purpose. Not because they're the same — they're not — but because once you've seen the classification chassis, you've seen 80% of these too.

Regression is the same skeleton as classification, just a different output and a different loss. Predicted house price. Estimated delivery time. Customer Lifetime Value. Real-time pricing.

> 💡 Pro tip from too many years of this: users do not understand point estimates. If your model says "delivery in 27 minutes" and it shows up at 41, you're getting a one-star review. Ship intervals. Ship "between 25 and 45 minutes, 80% of the time." Your future self will thank you.

Time-series forecasting adds a few twists that bite you the first time you build it:

- Hierarchical data. Forecasts at the SKU level need to reconcile with category, region, and total-company forecasts. There's a whole subfield (MinT reconciliation, hierarchical forecasting) for this. Most companies discover it the hard way.
- Backtesting, not random splits. I know. I know you know. I'm putting it here because I've personally caught this in code review many times ...
- Models range from "Prophet because the analytics team likes it" → ARIMA / ETS → gradient boosting on lag features (still incredibly competitive — see the M5 competition) → deep models like DeepAR, N-BEATS, and Temporal Fusion Transformers when the data volume actually justifies them.

The architecture is the same FTI skeleton, with one difference: in forecasting, your Inference Pipeline is often a batch job, not a real-time API. Airflow runs nightly, drops a forecast table, and downstream tools (BI dashboards, inventory planners) read from it.

Same chassis. Different body.

![](https://substackcdn.com/image/fetch/$s_!1LQz!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F96cda4f8-8b1e-44d6-9e1a-3ea34b026569_1774x887.png)

## The Recommender System

I have a working theory, based on n=8 companies of personal experience, that every company eventually wants a recommender system.

> Marketplaces want product recs. Media wants content recs. SaaS wants feature recs. HR wants candidate recs.

Even the boring B2B company you'd never expect wants one — they just call it "personalized email content."

I've spent 5+ years building recommenders in production — in fashion, in banking, in retail, etc.— and I'll tell you flat out: this is where I've learned the most about systems.

Because the model is maybe 20% of the work. The other 80% is logging, candidate generation, business rules, A / B testing, evaluation, and convincing the marketing team they cannot, in fact, hardcode their favorite product to position #1.

A few things you should read if you want to go deeper into Recommender Systems:

- [Eugene Yan’s blog](https://eugeneyan.com/) — in my opinion the best practitioner-grade material on RecSys on the open internet. His posts on system design and evaluation are required reading.
- My own deep dive on the modern setup most production systems converge to — the [4-stage recommender architecture](https://theneuralmaze.substack.com/p/how-to-build-production-ready-recommender). If you only read one The Neural Maze post on RecSys, make it that one.

The skeleton, mapped onto FTI:

- Feature Pipeline → user features, item features, interaction features. Embeddings. The works.
- Training Pipeline → two models, usually. A retrieval model (two-tower or similar) and a ranking model (XGBoost or DLRM-style).
- Inference Pipeline → a multi-stage pipeline at request time: candidate generation → ranking → re-ranking → business logic → top-K to user.

Same chassis. Bigger body.

![](https://substackcdn.com/image/fetch/$s_!nvoD!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa6e66c8f-ebfe-46b0-be53-6a75dc649bf9_1500x1200.png)

### What unifies the ML Engineering side

Look at the three diagrams above. Same chassis. Three different bodies.

- A Feature layer that decouples training from serving.
- A Training layer that produces versioned artifacts.
- An Inference layer with latency, throughput, and cost budgets.
- Monitoring & feedback loops wrapping the whole thing.

That's what Chip wrote a 350-page book about in 2022. That's what we mean by "ML Engineering".

Now let's add foundation models and watch what changes. (Spoiler: less than you'd think.)

# What "AI Engineering" actually looks like

Here's where most people get the framing wrong. They look at the AI Engineering field and conclude:

> "It's just calling the OpenAI API in a Python script."

Reader … it is not.

If anything, AI Engineering systems are harder to engineer than classical ML systems, because the model itself is suddenly:

- a non-deterministic black box you don't own,
- whose behavior changes when the vendor pushes an update on a Tuesday,
- whose failure modes include "confidently making things up",
- whose costs scale with input length, output length, and model choice in non-trivial ways,
- and whose evaluation is, charitably, a research-grade open problem.

Chip's AI Engineering book is essentially the field-guide to this new mess. Let's explore some typical AI Engineering Systems.

## RAG

The setup. Users ask natural-language questions. The system retrieves relevant context from a corpus (docs, tickets, code, transcripts) and generates a grounded answer. This is the single most common AI Engineering project at every company in 2026, and it's going to stay that way for a while.

Why people underestimate it. Because the demo is deceptively easy. Embed your docs, stick them in a vector DB, slap an LLM on top, ship it. The demo works. Then you put real users in front of it, and all the things you didn't think about hit at once: chunking strategy, retrieval quality, hybrid search vs. pure semantic, query rewriting, reranking, hallucination detection, citation enforcement, evaluation harnesses, latency, cost, freshness of the index.

> The naive RAG pipeline is the "hello world" of LLM apps. The real RAG system is the one that survives contact with users.

Mapped onto the chassis:

- Feature Pipeline → ingest sources → parse PDFs / HTML / code → chunk → embed → write to a vector DB and a keyword index (yes, both — pure semantic search loses to hybrid almost every time).
- Training Pipeline → here it's mostly prompt engineering + occasional fine-tuning of the embedding model or a reranker. Versioned artifact = the prompt + model config, in a prompt registry.
- Inference Pipeline → query → optionally rewrite → hybrid retrieve → rerank → prompt-build → generate → guardrails → citation validation → return.

Same chassis. New organs. Notice: the components are different, but the engineering shape is identical.

## Document Intelligence

Ever wondered how tools like ChatGPT, Claude, or Gemini ingest a PDF and answer almost instantly? It's not magic. It's a system. And it's a system that's very different from naive RAG.

The world is moving fast on this — modern document architectures use multimodal models, multi-vector retrieval, and ColPali-style approaches that treat the page itself (not OCR'd text) as the unit of retrieval. The results are dramatically better for anything that isn't pure prose: financial reports, legal contracts, scientific papers, slide decks.

Mapped onto the chassis:

- Feature Pipeline → render each page as an image → run a vision-language model that produces a grid of patch embeddings per page → store all of them.
- Training Pipeline → optionally fine-tune the retriever (ColPali) and the VLM on your private documents using synthetic data.
- Inference Pipeline → query → multi-vector retrieval → top-K pages → multimodal generator → answer with bounding boxes / page citations.

This isn't speculative content, by the way. This is the exact system built for his company, and that has been [accepted as an IEEE-CAI 2026 tutorial](https://www.ieeesmc.org/cai-2026/tutorial-2-leveraging-generative-ai-strategies-for-document-understanding/), one of the most important AI-for-industry conferences in the world.

![](https://substackcdn.com/image/fetch/$s_!IBZ5!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0be81d84-977c-4e87-b66c-a209a7fe9e45_1200x1161.png)

## The Agentic AI System

Alright. This is the hottest system in the field right now. [It's also the one Luis Serrano and I will be covering in detail in our next course](https://theneuralmaze.substack.com/p/my-new-course-with-luis-serrano) 😉

The setup. Instead of a single LLM call producing a single output, you have an LLM that:

- Plans a sequence of steps to accomplish a goal,
- Calls tools — APIs, search, code interpreters, internal services — to gather info or take action in the real world,
- Reflects on intermediate results and revises its plan,
- Maintains memory — short-term within a session, long-term across sessions,
- Coordinates with other agents in multi-agent setups, passing tasks, reviewing each other’s work, or specializing by role.

The leap from "LLM-as-text-generator" to "LLM-as-orchestrator-of-actions" is the single biggest shift in the field since transformers themselves. It's also, by an enormous margin, the most operationally fragile thing you can build. Here's why:

- Compounding failure rates. If each tool call is 95% reliable, a 10-step plan succeeds about 60% of the time. At 15 steps you're at 46%. Brutal.
- Cost explosion. Agents loop. Loops cost tokens. Tokens cost money. Without budget controls, a single misbehaving agent can burn through a month's API budget overnight. (Ask me how I know 🥲)
- Observability is genuinely hard. Logging a single LLM call is easy. Logging a 30-step trace with branching, tool calls, and reflections — and debugging why step 17 went sideways — is its own product category now.
- Evaluation is unsolved. Task success is binary on something with thousands of possible execution paths. We're collectively figuring this out as we go.
- Security is non-negotiable. The moment your LLM can call tools that touch the real world, prompt injection stops being a curiosity and becomes a vulnerability that ships your customer data to an attacker.

Mapped onto the chassis (and yes, it still maps):

- Feature Pipeline → the tool registry, the long-term memory store (vector DB), the user/session context.
- Training Pipeline → mostly prompt engineering, planner design, and evaluation suite construction (which is where you’ll spend most of your time, and most teams skip).
- Inference Pipeline → orchestrator → planner → tool calls → reflection → memory writes → next step → … → final response. Wrapped in safety, tracing, and cost guards.

![View image](https://substackcdn.com/image/fetch/$s_!-yK6!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe3571a7c-8f44-4289-808b-506a9fae630d_800x403.jpeg)

# Is AI Engineering ⊇ ML Engineering?

So, after this long ride, here's the question I want to leave you with:

> What's genuinely new in AI Engineering?

Here's my take (there's probably more, so drop your own in the comments)👇

- You usually don't train the core model. You compose, prompt, route, and occasionally fine-tune.
- The cost model is fundamentally different — token-based, vendor-dependent, decoupled from infrastructure cost.
- Evaluation went from "textbook procedure" to "research problem you have to solve in-house."
- The system can take actions in the world, which raises the failure-mode ceiling enormously.

But none of these new things make the old things go away. You still need everything Chip wrote about in 2022. The data pipeline doesn't disappear because you switched to a foundation model. The monitoring doesn't disappear. The feature store mutates into a vector store, but the underlying engineering principle — decouple representation from use — is identical.

This is why I think the AI-Engineer-vs-ML-Engineer debate is mostly a marketing artifact. The real role is the one that owns the whole system. Data, models (trained or otherwise), serving, evaluation, monitoring, and the feedback loops between them.

That role needs a name. I'm calling it the AI Systems Engineer. And no, I'm not just trolling. Let me explain.

# Why "AI Systems Engineer"?

I know. I know. I just spent 3,000 words complaining about people inventing job titles, and now I'm inventing one.

But here's the thing: I'm not trying to coin a new buzzword. I'm trying to name something that already exists but that has been awkwardly straddling the existing titles:

- MLOps Engineers typically own the platform — the registry, the serving, the CI/CD, the monitoring infra. Critical work, but often one layer below the actual product decision.
- ML Engineers typically own a model and its lifecycle. Also critical, but often scoped to one archetype (the recommender, the forecaster, the classifier).
- AI Engineers (in the post-2023 sense) typically own LLM-powered applications. Critical, but often disconnected from the classical ML stack the company also depends on.

The AI Systems Engineer is the role that says:

> “I own the system that produces the decision. Whether it’s an XGBoost model, a forecaster, a recommender, a RAG pipeline, or an agent — I care about the whole loop. The data, the model (trained, fine-tuned, or prompted), the serving, the evaluation, the monitoring, the iteration.”

That's the role I've been doing since my first day at my first company. That's the role this whole newsletter is now going to be about.

If you made it this far, you're exactly the kind of builder this newsletter is for. Hit reply with your thoughts, your war stories, or your favorite ridiculous job title from this week's LinkedIn feed. I read everything.

See you next Wednesday! 👋
