# The SLM-OCR Course Starts Now: The $10,000 OCR Pipeline We're Giving Away Free

Source: https://theneuralmaze.substack.com/p/the-slm-ocr-course-starts-now-the
Author: Miguel Otero Pedrido, Antonio Zarauz Moreno
Publisher: The Neural Maze
Published: 2026-07-22
Captured: 2026-07-22
Tags: unknown
Subtitle: A 6-week hands-on journey to build, deploy, and scale a production-grade OCR pipeline

Markdown Content:

Tired of watching your AI agent hallucinate, mistaking an invoice subtotal for the grand total, because a legacy OCR engine fed it garbled, flat text?

Tired of "Hello World" LangChain tutorials that work beautifully on tiny test images but explode the moment you upload a real-world, 20-page, 15MB PDF?

Tired of staring at four-figure cloud bills because you're paying for expensive A100 GPU pools sitting idle 24/7?

> Don't worry, friend, we've got you covered 😎
> Today we're officially kicking off the SLM-OCR Course: a 6-week, hands-on journey where we build, deploy, and scale an event-driven, production-grade OCR pipeline.

No high-level slides. No hand-wavy architecture diagrams. We're getting our hands dirty with Rust, Python, vLLM, Redis, KEDA, and real Kubernetes manifests that are ready for production.

Since this is the first article in the series, think of it as the map for the journey ahead: what we're building, how the weekly cadence works, and exactly what you get at each step.

So if you're ready… let's go! 👇

### 🎁 First, the part nobody else is doing: the code is free

