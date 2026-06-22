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

Everything from here on is a walkthrough of a small, complete project you can run yourself.

Rather than paste hundreds of lines into the article, I've packaged the whole thing — Docker Compose, the producer, the agent, and the optional Telegram bit — into a single download.

[Download the code here!](https://drive.google.com/file/d/1zECsXxm8cEIFJ7SW6UmrMvYR7tqesnM8/view?usp=sharing)

The rest of this article walks through why each piece looks the way it does. I'll show the parts that matter and skip the boilerplate — you've got the full source in front of you, so I'd rather explain the decisions than narrate every line.

### 🎥 Watch it run

Video embed: `data-video-id="acd2c5fd-89ea-4961-ac5e-1e971fb15c85"`; poster: `https://substack-video.s3.amazonaws.com/video_upload/post/200983183/acd2c5fd-89ea-4961-ac5e-1e971fb15c85/transcoded-00001.png?refresh=Mon Jun 22 2026 16:57:28 GMT+0800 (台北標準時間)`.

## The senses: streaming Coinbase into Kafka

The producer connects to Coinbase’s WebSocket, subscribes to the `ticker` channel, and republishes each tick in a normalized shape onto a Kafka topic. The key idea: the agent never talks to Coinbase. It only ever sees our own event schema. That’s what makes this a template — swap the producer for one that reads earthquakes or Wikipedia edits, and nothing downstream changes.

```
def to_event(msg: dict) -> dict | None:
    """Map a Coinbase ticker message to our normalized schema."""
    if msg.get("type") != "ticker" or "price" not in msg:
        return None
    return {
        "ts": msg.get("time"),
        "source": "coinbase",
        "symbol": msg["product_id"],
        "price": float(msg["price"]),
        "side": msg.get("side", ""),          # taker side: buy | sell
        "size": float(msg.get("last_size", 0) or 0),
        "best_bid": float(msg.get("best_bid", 0) or 0),
        "best_ask": float(msg.get("best_ask", 0) or 0),
        "vol_24h": float(msg.get("volume_24h", 0) or 0),
    }
```

The rest of the producer is plumbing: connect to Kafka (with retries, because the broker may still be electing a leader when we boot), subscribe, and on every message push the normalized event. It reconnects forever — an ambient agent’s senses should never stay down.

## The brain: window, filter, then reason

The agent is the heart of the project. It consumes the stream into per-symbol windows, and every `WINDOW_SECONDS` it runs the funnel.

Stage 1 is just arithmetic:

```
def summarize(symbol: str, ticks: list) -> dict:
    """Stage 1: cheap per-symbol stats over the window. No LLM."""
    prices = [t["price"] for t in ticks]
    first, last = prices[0], prices[-1]
    move_pct = ((last - first) / first * 100.0) if first else 0.0
    buys = sum(1 for t in ticks if t.get("side") == "buy")
    n = len(ticks)
    buy_share = buys / n if n else 0.0
    return {
        "symbol": symbol, "trades": n,
        "first_price": round(first, 2), "last_price": round(last, 2),
        "move_pct": round(move_pct, 3),
        "high": round(max(prices), 2), "low": round(min(prices), 2),
        "buy_share": round(buy_share, 2), "sell_share": round(1 - buy_share, 2),
        "volume": round(sum(t.get("size", 0) for t in ticks), 4),
    }
```

The gate decides whether this window is worth the LLM’s time:

```
def is_interesting(s: dict) -> bool:
    if s["trades"] < MIN_TRADES_TRIGGER:      # ignore thin, illiquid noise
        return False
    if abs(s["move_pct"]) >= MOVE_PCT_TRIGGER:    # a real price move
        return True
    if max(s["buy_share"], s["sell_share"]) >= IMBALANCE_TRIGGER:  # lopsided flow
        return True
    return False
```

Only if `is_interesting` returns `True` do we reach Stage 2 and ask Ollama. Notice the prompt does two jobs: it asks for a plain, sober description, and it forbids the model from giving advice or telling anyone to trade. The agent observes and notifies — nothing more.

```
SYSTEM_PROMPT = """You are an ambient crypto market-watch agent.
You receive a JSON summary of one symbol's trading over a short window...
You CANNOT trade. You only notify. Never give financial advice.
Respond with ONLY a JSON object: {notable, severity, headline, detail}."""
```

We call Ollama with `"format": "json"` so the response is constrained to valid JSON we can parse directly — no fragile string scraping.

## Notify-only, on purpose

When a window survives both stages, the agent does three things, none of which touch the market:

```
def notify(verdict: dict, summary: dict) -> None:
    """Notify-only: console + JSONL + optional Telegram. No trading."""
    # 1. print a human-readable line to the console
    # 2. append a structured record to alerts.jsonl
    # 3. (optional) push the same alert to Telegram
```

That `notify()` function is the single seam where the human-in-the-loop lives. Today it prints and optionally pushes to Telegram. Tomorrow you could point it at an approval inbox and graduate from notify to review — the rest of the agent wouldn’t change.

The optional Telegram bit is genuinely satisfying: with a bot token and a chat id dropped into `.env`, the alerts land on your phone.

Your laptop is now quietly watching the market and tapping you on the shoulder only when it matters! 🤣

## Watching it run

`docker compose up --build` brings up Kafka, Ollama (which pulls the model once), the producer, and the agent. Most windows look like this:

```
[agent] quiet — 412 ticks across 3 symbols, nothing tripped the filter
```

That’s the funnel working: 412 trades processed, zero LLM calls, zero cost. Then the market does something, Stage 1 trips, and:

```
================================================================
  ⚡ [MEDIUM] BTC-USD  Sharp upward move on heavy buy pressure
     Price rose ~0.6% in 30s with buyers taking 82% of trades.
     move 0.61%  |  143 trades  |  buy 0.82 / sell 0.18
================================================================
```

No one asked it a question. It just knew.

![](https://substackcdn.com/image/fetch/$s_!n27T!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fba3c3e8a-38cf-4a73-9fe1-ec7bd833d10f_2752x1536.png)

## Making it yours

The whole thing is a template, and the seams are deliberate:

- Different stream? Rewrite the producer to read any source from the awesome-public-real-time-datasets list — USGS earthquakes, Wikimedia edits, Binance, the Bluesky firehose. Keep the event schema and nothing else changes.
- More or less twitchy? Tune the three thresholds in `.env`.
- Different judgment? Edit the system prompt.
- Different model? Change one line in `.env` — `qwen2.5`, `mistral`, whatever runs on your machine.

## From laptop to production

This stack is a dev rig, but the path to production is short because every piece is already decoupled:

- Kafka → swap the local broker for a managed one (Confluent, Redpanda, MSK); point `KAFKA_BOOTSTRAP` at it and add SASL / TLS.
- The model → move off laptop Ollama to a GPU host or a hosted inference endpoint. The agent only needs a URL, so it’s a one-line change.
- producer + agent → each is a stateless container. Run them on a small VM with `docker compose up -d`, or as two services on Cloud Run / ECS / a Kubernetes Deployment. Because the agent uses a Kafka consumer group, you can run several replicas and they'll split the partitions automatically.
- Durability → give the topic real retention, supervise the agent so it restarts, and ship the alerts to a database or alerting service instead of a local file.
- Secrets → tokens and broker creds move into your platform's secret manager, out of `.env`.

## The takeaway

Ambient agents aren't a new model or a new framework. They're a shift in posture — from an agent that waits for you to one that watches the world and reaches out only when it should. The three organs (senses, a stream, a brain) and the two-stage funnel (cheap filter, then LLM) are all you need to start.

We built ours on crypto because the data is free and live, but the shape is universal. Point the senses somewhere else and you’ve got an entirely different agent for free.

Now go give yours something to watch.

> ⚠️ The complete, runnable project — Docker Compose, producer, agent, and Telegram integration — is included alongside this article. Clone it, `docker compose up`, and watch it work. This is a technical demo, not trading or financial advice; the agent only ever notifies.

## References

- LangChain — Introducing Ambient Agents — https://www.langchain.com/blog/introducing-ambient-agents
- Google Agent Development Kit — Ambient Agents — https://adk.dev/runtime/ambient-agents/
- Bijit Ghosh — Ambient Agents — https://medium.com/@bijit211987/ambient-agents-e80d3c77518e
- Coinbase Exchange — WebSocket Feed Overview (public market data) — https://docs.cdp.coinbase.com/exchange/websocket-feed/overview
- bytewax — Awesome Public Real-Time Datasets — https://github.com/bytewax/awesome-public-real-time-datasets
- Ollama — https://ollama.com
- Apache Kafka — https://kafka.apache.org
