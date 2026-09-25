# Claude Fable is relentlessly proactive

Source: https://simonw.substack.com/p/claude-fable-is-relentlessly-proactive
Author: Simon Willison
Publisher: Simon Willison’s Newsletter
Published: 2026-06-13
Captured: 2026-09-25
Tags: anthropic, llms, ai
Subtitle: I have a lot to say about Anthropic's new Mythos-class model

Markdown Content:

In this newsletter:

- Claude Fable is relentlessly proactive
- Initial impressions of Claude Fable 5

Plus 4 links and 3 quotations and 1 note and 5 releases and 1 TIL

Sponsor message: Engineering speed vs. security: End the tradeoff with unified identity Access shouldn’t take hours to approve. Security teams shouldn’t need to stitch audit data across different systems. [Teleport](https://fandf.co/42ImSdl) gives engineers and their workloads the just-in-time access they need with cryptographic identity for every human, machine, and agent and short-lived, just-in-time privileges issued at runtime. Faster engineering, unified audit trails – everyone wins.

### [Claude Fable is relentlessly proactive](https://simonwillison.net/2026/Jun/11/fable-is-relentlessly-proactive/) - 2026-06-11

After two days of experience with [Claude Fable 5](https://simonwillison.net/2026/Jun/9/claude-fable-5/) I think the best way to describe it is relentlessly proactive. It knows a whole lot of tricks and it will deploy pretty much any of them to get to its goal.

I’ll illustrate this with an example. I was hacking on [Datasette Agent](https://agent.datasette.io/) today when I noticed a glitch: a horizontal scrollbar that shouldn’t be there in the jump menu chat prompt. I snapped this screenshot:

![Screenshot of a modal dialog demonstrating a scrollbar bug. At the top is a focused search input with blue outline and placeholder "Jump to...", with an X close button to its right. Below, a heading reads "Start a new agent chat" above a textarea with the placeholder "Ask a question about your data..." — the bug: a thick gray horizontal scrollbar is incorrectly displayed along the bottom edge of the empty textarea, spanning nearly its full width, next to the resize handle. Below the textarea: "Press Enter to start. Shift+Enter adds a new line." followed by a blue "Start chat" button.](https://substackcdn.com/image/fetch/$s_!zcb0!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F06d92881-c3e2-44f7-aa2f-a8102c0ccf25_1494x782.jpeg)

Then I started a fresh `claude` session in my `datasette-agent` checkout, dragged in the screenshot and told it:

> `Look at dependencies to help figure out why there is a horizontal scrollbar here`

I had a hunch the cause was in a dependency of Datasette Agent (likely Datasette itself) and I knew Fable was good at digging into dependency code, either by inspecting installed files in its own virtual environment `site-packages` or by referencing a local checkout on disk. Telling it to start with dependencies felt like a good bet.

I got distracted by a domestic task and wandered away from my computer.

When I came back a few minutes later I saw my machine open a browser window in my regular Firefox and then navigate to the dialog in question. I had not told Claude Code to use any browser automation, and I was pretty sure it wasn’t possible for it to trigger mouse movements or keyboard shortcuts within a window, so how was it doing that?

I watched in fascination as it continued with its explorations, then saw it open a Safari window instead of Firefox. I also grabbed this snapshot from the Claude terminal:

![Screenshot of two Bash tool calls in a dark terminal interface. First: Bash(open -a Safari /tmp/textarea-scrollbar-test.html && sleep 4 && uv run --with pyobjc-framework-Quartz python - <<'EOF' import Quartz wins = Quartz.CGWindowListCopyWindowInfo(Quartz.kCGWindowListOptionOnScreenOnly, Quartz.kCGNullWindowID) for w in wins: if (w.get('kCGWindowOwnerName') or '') == 'Safari' and 'textarea' in (w.get('kCGWindowName') or '').lower(): print(w.get('kCGWindowNumber')) EOF) with output 153551. Second: Bash(screencapture -x -o -l 153551 /tmp/safari-cases.png && echo ok) with output ok.](https://substackcdn.com/image/fetch/$s_!cQbz!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F83ad005e-588d-4dec-8eb1-033ed2c6c084_2274x444.jpeg)

What was it doing there with `uv run --with pyobjc-framework-Quartz`?

It turns out Fable had hacked up its own pattern for taking screenshots of browser windows. It was using Python to iterate through all available windows on my machine, then filtering for Safari windows with expected strings such as `"textarea"` in the window name. It used that to find their window number - an integer like 153551 - which it could then use with the `screencapture` CLI tool to grab a PNG.

OK fine, that’s a neat way of taking screenshots. But what was it taking screenshots of?

Turns out it had been writing its own scratch HTML pages to try and recreate the bug, then opening Safari and grabbing screenshots.

Here’s that [/tmp/textarea-scrollbar-test.html](https://static.simonwillison.net/static/2026/textarea-scrollbar-test.html) page it created, and the screenshot it took with `screencapture -x -o -l 153551 /tmp/safari-cases.png`:

(I have way too many open tabs!)

![Screenshot of a Safari browser window showing a textarea scrollbar test page at file:///private/tmp/textarea-scrollbar-test.html. Page text reads: scrollbar thickness: 17px | UA: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.4 Safari/605.1.15 | devicePixelRatio: 2. Four numbered test cases follow, each with a textarea containing the placeholder "Ask a question about your data...": 1. Exact plugin CSS (resize: vertical, default overflow), 2. Plugin CSS + overflow-x: hidden, 3. Plugin CSS + resize: none, and 4. Bare default textarea, which is a much smaller box with the placeholder wrapping onto two lines.](https://substackcdn.com/image/fetch/$s_!TTPb!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F267fa825-e1d0-4396-8c9d-8b8161a66d6f_2780x1445.jpeg)

OK, so I can see how it’s opening test pages and taking screenshots, but how on earth was it triggering the modal dialog that was meant to be under test? That’s only available via a click or a keyboard shortcut, and I couldn’t see a mechanism for it to run those in Safari.

I eventually figured out what it had done.

Claude was running in a folder that contained the source code for the application. It knows enough about [Datasette](https://datasette.io/) to be able to run a local development server. It turns out it was editing Datasette’s own templates to add JavaScript that would trigger the correct keyboard shortcut as soon as the window opened, adding code like this:

```text
<script>
window.addEventListener(”load”, function () {
  setTimeout(function () {
    document.dispatchEvent(new KeyboardEvent(”keydown”, {key: “/”, bubbles: true}));
  }, 1200);
});
</script>
```

1.2 seconds after the window opens, this code triggers a simulated `/` key, which is the keyboard shortcut for opening the modal dialog.

There was one challenge left. In order to understand what was going on, Claude needed to run JavaScript on the page to take measurements for itself.

It wrote its own custom web application to capture information via CORS, then ran that as a local server and opened a page with JavaScript that would POST directly to it!

Here’s the Python web app it wrote, using the standard library [http.server](https://docs.python.org/3/library/http.server.html) package:

```text
from http.server import HTTPServer, BaseHTTPRequestHandler

class H(BaseHTTPRequestHandler):
    def do_POST(self):
        n = int(self.headers.get(”Content-Length”, 0))
        open(”/tmp/diag.json”, “w”).write(self.rfile.read(n).decode())
        self.send_response(200)
        self.send_header(”Access-Control-Allow-Origin”, “*”)
        self.end_headers()
    def do_OPTIONS(self):
        self.send_response(200)
        self.send_header(”Access-Control-Allow-Origin”, “*”)
        self.send_header(”Access-Control-Allow-Headers”, “*”)
        self.end_headers()
    def log_message(self, *a):  # quiet
        pass

HTTPServer((”127.0.0.1”, 9999), H).serve_forever()
```

All this does is accept a POST request full of JSON and write that to the `/tmp/diag.json` file. It sends `Access-Control-Allow-Origin: *` headers (including from `OPTIONS` requests) so that code running on another domain can still communicate back to it.

Then Claude injected this code into the template that it was loading in a browser:

```text
const host = document.querySelector(”navigation-search”);
const ta   = host.shadowRoot.querySelector(”textarea”);
const cs   = getComputedStyle(ta);
fetch(”http://127.0.0.1:9999/diag”, {
  method: “POST”,
  body: JSON.stringify({
    dpr: window.devicePixelRatio,
    scrollWidth: ta.scrollWidth, clientWidth: ta.clientWidth,
    whiteSpace: cs.whiteSpace, width: cs.width,
  }),
});
```

This took measurements of the `<textarea>` inside the `<navigation-search>` Web Component and sent them to the server, which wrote them to a file on disk, which Claude could then read.

Having figured out all of these tricks Fable... hit some invisible guardrail and downgraded itself to Opus. Thankfully Opus had access to the full transcript and could continue using the tricks pioneered by Fable, and shortly afterwards found, tested and verified [the fix](https://github.com/datasette/datasette-agent/commit/a75a8b727b42c30ced1fc41dc8add7eb9f04fefe).

I prompted Opus to:

> `Write a report in /tmp/automation-report.md where you note down all of the tricks you have used in this session to test against real browsers on my computer, include runnable code examples`

Which produced [this report](https://gist.github.com/simonw/aef7f7db9ac992643110a74e43d6d42f), which was invaluable for piecing together the details of what had happened for this post.

I’ve shared [the full terminal transcript](https://gisthost.github.io/?cc14774f6d37eb67bf089f3ac3925f8f) of the Claude Code session as well.

#### A review of everything it did

Based on a screenshot and a one-line prompt, Claude Fable 5 + Claude Code:

- Figured out the recipe to run the local development server (with fake environment variables needed to get it running)
- Fired up a Playwright Chrome session
- Turned on the visible scrollbars setting for Chrome `defaults write com.google.chrome.for.testing AppleShowScrollBars Always` (it turned that off again later)
- Cycled through Firefox and WebKit in Playwright too, failing to recreate the bug
- Worked out my default browser was Safari
- Built a `textarea-scrollbar-test.html` HTML document
- Opened that in real (not Playwright) Firefox
- Found that `osascript -e 'tell application "System Events" to tell process "firefox" to id of window 1'` was blocked because “osascript is not allowed assistive access”
- Figured out that `uv run --with pyobjc-framework-Quartz python` workaround, described above
- Added JavaScript to the site templates in order to trigger the `/` key
- Built its own little Python CORS web server to capture JSON data
- Rewrote the template to capture that data and send it to the server
- Scripted its way through the Web Component shadow DOM to the information it needed
- Opened Safari to confirm the source of the bug
- Modified its custom template to hack in a potential fix
- Confirmed the hacked fix worked
- Reported back on how to fix the problem

Like I said, relentlessly proactive!

#### An estimate of the cost

I’m currently on the $100/month Claude Max plan, which includes a generous allowance for Fable up until June 22nd after which Anthropic say they’ll start charging full API prices for it.

I’m using [AgentsView](https://www.agentsview.io) to track my spending (see [this TIL](https://til.simonwillison.net/llms/agentsview-custom-model-price)). Here’s what AgentsView says this session would have cost me if I was paying full price for it:

```text
~ % uvx agentsview session usage be8850a7-6119-46a0-b5d6-79c7fff5ae2b
Session:       be8850a7-6119-46a0-b5d6-79c7fff5ae2b
Agent:         claude
Output:        68606
Peak ctx:      113178
Cost:          ~$12.11 (claude-fable-5, claude-opus-4-8)
```

If you don’t keep a close eye on it, Fable will quite happily burn $12 in tokens inventing new ways to debug your CSS.

#### I really need to lock this thing down

On the one hand, watching Fable go to extreme lengths to get the information that it needed to debug what was, in the end, a two-line CSS fix, was fascinating.

But on the other hand... this is a robust reminder that coding agents can do anything you can do by typing commands into a terminal - and frontier models know every trick in the book, and evidently a few that nobody has ever written down before.

If Fable had been acting on malicious instructions - a prompt injection attack hidden in code or an issue thread, or something I’d carelessly pasted into my terminal - it’s alarming to think quite how far it could go to exfiltrate data or cause other forms of mischief.

Running coding agents outside of a sandbox has always been a bad idea - it’s my top contender for [a Challenger disaster](https://simonwillison.net/2026/Jan/8/llm-predictions-for-2026/#1-year-a-challenger-disaster-for-coding-agent-security) incident, as described by Johann Rehberger in [The Normalization of Deviance in AI](https://embracethered.com/blog/posts/2025/the-normalization-of-deviance-in-ai/).

Fable is arguably smarter and hence more suspicious of potentially malicious instructions. But that smartness is very much a two-edged sword: if it does get subverted by instructions, the amount of damage it can do given its relentless proactivity is terrifying.

### [Initial impressions of Claude Fable 5](https://simonwillison.net/2026/Jun/9/claude-fable-5/) - 2026-06-09

I didn’t have early access to today’s [Claude Fable 5](https://www.anthropic.com/news/claude-fable-5-mythos-5) release, but I’ve spent the past ~5.5 hours putting it through its paces. My initial impressions are that this is something of a beast. It’s slow, expensive and has been quite happily churning through everything I’ve thrown at it so far. As is frequently the case with current frontier models the challenge is finding tasks that it can’t do.

First, let’s review the key characteristics.

Anthropic claim that [Claude Fable 5](https://www.anthropic.com/news/claude-fable-5-mythos-5) offers the same performance as Claude Mythos 5, except with much more strict guardrails in place to prevent it being used for harmful things. Those guardrails trigger often enough that the Claude API has new mechanisms for letting you know when you hit them, and even has a [new option](https://platform.claude.com/docs/en/build-with-claude/refusals-and-fallback) to request it falls back to another model automatically if something gets rejected.

Claude Mythos 5 is out today as well, [Anthropic say it](https://platform.claude.com/docs/en/about-claude/models/introducing-claude-fable-5-and-claude-mythos-5) “Shares Claude Fable 5’s capabilities without the safety classifiers”.

The models have a 1 million token context window, 128,000 maximum output tokens and a knowledge cut-off date of January 2026.

They are priced at twice the price of Claude Opus 4.5/4.6/4.7/4.8: $10/million input tokens and $50/million output tokens. There’s no increase in price for longer context usage.

Other than that the [upgrade guide](https://platform.claude.com/docs/en/about-claude/models/introducing-claude-fable-5-and-claude-mythos-5) is substantially thinner than [the similar guide for Opus 4.8](https://platform.claude.com/docs/en/about-claude/models/whats-new-claude-4-8).

#### The big model smell

The best way to describe Fable is that it feels big. Not just in terms of speed and cost, but also in how much it knows.

Here’s an example prompt, which I used to compare Fable’s knowledge with Opus 4.8 (typo included):

> `List all of Simon Willion's open source projects, most recent first, each with a rough date of when they were first released`

Opus 4.8’s reply [started like this](https://gist.github.com/simonw/e77abf645156ade8c5c610f524226dcb#response-1):

- LLM (~2023) – A command-line tool and Python library for interacting with large language models.
- Datasette (~2017) – A tool for exploring and publishing data, probably his most prominent recent project.
- sqlite-utils (~2018-2019) – A Python library and CLI tool for manipulating SQLite databases, often used alongside Datasette.
- Django (2005) – He is one of the co-creators of the Django web framework, along with Adrian Holovaty, originally developed at the Lawrence Journal-World newspaper.

> I don’t have a reliable, comprehensive, and date-verified list of all of Simon Willison’s open source projects, and I want to be honest about that rather than risk giving you inaccurate dates or fabricated entries.
> Here’s what I can tell you with reasonable confidence:
> Well-known projects by Simon Willison:
> He also maintains a large ecosystem of Datasette plugins and many smaller utilities (often with names like `shot-scraper`, various `*-to-sqlite` tools for importing data, etc.).

That’s not bad. Here’s [the start of the response](https://gist.github.com/simonw/e77abf645156ade8c5c610f524226dcb#response) for the exact same prompt from Fable 5 - both models were running without access to search:

## Notable projects (approximate dates)

- files-to-prompt (April 2024) – concatenates files into a single prompt for LLMs
- datasette-extract (2024) – plugin for extracting structured data using LLMs
- LLM (May–June 2023) – CLI tool and Python library for interacting with large language models, plus a large ecosystem of plugins (llm-gpt4all, llm-mistral, llm-claude, etc., 2023 onward)
- symbex (June 2023) – search Python code for symbols
- ttok and strip-tags (May 2023) – CLI tools for token counting and HTML cleanup for LLM pipelines
- datasette-lite (May 2022) – Datasette running entirely in the browser via WebAssembly/Pyodide
- shot-scraper (March 2022) – automated website screenshots via Playwright
- s3-credentials (November 2021) – CLI for creating scoped AWS S3 credentials
- django-sql-dashboard (2021) – SQL reporting dashboards for Django
- Dogsheep suite (2019) – personal analytics tools: twitter-to-sqlite, github-to-sqlite, healthkit-to-sqlite, dogsheep-beta, etc.
- sqlite-utils (2018) – CLI and Python library for manipulating SQLite databases
- Datasette (November 2017) – his flagship project; tool for exploring and publishing data
- csvs-to-sqlite (2017) – convert CSV files to SQLite
- Various early tools (~2007–2010) – soupselect, json-head, geocoders, and others
- Django (developed 2003–2005, open-sourced July 2005) – co-created with Adrian Holovaty at the Lawrence Journal-World

> I think you mean Simon Willison — the prolific open source developer, co-creator of Django, and creator of Datasette.
> An important caveat upfront: a truly complete list isn’t feasible. Simon Willison is famously prolific — he has published hundreds of repositories (Datasette alone has 100+ plugins, many written by him), and my knowledge has a cutoff date, so I’ll be missing his most recent work. Below are his notable projects with approximate initial release dates, most recent first:

(Here’s [GPT-5.5 for good measure](https://gist.github.com/simonw/8d05ce836d44bd8543055c9614f7c478). It listed even more projects than Fable did!)

In the past I’ve stated that I don’t care about how much models know - I want them to be able to manipulate text and code in useful ways and actively look up the information they need via search tools, not bake it into their weights.

But knowledge like this is a reasonably good proxy for model size - you can cram a whole lot more details about the world into a larger number of parameters.

Does knowing more stuff mean the model is better at the tasks we pose to it? I can certainly imagine how a coding model with deeper knowledge of modern libraries and patterns could crunch through coding tasks more effectively.

Is Fable really bigger than Opus? Anthropic haven’t said anything about model size, so all we have are tea-leaves, but the speed, pricing and my own poking at its knowledge make me think that it’s a large model. Maybe the largest yet from any vendor.

#### Using Fable in Claude.ai

Anthropic made Fable 5 available across all of their surfaces - the [Claude.ai](https://claude.ai/) chat interface, Claude Code for web, Claude Code CLI and Claude Cowork as well. The model is available “until June 22nd” on the subscription plans (I’m on $100/month Max at the moment), after which it will be billed extra.

Claude.ai is often under-estimated. Since [September 2025](https://simonwillison.net/2025/Sep/9/claude-code-interpreter/) every chat has had access to a full container environment to run code, including the ability to install additional packages and even clone repositories directly from GitHub.

Last week [I released micropython-wasm](https://simonwillison.net/2026/Jun/6/micropython-in-a-sandbox/), a Python library that uses [wasmtime](https://wasmtime.dev/) to run a custom build of MicroPython in WebAssembly to act as a sandbox for untrusted Python code.

I decided to see if Fable could upgrade that to running full Python instead. I started with this prompt:

> `Clone simonw/micropython-wasm from GitHub and research how this could use a full Python as opposed to MicroPython`

Fable identified that it could use Brett Cannon’s [cpython-wasi-build](https://github.com/brettcannon/cpython-wasi-build/releases) builds for this, but was unable to download them itself due to environment restrictions.

So I grabbed the two zip files from that page and uploaded them to Claude:

> `Here's the Brett Cannon builds` (`python-3.zip`, `_build-python-3.zip` as attachments)

And that was that. It churned away for a few minutes and got the entire thing working.

Part of the response included:

> I tried the cleaner single-zip-stdlib approach to shrink the filesystem surface, but CPython’s `getpath` bootstrap fails to find `encodings` from inside a zip without more prefix finessing — the directory-preopen approach works reliably, so that’s what the PoC uses. The zip path is solvable but needs `_PYTHONHOME`/frozen-getpath work.

So I said:

> `Try a bit more at the single-zip-stdlib problem`

Then a little later:

> `I want a wheel that has the whole system in it, the Python wrappers and the WASM files and the stdlibrary, so I can do uv run --with path-to-whl python -c "demo code"`

... and it gave me [this 13.9MB cpython_wasm-0.1.0-py3-none-any.whl](https://static.simonwillison.net/static/cors-allow/2026/cpython_wasm-0.1.0-py3-none-any.whl) file. You can try running Python code in a sandbox using that wheel URL and `uv` like this:

```text
uv run --with https://static.simonwillison.net/static/cors-allow/2026/cpython_wasm-0.1.0-py3-none-any.whl \
  cpython-wasm -c ‘print(45 ** 56)’
```

Here’s [the full chat transcript](https://claude.ai/share/a73b8b8b-8ebc-4fef-9e5c-7438e5e7ae35).

This was a very strong start.

#### Adding features to Datasette Agent and LLM using Claude Code

Before I’d realized it was Fable day, my stretch goal for today was to add a new feature to [Datasette Agent](https://agent.datasette.io/): I wanted tool calls within that agent software to gain the ability to pause mid-execution and request approval directly from the user.

This felt like a suitably meaty task to throw at the new model.

Over the course of the day Fable not only [solved that problem](https://github.com/datasette/datasette-agent/pull/20), it also identified and then implemented four issues in my underlying LLM library that would help support this kind of advanced pause-resume mechanism in tool calls.

It got everything working first using somewhat gnarly hacks, but the moment I told it that changes to LLM itself were in scope it set to work unraveling the hacks and turning them into supported features of LLM instead.

My stretch goal turned into [LLM 0.32a3](https://llm.datasette.io/en/latest/changelog.html#a3-2026-06-09), almost entirely written by Fable. Here are the release notes:

- Tool implementations can declare a parameter named `llm_tool_call` in order to be passed the `llm.ToolCall` object for the current invocation. This allows them to access the current `llm_tool_call.tool_call_id`. See [Accessing the tool call from inside a tool](https://llm.datasette.io/en/latest/python-api.html#python-api-tools-llm-tool-call). [#1480](https://github.com/simonw/llm/pull/1480)
- Every tool call is now guaranteed a unique `tool_call_id` - providers that do not supply one get a synthesized `tc_`-prefixed ULID. [#1481](https://github.com/simonw/llm/pull/1481)
- Tools can raise a `llm.PauseChain` exception to cleanly pause the tool chain, useful for things like waiting for human approval. The exception propagates to the caller with `.tool_call` and `.tool_results` (completed sibling results) attached, and no model call is made with a placeholder result. See [Pausing a chain from inside a tool](https://llm.datasette.io/en/latest/python-api.html#python-api-tools-pause). [#1482](https://github.com/simonw/llm/pull/1482)
- Failure semantics for concurrent tool execution: async sibling tool calls always run to completion before a pause or hook exception propagates. [#1482](https://github.com/simonw/llm/pull/1482)
- Chains can now resume from a `messages=` history ending in unresolved tool calls: the calls are executed through the normal `before_call`/`after_call` machinery before the first model call, skipping any that already have results. The `execute_tool_calls()` method also accepts a new optional `tool_calls_list=` argument for executing an explicit list of `ToolCall` objects in place of the calls requested by the response. See [Resuming a chain with pending tool calls](https://llm.datasette.io/en/latest/python-api.html#python-api-tools-resume). [#1482](https://github.com/simonw/llm/pull/1482)
- Fixed a bug where the async tool executor silently dropped calls to tools not present in `tools=` - these now return `Error: tool "..." does not exist` results, matching the sync executor. [#1483](https://github.com/simonw/llm/pull/1483)

> Driven by the needs of [Datasette Agent](https://github.com/datasette/datasette-agent)‘s human-in-the-loop `ask_user()` feature, made the following improvements to how tool calls work:

I’m really impressed with the quality of API design, tests, code and documentation that Fable put together for this. I spent several hours on it today, but it feels like several days’ worth of work.

#### How much I’ve spent

I recently started using [AgentsView](https://agentsview.io) to help track my local LLM usage across all of the different coding agents. I published a [TIL today](https://til.simonwillison.net/llms/agentsview-custom-model-price) about adding custom Fable pricing to that tool, which I expect will not be necessary in the very near future.

After setting the price, I ran this command to start a localhost web server to explore my usage:

```text
uvx agentsview serve
```

Here’s the treemap showing the breakdown of my Fable usage across various projects today:

![Screenshot of a cost tracking dashboard with two panels. The first panel is titled "Cost Attribution" with toggle buttons for Project / Model / Agent and Treemap / List, with Project and Treemap selected. Italic text reads "Click to hide from chart". A treemap shows a large red block labeled prod_datasette_agent $99.26 89.9%, with smaller blocks to its right labeled cloud (blue), datasette (teal), llm (red), and money (pink), plus a tiny orange sliver. A legend lists: 1 prod_datasette_agent $99.26, 2 cloud $3.98, 3 datasette $2.81, 4 llm $2.30, 5 money $1.92, 6 simon $0.15. The second panel is titled "Top Sessions by Cost" and lists nine sessions, each with a "Claude" badge, a prompt excerpt, a project name with a session UUID (omitted here), a token count, and a cost: 1. Review ./datasette-agent and ./datasette-apps - we are going to add a new feature to agent but you ... prod_datasette_agent, 78.2M, $99.26. 2. issues.db is a copy of the Datasette issues database. There are a LOT of notes in there relating to... datasette, 826.8k, $2.81. 3. Consult fly-docs and then look at datasette.cloud (which launches fly machines) and datasettecloud-... cloud, 924.7k, $2.61. 4. simonwillisonblog.db is a copy of my blog, plus all my software releases and other interesting thin... money, 542.9k, $1.92. 5. Look in datasette.cloud and figure out all remaining steps and decisions that need to be made in or... cloud, 455k, $1.37. 6. Review PRs and issues filed against this repo within the last 4 weeks and see if any deserve to be ... llm, 323.3k, $0.95. 7. run mypy, llm, 320.9k, $0.76. 8. \[Image #1\] fix this in github actions, llm, 183.9k, $0.59. 9. simon, simon, 26.4k, $0.15.](https://substackcdn.com/image/fetch/$s_!2LrF!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fbc0a49f4-5442-457e-8abe-c843fd42ce2e_1550x1578.jpeg)

I used $110.42 worth of tokens today, all as part of my $100/month subscription.

#### And some pelicans

I ran “Generate an SVG of a pelican riding a bicycle” against all five thinking effort levels with Fable.

Here are [the results](https://tools.simonwillison.net/markdown-svg-renderer#url=https%3A%2F%2Fgist.github.com%2Fsimonw%2F94fde31c34a0400c1d29f57e6a708e6b), including the token cost for each one:

![Comparison grid of five cartoon SVG illustrations of a pelican riding a red bicycle, each generated at a different thinking level with output token counts and costs shown as links beneath. Top row: low: 1,929 out, 9.67c shows a simple small pelican perched on a basic bike on green grass with a sun; medium: 2,290 out, 11.475c is similar but adds a cloud and speed lines, though the bike frame is more jumbled; high: 2,057 out, 10.31c has a slightly more upright pelican whose beak overlaps the sun. Bottom row, larger images: xhigh: 5,992 out, 29.985c is noticeably more polished, with a bigger expressive pelican leaning forward, wing on the handlebars, orange legs on the pedals, cloud, sun and speed lines; max: 14,430 out, 72.175c is the most detailed and dynamic, with a streamlined pelican with a long curved neck and large beak pedaling a well-drawn bike with realistic spokes and crank, speed lines suggesting motion. Quality and detail generally increase with thinking level, with the bigge](https://substackcdn.com/image/fetch/$s_!kRzi!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F22a38494-4dbb-4cba-b73c-6c690f327b0b_1316x1042.png)

It’s interesting that high ended up using fewer tokens than medium for this particular run.

Here are the [Opus 4.8 pelicans](https://simonwillison.net/2026/May/28/claude-opus-4-8/#and-some-pelicans) for comparison.

Release: [datasette-agent-edit 0.1a0](https://github.com/datasette/datasette-agent-edit/releases/tag/0.1a0)

I’m planning several plugins for [Datasette Agent](https://agent.datasette.io/) which can make edits to existing pieces of text - things like collaborative Markdown editing, updating large SQL queries, and editing SVG files.

Agentic editing of text is a little tricky to get right. My favorite published design for this is for the [Claude text editor](https://platform.claude.com/docs/en/agents-and-tools/tool-use/text-editor-tool#use-the-text-editor-tool), which implements the following tools:

- `view` - view sections of a file, with line numbers added to every line.
- `str_replace` - find an exact `old_str` and replace it with `new_str` - fail if the original string is not unique
- `insert` - insert the specified text after the specified line number

Rather than recreate these patterns for every plugin that needs them I decided to create this base plugin, `datasette-agent-edit`, which implements the core tools in a way that allows them to be adapted for other plugins.

Note [2026-06-08](https://simonwillison.net/2026/Jun/8/wwdc/)

Given how badly burned anyone who took Apple’s [2024 WWDC Apple Intelligence announcements](https://simonwillison.net/2024/Jun/10/apple-intelligence/) at face value was, I’m holding to a strict “I’ll believe it when I see it” policy for everything [they announced today](https://www.apple.com/newsroom/2026/06/apple-unveils-next-generation-of-apple-intelligence-siri-ai-and-more/).

The new Siri AI features do at least look feasible with today’s technology, especially since Apple are licensing a custom Gemini-derived model that they can run on their own [Private Cloud Compute](https://simonwillison.net/2024/Jun/11/private-cloud-compute/).

It sounds like they’ll be taking advantage of vision LLMs to extract information from the user’s screen, which neatly sidesteps the need for every existing application to ship custom code in order to integrate with Apple Intelligence. Vision LLMs were a much less mature category in June 2024.

The new Core AI library looks like a good step in enabling developers to finally take full advantage of Apple’s hardware for running their own models. It integrates with Meta’s open source PyTorch ecosystem, using these [Core AI PyTorch extensions](https://apple.github.io/coreai-torch/main/):

> Core AI PyTorch Extensions (`coreai-torch`) is a Python package that bridges PyTorch and Core AI. You can use it to bring up an existing PyTorch model — exported as a `torch.export.ExportedProgram` — into a Core AI `AIProgram` ready to run on Apple hardware, traversing the FX graph node-by-node and mapping ATen operators to Core AI operations.

You can install an iOS 27 Developer Beta today, which supposedly has the new features - but you then have to make it through a waiting list for access to the new Siri AI. Aaron Perris from MacRumors reports having [made it off the waitlist](https://twitter.com/aaronp613/status/2064078063814471977) so we may start seeing credible reports on how well Siri AI works in the very near future.

Update: These Private Cloud Compute Gemini models are running in Google Cloud, and using NVIDIA hardware. According to [Expanding Private Cloud Compute](https://security.apple.com/blog/expanding-pcc/?linkId=100000425571569) on Apple’s Security Research blog:

> For the most demanding tasks, including agentic tool-use and complex reasoning, we worked with Google and NVIDIA to extend our PCC infrastructure to Google Cloud systems using NVIDIA GPUs, while maintaining Apple’s powerful security and privacy protections. [...]
> PCC on Google Cloud leverages many of the same architectural security patterns as PCC on Apple silicon to implement these layered protections: initial network data parsing for each request happens in a dedicated process within its own namespace, shared inference software is recycled with a short time-to-live duration, and attested keys are held in a separate, dedicated confidential VM isolated from external inputs. [...]
> As with PCC on Apple silicon, all binaries will be published for public inspection.

Quote 2026-06-09

> I feel a lot of things changing as working software increasingly comes out on a tap. The Jevon’s paradox kicks in and I feel my own demand for software growing substantially. You can ask for anything - explainers, visualizers, dashboards, bespoke single-use apps (e.g. a full wandb that is hyper-specific just for your project), you can 10X your test suite, auto-optimize code, run giant research projects with custom HTML for the results, anything! “Free your mind” (Matrix ref).

[Andrej Karpathy](https://twitter.com/karpathy/status/2064409694761054332), on Claude Fable 5

TIL: [Setting a custom price for a model in AgentsView](https://til.simonwillison.net/llms/agentsview-custom-model-price)

I’ve been really enjoying [AgentsView](https://agentsview.io/) by Wes McKinney as a tool for exploring my token usage across different coding agents running on my laptop.

Claude Fable 5 came out today and wasn’t yet included in the pricing database AgentsView uses. I used Fable to reverse-engineer AgentsView and figured out this recipe for setting custom prices.

Here’s my Claude Fable 5 usage for today so far, plotted by AgentsView as a treemap across my different local projects:

![Screenshot of a cost analytics dashboard. Cost Attribution - Click to hide from chart - toggle buttons for Project / Model / Agent and Treemap / List. A treemap shows a large red block: prod_datasette_agent $74.06 89.3%, then blue: cloud $3.98 4.8%, teal: datasette $2.81 3.4%, pink: money $1.92 2.3%, and a thin orange sliver. A legend lists 1 prod_datasette_agent $74.06, 2 cloud $3.98, 3 datasette $2.81, 4 money $1.92, 5 simon $0.15. Below left, Top Sessions by Cost: 1 Claude - Review ./datasette-agent and ./datasette-apps - we are going to a... - prod_datasette_agent · 08a1f374-0e77-420f-be2d-af805d67e8aa - 55.9M $74.06; 2 Claude - issues.db is a copy of the Datasette issues database. There are a... - datasette · 8caa2d2d-b91f-43b3-bf3a-4268995b6011 - 826.8k $2.81; 3 Claude - Consult fly-docs and then look at datasette.cloud (which launche... - cloud · bfcacc70-09d7-4b27-aaec-4bb8accd9fec - 924.7k $2.61; 4 Claude - simonwillisonblog.db is a copy of my blog, plus all my software re... - money · 0c0fb9dc-6347-4e1b-9307-3709a7cdf0c8 - 542.9k $1.92; 5 Claude - Look in datasette.cloud and figure out all remaining steps and dec... - cloud · 45963b5f-608a-4caa-ad6b-6ae81e1dbf0d - 455k $1.37; 6 Claude - simon - simon · deeccb5d-9e90-4b1e-bfe6-c2b271e1b1d4 - 26.4k $0.15. Below right, Cache Efficiency with horizontal bars: Cache Reads 57.6M (nearly full green bar), Cache Writes 769.3K, Uncached Input 64.4K, Output 300.9K (all tiny bars), and a green highlighted note: $516.62 saved vs uncached.](https://substackcdn.com/image/fetch/$s_!9U2F!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F159f532d-a9af-45a4-bb34-fbbb3dd24cbf_2244x1336.jpeg)

Release: [llm 0.32a3](https://github.com/simonw/llm/releases/tag/0.32a3)

Almost entirely written by the new Claude Fable 5, see [my write-up for more details](https://simonwillison.net/2026/Jun/9/claude-fable-5/#adding-features-to-datasette-agent-and-llm-using-claude-code).

Link 2026-06-10 [If Claude Fable stops helping you, you’ll never know](https://jonready.com/blog/posts/claude-fable5-is-allowed-to-sabotage-your-app-if-youre-a-competitor.html):

Jonathon Ready highlights one of the more eyebrow-raising details from the [319 page system card](https://www-cdn.anthropic.com/d00db56fa754a1b115b6dd7cb2e3c342ee809620.pdf) for Fable 5 and Mythos 5. Here’s a longer excerpt, highlights mine:

> In light of the ability of recent models to [accelerate their own development](https://www.anthropic.com/institute/recursive-self-improvement), we’ve implemented new interventions that limit Claude’s effectiveness for requests targeting frontier LLM development (for example, on building pretraining pipelines, distributed training infrastructure, or ML accelerator design). Using Claude to develop competing models already violates our [Terms of Service](https://www.anthropic.com/legal/consumer-terms), but enforcing this restriction through our safeguards avoids accelerating the actors most willing to violate these terms.
> Unlike our interventions for cybersecurity, biology and chemistry, and distillation attempts, these safeguards will not be visible to the user. Fable 5 will not fall back to a different model. Instead, the safeguards will limit effectiveness through methods such as prompt modification, steering vectors, or parameter-efficient fine-tuning (PEFT). These interventions will not affect the vast majority of coding work. We estimate they will impact ~0.03% of traffic, concentrated in fewer than 0.1% of organizations.

I believe this is the first time Anthropic have announced these kinds of silent interventions. The justification still feels pretty science-fiction to me - the linked article talks about “recursive self-improvement”. I’m not at all keen on a model that silently corrupts its replies to questions about “ML accelerator design” purely to slow down research that might conflict with Anthropic’s own goals!

Update: Anthropic [walked back this policy](https://simonwillison.net/2026/Jun/11/anthropic-walks-back-policy/) in the face of widespread outrage from the research community.

Quote 2026-06-10

- The lab with the top-ranked model must agree THEY must not use it for working on frontier AI
- But everyone else should have access to it.

> Easy solution to slow down recursive AI self improvement:
> By definition, this means the frontier doesn’t advance.
> It also has the critical benefit of avoiding a dangerous power imbalance.
> Anthropic has chosen the opposite of the safe path: they are allowing themselves, the current top lab, to use their top model for frontier AI research. They’ve said they’ll sabotage others who try.
> This means the AI frontier advances, & power imbalance increases.
> (To be clear, I don’t think we should try to slow down recursive AI self improvement - I think we should open it up and democratize it as much as possible. My point is: if you claim we should slow down, and you have the best model, you should ensure your org can’t use it.)

[Jeremy Howard](https://twitter.com/jeremyphoward/status/2064595816875217362), in a Twitter thread

Link 2026-06-10 [DiffusionGemma](https://blog.google/innovation-and-ai/technology/developers-tools/diffusion-gemma-faster-text-generation/):

Last May Google briefly released an experimental Gemini Diffusion model. I [tried the preview at the time](https://simonwillison.net/2025/May/21/gemini-diffusion/) and recorded it running at 857 tokens/second. It was an exciting model, but Google made no further announcements about it.

That research has returned in the best possible way: as a new open weight (Apache 2 licensed) Gemma model, [google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it).

NVIDIA are currently [hosting the model for free](https://build.nvidia.com/google/diffusiongemma-26b-a4b-it) on their NIM cloud API. I used that API to [generate this pelican](https://tools.simonwillison.net/markdown-svg-renderer#url=https%3A%2F%2Fgist.github.com%2Fsimonw%2Fe5e234a6dc6eef61e209ce1629620042), which took 4.4s (according to `time uv run generate.py`) to return 2,409 tokens - so at least 500 tokens/second.

![Flat minimalist illustration of a white pelican with a large orange beak riding a red bicycle with black wheels, against a pale blue background with a green line representing the ground](https://substackcdn.com/image/fetch/$s_!Uc5u!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F89def1fe-7dac-426e-b55e-d0a07c9b6619_800x800.png)

Release: [datasette-agent 0.2a0](https://github.com/datasette/datasette-agent/releases/tag/0.2a0)

Highlights from the release notes:

- Tools can now ask the user questions mid-execution. Tools that declare a `context` parameter receive a `ToolContext` object, and `await context.ask_user(...)` can ask a yes/no, multiple-choice (`options=[...]`) or free-text (`free_text=True`) question. While a question is unanswered the agent turn suspends: the question renders as a form in the chat UI and persists to the internal database, so suspended conversations survive a server restart. Once answered, the tool re-executes from the top with stored answers replayed, so call `ask_user()` before performing side effects. [#20](https://github.com/datasette/datasette-agent/pull/20)
- New built-in `save_query` tool: the agent can save SQL it has written as a [Datasette stored query](https://docs.datasette.io/en/latest/sql_queries.html#saved-queries). Saving always requires human approval - the agent shows the full SQL plus the proposed name, database and visibility, and nothing is stored until you click Yes. [#20](https://github.com/datasette/datasette-agent/pull/20)

The `ask_user()` feature was enabled by the new LLM alpha I [built yesterday](https://simonwillison.net/2026/Jun/9/claude-fable-5/#adding-features-to-datasette-agent-and-llm-using-claude-code) with the help of Claude Fable 5.

Link 2026-06-11 [Anthropic Walks Back Policy That Could Have ‘Sabotaged’ AI Researchers Using Claude](https://www.wired.com/story/anthropic-responds-to-backlash-on-claudes-secret-sabotage-on-ai-research/):

Big scoop for Maxwell Zeff at Wired:

> “We’re changing Fable 5’s safeguards for frontier LLM development to make them visible.” Anthropic said in a statement to WIRED. “We made the wrong tradeoff and we apologize for not getting the balance right.”

There’s been a huge outcry about Anthropic’s policy, [tucked away in their system card](https://simonwillison.net/2026/Jun/10/if-claude-fable-stops-helping-you/), that Claude Fable/Mythos would identify “requests targeting frontier LLM development” and “limit effectiveness” without notifying the user.

It’s good news that they’re dropping the invisible aspect of this. It would be a whole lot better of they dropped this category of refusals entirely.

Update: More details from [@ClaudeDevs on Twitter](https://twitter.com/claudedevs/status/2064949876463645026):

> We’re rolling out changes to make Fable 5’s safeguards for frontier LLM development visible.
> Starting this week, flagged requests will visibly fall back to Opus 4.8—the same as our safeguards for cyber and bio. You will see this every time it happens. On the API, any flagged requests will return a reason for their refusal (coming to server-side fallback in the next few days).
> We wanted to deploy Fable 5 to our users quickly and safely. Visible safeguards can be probed, so they have to be robust, which takes time to get right. Invisible safeguards can be targeted more narrowly, allowing us to ship quickly with very few false positives. We went with invisible safeguards for this reason—and that was the wrong tradeoff. You should have visibility into the safeguards we have in place, and why. We’re sorry for not getting the balance right.

Release: [asyncinject 0.7](https://github.com/simonw/asyncinject/releases/tag/0.7)

I built this utility library to support an `asyncio` dependency injection pattern a few years ago. I was using it with Datasette and Claude Fable 5 spotted some bugs in the dependency which it then fixed for me. It’s a very proactive model!

Release: [datasette 1.0a33](https://github.com/simonw/datasette/releases/tag/1.0a33)

This alpha is a significant step on the road to a stable 1.0, finally extending the `?_extra=` pattern I introduced [in Datasette 1.0a3](https://docs.datasette.io/en/1.0a3/changelog.html#a3-2023-08-09) to cover queries and rows in addition to tables. That pattern is also [now documented](https://docs.datasette.io/en/latest/json_api.html#expanding-json-responses)!

I wrote a whole lot more about the new release on the Datasette project blog: [Datasette 1.0a33 with JSON extras in the API](http://datasette.io/blog/2026/api-extras/).

Because API explorer tools are almost free to build now I had Claude Fable 5 in Claude Code (for [the plan](https://gist.github.com/simonw/d8bf1a8f36e28fbd595cede946e0ab6d)) and GPT-5.5 xhigh in Codex Desktop (for [the implementation](https://gist.github.com/simonw/12d5e09797072a6807d7b9cfcc8ff6b7)) build me this [custom extras API explorer](https://tools.simonwillison.net/datasette-extras-explorer) to help demonstrate the feature:

![Screenshot of a web application titled "Datasette extras explorer". A URL input field contains https://latest.datasette.io/fixtures/facetable.json with a teal Explore button next to it. Below, a left panel labeled EXTRAS (30) lists checkboxes: all_columns - All columns in the table, regardless of _col/_nocol filtering; column_types - Column type assignments for this table; columns (checked) - Column names returned by this query; count - Total count of rows matching these filters; count_sql - SQL query used to calculate the total count; custom_table_templates - Custom template names considered for this table; database - Database name; database_color - Color assigned to the database. A right panel labeled RESPONSE shows GET /fixtures/fac… with Copy JSON and Copy URL buttons, then a dark JSON viewer showing 200 - 9.9 KB - 114ms and JSON: "ok": true, "next": null, "columns": (highlighted array) "pk", "created", "planet_int", "on_earth", "state", "_city_id", "_neighborhood", "tags", "complex_array", "distinct_some_null", "n", "rows": list of objects.](https://substackcdn.com/image/fetch/$s_!7Ysw!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F02989e68-90fa-4a95-b104-b66d60d9330b_2048x1390.png)

Quote 2026-06-12

> Jenny owns a crematorium. John’s propane company gives her a $20 billion investment in return for 5 percent of her operation. Jenny throws $10 billion into the incinerator, then pays John $10 billion to buy propane to burn that money to ashes. John reports that his AI investments have generated $10 billion in revenue this quarter and that he owns 5 percent of a $100 billion business. A reporter from Forbes is assigned to profile John and Jenny, and over the course of his research, he becomes embroiled in a passionate but confusing three-way love affair with them, which eventually turns into a polyamorous common-law marriage. His profile is glowing, but light on financial details.

[Andrew Singleton](https://www.mcsweeneys.net/articles/ai-economics-for-dummies), AI Economics for Dummies

Link 2026-06-12 [OpenAI WebRTC Audio Session, now with document context](https://tools.simonwillison.net/openai-webrtc):

I built the first version of this tool [in December 2024](https://simonwillison.net/2024/Dec/17/openai-webrtc/) to try out the then-new OpenAI WebRTC API for interacting with their realtime audio models.

Last month OpenAI [introduced a brand new model](https://openai.com/index/advancing-voice-intelligence-with-new-models-in-the-api/) to that API called [GPT‑Realtime‑2](https://developers.openai.com/api/docs/models/gpt-realtime-2), which they promoted as “our first voice model with GPT‑5‑class reasoning” - with a Sep 30, 2024 knowledge cut-off.

I’ve been waiting for that model to show up in the ChatGPT iPhone app but it still hasn’t, so I revisited my old playground.

You can now pick the better model, and you can also paste in a big chunk of document context so you can have as audio conversation in your browser about whatever information you think would be useful to explore in a conversational way.

![Screenshot of a web interface titled "OpenAI WebRTC Audio Session" with a gray status dot. Form fields: "OpenAI API Token" showing a masked password of dots, "Voice" dropdown set to "Coral", "Model" dropdown set to "gpt-realtime-2". A collapsible section labeled "▼ Document context (optional — paste text to talk about)" with bold instruction "Paste a document here before starting the session and the model will be able to discuss it with you" above a textarea containing a pasted Markdown document about whether DuckDB can run untrusted SQL as safely as Datasette runs SQLite. Below are a blue "Start Session" button and a gray disabled "Mute Mic" button, then a green success message "Session established successfully!" At the bottom, a dark panel headed "Last transcript" reads: "DuckDB can be made about as safe as SQLite for running untrusted SELECT queries, but only if you lock it down properly. Using read only true by itself is not enough, because SQL can still" (text cut off).](https://substackcdn.com/image/fetch/$s_!0scw!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb2362b40-3661-4f9f-a0ad-b111946c1a02_1438x1960.jpeg)

If you find this newsletter useful, please consider [sponsoring me via GitHub](https://github.com/sponsors/simonw). $10/month and higher sponsors get a monthly newsletter with my summary of the most important trends of the past 30 days - here are previews from [February](https://github.com/simonw/monthly-newsletter-archive/blob/main/2026-02-february.md) and [March](https://github.com/simonw/monthly-newsletter-archive/blob/main/2026-03-march.md) and [April](https://github.com/simonw/monthly-newsletter-archive/blob/main/2026-04-april.md).
