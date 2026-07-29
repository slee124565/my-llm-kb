# MCP vs CLI was the wrong debate

Source: https://x.com/akshay_pachaar/status/2053166970166772052
Canonical status: https://x.com/akshay_pachaar/status/2053166970166772052
Author: Akshay @akshay_pachaar
Status ID: 2053166970166772052
Published: 2026-05-10
Captured at: 2026-07-29T21:37:14+08:00
Extraction: myAgentTools/xcom-article-import
Extraction file: `/Users/lee/ws/myKBs/myAgentTools/xcom-article-import/runs/xcom-2053166970166772052.md`
Import mode: X.com browser extraction
Content status: complete

Note: This article is a cleaned KB inbox article based on an X.com browser extraction. Source claims are preserved as source framing unless independently verified.

## 核心觀點

MCP vs CLI was the wrong debate

For most of 2025, AI engineers argued about how agents should call tools.

One camp said use MCP, the protocol Anthropic released for connecting agents to external services. The other camp said skip the protocol and just give the agent a shell.

Both sides had real arguments. Both sides were also missing the point.

# What each camp got right

The skeptics measured what MCP servers actually cost in context:

- Playwright MCP eats 13.7K tokens
- Chrome DevTools MCP eats 18K
- A 5-server setup burns 55K tokens before any work ![Image](https://pbs.twimg.com/media/HH5N7nNaUAAjmDT?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2053166970166772052/media/2053164166660378624)

The defenders pushed back with the multi-tenant case:

- CLIs break on multi-tenant apps
- No typed contracts, so the agent guesses at outputs
- On unfamiliar APIs, agents waste turns parsing text ![Image](https://pbs.twimg.com/media/HH5N-wWaAAA1MpH?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2053166970166772052/media/2053164220653633536)

If you are reading this and thinking "okay, so which one wins?", that was the wrong question.

# The reframe

On November 4, 2025, Anthropic published " [Code execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp)

" and changed the conversation.

The problem was never the protocol. It was the habit of loading every tool's full description into context the moment a session starts. Add the data those tools return, passed through the model on every step, and a single workflow can balloon to 150K tokens.

The fix is to flip the model's job. Instead of calling tools through its context, the model writes code that calls tools through a runtime. The model only sees what it imports.

In Anthropic's example, a Google Drive transcript flows into a Salesforce CRM update. The old way loaded both tool schemas and piped the transcript through the model twice. The new way is a few lines of TypeScript that import what they need. Same task, 2K tokens. A 98.7% drop.

[Cloudflare pushed it further](https://blog.cloudflare.com/code-mode-mcp/)

. They collapsed their entire 2,500-endpoint API from 1.17M tokens of schemas down to 1K tokens, by exposing just two functions: `search` and `execute`. The agent writes code that searches the catalog, then executes only what matches.

![Image](https://pbs.twimg.com/media/HH5OqqkagAAOMcx?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2053166970166772052/media/2053164975016017920)

# The new pattern: Code Mode

Code Mode is a runtime where the agent writes code that mixes two primitives.

Bash , for anything with a binary already installed like git, curl, or grep. The model has seen these in training data and knows how to compose them. Need to find every Python file that imports pandas? The agent writes one line:

```bash
grep -r "import pandas" --include="*.py" .
```

No tool definition needed. The shell does the work.

Typed module imports , for proprietary APIs like Salesforce, Stripe, or your internal services. Think of these as small TypeScript files the agent can pull in on demand. Each file describes one tool, with its inputs and outputs spelled out. The agent only loads the files it actually uses.

That second part is the unlock. The type signatures travel with the import. The agent gets a strict contract for the tools it picks, and pays nothing for the ones it skips.

Here is what that looks like in practice:

```typescript
// The agent writes this. Types load only on these import lines.
import { searchFiles } from "@tools/github";
import { sendMessage } from "@tools/slack";

const files = await searchFiles({ pattern: "*.py", path: "./src" });
const summary = files.map(f => f.path).join("\n");

await sendMessage({
 channel: "#engineering",
 text: `Found ${files.length} Python files:\n${summary}`,
});
```

Three things are happening here that were not possible before.

The GitHub and Slack tool definitions enter context only on the import lines. Every other tool the runtime offers stays out.

The file list is processed in code, not piped through the model. The model never sees the raw list of paths. It only sees the summary the code built.

The agent composes loops and transforms in actual code. No round-tripping through the model for every step.

A useful way to picture it: in the old model, the agent walks into a room with every tool laid out on the table. In Code Mode, the agent walks into a room with a directory of tools on the wall and picks up only what it needs.

MCP's typed contracts plus CLI's lazy loading, in one runtime. The agent picks per task.

![Image](https://pbs.twimg.com/media/HH5PFRPaEAApTP3?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2053166970166772052/media/2053165432073490432)

# Putting it all together

Three approaches, side by side, tell the full story.

![Image](https://pbs.twimg.com/media/HH5Pi-CaYAALNZG?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2053166970166772052/media/2053165942314786816)

MCP gave us typed contracts, but loaded everything upfront. CLI gave us lazy access, but no contracts. Code Mode took the typed contracts from MCP and the lazy loading from CLI, and put both inside one runtime.

The footer of the diagram is the practical takeaway. Code Mode is not a replacement for either approach. It is a runtime that uses both. Bash for anything with a binary on [$PATH](https://x.com/search?q=%24PATH&src=cashtag_click)

. Typed module imports for proprietary APIs.

The agent decides per task. A file search is bash. A Salesforce update is a typed import. The same workflow can mix both in a few lines of code.

This is also why the debate framed as "MCP versus CLI" missed the point. Both approaches survived. They just stopped being the runtime, and became the primitives the runtime composes.

# What this means

"MCP is dead" was the wrong takeaway from the debate.

Anthropic just reported 300M MCP SDK downloads, up from 100M at the start of the year. The protocol is not dying. It is the fastest growing piece of agent infrastructure right now.

What died was loading every tool upfront. That was always a bad idea.

If you are building agents in 2026, the rule is simple. Tool definitions belong in code, not in context. The model writes a few lines that call them. The runtime does the rest.

That is what the debate was actually about.

Thanks for reading!

If you found it insightful, reshare with your network.

Find me → [@akshay_pachaar](https://x.com/@akshay_pachaar)

✔️

For more insights and tutorials on LLMs, AI Agents, and Machine Learning!

[Upgrade to Premium](https://x.com/i/premium_sign_up)

[1:35 AM · May 10, 2026](https://x.com/akshay_pachaar/status/2053166970166772052)

## Source Notes

- Source URL: https://x.com/akshay_pachaar/status/2053166970166772052
- Author: Akshay @akshay_pachaar
- Status ID: 2053166970166772052
- Published: 2026-05-10
- Captured at: 2026-07-29T21:37:14+08:00
- Extraction file: `/Users/lee/ws/myKBs/myAgentTools/xcom-article-import/runs/xcom-2053166970166772052.md`
- Content status: complete
