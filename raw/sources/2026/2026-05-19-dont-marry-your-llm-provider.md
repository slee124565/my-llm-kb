# Don't Marry Your LLM Provider

Source: https://theneuralmaze.substack.com/p/dont-marry-your-llm-provider
Author: Miguel Otero Pedrido
Publisher: The Neural Maze
Published: 2026-05-19
Captured: 2026-06-19
Tags: AI Systems Engineer Journey
Subtitle: Issue #03 — Why every production agent ends up behind a reverse proxy

Markdown Content:

Hey friends! 👋

Welcome to Issue #03 of The AI Systems Engineer Journey.

Last week we covered how real agentic systems actually look, walking through every box in the diagram. If you missed it, [here it is](https://theneuralmaze.substack.com/p/hidden-technical-debt-in-agentic) (bookmark it, then come back!).

Today I want to go deeper into one of those boxes, in particular the Model Layer. You might think it's a pretty straightforward one, but there's a sentence I dropped last week that I want to focus on, because I think it deserves its own issue.

> "The other thing you want — and almost nobody has on day one — is provider-agnostic abstractions. LiteLLM, OpenRouter, Vercel AI Gateway, etc. are good examples."

So in today's issue we'll go through what an AI gateway is, what it looks like in code, and what actually happens when a request hits one of these.

I'll also share three real-world patterns you'll need the moment your agent leaves localhost. There's a working example at the bottom (Dockerfile, config, example client) you can run locally too!

Let's go 😎

Quick reminder before we dive in: on May 20th (yes, TOMORROW 😱), [Luis Serrano](https://open.substack.com/users/360972495-luis-serrano?utm_source=mentions), , and I are running a free live masterclass for real agentic builders.

> 👉 [Save your spot here](https://tinyurl.com/agentsmasterclass)

Think of this issue as the map of an agentic system. The masterclass is the territory. Luis on the theory of how agents reason and plan, me on what it actually takes to ship one without setting production on fire 🔥. One hour, completely on the house.

![](https://substackcdn.com/image/fetch/$s_!dUMp!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F77bd8607-bd4c-40ac-bc60-22e4ab6f1dd3_1280x720.png)

It's also an official sneak peek of [Grokking Agents in Production](https://serranoacademy.mykajabi.com/grokking-agents), our 6-week course launching on June — Luis on theory, Antonio and me on production, GCP throughout.

# The reverse proxy lesson

![](https://substackcdn.com/image/fetch/$s_!RaJs!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F48fb8dee-4aae-43b2-9273-ad2c6d78951a_2128x1262.png)

Mid-2010s, every web app on the internet grew the same box on its architecture diagram: an nginx out in front. The reason was always the same: a class of concerns — TLS, request logging, rate limiting, auth, fan-out — doesn't belong inside the app. It belongs in one box every request passes through.

That box has a name: reverse proxy.

> The whole point of a reverse proxy is to pull cross-cutting concerns out of N apps and into 1 box.

Now look at what teams building agents are doing on day one. Every app calls OpenAI directly with the raw key, retry logic gets reinvented from scratch in each repo (subtly different in every one, of course), and when the key inevitably leaks, somebody loses an afternoon rotating it across seventeen places.

> It's the 2010 web architecture, with API keys instead of TLS certs.

The fix is the same fix: you put a box in the middle. In the web world we called it nginx. In the LLM world we call it an AI gateway — mechanically the same idea, with LLM-specific superpowers.

# What the gateway actually solves

Concretely, the moment you have more than one app calling more than one LLM, here's the list of concerns you want out of your apps and into the gateway:

- One API shape, many backends. Your apps speak the OpenAI `/chat/completions` format. The gateway translates to whatever the provider needs — Anthropic Messages, Bedrock invoke, Gemini's generateContent, your local Ollama. Client code doesn't change when you swap providers.
- Fallbacks. If provider A returns a 529, the gateway transparently retries on Provider B. Your agent doesn't know the failover happened.
- Routing strategies. Round-robin across deployments. Latency-aware load balancing. Send "easy" calls to small/cheap models, "hard" ones to a frontier model. Declarative config, not application code.
- Virtual API keys. Devs don't see the raw OpenAI key. They get a scoped, budgeted, revocable virtual key the gateway issued.
- Budgets and rate limits. The intern team gets $50/mo. The production app gets $5,000. The gateway enforces it (… and nobody calls you at 3am!)
- Cost attribution. Every call tagged by app/team/user. Real breakdowns at month-end, not one giant opaque OpenAI invoice.
- Caching and observability. Once at the gateway, applied to every app behind it. Traces flow to your observability stack via OpenTelemetry.
- MCP and tool routing. The 2026 plot twist! Modern gateways proxy MCP servers too — your `/chat/completions` call can include tools from a registered MCP server and the gateway handles discovery, auth, and routing.

None of these are business logic. They're all plumbing. And plumbing belongs in the box in front of your app, not in the app itself.

# Meet LiteLLM

![Getting Started | liteLLM](https://substackcdn.com/image/fetch/$s_!RBSd!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd7c95824-e3e7-4a1c-bcc4-ca1b3bf404c1_1920x801.png)

Three categories of gateway exist in the wild: managed (OpenRouter, Vercel AI Gateway), self-hosted open source (LiteLLM, Portkey, Helicone), and "we'll build it ourselves" (don't).

I'm spending the rest of this issue on [LiteLLM](https://github.com/BerriAI/litellm) — open source, 140+ providers, north of 240M Docker pulls. LiteLLM ships in two modes:

1. SDK mode — `pip install litellm`, call it as a Python library. Same shape as the OpenAI SDK, but you can pass any model name from any provider. Fine for prototypes; not a gateway.
2. Proxy mode — run the official Docker image, point it at a `config.yaml`, it starts an HTTP server on port 4000 speaking the OpenAI API. This is the gateway. This is what we want.

LiteLLM offers a managed cloud version if you want somebody else to operate the box. But the reason LiteLLM has become the default open-source AI gateway is that the exact same software runs self-hosted with one Docker image — your hardware, your network, your data.

That's what we're going to do today.

# The config that does all the work

The thing that hooked me on LiteLLM the first time: the entire gateway is configured in one YAML file. You describe the box's behavior declaratively and the proxy does the rest.

Minimal three-provider setup:

```text
model_list:
  - model_name: gpt-4o-mini
    litellm_params:
      model: openai/gpt-4o-mini
      api_key: os.environ/OPENAI_API_KEY

  - model_name: claude-haiku
    litellm_params:
      model: anthropic/claude-haiku-4-5
      api_key: os.environ/ANTHROPIC_API_KEY

  - model_name: groq-llama
    litellm_params:
      model: groq/llama-3.3-70b-versatile
      api_key: os.environ/GROQ_API_KEY
```

Start the proxy, and your apps now hit

`http://localhost:4000/chat/completions`

and pick any of those three by name. Three providers, but same code path.

Add a simple fallback chain on top:

```text
router_settings:
  num_retries: 2
  timeout: 30
  fallbacks:
    - gpt-4o-mini: ["claude-haiku", "groq-llama"]
```

If `gpt-4o-mini` errors, the gateway transparently retries on `claude-haiku`, then on `groq-llama`. Your agent code never knew anything went wrong.

And the 2026 plot twist — MCP servers in the same config:

```text
mcp_servers:
  github_mcp:
    url: "https://api.githubcopilot.com/mcp"
    transport: "http"
    auth_type: oauth2
    client_id: os.environ/GITHUB_OAUTH_CLIENT_ID
    client_secret: os.environ/GITHUB_OAUTH_CLIENT_SECRET
```

Once that block is in the config, any client calling the gateway can use GitHub's MCP tools by including them in `tools` in a `/chat/completions` request — with zero MCP wiring on the client side.

This is the framing I want you to internalize: the gateway is becoming the single chokepoint for all agent runtime traffic — model calls, tool calls, sub-agent calls.

# Life of a request

![](https://substackcdn.com/image/fetch/$s_!ZXWm!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1c42d405-38d8-4beb-9110-808704b4d27a_1792x766.png)

What actually happens when one of your apps hits port 4000?

Request arrives at `/chat/completions` carrying a Bearer token in the header. The proxy doesn't reach for a provider yet — first it walks the request through three gates, in order, before any expensive work happens.

- Gate 1 — Auth. The Bearer token is a virtual key. The proxy checks if it knows about it — cache first (Redis or in-memory), DB only on a miss. The order is the point: a key that's hot in cache is resolved in microseconds; a DB lookup is milliseconds. At high RPS those compound. The cache hit ratio on this check is the difference between a 5ms gateway and a 50ms one.
- Gate 2 — Rate limits. Four checks in parallel: global server limit, virtual key limit, user limit, team limit. Whichever is tightest wins. Critically, this happens before any provider call. The gateway refuses overrun requests for free — you don't pay OpenAI for a request your own budget already said no to.
- Gate 3 — Routing. The request leaves the entry-point endpoint and lands in a separate component: the Router. Keep this distinction in your head. The proxy server polices the door (auth, limits). The Router does the actual routing — picks which deployment to call (round-robin, latency-aware, cost-aware, your choice in the YAML), walks the fallback chain on error, drives the circuit breaker, manages retries.

The provider call. Once the Router picks a deployment, it makes the actual HTTP call — translating your OpenAI-shaped request into the provider's native format, then translating the response back. Your client never sees the wire format of the upstream API.

Response goes back to the client. Done.

…almost.

Here's the design choice worth pointing at directly. Everything observability-related runs after the client already has its answer, asynchronously, off the critical path.

- Spend tracking written to the database? Async.
- Traces shipped to Langfuse / MLflow / Opik ? Async.
- Rate-limit counters updated so the next request sees fresh numbers? Async.

This asymmetry is why a well-configured LiteLLM proxy adds only single-digit-millisecond latency to a model call. The hot path is auth → limits → route → call → respond, and nothing else. All the platform work — logging, accounting, monitoring — happens in background tasks the user never waits for.

That kind of separation is the thing you can only do because it's a gateway. Inside your app, you'd have to wait for the logger to flush. In the gateway, you don't.

> That’s the difference between a feature and an architecture.

# Three patterns the docs bury

Everything above is the demo. Here are the three patterns I've watched separate the teams that get into production from the teams that don't.

## Pattern A — Federate API keys to escape your own rate limits

Every provider gives you a per-account rate limit.

The naive fix is "wait it out" or "throttle the app." The actual fix is this: register the same model multiple times under the same `model_name`, each with a different API key.

The router treats them as separate deployments and round-robins across them. Your effective rate limit is the sum.

```text
model_list:
  - model_name: gpt-4o
    litellm_params:
      model: openai/gpt-4o
      api_key: os.environ/OPENAI_API_KEY_PROD
      rpm: 500

  - model_name: gpt-4o
    litellm_params:
      model: openai/gpt-4o
      api_key: os.environ/OPENAI_API_KEY_BACKUP
      rpm: 500

router_settings:
  routing_strategy: simple-shuffle
  allowed_fails: 3       # take a deployment out after 3 failures
  cooldown_time: 60      # try it again after 60 seconds
```

Same model name to the client. Two real keys under the hood. 1,000 RPM instead of 500, with automatic circuit-breaker behavior baked in.

This is the cheapest scaling win you'll ever ship.

## Pattern B — The two fallbacks nobody knows exist

When most people say "fallback," they mean the basic kind: provider A errors out, retry on provider B.

LiteLLM ships two more fallback types that are buried in the docs and solve real problems most teams discover the painful way:

```text
litellm_settings:
  fallbacks:
    - gpt-4o: ["claude-sonnet"]

  # When the provider refuses a prompt on content-policy grounds,
  # try a different provider instead of failing the user.
  content_policy_fallbacks:
    - gpt-4o: ["claude-sonnet"]

  # When the input is too long for the small/cheap model,
  # automatically escalate to a bigger context window.
  context_window_fallbacks:
    - gpt-4o-mini: ["gpt-4o", "claude-sonnet"]
```

Content policy fallback is the answer to "OpenAI's moderator refused the request but Claude is happy to answer it" (and vice versa) — a routine occurrence in production. Instead of returning an error, the gateway just tries the other one.

Context window fallback is the answer to "my agent stuffed too much context into the request and the small model rejected it." Instead of crashing, the gateway escalates to a model that can handle the size. Your agent doesn't have to know which model is which — it just asks for `gpt-4o-mini` and the gateway gives back the right size automatically.

Both convert "user-visible error" into "slightly more expensive successful response." That's an obviously good trade you're not making until you turn them on.

## Pattern C — Cost-based routing across a model fleet

Callback to [Issue #02](https://theneuralmaze.substack.com/p/hidden-technical-debt-in-agentic):

> "Move 60% of those calls to a small model and you’re around $0.18 instead of $0.40 per run.”

That math only works if you actually have a routing layer. Here's that layer:

```text
model_list:
  - model_name: cheap-tier
    litellm_params:
      model: gemini/gemini-2.0-flash
      api_key: os.environ/GEMINI_API_KEY

  - model_name: cheap-tier
    litellm_params:
      model: openai/gpt-4o-mini
      api_key: os.environ/OPENAI_API_KEY

  - model_name: cheap-tier
    litellm_params:
      model: anthropic/claude-haiku-4-5
      api_key: os.environ/ANTHROPIC_API_KEY

router_settings:
  routing_strategy: cost-based-routing
```

Three deployments backing one logical name. The router knows the per-token pricing for each and routes each call to the cheapest available option, falling back to the next when one is unavailable.

Your client code just calls `cheap-tier`. The cost optimization is decoupled from the agent. The day Gemini drops its price by 30%, you change nothing — the router silently shifts the traffic. The day Anthropic releases a better Haiku at a lower price, you add it to the list and you're done.

That's what "your model is rented" actually means, in production. Not "I could swap providers if I wanted to." "My gateway is constantly swapping providers and my code never sees it."

# Self-host it in five minutes
