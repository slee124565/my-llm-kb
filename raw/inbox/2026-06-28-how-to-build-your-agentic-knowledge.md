# How to Build Your Agentic Knowledge Base (after 16 months of running my own)

Source: https://bitsofchris.com/p/how-to-build-your-agentic-knowledge
Author: Chris Lettieri
Publisher: Bits of Chris
Published: 2026-06-28
Captured: 2026-09-23
Tags: unknown
Subtitle: Get started, let the structure emerge.

Markdown Content:

I’m an Obsidian power user. 16 months ago I built a system of agents (back when we just called it prompting) to help me extract value from my notes.

It was overly complex but it worked.

Since then this field of agentic knowledge bases has grown up.

Here’s the TLDR I wish I’d had when I started building my own system almost two years ago. I’ll compare several other systems and show you the simplest version you can stand up this week, how to use it, and the one decision that matters most.

![](https://substackcdn.com/image/fetch/$s_!unaY!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdf43a12e-0768-4e59-a448-58ef9bf07eb1_1086x1448.png)

## Start simple. Don’t design a schema or over-engineer.

The most reliable way to never ship a knowledge base is to begin by designing the perfect one.

I made this mistake.

I tried to map the taxonomy, define the tags, and build a complete ontology before I had enough material to know what the structure should be. Then I added more parts: semantic clustering, entity extraction, knowledge graphs, and other useful ideas that I did not yet have a clear use for.

All of that was premature.

When you are starting, you do not know the shape of your knowledge yet. Any structure you design up front is mostly a guess, and you will have to revise it once real notes begin moving through the system.

So begin with one folder, one agent, and one maintenance loop:

- A folder of plain markdown files that remains the source of truth.
- An agent that knows how to capture information and retrieve it later.
- A janitor that regularly organizes new notes and maintains a lightweight map.

Inside the folder, everything new lands in an inbox. The janitor processes that inbox, connects related notes, and moves the ones it understands into the notes folder. As recurring themes become visible, it records them in the map.

You are not designing the taxonomy. You are giving it room to emerge.

That is close to the approach behind [Karpathy’s LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). Its simplicity initially frustrated me because I had spent so much time building something more elaborate. But the simplicity is the point: this version is small enough to start using today.

Over time, the knowledge base will begin to stratify and cluster.

A few broad areas will appear, followed by more specific themes within them. In my Obsidian vault, that eventually became five large areas: research, OpenAugi, content, personal growth, and personal systems. Loosely based on [PARA](https://fortelabs.com/blog/para/) from Tiago Forte.

I did not devise that structure in advance. It emerged from several years of capture.

Start capturing first. Let the patterns earn their place.

### Try this to get started

Just hand this to an agent and tell it you’d like to start a knowledge base with this rough structure.

```text
# The Knowledge Base

1. The folder — the whole "database"

knowledge-base/
├── AGENTS.md     # how the agent behaves
├── JANITOR.md    # the scheduled cleanup pass
├── MAP.md        # the index the janitor maintains (starts almost empty)
├── inbox/        # everything you capture lands here, unsorted
└── notes/        # everything the janitor has filed

2. AGENTS.md — the agent's brain

# Agent instructions

You work inside a knowledge base of plain markdown files.
The files are the source of truth. Never delete; only add or refine.

## When I capture
- New thoughts go in `inbox/` as a dated markdown file. Don't sort yet.

## When I ask a question
1. Read `MAP.md` first to see where things live.
2. Open only the notes the map points you to. Don't read everything.
3. Answer from my notes. Quote the file you used.

## Conventions
- One idea per note. Link related notes with [[wikilinks]].
- Tags are lowercase (#like-this). Use existing tags before inventing new ones.
- Do NOT design a taxonomy up front. Let structure emerge from what's captured.

3. JANITOR.md — the scheduled pass

# Janitor pass

Run on a schedule (or when `inbox/` gets full). You are tidying, not re

## Each run
1. Read everything in `inbox/`. For each note:
   - Apply existing tags from `MAP.md`. Reuse before inventing.
   - Add [[wikilinks]] to clearly related notes.
   - If it's clear where it belongs, move it to `notes/`.
2. Fix obviously broken links and duplicate tags.
3. Update `MAP.md`: add any new tag or theme that has earned its place
   (3+ notes), with a one-line description and example links.

## Rules
- Never delete a note or rewrite my words.
- If you're unsure where something goes or spot a contradiction,
  leave it in `inbox/` and add a line to `inbox/_review.md` for me.

4. MAP.md — the index (this is the magic: it starts empty)

# Map

The janitor maintains this. It starts almost empty and fills in as I capture.
This is the index the agent reads first — not a taxonomy I designed up front.

## Themes
<!-- A theme gets a line here once 3+ notes share it. -->
<!-- e.g. - #context-engineering — how I think about data for agents → [[note]], [[note]] -->

## Tags in use
<!-- The janitor lists active tags here so it reuses them instead of in

## Open questions
<!-- Recurring things I haven't resolved. -->
```

## How it works

Strip the system down and it is one small loop:

You capture → the janitor maintains → the agent retrieves.

### 1. You capture

A new thought, source, observation, or unfinished idea goes into `inbox/` as a dated markdown file.

Nothing has to be tagged or categorized when it enters the system. The goal at this stage is simply to preserve it without interrupting your work to decide where it belongs.

### 2. The janitor maintains

On a schedule—or whenever the inbox begins to fill—the janitor reads the new notes.

It reuses existing tags, adds links to clearly related notes, and moves a note into `notes/` when its place is clear. When it finds something ambiguous, contradictory, or difficult to classify, it leaves the original note alone and adds it to the review file.

The janitor also maintains `MAP.md`. A higher level theme/area/concept is added to the map only after it has appeared often enough to be useful. That is how the structure grows from the material instead of being imposed on it beforehand.

The janitor does not replace your thinking. It keeps the system navigable.

### 3. The agent retrieves

When you ask a question, the agent reads `MAP.md` first. Think of this map as an [index for agentic retrieval](https://bitsofchris.com/p/context-engineering-is-index-design).

The map gives it a lightweight view of the themes, tags, and relevant notes already in the knowledge base. Instead of reading every file or dumping the entire folder into its context, the agent uses the map to decide where to look and opens only the notes that appear relevant.

It then answers from those notes and tells you which files it used.

The markdown files remain the source of truth throughout this process. `MAP.md` is a routing layer, not a replacement for the underlying material. Any search index, embedding store, or database you add later should also be treated as a derived layer that can be rebuilt from the files.

At a small scale, you do not need those additional systems. A maintained map and a clear set of agent instructions are enough to get started.

## How to use it

Day to day, the system asks you to develop three habits.

### Capture without sorting

Put new material into `inbox/` and continue with your work.

Do not stop to create a new category, invent a tag, or decide where the note belongs. The inbox exists to remove that decision from the moment of capture.

You might tell the agent:

> Capture this thought in the knowledge base. (My MCP is a two-way street, letting the agent retrieve but also allow us to capture artifacts from the work we do).

The agent should save it as a dated markdown file in `inbox/` without trying to redesign the system around it.

Today we capture by typing or talking, but one day we will all be wearing augmented reality glasses that capture every second of our day. If we know how to make sense of that data we can each have a personal JARVIS.

### Ask questions through the map

When you want to use what you have collected, ask the agent a normal question:

> What have I written about context engineering?
> Which of my notes discuss maintenance loops?
> What unresolved questions keep appearing in my research?

The agent reads `MAP.md`, follows the relevant links, and answers from the source notes. It should not search by opening everything, and it should not present generated summaries as though they were your original material.

This distinction is important:

- `AGENTS.md` tells the agent how to behave.
- `MAP.md` tells the agent where to look.

Keeping those jobs separate makes both files easier to understand and maintain.

### Run the janitor and review the exceptions

Run the janitor on a regular schedule or whenever `inbox/` becomes difficult to scan.

Most notes should move through the system without your involvement. Your attention is reserved for the exceptions collected in `inbox/_review.md`: unclear relationships, contradictions, or notes whose destination is genuinely uncertain.

That gives you a simple operating rhythm:

1. Capture freely.
2. Run the janitor.
3. Review only what requires judgment.
4. Ask the agent questions using the map.

You can add more sophisticated retrieval later, once the folder has grown enough to reveal a specific limitation. Until then, the best thing you can do is keep the loop running.

## The agentic knowledge bases of today look similar

There’s [Karpathy’s LLM wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), [Garry Tan’s gbrain](https://github.com/garrytan/gbrain), [knowledge-agent](https://github.com/j-wang/knowledge-agent-template) templates, my own [OpenAugi](https://github.com/bitsofchris/openaugi), and I’m sure several hundred more.

Different names, but strip the branding off and every one of them is the same eight parts:

1. Raw source files — markdown you own; the agent reads, never overwrites.
2. A knowledge unit — the chunk it reasons over (a page, a block, a concept).
3. A typed graph — real links between units, not just similarity.
4. A routing index — a cheap map that says where to look before spending tokens. This is the piece that makes the rest scale.
5. A config file — `AGENTS.md`, a skill file, schema packs. Turns a generic agent into a librarian who knows your shelves.
6. Hybrid retrieval — keyword + vector + graph together. Time as another attribute to filter by.
7. A maintenance loop — the janitor, grown up: dedupe, fix links, consolidate.
8. An agent interface — almost always MCP or CLI for the agent to use.

![](https://substackcdn.com/image/fetch/$s_!6yJy!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fec12170e-dec8-404f-b65c-a2d8aba605cb_1491x1055.png)

The TLDR of these systems:

1. Keep raw markdown as truth
2. Split it into linked units
3. Build a cheap routing index
4. Expose hybrid retrieval to an agent via MCP, governed by a config file
5. Maintain it consistently
6. Profit

## What you grow into as a power user

The comparison above can make these systems look more different than they are. Most of them begin with the same foundation: files, an agent, and a maintenance loop.

![](https://substackcdn.com/image/fetch/$s_!XgXu!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F07f01238-2e81-4eea-a17a-0edfedc092d9_3280x2120.png)

The architecture on the right side of the diagram is what you add when that foundation starts to break. When retrieval is getting noisy or the agent is pulling too much extra context, you can graduate to the full system above.

You do not replace the flat folder. Your markdown files remain the source of truth. Instead, you bolt on a derived index that helps the agent navigate them more efficiently.

Instead of stuffing a large pile of notes into the agent’s context and asking it to make sense of everything at once, you give it a cheap map of the knowledge base. The agent uses that map to decide where to look, then drills into the original files only where it matters.

The map grows in layers.

First, the system splits documents into smaller knowledge units: sections or blocks that can be retrieved and reasoned over independently.

Then it records explicit relationships between them in a typed graph. A connection can mean more than “these two things are similar.” One block might link to another, be split from it, support it, contradict it, or share a tag with it.

On top of that sits a routing index: lightweight summaries that tell the agent, “Look here first.” The index narrows the search space before the system spends time loading full notes.

Finally, retrieval becomes hybrid. The agent can combine semantic similarity, keyword search, graph relationships, and other signals such as time. Rather than depending on one search method, it can choose and combine the abilities that fit the question.

Those layers are exposed to the agent through an interface such as MCP. The agent does not need the entire index in its prompt. It receives tools for exploring the map, assessing possible routes, drilling into the relevant material, and retrieving the underlying source.

This is the idea behind my [Contextgraph](https://bitsofchris.com/p/context-engineering-is-index-design) data model, with [OpenAugi](https://github.com/bitsofchris/openaugi) as its working implementation. The files are still canonical; the knowledge units, graph, routing index, and retrieval infrastructure are derived from them and can be rebuilt.

The janitor evolves too. What began as a small cleanup pass becomes an ingestion and maintenance pipeline: splitting new material, updating links, refreshing summaries, consolidating duplicates, and keeping the index synchronized with the files.

[gbrain](https://github.com/garrytan/gbrain) is a useful reference for this more developed stage. It keeps markdown as the source of truth, builds a typed graph around it, and uses a nightly “dream cycle” to consolidate and de-duplicate what the system has learned.

But none of this belongs in your first version.

Start with the three blue pieces: the folder, the agent, and the janitor. Add knowledge units when whole files become too coarse. Add a graph when relationships begin to matter. Add routing and hybrid retrieval when search becomes noisy.

Each new layer should solve a problem the simpler system has actually created.

You do not architect the final machine on day one. You grow into it.

## Keep yourself in the loop

One warning as you automate more of the system: don’t confuse a better knowledge base with better thinking.

The agent can capture, clean, link, retrieve, and summarize. But if it does all the reading and synthesis for you, you may end up with a useful reference system without developing your own understanding.

Keep your notes—especially the messy, unfinished ones—as the source of truth. Let the system route you back to them, surface connections, and help you explore what you have already thought.

Then synthesize when you need an output. Treat that synthesis as a temporary view or a draft for you to respond to, not as a replacement for the material that produced it.

That is the balance I’m moving toward: route by default, synthesize on demand, and keep a human review step wherever meaning is being made.

The AI’s job is not to remove you from the loop. It is to help you see and develop your own thinking.

I wrote more about why this matters in [An LLM Wiki Won’t Compound Your Knowledge](https://bitsofchris.com/p/an-llm-wiki-wont-compound-your-knowledge).

## Where to start

If you take one thing from this: don’t start designing your knowledge base, just start using one.

This week point an agent at a folder of docs you already have, take the prompt above and let an agent get you started. Make it more complex only when you need to.

That’s the whole map. The systems people are building at the frontier are this same simple start that kept growing.

So go get started.

If your an Obsidian power user - I’d love to hear how you are extracting value from your notes using agents. What’s been the most useful way to use your vault?
