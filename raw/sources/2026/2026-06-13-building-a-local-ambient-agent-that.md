# Building a Local Ambient Agent That Never Sleeps

Source: https://theneuralmaze.substack.com/p/building-a-local-ambient-agent-that
Author: Miguel Otero Pedrido
Publisher: The Neural Maze
Published: 2026-06-13
Captured: 2026-06-19
Tags: AI Systems Engineer Journey
Subtitle: Issue #05 — The theory, the design trade-offs, and a Kafka + Ollama agent you can run today

Markdown Content:

Hey friends! 👋

This is Issue #05 of [The AI Systems Engineer Journey](https://theneuralmaze.substack.com/t/ai-systems-engineer-journey).

In the [last issue](https://theneuralmaze.substack.com/p/building-agent-memory-with-knowledge) we gave an agent a real long-term memory, that is, a temporal knowledge graph it could actually reason over. But there's a habit none of our agents have shaken yet, and I want to call it out today, because it's been hiding in plain sight in every demo I've shipped.

> Our agents only do anything when we poke them!

You open a chat box, you type, they reply, they go quiet. Useful, of course. But it's a narrow way to use a model that could, in principle, be paying attention all the time.

Here's what I mean. A huge amount of the software that earns its keep never waits for a human at all. Your phone buzzes when a payment looks off. Pagers go off when a server starts misbehaving at 3am. Nobody asked a question — a system was watching a stream of events and decided, on its own, that you needed to know.

> 🙋 That "watching, then deciding when to interrupt you" behaviour has a name: ambient agents.

And the gap between them and the chat-box agents most of us build isn't model quality — it's a different relationship with time. A chat agent is summoned. An ambient agent is resident: it lives on a stream and reacts to the world instead of to you.

So that's what we're building this week — and we're building it the way I like to build things here: end to end, locally, nothing hidden behind a framework. By the end you'll have an agent that sits on a feed of live crypto trades (Coinbase's public WebSocket, no key required), pipes them through Kafka, lets a local Ollama model decide whether anything's worth flagging, and pings you — on your terminal, or your phone via Telegram — only when it is.

> ⚠️ And to be clear up front: it watches and reports … it never places a trade! 🤣

A quick map of where we're headed: first the theory (what "ambient" actually means, and why it's really just event-driven architecture with a model in the loop), then the one design choice that makes or breaks the whole thing, then the build itself.

Alright … let's get into it!

## What "ambient" actually means

![](https://substackcdn.com/image/fetch/$s_!tcyv!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F39bd170f-0e66-42ce-b551-fd419af48f88_2752x1536.png)

Let's pin down the definition before we lean on it.

[LangChain frames an ambient agent](https://www.langchain.com/blog/introducing-ambient-agents) as one that listens to an event stream and acts on it, instead of being invoked by a human message. It's triggered by events, not by you. It can juggle many things at once in the background, and it only surfaces to a human when it has a reason to.

The mental model I keep coming back to is a four-step loop:

1. Observe — consume a stream of signals from the world.
2. Infer — work out whether anything in there actually matters.
3. Decide — choose what, if anything, to do about it.
4. Notify — escalate to a human when human judgment is warranted.

[Google's Agent Development Kit](https://adk.dev/runtime/ambient-agents/) describes the same shape from the infrastructure angle: agents that are triggered by events arriving on a stream, rather than sitting behind a request / response call. Different words, same skeleton.

## Three things to understand before we build

"Ambient agent" sounds obvious until you try to build one well. Three ideas do most of the heavy lifting.

### 1. It's an inversion of who holds the initiative

In a reactive agent, the human holds the initiative — nothing happens until you type. In an ambient agent, the environment holds it — the world emits events and the agent, always-on, reacts to them.

That single flip changes everything downstream: how you trigger the agent, how you reason about cost, how you keep a human safe in the loop.

A chat agent that sits idle costs nothing. An ambient agent is by definition always consuming a stream — so efficiency stops being a nice-to-have and becomes the central design constraint. (Hold that thought; it's the reason for the one big trade-off later.)

### 2. It's event-driven architecture with a model in the loop

If you've ever built anything with a message queue, a stream processor, or a webhook handler, you already know two-thirds of this. The classic event-driven pipeline is source → bus → consumer. An ambient agent keeps that exact spine and swaps the consumer’s hard-coded rules for an LLM-powered reasoner.

That's why Kafka slots in so naturally and why none of this should feel exotic — we're not inventing a new architecture, we're putting a language model where the `if/else` used to be.

![](https://substackcdn.com/image/fetch/$s_!9YTZ!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1e1c4e61-cac3-495d-ac40-7786046c0f01_2752x1536.png)

### 3. The risk profile is different

A reactive agent acts in front of you: you see the output immediately and can stop it.

An ambient agent acts when you're not looking — possibly at 3am, possibly hundreds of times a day. An always-on agent that can take irreversible actions on its own is a genuinely risky thing to ship casually.

This is exactly why the literature is so insistent on human-in-the-loop, and why the serious treatments frame the agent as something that escalates to a human rather than something that acts alone. LangChain names three escalation patterns, which are really three levels of trust you choose to extend:

- Notify — "Here's something you should see." The lowest level of trust: the agent only informs.
- Question — "I'm stuck — which did you mean?" A medium level: the agent pauses to ask before acting.
- Review — "I'm about to do X — approve it?" The highest level: the agent acts, pending your sign-off.

For this build we stay on the bottom rung: notify. Our agent watches, reasons, and tells us — and never takes an irreversible action. That's not a limitation; for a first ambient agent it's the right call, and the design leaves the door open to climb to question or review later.

### Where this shows up in the wild

Once you have the lens, you see ambient agents everywhere people are excited about agents doing real work:

- an email assistant that drafts replies in the background and asks you to approve the risky ones;
- an SRE / observability agent that watches logs and pages a human when it correlates an incident;
- a research agent that monitors new papers or filings and surfaces only the relevant ones.

They all share one skeleton: a stream, a filter, a reasoner, and an escalation path to a human. Build one and you've effectively built all of them — only the senses change. We'll build ours on live crypto, but you could repoint it at any of the above with a new producer and a new prompt.

And the reason all of this is suddenly a weekend project rather than a research effort: three things finally lined up.

Models got cheap and fast enough to run locally, so you can afford to keep one parked on a stream. Structured output (JSON mode) made their responses reliable enough to act on in code, not just show to a human.

And the human-in-the-loop patterns matured, so "always-on" stopped meaning "unsupervised." Take any one away and ambient agents stay impractical; together, they put this within reach on a laptop.

## The architecture

![](https://substackcdn.com/image/fetch/$s_!7NLh!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fac8a364c-dd4b-4b21-8d39-367a459d2e9d_2752x1536.png)

Every ambient agent has the same three organs, whatever the domain:

1. Senses — something that turns the outside world into a stream of events.
2. A nervous system — a bus that carries those events reliably.
3. A brain — something that looks at the events and forms a judgment.

We're going to build all three locally:

- Senses: the public Coinbase WebSocket feed. It pushes live crypto trades to anyone, no API key. Every time a trade matches on the exchange, we get a tick: price, side, size.
- Nervous system: Kafka. This is the part most ambient-agent tutorials skip, and it's a shame, because a Kafka topic is the event stream the definition keeps talking about. It decouples the senses from the brain — the producer doesn't know or care that an LLM is downstream.
- Brain: a local LLM via Ollama. No cloud, no API bill, no key. The model reasons about what's happening in the market and writes a human-readable read.

## The one design decision that matters

![](https://substackcdn.com/image/fetch/$s_!7js2!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff6d92870-dd2a-4c36-a043-6a665a09a49f_1856x2304.png)

Here's the trap. A liquid market emits hundreds of trades a second. If you hand every tick — or even every one-second window — to an LLM, two things happen: your tokens evaporate, and your agent falls behind the stream it's supposed to be watching.

> An ambient agent that can't keep up with its own input is useless. (This is point #1 from the theory coming home to roost: efficiency is the core constraint.)

The fix is a two-stage funnel, and it's the single most important idea in this build:

- Stage 1 — cheap math, runs on every window, no LLM. For each symbol over a short window we compute a few numbers: percentage price move, number of trades, the buy/sell imbalance, the volume. If nothing crosses a threshold, the window dies right here, for free. The vast majority of windows are boring, and boring is free.
- Stage 2 — the LLM, only when Stage 1 trips. When a window does look interesting — a sharp move, a lopsided flood of sells — only then do we wake the model and ask it for a human-readable judgment.

This is the same principle every good monitoring system uses: cheap filters up front, expensive analysis only on the candidates that survive. The LLM is precious; spend it deliberately.

## Let's build it (grab the code first!)
