# Stateful vs. Stateless MCP core.

Source: https://x.com/akshay_pachaar/status/2082454281630961687
Canonical status: https://x.com/akshay_pachaar/status/2082454281630961687
Author: Akshay @akshay_pachaar
Status ID: 2082454281630961687
Published: 2026-07-29
Captured at: 2026-07-29T21:39:32+08:00
Extraction: myAgentTools/xcom-article-import
Extraction file: `/Users/lee/ws/myKBs/myAgentTools/xcom-article-import/runs/xcom-2082454281630961687.md`
Import mode: X.com browser extraction
Content status: complete

Note: This article is a cleaned KB inbox article based on an X.com browser extraction. Source claims are preserved as source framing unless independently verified.

## 核心觀點

Stateful vs. Stateless MCP core.

(Anthropic's biggest MCP update)

Let me explain what that means:

Until this release, talking to an MCP server worked like a phone call. Both sides ran an initialize handshake, and the server returned a session id carried on every later request.

That session was a live object inside one specific server process, holding the negotiated state.

Picture a restaurant where the waiter who took the order is the only one who knows what was ordered. Everything works until that waiter goes home.

Because that state lives in one process, a balancer could not spread requests across three MCP server instances. Teams pinned clients with sticky sessions or pushed session state into shared storage, which blocked autoscaling and made a single restart drop every open session.

The latest update deletes all of it. The handshake and the Mcp-Session-Id header are gone, and each request now carries its own protocol version, client identity, and capabilities in a _meta field.

Clients that want the capability list up front can call server/discover, but nothing requires it.

The restaurant works the other way around now. That flips the restaurant around. Every request is a written order slip now, and any waiter can fill it.

So any request can land on any instance behind a plain round-robin balancer, with no shared session store. MCP servers become ordinary HTTP services that run on serverless and edge, and survive restarts.

Removing sessions broke three features, so each got rebuilt.

→ Tools that need to ask the user something mid-call used to push that request down a held-open stream. Now the server returns input_required and the client retries with the answers attached.

→ Method and tool names moved into the Mcp-Method and Mcp-Name headers, so a gateway or rate limiter can route and meter without parsing the JSON-RPC body.

→ List responses carry ttlMs and cacheScope, so clients cache tool catalogs instead of refetching them on every reconnect.

State did not disappear here, it moved somewhere the model can see it.

Applications that need continuity get an explicit handle from a tool and have the model pass it back as an argument on the next call.

A session id in a header is invisible to the model, while a handle in the arguments is something it can read, thread between tools, and recover from after a failed call.

Official Spec: [modelcontextprotocol.io/specification/](https://t.co/jC4Lu7eGi5) Since we are on MCP, I also wrote about why the MCP versus CLI debate was the wrong one, and how agents can call tools by writing code instead of loading every schema into context.

The article is quoted below.

![Article cover image](https://pbs.twimg.com/media/HH4Rw7RbsAAQ5JQ?format=jpg&name=medium)

MCP vs CLI was the wrong debate

For most of 2025, AI engineers argued about how agents should call tools.
One camp said use MCP, the protocol Anthropic released for connecting agents to external services. The other camp said skip...

## Source Notes

- Source URL: https://x.com/akshay_pachaar/status/2082454281630961687
- Author: Akshay @akshay_pachaar
- Status ID: 2082454281630961687
- Published: 2026-07-29
- Captured at: 2026-07-29T21:39:32+08:00
- Extraction file: `/Users/lee/ws/myKBs/myAgentTools/xcom-article-import/runs/xcom-2082454281630961687.md`
- Content status: complete
