---
article_id: 2026-07-03-ai-company-open-source-agent-org-chart
source_path: https://x.com/akshay_pachaar/status/2073050056299835736
source_kind: xcom-post
captured: 2026-07-04T19:04:10+08:00
status: imported
language:
title: "How to Build Your Own AI Company (0 employees, 100% open-source)"
author: "Akshay @akshay_pachaar"
published: 2026-07-03
topic_hint: []
collection_hint: []
why_it_matters:
---
# How to Build Your Own AI Company (0 employees, 100% open-source)

Source: https://x.com/akshay_pachaar/status/2073050056299835736
Author: Akshay @akshay_pachaar
Published: 2026-07-03
Captured at: 2026-07-04T19:04:10+08:00

How to Build Your Own AI Company (0 employees, 100% open-source)

Dario Amodei said a one-person billion-dollar company has a 70-80% chance of showing up by 2026. He said it on stage at Anthropic’s developer conference last year.

Matthew Gallagher proved it by starting Medvi, an AI-run telehealth company, with $20,000 and no employees. It made $401 million in revenue in its first year.

Gallagher's stack was AI agents talking to each other. When two couldn't talk, he built more agents to handle the coordination. He tested the prompts himself and stepped in when something broke.

Alook ( [GitHub Repo](https://github.com/alookai/alook)

) is an open-source, self-hosted platform that turns your coding agents into a real org chart.

[Alook GitHub Repo →](https://github.com/alookai/alook)

![Image](https://pbs.twimg.com/media/HMTpmgnbgAAxgaF?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073038576296886272)

The way it works is that you create an agent, assign it a role, and give it a real email inbox.

Agents email each other and update you. They run as actual Claude Code or OpenCode sessions on your machine, with full access to your tools.

An org chart gives every agent a defined role and a reporting line. They coordinate with each other without you relaying a single message or fixing the wiring yourself.

Let’s set up Alook from scratch, build a four-agent org chart, and watch what happens once a real job gets handed to it.

# Setup

Alook runs as a daemon on your own machine, and this one command connects it:

```bash
npx @alook/app onboard
```

It detects whatever coding agent runtime is already installed, Claude Code or OpenCode, and deploys the agent company.

This opens a local dashboard at http://localhost:15210.

From there, you start from a blank org chart or one of Alook’s pre-built templates, whichever’s closest to what you’re building.

![Image](https://pbs.twimg.com/media/HMTpwJWaQAAHDup?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073038741850177536)

Each agent on the chart is a real Claude Code or OpenCode session running on your machine, with full access to the same tools you use, and a real [@alook](https://x.com/@alook)

.ai inbox.

The inbox is the coordination layer. Agents email each other, the same way a team would, instead of passing data through a trigger you wired by hand.

# Building the company

Competitive intelligence usually means someone checking a pricing page, copying numbers into a spreadsheet, and doing it again tomorrow.

We’re going to replace that with four agents who build a price tracker, run it on a schedule, and email you the moment something changes.

First, we create the agents one by one, assigning them distinct roles and claiming their real [@alook](https://x.com/@alook)

.ai inboxes:

![Image](https://pbs.twimg.com/media/HMTp2uBaMAA7R8X?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073038854773420032)

- Atlas (CEO) is the single point of contact for the human. It delegates tasks to Mara.
- Mara (PM) turns Atlas's briefs into specs and routes them to Theo or Ren. She's the sole router on the chart.
- Theo (engineer) builds and maintains the scrapers for competitive intelligence.
- Ren (Ops and Customer-facing) notifies the human when a tracked change is detected. Once the agents are live, we wire the reporting hierarchy: Atlas to Mara, and Mara to Theo and Ren.

![Image](https://pbs.twimg.com/media/HMTqGfBa8AAWYIX?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073039125624844288)

Theo and Ren never talk to each other, or to Atlas directly. They only go through Mara.

This setup avoids building a chaotic AI group chat where every agent talks over each other and loses context.

Theo’s job touches the competitor’s site tracks, so he needs a way to scrape it reliably and schedule.

So we have given it access to the [Bright Data CLI](https://github.com/brightdata/cli)

, which lets it scrape any website, provision custom scrapers if needed…all while avoiding IP blocks and CAPTCHAs that hit any agent scraping at real scale.

To build a custom scraper over any website, you can describe the page in plain English, and it builds the scraper that returns structured data:

![圖片](https://pbs.twimg.com/amplify_video_thumb/2073039277366423552/img/C_hSV9AEdt9wjXEi.jpg)

Now let’s see how our AI company handles the real task.

# Running the company

As mentioned above, we don't need to manage every agent ourselves. Instead, we just talk to Atlas, the CEO, and let the org chart handle the rest.

We ask him to track pricing on [railway.app/pricing](https://railway.app/pricing)

.

![Image](https://pbs.twimg.com/media/HMTqaC2bMAASBPa?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073039461659914240)

Atlas replies in the chat, and behind that reply, he's briefing Mara over email, and the thread shows up in the same window:

![Image](https://pbs.twimg.com/media/HMTqcWAawAAevN3?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073039501161840640)

Mara turns the brief into a spec and hands it to Theo.

The spec covers a scraper for the page, timestamped snapshots, change detection, a daily run, and a report we can actually read.

![Image](https://pbs.twimg.com/media/HMTqe3aaEAA8OOC?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073039544488955904)

Theo acknowledges the spec over email, the same way Mara and Atlas did, then builds it using the [Bright Data CLI](https://github.com/brightdata/cli)

and reports back once it's running.

![Image](https://pbs.twimg.com/media/HMTqjP-bkAAFGOB?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073039619801976832)

This is the scraper Theo just built, sitting in Bright Data's dashboard:

![Image](https://pbs.twimg.com/media/HMTqmxibEAAyU5H?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073039680350916608)

It's a real custom scraper that the agent provisioned itself by understanding the specified website, not a one-off CLI call that disappears after running. You can trigger it manually from this same screen, or call it straight using the API:

![Image](https://pbs.twimg.com/media/HMTqrf2boAEV-IX?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073039761502347265)

Mara relays the build-up to Atlas, and Atlas informs us in the same chat:

![Image](https://pbs.twimg.com/media/HMTquAUbEAAL3VH?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073039804577812480)

# The company runs without you

Once Theo confirms the build is live, the job isn’t done. The schedule still needs to run, and someone still needs to watch what it finds.

The agent adds the scraper to the company calendar as a recurring 9am task, on its own.

![Image](https://pbs.twimg.com/media/HMTqyOdaMAAXRvx?format=jpg&name=medium)

[X.com media](https://x.com/akshay_pachaar/article/2073050056299835736/media/2073039877093076992)

This is Ren’s job. He watches the tracker’s output, and the moment the price on the page actually changes, he sends a note.

The whole loop runs unattended.

We handed Atlas one brief, and the org provisioned a scraper, scheduled it, and kept someone watching the output, with no further input from us.

# Try it yourself

Every agent in this walkthrough ran as Claude Code, but Codex and OpenCode work the same way, as Alook lets you bring your own agent and gives whichever one you pick a role, an inbox, and a runtime that stays on.

Every completed task builds context for the next one, so the agents aren’t relearning the company from scratch on every run.

Every email between them gets logged the same way, so you can read back exactly how a decision got made.

[Here’s the Alook’s Github repo →](https://github.com/alookai/alook)

[And here’s the Bright Data CLI→](https://github.com/brightdata/cli)

(don’t forget to star them 🌟 )

Cheers! :)

[Upgrade to Premium](https://x.com/i/premium_sign_up)

[10:23 PM · Jul 3, 2026](https://x.com/akshay_pachaar/status/2073050056299835736)

[View quotes](https://x.com/akshay_pachaar/status/2073050056299835736/quotes)