![](https://substackcdn.com/image/fetch/$s_!Bpaa!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcf13633e-6134-4880-8055-c7a0017bcfa3_719x933.png)

Let's get the most important thing out of the way …

> We are open-sourcing the entire repository from day one!
> 💻 [Get the code here!](https://github.com/neural-maze/production-ocr-course)

In other words, you get immediate access to the full, production-ready system.

Here's the part worth sitting with: this is a $10,000 production codebase, and we're giving it away for free.

Plenty of companies are building exactly this kind of pipeline right now and locking it behind closed-source repos and enterprise contracts. We're doing the opposite. The full codebase is yours, publicly, from the first day of the course.

> Clone it, fork it, ship it, put it in production. Don't be shy! 🙌

### 💎 So what do Premium subscribers actually pay for?

Fair question. If the code is free, what's the value of going Premium?

The reasoning. The code tells you what we built. Premium tells you why.

Anyone can read a Kubernetes manifest. Very few people can tell you why `MAX_NUM_BATCHED_TOKENS` is set the way it is, when a two-stage pipeline beats an end-to-end model, why we reached for Rust instead of Python at the ingest layer, or how to reason about scaling GPU workers to zero without cold-start pain.

That understanding, the kind that lets you adapt the system to your problem instead of just copy-pasting ours, is what Premium unlocks:

- 📘 Weekly Production Article (Wednesday · Premium): the complete package. Deep-dive architectural walk-throughs, the math behind the systems decisions, and step-by-step code explanations mapped directly to the open-source repo.
- 🎙️ Live Office Hours (Sunday · Premium): live sessions where we review the code together, spin up the cluster, trigger scaling events, debug configs, and answer your implementation questions in real time.

> 💡 The code is the what. The articles and office hours are the why and the how: the engineering judgment you can't get from reading a repo alone.

[Go Premium](https://theneuralmaze.substack.com/subscribe) to unlock every weekly deep-dive article and all live Sunday office hours!

### 🏛️ The Architecture Philosophy: Why Two-Stage OCR?

Before diving into the curriculum, let's address a critical debate in the SOTA (State of the Art) OCR landscape today:

1. Single-Stage (End-to-End) Models: Using 2B to 5B visual-language models to directly generate Markdown or parse layout. It's incredibly easy to deploy, but has a massive drawback: high hallucination rates due to very long outputs and a lack of deterministic layout control on dense tables or low-resolution scans.
2. Two-Stage Hybrid Pipelines (Our Approach): Decoupling the problem. First, a deterministic layout detector (PP-DocLayoutV3 via the GLM-OCR SDK) scans the document to identify, segment, and crop semantic regions (paragraphs, tables, formulas, charts). Second, we pass those crops of high-resolution regions to a specialized LLM decoder (Qwen 3.5 4B) served on vLLM for transcription and contextual understanding.

> While the two-stage approach is harder to orchestrate and deploy, it is infinitely more reliable, customizable, and cost-effective.

And that is exactly what you are going to master.

### 📅 Course Cadence & Structure

Because we're giving you the entire codebase up front, we merge theory and implementation into a single weekly release rhythm:

- 📘 Weekly Production Article → Premium · Released on Wednesdays
- 🎙️ Live Office Hours → Premium · Live on Sundays

> 🙋 And for Week 1 only, a bonus cloud-setup article on Friday (GCP + Azure) to get your environment ready.

### 🛣️ The 6-Week Roadmap

Here's what we'll be covering, week by week, from now on. Each week we ship the deep-dive article and run the live office hours, working straight through the pipeline from the cluster foundations to the enterprise gateway. By the end, you'll have built and understood the whole system.

#### 🧭 Week 0: Cloud Setup (This Week)

Before we touch a cluster, we get your cloud account ready. This Friday's bonus article walks you through configuring Azure from scratch, so you're fully set up before Week 1 begins.

> 📘 Cloud Setup Article → Friday, July 24, 2026

#### ⛵ Week 1 - Kubernetes for AI Systems

![](https://substackcdn.com/image/fetch/$s_!ZRcG!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F09fdb532-58ae-4919-806b-bc22c4269bea_1024x1024.webp)

Stepping into K8s can feel intimidating if you've only written local Python scripts.

We'll start with the bare-metal concepts: What is a Pod, a Service, and a Node Pool? How does resource scheduling work? Then, we will immediately dive into the codebase to provision an AKS cluster, configure GPU node pools, and install the NVIDIA GPU Operator (handling PSA labels and taints/tolerations) so our nodes are ready to schedule GPU workloads.

> 📘 Article → Wednesday, July 29, 2026
> 🎙️ Office Hours → Sunday, August 2, 2026

#### 🧠 Week 2 - SOTA OCR Approaches & Visual Document Understanding

![](https://substackcdn.com/image/fetch/$s_!YxBG!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb76ea361-7200-4bf6-85bc-3417f573d219_1024x1024.webp)

We will dissect the SOTA approaches in document intelligence.

You'll learn the underlying architecture of image-to-markdown models versus layout-first pipelines. We will explain how a deterministic layout detector (PP-DocLayoutV3) acts as a pre-input visual encoder, restricting the VLM's decision space and mitigating structural hallucinations typical of generative models. We'll walk through the GLM-OCR SDK layout parser code and run comparison benchmarks.

> 📘 Article → Wednesday, August 5, 2026
> 🎙️ Office Hours → Sunday, August 9, 2026

#### ⚡ Week 3 - Deploying the vLLM Inference Engine & Orchestrator

![](https://substackcdn.com/image/fetch/$s_!10PK!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0f8bdd37-d0cb-4a8e-b594-d52ec9c6043a_1024x1024.webp)

Learn how to squeeze maximum throughput out of A100 GPU pools running vLLM.

We will analyze continuous batching, PagedAttention, and how to eliminate the "prefill bottleneck" by setting MAX_NUM_BATCHED_TOKENS=262144 and enabling chunked prefills (`--enable-chunked-prefill`). We'll walk through the Kubernetes deployment manifests and configure Multi-Token Prediction (MTP).

> 📘 Article → Wednesday, August 12, 2026
> 🎙️ Office Hours → Sunday, August 16, 2026

#### 🦀 Week 4 - Introduction to Rust: Building a High-Concurrency Ingest Gateway

![](https://substackcdn.com/image/fetch/$s_!4TfY!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe4de5b1f-b213-423a-8823-614a768b1c7a_1024x1024.webp)

Why are we using Rust?

Traditional Python web frameworks choke when handling high-concurrency streams of 10MB+ binary file uploads. We'll cover Rust fundamentals (ownership, borrowing, and Tokio async runtime) and walk through `client_rt_producer`, a high-throughput API gateway built with Axum that handles multipart file uploads and writes task payloads atomically to Redis using a single async HSET.

> 📘 Article → Wednesday, August 19, 2026
> 🎙️ Office Hours → Sunday, August 23, 2026

#### 🔄 Week 5 - Asynchronous Architectures & Zero-Copy Ingestion

![](https://substackcdn.com/image/fetch/$s_!7d2E!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe3981168-9e81-4a54-97f7-25f74a65f7eb_1024x1024.webp)

Deep dive into why event-driven queues are the gold standard for heavy multimedia processing. We will dissect the `client_rt_consumer` worker code, exploring the Collector Pattern (Dynamic Batching) to maximize GPU batch sizes, and zero-copy I/O using Linux shared memory (`/dev/shm`).

Finally, we'll look at the KEDA (Kubernetes Event-driven Autoscaling) manifests that scale T4 workers and vLLM servers to zero.

> 📘 Article → Wednesday, August 26, 2026
> 🎙️ Office Hours → Sunday, August 30, 2026

#### 🛡️ Week 6 - Enterprise Gateway (APIM) & Claude Code MCP Integration

![](https://substackcdn.com/image/fetch/$s_!j7NJ!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fec4097dc-7290-4574-b882-99a57dfdb37f_1024x1024.webp)

Exposing raw GPU APIs directly to the internet is a recipe for instant financial ruin or DDoS exploits.

We'll configure Azure API Management (APIM) in a secure Virtual Network (VNet) to act as a gateway, implementing subscription validation, JWT checks, IP whitelisting, and rate-limiting policies.

Finally, we'll walk through the implementation of a custom Model Context Protocol (MCP) server, connecting our AKS pipeline directly with Claude Code so your local AI agent can read dense visual documents natively.

> 📘 Article → Wednesday, September 2, 2026
> 🎙️ Office Hours → Sunday, September 6, 2026

### 📊 System Architecture

By the end of the course, this is the production topology you'll have deployed and orchestrated end to end, from the Rust ingest gateway, through the Redis queue and KEDA-driven autoscaling, to the vLLM serving layer and the APIM security gateway.

![](https://substackcdn.com/image/fetch/$s_!iEvM!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F039b6327-944d-431d-8616-b91fb66a0e67_2048x1369.png)

### 🧭 Next Steps

To get started, keep two things in mind:

- This Friday, we'll send the bonus cloud-setup article (GCP and Azure, step by step) so your environment is ready before Week 1's hands-on work.
- This Sunday, we'll host our first live office hours, where you can ask questions and clear up any doubts before we start provisioning clusters.

If you've been searching for a reason to transition from writing prompt scripts to building low-latency, multi-GPU infrastructure in the cloud… this is it.

The code is free and open from day one. The reasoning behind every engineering decision, the part that turns "I cloned a repo" into "I can build this myself," lives in the Premium articles and Sunday office hours.

[Become a Premium Subscriber of The Neural Maze](https://theneuralmaze.substack.com/subscribe) and let's build this thing together.

See you Friday, builders! 👋
