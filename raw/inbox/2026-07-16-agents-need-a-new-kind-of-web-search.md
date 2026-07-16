# Agents Need a New Kind of Web Search

Source: https://x.com/akshay_pachaar/status/2077753829526056985
Canonical status: https://x.com/akshay_pachaar/status/2077753829526056985
Author: Akshay @akshay_pachaar
Status ID: 2077753829526056985
Published: 2026-07-16
Captured at: 2026-07-17T07:37:13+08:00
Extraction: myAgentTools/xcom-article-import
Extraction file: `/Users/lee/ws/myKBs/myAgentTools/xcom-article-import/runs/xcom-2077753829526056985.md`
Import mode: X.com browser extraction
Content status: complete

Note: This article is a cleaned KB inbox article based on an X.com browser extraction. Source claims are preserved as source framing unless independently verified.

## 核心觀點

Agents Need a New Kind of Web Search

Andrej Karpathy once said LLMs are a bit like a coworker with anterograde amnesia. That’s the condition where you keep your old memories but can’t form new ones.

![Image](https://pbs.twimg.com/media/HNWcZ36aIAAN5lr?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2077753829526056985/media/2077738771420946432)

An LLM lives with that condition in two ways. It doesn’t remember you across conversations, and it never learns anything that happened after its training ended.

Memory features exist to patch the first gap. This piece is about the second one, because agents mostly get hired to deal with the present.

Markets move, people change roles, prices update, news breaks. Web search is how the model sees any of it, and how well it works ends up deciding how useful the whole agent is.

So you bolt a search tool onto your agent and assume it can now read the web. Then you check the first few traces, and the result is disappointing.

Nearly all the tokens you paid for went into raw page text the agent had to dig through. Only a thin slice went into answering your question.

The reason is what a search call actually returns. A typical search API hands back links and thirty-word snippets, nothing more.

So the agent isn’t reading the web, it’s reading a table of contents. Fetching the actual pages becomes its job, which means pulling the HTML, stripping the markup, and digging out the usable text before any real work starts.

On a single query you barely notice the overhead. In a task that takes several searches, like a research run or a briefing pipeline, you pay it again on every single one.

![Image](https://pbs.twimg.com/media/HNWccyeaUAEoDz7?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2077753829526056985/media/2077738821500948481)

The problem isn’t that agents search badly. It’s that each search call returns pointers to content instead of the content itself, and the agent pays to close that gap on every call.

We ran the same question through three retrieval setups and counted tokens. The most expensive setup cost roughly 4x the cheapest retrieval option.

This piece walks through those numbers and shows what a search response should look like when an agent is the one reading it. It also covers a class of questions that only full documents can answer.

Let’s start with where the cost actually comes from.

Every loop iteration pays the retrieval tax

That repeated fetch-and-clean work has a name. Call it the retrieval tax, the tokens an agent burns preparing content before it can reason about your problem.

One looping agent is enough to feel it. A research agent searches, reads what came back, decides what to look up next, and searches again, and every pass pays the tax on top of the last one.

![Image](https://pbs.twimg.com/media/HNWchIfaoAAPTpi?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2077753829526056985/media/2077738896130220032)

Here’s what that costs on a single question. We picked “What was Y2K?” on purpose, because the model already knows the answer from training.

We answered it three ways, straight from memory, through a web search loop, and through an owned index (a search service that crawls and cleans pages ahead of time and stores its own processed copy of the web), counting the total tokens billed each time.

Picking a question the model already knows is what keeps the experiment clean. The thinking cost is identical in all three runs, so any tokens above it come purely from the retrieval.

- From memory, the whole thing took about 600 tokens. That’s the baseline, the cost of just answering with zero retrieval.
- An owned index is a search service that has already crawled and cleaned the pages, so one call returns the full document. Going through one took roughly 6,900 tokens.
- A single web search hop cost about 3,750 tokens. But snippets are often too thin to answer from, so the agent refetches and refines, and three hops climbed to roughly 28,700, more than 4x the owned index. ![Image](https://pbs.twimg.com/media/HNWcnQAa4AAzNWr?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2077753829526056985/media/2077739001226911744)

The gap between the loop and the index is the tax made visible. Every hop re-billed the entire growing context window, so by the third pass the agent was mostly paying to carry pages it had already read.

The owned index skipped all of that. The full document was already there when the query arrived.

What makes that possible is what comes back from the search call itself, so let’s look at that next.

# Good retrieval returns documents, not directions

The fix isn’t a smarter agent or a better prompt. The fix is what comes back from the search call.

- A SERP, the plain list of results a search API returns, hands you URLs and asks the agent to go read the web itself.
- A scraper-first tool gets you closer by returning raw HTML or markdown, but the agent still has to clean it before it can use anything.
- An owned index does all of that work before the query ever arrives, so what comes back is already readable. ![圖片](https://pbs.twimg.com/tweet_video_thumb/HNWdl-DbIAAib9V.jpg)

GIF

Here’s the same lookup across all three. We’ll search for Christoph Molnar, the author of the Interpretable Machine Learning book.

SERP

```plaintext
# query
results = search("Christoph Molnar interpretable ML")

# response
[
 {"title": "Interpretable Machine Learning", "url": "christophmolnar.com/books/...", "snippet": "A guide for making black box models explainable..."},
 {"title": "Christoph Molnar - Google Scholar", "url": "scholar.google.com/...", "snippet": "Cited by 12,847..."},
 # 5 more results across different domains
]
```

The agent got a list of tabs, not an answer.

Neural search

```plaintext
# query
results = neural_search("Christoph Molnar", type="person")

# response
[
 {"highlight": "Christoph Molnar is a statistician and machine learning interpretability researcher..."},
 {"highlight": "Author of Interpretable Machine Learning, an open access book with 400k+ readers..."},
 # one stray paragraph about a different researcher
]
```

It found the right person, but as highlight fragments. Getting the full record still needs another call.

[Owned index](https://seltz.ai/)

```plaintext
# query
result = client.search("Christoph Molnar", scope="people")

# response
{
 "name": "Christoph Molnar",
 "roles": [
 {"title": "Research Scientist", "org": "Mindful Modeler", "start": "2021"},
 {"title": "Author", "work": "Interpretable Machine Learning", "editions": 3}
 ],
 "education": [{"degree": "PhD Statistics", "institution": "LMU Munich"}],
 "websites": ["christophmolnar.com", "github.com/christophM"],
 "languages": ["German", "English"]
}
```

One call returns the complete record, and the agent goes straight to reasoning.

[Seltz](https://seltz.ai/)

is a web index built exactly for this. It crawls the web ahead of time, processes every page into a structured document, and returns finished content through a single API call.

![Image](https://pbs.twimg.com/media/HNWeLBwaoAANzNd?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2077753829526056985/media/2077740715388608512)

It comes with three scopes, and each one returns a different kind of finished document depending on what your agent needs.

- The people scope returns full structured profiles, with every role and its dates, education, websites, and the organizations someone has worked at.
- The news scope returns complete article text, date-windowed, so you can pull only what was published in a specific period.
- The wiki scope returns clean Wikipedia documents, useful for building context around companies, industries, or topics before going deeper. One caveat is worth knowing before you build on the people scope. It works best at the director and regional-leader layer.

For the most senior executives, start with open web search and use Seltz to enrich everyone below them.

# Some answers only exist across records

Full documents unlock something that goes beyond cutting the retrieval tax.

Some questions don’t live in any single search result. The answer only exists once you read across multiple records and find where they intersect.

Neither a SERP nor a neural search tool can do this on the first pass. They don’t hold enough of each record to join them, so the work lands back on the agent.

![Image](https://pbs.twimg.com/media/HNWeYINaQAAD3tI?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2077753829526056985/media/2077740940459130880)

Consider a question a GTM team actually runs. You want every target account that hired someone into a data or AI leadership role in the last quarter.

Answering it needs two things together. Full role histories to find who started a new position and when, plus recent news to confirm the timing and surface the trigger event.

You query the people scope to find who moved into a relevant role recently, then cross-reference the news scope for the trigger event.

What comes out is a ranked list of warm accounts with enough context to write a relevant first outreach line for each one.

That answer doesn’t exist anywhere on the web as a page. It only exists once you join the records, and the join only works when you hold the full records to begin with.

# [Chain discovery and depth, and every iteration gets cheaper](https://seltz.ai/)

[Seltz](https://seltz.ai/)

isn’t a replacement for open web search. It’s the right tool for a specific class of questions.

Open web search handles discovery well. Finding who currently holds a title, confirming something launched last week, reading a page that went live this morning.

Once you know what you’re looking for, Seltz returns the complete record in one hop rather than a headline and a link.

Many pipelines use the same search tool for every query regardless of what the question needs. Discovery queries go through the same call as deep-dive lookups, and the loop pays the retrieval tax on both.

Chain the two instead and each loop iteration gets the right retrieval shape for what it’s actually trying to do.

That’s the core argument here. The cost of an agent loop is set less by the model and more by what each search call hands back, and returning finished documents is how you stop paying for the same pages twice.

If you’re building loops that hit these query shapes, you should give Seltz a try.

[Get started here →](https://seltz.ai/)

Stay tune as I dig more into efficient web search for Agents and share what I learn along the way.

Thanks for reading and Seltz for partnering with me on this article.

Cheers! :)

[Upgrade to Premium](https://x.com/i/premium_sign_up)

[9:54 PM · Jul 16, 2026](https://x.com/akshay_pachaar/status/2077753829526056985)

## Source Notes

- Source URL: https://x.com/akshay_pachaar/status/2077753829526056985
- Author: Akshay @akshay_pachaar
- Status ID: 2077753829526056985
- Published: 2026-07-16
- Captured at: 2026-07-17T07:37:13+08:00
- Extraction file: `/Users/lee/ws/myKBs/myAgentTools/xcom-article-import/runs/xcom-2077753829526056985.md`
- Content status: complete
