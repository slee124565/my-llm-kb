# 逐字稿

- Title: Demis Hassabis: Agents, AGI & The Next Big Scientific Breakthrough
- URL: https://www.youtube.com/watch?v=JNyuX1zoOgU
- Channel: Y Combinator
- Video ID: JNyuX1zoOgU
- Generated At: 2026-05-02T01:50:11Z
- Mode: sync
- Model: gemini-2.5-flash

## Gemini Output

## Summary

* Demis Hassabis 認為，持續學習、長期推理和記憶的某些方面對於實現通用人工智慧 (AGI) 仍然是未解決的問題。
* 他指出，目前的 AI 系統在處理大量數據時，雖然上下文窗口很大，但仍存在效率問題，需要創新來改進記憶和推理。
* Hassabis 相信，DeepMind 在強化學習和搜尋方面的經驗，特別是 AlphaGo 和 AlphaZero 的成功，對於開發像 Gemini 這樣的代理系統至關重要。
* 他強調，將 AI 應用於科學領域，特別是材料科學、藥物發現和氣候建模，是 AI 最大的潛力所在，並將 AlphaFold 視為這類突破的典範。
* Hassabis 鼓勵新創公司專注於深度技術，並將 AI 與其他科學領域結合，以創造出真正具有影響力的解決方案，同時也要考慮到 AGI 出現的潛在影響。

## Transcript
00:00:00 Demis Hassabis: continual learning, long-term reasoning, uh, some aspects of memory, these are still unsolved.
00:00:06 Demis Hassabis: I think all of these are going to be required for AGI.
00:00:09 Demis Hassabis: Depending on what your AGI timeline is, you know, mine's like 2030 or something like this, then if you start off on a deep tech journey today, you have to just consider AGI appearing in the middle of that journey.
00:00:22 Demis Hassabis: It's not bad necessarily, but you have to take that into account.
00:00:26 Demis Hassabis: You have to have an active system, uh, that can actively solve problems for you to get to AGI.
00:00:31 Demis Hassabis: So agents are that path, and I think we're just getting going.
00:00:35 How to build the future.
00:00:40 Garry Tan: Demis Hassabis has had one of the most unusual careers in tech.
00:00:46 Garry Tan: He was a chess prodigy as a kid, then designed his first hit video game, Theme Park, at 17.
00:00:53 Garry Tan: He then went back to school, got a PhD in cognitive neuroscience, published foundational work on how memory and imagination work in the brain.
00:01:02 Garry Tan: And then in 2010, co-founded DeepMind with one mission: solve intelligence.
00:01:09 Garry Tan: And I think they've done it.
00:01:12 Garry Tan: Since then, uh, his lab has gone on to do things most people thought were decades away.
00:01:17 Garry Tan: AlphaGo beat a world champion at Go.
00:01:19 Garry Tan: AlphaFold cracked protein structure prediction, a 50-year grand challenge in biology, and they gave it away for free to every scientist on Earth.
00:01:30 Garry Tan: That work won him the Nobel Prize in Chemistry last year.
00:01:34 Garry Tan: Today, Demis leads Google DeepMind, where he's building Gemini and pushing toward the same goal he set when he was a teenager: artificial general intelligence.
00:01:45 Garry Tan: Please welcome Demis Hassabis.
00:01:53 Garry Tan: So you've been thinking about AGI longer than almost anyone.
00:01:56 Garry Tan: Uh, when you look at the current paradigm, large-scale pre-training, RLHF, chain of thought, how much of the final architecture for AGI do you think we already have and what's fundamentally missing right now?
00:02:08 Demis Hassabis: Well, first of all, thank thanks Gary for that great introduction and it's great to be here.
00:02:12 Demis Hassabis: Thanks for for welcoming here.
00:02:13 Demis Hassabis: It's amazing space actually.
00:02:14 Demis Hassabis: I'll have to come back here often, very inspiring that you all get to work in in in this space.
00:02:20 Demis Hassabis: So the question is, I think the components that you just mentioned, I'm pretty sure will be part of the final architecture for AGI.
00:02:29 Demis Hassabis: So, uh, I think they've come such a long way now, uh, and we've proven out so many things about what they can do.
00:02:36 Demis Hassabis: Um, I can't see a world in which we'll sort of realize in a couple of years this was a dead end.
00:02:41 Demis Hassabis: That doesn't make sense to me.
00:02:42 Demis Hassabis: But there's still might be one or two things missing on top of, uh, of of what you've, you know, what we already know works.
00:02:50 Demis Hassabis: So, um, continual learning, long-term reasoning, uh, some aspects of memory, these are still unsolved.
00:02:56 Demis Hassabis: Um, and how to get the systems to be more consistent across the board.
00:03:02 Demis Hassabis: Um, I think all of these are going to be required for AGI.
00:03:04 Demis Hassabis: Now, it might be that the existing techniques can just scale up to that with some innovation and some incremental innovation.
00:03:11 Demis Hassabis: Um, but it could be that there's still one or two big ideas left, uh, that need to be cracked.
00:03:18 Demis Hassabis: I don't think it's more than one or two, if there are out there.
00:03:20 Demis Hassabis: And I think, you know, my betting is, uh, about 50/50 if that's the case.
00:03:25 Demis Hassabis: So, of course, at DeepMind, at Google DeepMind, we work on both those things.
00:03:29 Garry Tan: I guess that's what I mean, working with a bunch of identical systems, the wildest thing to me is to what degree it's the same weights over and over.
00:03:37 Garry Tan: So this idea of continual learning is so interesting because like, you know, right now we're sort of cobbling it together with duct tape, you know?
00:03:45 Demis Hassabis: Yes.
00:03:45 Garry Tan: These dream cycles at night and things like that.
00:03:47 Demis Hassabis: It's pretty cool the dream cycles and we we used to think about this with consolidation with episodic memory.
00:03:53 Demis Hassabis: That's actually what I studied for my PhD is how the hippocampus works and integrates, you know, new knowledge gracefully into the existing knowledge base.
00:04:03 Demis Hassabis: So the brain does that amazingly well.
00:04:05 Demis Hassabis: It it it does it through, you know, during sleep, uh, especially things like REM sleep, replaying back episodes that that are important so that you can learn from it.
00:04:13 Demis Hassabis: In fact, our very first Atari program, DQN, one of the ways it was able to master Atari games was by doing experience replay.
00:04:22 Demis Hassabis: So we sort of borrowed that from from neuroscience and replayed successful trajectories, uh, many times, you know, that's way back in 2013 now in the dark ages of AI.
00:04:31 Demis Hassabis: It was uh, a really important thing.
00:04:32 Demis Hassabis: And and I agree with you, we're kind of using duct tape right now.
00:04:36 Demis Hassabis: So like shove it all in the context window.
00:04:39 Demis Hassabis: Um, this seems a bit unsatisfying, right?
00:04:41 Demis Hassabis: And actually, even though, uh, we're working on machines, not biological brains, and so potentially you could have, you know, millions or tens of millions size context window or memory, and it can be perfect.
00:04:55 Demis Hassabis: There's still a cost to looking it up and finding the right thing, uh, that that's actually relevant for the specific, uh, decision you've got to make right now.
00:05:05 Demis Hassabis: And that's non-trivial that cost, even if you can potentially store it all.
00:05:08 Demis Hassabis: I think there's actually a lot of room for innovation in in areas like memory.
00:05:13 Garry Tan: Yeah.
00:05:13 Garry Tan: I mean, the wild thing is that it feels like a million token context window is actually bigger than, I mean, it's plenty big, honestly.
00:05:19 Garry Tan: You can do so much.
00:05:19 Demis Hassabis: Well, it's it's plenty big for for for most things that it should be useful for.
00:05:24 Demis Hassabis: I mean, if you think about the context window is sort of equivalent to working memory, you know, humans have, we have like a few digits.
00:05:33 Demis Hassabis: It's like a a dozen digits maybe, you know, average of seven.
00:05:35 Demis Hassabis: We've got a million or, you know, 10 million context windows, but the problem is is that we're trying to store everything in that.
00:05:43 Demis Hassabis: You know, things that aren't not important, things that are wrong.
00:05:46 Demis Hassabis: It's pretty brute force currently, and that doesn't seem, uh, right.
00:05:49 Demis Hassabis: And then the problem is if you're trying to try and process live video and you're just going to naively record all the tokens, then actually a million tokens isn't that much.
00:05:59 Demis Hassabis: It's only like 20 minutes.
00:06:01 Demis Hassabis: So, actually, you need more if you want something that's going to understand your, you know, your what's going on in your life over maybe a month or two.
00:06:08 Garry Tan: DeepMind has historically leaned into reinforcement learning and search.
00:06:14 Garry Tan: Uh, AlphaGo, AlphaZero, and MuZero.
00:06:18 Garry Tan: Uh, how much of that philosophy is actually embedded in how you're building Gemini to get today?
00:06:22 Garry Tan: Uh, is RL still underrated?
00:06:24 Demis Hassabis: Yeah, I think potentially it is.
00:06:25 Demis Hassabis: It's sort of goes in in ebbs and waves.
00:06:27 Demis Hassabis: You know, we've worked on agents since the beginning of DeepMind.
00:06:30 Demis Hassabis: In fact, we also that's what we said we were working on.
00:06:33 Demis Hassabis: So all of the Atari work and AlphaGo and most specifically, they're agent systems.
00:06:39 Demis Hassabis: And what we meant by that is systems that are able to, you know, accomplish goals on their own, uh, and make active decisions and and make plans.
00:06:47 Demis Hassabis: And so, of course, we were doing it in the domain of games to to to make it tractable, uh, and then doing increasingly complex games, things like StarCraft after AlphaGo, AlphaStar.
00:06:59 Demis Hassabis: So, um, we basically did all the games that are out there.
00:07:02 Demis Hassabis: And then of course, the question is, can you generalize those models to be world models or models of language, not just models of simple games, uh, or even complex games.
00:07:12 Demis Hassabis: And that's what the last few years has been about.
00:07:14 Demis Hassabis: But really, you can think of a lot of the things we're doing today, all the leading models with thinking modes and chain of thought reasoning as aspects of what was sort of pioneered with AlphaGo coming back now.
00:07:27 Demis Hassabis: And I actually think there's a lot of work we did back then that is relevant today, and we're sort of re-looking at some of those old ideas, um, at scale today in a more general way.
00:07:40 Demis Hassabis: Including things like Monte Carlo tree search and other other ways of doing augmenting the RL, uh, on top of the the reinforcement learning we're ready to do today.
00:07:47 Demis Hassabis: And I think a lot of those ideas both from AlphaGo and AlphaZero are really really relevant, uh, to to where we are with today's foundation models.
00:07:58 Demis Hassabis: And I think, uh, a lot of that is what we're going to see of the advances in the next few years.
00:08:00 Garry Tan: One question I would have is like, obviously, today you need bigger and bigger models to be smarter and smarter, but then we're also seeing distillation working.
00:08:09 Garry Tan: And then smaller models can be like quite a bit faster.
00:08:12 Garry Tan: I think, you know, you guys have incredible flash models that are like 90, like you're finding that they're 95% as good as, uh, the frontier and at like 1/10th the price.
00:08:22 Garry Tan: Is that right?
00:08:22 Demis Hassabis: I think that's one of our core strengths is, I mean, you have to build the biggest models to to to have, uh, the frontier capabilities.
00:08:30 Demis Hassabis: But I think one of our biggest strengths has been, uh, distilling and packing that power into smaller and smaller models very quickly.
00:08:37 Demis Hassabis: Obviously, we we, you know, we invented the kind of distillation process and and people like Jeff and Oriol and and others.
00:08:44 Demis Hassabis: And we're still world experts in that.
00:08:46 Demis Hassabis: And we also have a huge need to, uh, do it because we've got to serve the biggest probably AI surfaces, um, there are.
00:08:58 Demis Hassabis: Obviously, there's search with AI overviews and AI mode.
00:09:01 Demis Hassabis: Then there's Gemini app.
00:09:02 Demis Hassabis: And now increasingly every single product at Google has, you know, Maps and YouTube and so on has some aspect of Gemini or Gemini related technology in it.
00:09:11 Demis Hassabis: And so that's billions of users, a dozen, more than a dozen billion user products.
00:09:16 Demis Hassabis: Um, and they have to be served extremely fast, extremely efficiently and cheaply and with low latency.
00:09:23 Demis Hassabis: So that that gives us a really important incentive to to make these flash and even smaller models, flash light models, uh, extremely efficient.
00:09:32 Demis Hassabis: And hopefully that ends up then being really useful for many of the workloads that all of you use for for.
00:09:35 Garry Tan: I'm curious about how much smarter these smaller models can actually be.
00:09:40 Garry Tan: Like are there limits to the distillation process?
00:09:42 Garry Tan: Like could a 50B or a 400B model be as smart as like a Mythos for today?
00:09:48 Demis Hassabis: Yeah, I don't I don't see any, I don't think we've got to any kind of, or at least none of us know yet if we've got to any kind of informational limit.
00:09:56 Demis Hassabis: I mean, maybe at some point that will be the case where there's just an information density that can't we can't get beyond.
00:10:01 Demis Hassabis: But I think for now, there's the the assumption we make is that, you know, a year later after one of our, uh, leading, you know, pro models or frontier models goes out, half a year later, a year later, you'll have them in the the really tiny almost edge models.
00:10:17 Demis Hassabis: And you also see some of that goodness in our Gemma models, which hopefully you're all enjoying our Gemma 4 models, which I think are really amazing power for their sizes.
00:10:26 Demis Hassabis: So again, that uses a lot of this, uh, these distillation techniques and the idea of how to make things really efficient in these very small models.
00:10:34 Demis Hassabis: So I don't really see any limit yet in terms of like some kind of theoretical limit.
00:10:38 Demis Hassabis: I think we're still pretty far off of that.
00:10:39 Garry Tan: That's amazing.
00:10:40 Garry Tan: I mean, that is really good.
00:10:41 Garry Tan: Yes.
00:10:42 Garry Tan: Uh, you know, one of the weirder things that we're seeing right now is like engineers can do like 500 to 1,000 times the amount of work that they were doing like six months ago, I guess.
00:10:53 Garry Tan: I mean, the people in this room, there are people who are doing about like a thousand X the work that like I Steve Yegge talks about this.
00:11:00 Garry Tan: It's like a thousand X the work that a Google engineer from the 2000s was doing.
00:11:04 Demis Hassabis: I think it's very exciting.
00:11:05 Demis Hassabis: I mean, I think the small models have many uses.
00:11:08 Demis Hassabis: One is obviously cost, but the speed can allow, you know, if you think about coding even or other things, you can iterate a lot faster also, especially if there's if you're collaborating with the system.
00:11:19 Demis Hassabis: I think there's a there's a a lot of need for having fast systems, um, that maybe are not quite frontier, like you said, like 95%, 90%, but that's plenty good enough and actually you gain back more than the 10% on the the iteration speed.
00:11:34 Demis Hassabis: So and then the other big thing I think is running these things on the edge.
00:11:37 Demis Hassabis: Again, for efficiency reasons, but also for privacy and security reasons too.
00:11:43 Demis Hassabis: Um, if you think about different devices that you might run these systems on, that that, you know, process very personal information, can also think about robotics as well.
00:11:52 Demis Hassabis: Um, you know, robots in your house.
00:11:54 Demis Hassabis: I think you're going to want very efficient, uh, very powerful, uh, local models, which maybe are orchestrated, you know, with some bigger models, frontier models that are in the in the cloud, but you only delegate to that in certain circumstances.
00:12:08 Demis Hassabis: And perhaps you, you know, you process all of the audio visual feed, let's say, locally and that stays local.
00:12:15 Demis Hassabis: I could imagine, uh, that would be a very good sort of, um, end state.
00:12:19 Diana Hu: YC Startup School is back.
00:12:20 Diana Hu: We're hand selecting the most promising builders in the world and flying them out to San Francisco for July 25th and 26th to discuss the cutting edge of tech.
00:12:31 Diana Hu: Apply now for a spot.
00:12:32 Diana Hu: Okay, back to the video.
00:12:33 Garry Tan: Going back to context and memory, models currently stateless, but, you know, continue like what would the developer experience even be like for someone who's using a continual learning model?
00:12:44 Garry Tan: Like, you know, any idea like how you'd steer it?
00:12:47 Demis Hassabis: I think it's really interesting.
00:12:48 Demis Hassabis: I think that's one of the not having continual learning currently is one of the things holding back agents from doing full, uh, tasks.
00:12:56 Demis Hassabis: You know, I think they're really useful for aspects of tasks right now and you can patch them together and do some really cool things, but they don't adapt well with the context that you're in.
00:13:06 Demis Hassabis: And I think that's the missing piece for them being really kind of fire and forget and they'll figure it out themselves.
00:13:13 Demis Hassabis: You know, I think they need to be able to learn, um, about the specific context, um, that you're going to put them in.
00:13:22 Demis Hassabis: So, uh, I think we have to crack that to get full general intelligence.
00:13:26 Garry Tan: Where are we on reasoning?
00:13:27 Garry Tan: So models can do really impressive chain of thought now, but they still fail on things a smart undergrad wouldn't.
00:13:34 Garry Tan: What specifically needs to change and what progress do you expect in reasoning?
00:13:38 Demis Hassabis: There's a lot of, uh, innovation left in in thinking paradigms, I would say.
00:13:42 Demis Hassabis: Again, I think we're fairly, we're doing fairly simplistic things, fairly brute force.
00:13:48 Demis Hassabis: Um, one could imagine, uh, I think there's a lot of scope, for example, in monitoring the chain of thought, maybe interjecting midway through a thought process.
00:13:58 Demis Hassabis: I often get the impression with our systems and and our competitor systems that they're almost overthinking.
00:14:03 Demis Hassabis: They're almost getting into sort of loops of things.
00:14:05 Demis Hassabis: Like one thing, uh, I sometimes like to do is is play chess against Gemini.
00:14:10 Demis Hassabis: And, you know, it's all the leading foundation models are pretty poor at games, which is quite interesting.
00:14:16 Demis Hassabis: It's very, uh, uh, cool to kind of look at the thinking traces because obviously these are can be a well understood, you know, I can tell quite quickly if it's going off on a tangent, and it's very sort of provable what the what the thinking is doing, uh, whether it's useful or not.
00:14:32 Demis Hassabis: And so what we see is that, you know, sometimes it will it will it will consider a move, it will realize it's a blunder, but it can't find anything better, so it kind of goes back to that move and does it anyway.
00:14:42 Demis Hassabis: So it, you know, you just shouldn't be seeing that, uh, happening in a in a very precise reasoning system.
00:14:50 Demis Hassabis: So there's just sort of huge gaps, I think, still, but it may only be one or two tweaks that are required to fix those kind of gaps, just to be clear.
00:15:00 Demis Hassabis: But I think that's pretty pretty obvious there are there.
00:15:02 Demis Hassabis: And that's why you get this kind of jagged intelligence.
00:15:05 Demis Hassabis: You know, on the one hand, it can solve gold medal problems in IMO, which is super hard.
00:15:10 Demis Hassabis: But on the other hand, as we've all seen, it can still make basic elementary math errors if you pose the question in a certain way, right?
00:15:20 Demis Hassabis: So or elementary reasoning errors.
00:15:22 Demis Hassabis: So there's just something to me about the almost an introspection about its own thought process that I feel like there's there's something maybe missing there.
00:15:27 Garry Tan: Agents are really big.
00:15:28 Garry Tan: Some would say they're hyped.
00:15:29 Garry Tan: I personally think they're just getting started.
00:15:31 Garry Tan: It's totally insane.
00:15:32 Garry Tan: What does DeepMind's internal research tell you about where agent capabilities actually are right now versus, you know, sort of the hype out there?
00:15:40 Demis Hassabis: I think we are, I agree with you.
00:15:41 Demis Hassabis: I think we're just at the beginning.
00:15:42 Demis Hassabis: You have to have an active system, uh, that can actively solve problems for you to get to AGI.
00:15:48 Demis Hassabis: That was always clear to us.
00:15:49 Demis Hassabis: So agents are that path, and I think we're just getting going.
00:15:52 Demis Hassabis: I think all of us are getting used to how do we best work and you're leading the way in a lot of this in your own personal experiments.
00:15:59 Demis Hassabis: I'm sure many of you are doing that.
00:16:00 Demis Hassabis: I think how do you incorporate it into your, uh, workflow in a way that isn't just, um, sort of a nice to have, but actually starting to do fundamental things.
00:16:11 Demis Hassabis: My impression is at the moment we're all experimenting, we're experimenting on lots of things, but we're only in the maybe the last couple of months starting to find the really valuable places.
00:16:20 Demis Hassabis: And the technology is probably only getting good enough for that to be the case, right?
00:16:24 Demis Hassabis: That it's not a kind of toy, um, nice demonstration, but actually really adding value to your to your, um, to your time and efficiency.
00:16:32 Demis Hassabis: I often wonder, I see a lot of people working on, uh, like setting off, you know, dozens of agents for like 40 hours, but I'm not sure I've seen the output that yet of that quite justify that level of input going in.
00:16:49 Demis Hassabis: But I I think it will come.
00:16:50 Demis Hassabis: So I still think we're in the experimentation phase.
00:16:52 Demis Hassabis: We haven't seen a AAA game that tops the App Store charts that was sort of vibe coded yet, right?
00:17:00 Demis Hassabis: I've seen, and I've programmed and I'm sure many we've all done little nice demonstrations and it's like amazing.
00:17:06 Demis Hassabis: I can do a prototype of Theme Park in half an hour now, which took me six months back when I was 17.
00:17:12 Demis Hassabis: It's kind of mind-blowing.
00:17:14 Demis Hassabis: And I and I wish I I got this feeling if I spent the whole summer working on it, you could make something really incredible, but it still needs craft and, you know, human sort of soul into it and taste.
00:17:24 Demis Hassabis: I think that's that's something that can that's you have to make sure you still bring that to to whatever it is you're building.
00:17:28 Demis Hassabis: And I think it still shows like it's not quite there yet because why haven't we seen a kid making a hit game that's that sells 10 million copies, right?
00:17:39 Demis Hassabis: That should be possible given the effort that's gone in.
00:17:41 Demis Hassabis: So something's still somehow missing.
00:17:43 Demis Hassabis: Maybe it's to do with the process or maybe it's to do with the tools.
00:17:45 Demis Hassabis: I'm not quite sure.
00:17:46 Demis Hassabis: You all will probably know better than me because I'm sure you're all experimenting on that.
00:17:48 Demis Hassabis: But I haven't seen the result yet, which I would expect once this is really delivering that full value.
00:17:56 Demis Hassabis: Which I think will come in the next six to 12 months.
00:17:58 Garry Tan: Some of it is like how much of it will be autonomous versus, I mean, I don't think we'd see autonomous first.
00:18:02 Garry Tan: We would actually probably see people in this room operating at a thousand X and then.
00:18:08 Demis Hassabis: That's what you should see first.
00:18:09 Demis Hassabis: And then many of you, you know, there'll be like games companies or, you know, other types of companies that have built some kind of best-selling app, best-selling game using, uh, these tools.
00:18:21 Demis Hassabis: That's what you should see first, and then more of that will get automated.
00:18:25 Garry Tan: I mean, some of it is like there's a human in there and then the human doesn't want to say that the the agents did it.
00:18:32 Demis Hassabis: I think part of it might be though that, um, this we want to discuss like creativity.
00:18:38 Demis Hassabis: What I often say about that is like if we look at the things we've done like AlphaGo.
00:18:42 Demis Hassabis: So obviously very famously, you'll all know about the move 37 in game two.
00:18:47 Demis Hassabis: And for me, I was waiting for a moment like that to start the science projects like AlphaFold.
00:18:52 Demis Hassabis: So we started AlphaFold like the day we got back from Seoul, which is 10 years ago now.
00:18:57 Demis Hassabis: I'm going to career it after this to celebrate the 10-year anniversary of AlphaGo.
00:19:00 Demis Hassabis: But it's not enough to come up with move 37.
00:19:04 Demis Hassabis: Like that's pretty cool, very useful, um, but can it invent Go?
00:19:10 Demis Hassabis: That's what I I want a system that can invent Go if you give it a high-level description, you know, like a game you can learn the rules of in five minutes, but it takes many lifetimes to master.
00:19:20 Demis Hassabis: It's beautiful aesthetically, um, but you can play it in a few hours in an afternoon.
00:19:26 Demis Hassabis: So, you know, maybe you could imagine that would be the high-level description I would give and then I'd want the the return, the thing I get back is Go, right?
00:19:35 Demis Hassabis: And, um, clearly today's systems, I think can't do that.
00:19:40 Demis Hassabis: So the question is why?
00:19:42 Demis Hassabis: Um, and I think there's something still missing there.
00:19:43 Garry Tan: Well, someone in this room might might make it.
00:19:44 Demis Hassabis: Then the answer would be there's nothing missing.
00:19:46 Demis Hassabis: It just was the way we were using the systems.
00:19:48 Demis Hassabis: And that might actually be the answer.
00:19:49 Demis Hassabis: It might be that our today's systems are capable of that with a brilliant enough creative person using it and providing that impetus, that the soul of the project and being able to probably being enough with the tools to like almost be at one with the tools.
00:20:08 Demis Hassabis: I could imagine that would be happening if you experimented with the tools all day and all night like probably many of you are doing that and you combine that with proper deep creativity, um, something, you know, more incredible could be done.
00:20:20 Garry Tan: Switching gears to open source.
00:20:21 Garry Tan: I mean, or open open and open weights.
00:20:23 Garry Tan: I mean, the recent release of Gemma, you're making highly capable open and accessible ones that can actually run locally.
00:20:31 Garry Tan: What do you think that means for, you know, will AI be something that is in the hands of the users instead of primarily in the cloud?
00:20:40 Garry Tan: And does that change who gets to, you know, build with these models?
00:20:42 Demis Hassabis: We're huge proponents of in general of open source and open science and you mentioned AlphaFold at the beginning.
00:20:50 Demis Hassabis: You know, we put that all out there for free and all of our science work even still today we publish in, you know, the big journals.
00:20:56 Demis Hassabis: We wanted to create, uh, world leading models for their their sizes.
00:21:01 Demis Hassabis: And so that's what hopefully we've done with Gemma and we're, you know, very committed to that path and hopefully you all experiment and build and and enjoy using Gemma.
00:21:09 Demis Hassabis: I think it's been like 40 million downloads now.
00:21:12 Demis Hassabis: And, uh, in just in, you know, two and a half weeks.
00:21:14 Demis Hassabis: So we're really excited about that.
00:21:15 Demis Hassabis: And I also think it's important for there to be Western stacks on open source.
00:21:20 Demis Hassabis: You know, obviously a lot of the Chinese models are excellent and and they're currently well leading in open source and we think Gemma is very competitive for its sizes, uh, uh, in in all those respects.
00:21:30 Demis Hassabis: And for us, I mean, there is a question of resources, talent and compute.
00:21:36 Demis Hassabis: Like nobody has enough spare compute to just make two, you know, uh, frontier models at maximum size, right?
00:21:44 Demis Hassabis: With different attributes.
00:21:45 Demis Hassabis: So that's pretty difficult.
00:21:45 Demis Hassabis: But also for what for now what we've we've decided is that our edge models, the things we want to use for Android and glasses and robotics, um, it's best that they're open models because they're vulnerable anyway on the once you put them out on the surfaces, so they might as well be actually fully open, right?
00:22:03 Demis Hassabis: So we've sort of made a decision to kind of unify that, uh, at the at the kind of, we call it nano size level.
00:22:10 Demis Hassabis: So that actually works for us, uh, strategically as well.
00:22:15 Demis Hassabis: Um, and, you know, we hope as many people as possible build on it.
00:22:17 Demis Hassabis: And of course, we'll be building on that too.
00:22:19 Garry Tan: Earlier, uh, before we came on, I got to show you a demo of, uh, my version of Samantha from Her, which is, uh, harrowing for me to try to demo something to you.
00:22:29 Garry Tan: Um, and it worked, which is amazing.
00:22:31 Garry Tan: Gemini was built multimodal and I spent a lot of time with a bunch of the models and I mean, the depth of the context and the tool use with speech directly to model, like there's nothing like bar none, like the best one, actually.
00:22:45 Demis Hassabis: Yeah.
00:22:45 Demis Hassabis: Yeah, I think I think that's sort of still a slightly underappreciated aspect of of of the Gemini series is we we started it being multimodal from the start.
00:22:55 Demis Hassabis: That made it a little bit more difficult actually to begin with because then just focusing on text, for example.
00:23:00 Demis Hassabis: But we believe we're going to gain from that in the long run.
00:23:04 Demis Hassabis: And I think we're seeing that now for, uh, things like world model building.
00:23:10 Demis Hassabis: So stuff like Genie that we build on top of Gemini.
00:23:14 Demis Hassabis: I think it's going to be really important for things like robotics.
00:23:17 Demis Hassabis: So this is why Gemini Robotics, which many of you probably played around with.
00:23:20 Demis Hassabis: I think it's going to be built on multimodal foundation models, the robotics models.
00:23:25 Demis Hassabis: And, uh, we think we have a sort of competitive advantage with with Gemini being so strong at multimodal.
00:23:31 Demis Hassabis: We're using it increasingly in things like Waymo, um, but also if you imagine devices and assistants, uh, that digital assistants that come with you into the real world, you know, maybe on your phone or glasses or some other device.
00:23:44 Demis Hassabis: Um, it needs to understand the physical world around you and intuitive physics, uh, and the and the physical context you're in.
00:23:51 Demis Hassabis: And that's what our systems are extremely good at.
00:23:53 Demis Hassabis: And I think you found that's why you've enjoyed using it in your setup.
00:23:56 Demis Hassabis: We're planning to continue on that and I think we're far and away the strongest models on on those types of, uh, problems.
00:24:02 Garry Tan: So the cost of inference is, uh, dropping fast.
00:24:05 Garry Tan: What becomes possible when inference is essentially free and how does that change what your team is actually optimizing for?
00:24:11 Demis Hassabis: Yeah, I'm not sure inference will ever be essentially free.
00:24:16 Demis Hassabis: I mean, there's sort of Jevons paradox and other things about like, I think we'll just end up using all of us will end up using whatever we can get our hands on.
00:24:25 Demis Hassabis: And you could imagine, uh, millions of agents, swarms of agents working together on things.
00:24:30 Demis Hassabis: So that's one way to use the inference.
00:24:32 Demis Hassabis: Or you could imagine, uh, single agents or group smaller groups of agents thinking for in multiple directions and then ensembling that.
00:24:40 Demis Hassabis: So we're experimenting with all these things, probably many of you are.
00:24:43 Demis Hassabis: All of that will use up any inference, I think, that's available.
00:24:48 Demis Hassabis: I mean, one day, maybe it can be almost cost zero.
00:24:51 Demis Hassabis: Certainly the energy if we solve fusion or, you know, superconductors or, you know, optimal batteries or some set of those things, which I think we will do with material science.
00:25:00 Demis Hassabis: Energy cost will be essentially zero, but there'll still be the physical creation of the chips and other things.
00:25:06 Demis Hassabis: There'll still be some bottleneck, um, at least for the next few decades, I think.
00:25:12 Demis Hassabis: And so if that's the case, there'll still be rationing on the inference side.
00:25:17 Demis Hassabis: You still have to use it, I think, efficiently.
00:25:18 Garry Tan: Yeah.
00:25:18 Garry Tan: Well, luckily, the smaller models are getting smarter and smarter, which is fantastic.
00:25:22 Garry Tan: Uh, we got a lot of bio and biotech founders in the audience.
00:25:26 Garry Tan: I can see a few.
00:25:27 Garry Tan: AlphaFold 3 took us beyond proteins to a broad spectrum of biomolecules.
00:25:31 Garry Tan: How close are we to modeling full cellular systems or is that still a fundamentally harder problem in a class of its own?
00:25:38 Demis Hassabis: Well, Isomorphic Labs, which we spun out from from from DeepMind after we did AlphaFold 2, um, it's it's which is going amazingly well.
00:25:50 Demis Hassabis: It's it's trying to build out, uh, not just AlphaFold, it's just one piece of the drug discovery process, uh, as many you know, but we're trying to do the the adjacent biochemistry and chemistry to design the right compounds with the right properties and so on.
00:26:02 Demis Hassabis: Well, have some big announcements for, you know, very soon to talk about on the on that front.
00:26:06 Demis Hassabis: I think that's going really well.
00:26:08 Demis Hassabis: Eventually, you want a whole virtual cell.
00:26:10 Demis Hassabis: So I've talked about this in many of my science talks about a full working simulation of a cell that you can perturb and then the, you know, the the outputs of that would be close enough to experimental that it's useful, right?
00:26:24 Demis Hassabis: You could skip out a lot of the the search steps and generate lots of synthetic data to train other models that then would predict things about, you know, real cells.
00:26:34 Demis Hassabis: And, um, I think we're about 10 years away probably from something like a virtual cell, like a full virtual cell.
00:26:40 Demis Hassabis: You know, we're starting out, this is where we're working on the DeepMind side, science side on a, you know, virtual nucleus, cell nucleus first because it's relatively self-contained.
00:26:50 Demis Hassabis: The trick with all of these things is, can you pick a slice of the complexity?
00:26:55 Demis Hassabis: You know, eventually you want to want to model a human body, but can you model it down to the right level of detail?
00:27:02 Demis Hassabis: And what slice can you, uh, take out of it that will be self-contained enough?
00:27:10 Demis Hassabis: You can kind of model and approximate the inputs and outputs into that self-contained system and then just focus on the self-contained system.
00:27:15 Demis Hassabis: So a nucleus is quite interesting from that perspective.
00:27:18 Demis Hassabis: Um, then the other issue is just there's not enough data yet.
00:27:21 Demis Hassabis: So you need data, uh, and I talked to various, you know, top scientists about who work on electron microscopes and other imaging things.
00:27:29 Demis Hassabis: If we could image a live cell without killing the cell, that would be, um, game changing, obviously, because then you could convert it into a vision problem, which we would know how to solve, right?
00:27:38 Demis Hassabis: But at the moment, there are at least I I'm not aware of any techniques that can give you a kind of, you know, nanometer resolution, uh, but without destroying, but in, you know, in a live dynamic cell.
00:27:50 Demis Hassabis: So you can see all the interactions, right?
00:27:52 Demis Hassabis: You can take static images at that resolution, obviously, um, really detailed now.
00:27:56 Demis Hassabis: And that's quite exciting.
00:27:57 Demis Hassabis: But it's not enough, uh, to turn it just into just into a complex vision problem.
00:28:04 Demis Hassabis: So that's one way it could be solved.
00:28:06 Demis Hassabis: So it could be a hardware driven, data driven solution, or we could be that we build better, uh, learned simulators of, uh, these dynamical systems.
00:28:16 Demis Hassabis: So that's that's the more modeling way of solving it.
00:28:18 Garry Tan: Uh, you've been looking at all kinds of science, not just bio.
00:28:21 Garry Tan: Uh, there's material science, drug discovery, climate modeling, mathematics.
00:28:25 Garry Tan: If you had to rank which scientific domain will transform the most dramatically the next five years, what's in your list?
00:28:30 Demis Hassabis: Well, they're all so exciting and that's why, I mean, that that for me has been my main passion and always the reason why I've worked on AI for my whole career for 30 plus years now is to use AI as the ultimate tool.
00:28:43 Demis Hassabis: I always thought AI would be the ultimate tool for science and to invite such advanced scientific understanding, scientific discovery and things like medicine and just our understanding of the universe around us.
00:28:53 Demis Hassabis: So actually when you mentioned our original way we used to articulate our mission statement, which is still the way we think about it is there was two steps to it.
00:29:00 Demis Hassabis: One was step one was solve intelligence, I build AGI, and then step two was use it to solve everything else.
00:29:06 Demis Hassabis: We had to change that a bit over time because people were like, do you really mean solve everything else?
00:29:10 Demis Hassabis: And we did mean that and I think people are sort of understanding what that means today.
00:29:14 Demis Hassabis: But specifically, I was meaning solve other what I call root node problems in science.
00:29:20 Demis Hassabis: So areas of science that would unlock whole new branches or avenues of discovery.
00:29:25 Demis Hassabis: And AlphaFold is the prototypical example of what we want to do.
00:29:28 Demis Hassabis: So over 3 million researchers around the world, pretty much every biology researcher in the world uses AlphaFold now.
00:29:35 Demis Hassabis: And I was told by some of my, you know, farmer executive friends that, you know, almost every drug discovered from now on will have used AlphaFold at some point in its in the drug discovery process.
00:29:49 Demis Hassabis: So there's something we're very proud of and it's the sort of impact that we hope to have with with AI.
00:29:54 Demis Hassabis: But I do think it's just the beginning.
00:29:55 Demis Hassabis: I I don't really see any area of science or engineering that this won't be able to help be helpful with.
00:30:00 Demis Hassabis: And the ones you mentioned, I think we're almost like an AlphaFold one moment.
00:30:04 Demis Hassabis: So it's we've got very promising results, but it's not quite solved the grand challenge yet in that domain.
00:30:10 Demis Hassabis: But I think we're going to have a lot to talk about, you know, in the next couple of years on all those areas you mentioned materials, which I I think it's very exciting, all the way to mathematics.
00:30:18 Garry Tan: In in science, I mean, it feels Promethean.
00:30:20 Garry Tan: It's like here is this capability and you know.
00:30:23 Demis Hassabis: I think so.
00:30:24 Demis Hassabis: I mean, of course, along with that including what the the parable of Prometheus, we have to also be careful with how we use that and what we use it for and also the misuse, uh, that can happen with those same tools.
00:30:37 Garry Tan: A lot of people in this room are trying to build companies applying AI to science.
00:30:40 Garry Tan: For them, what's the difference between a startup that actually advances the frontier in your view versus one that's just wrapping an API around a foundation model and calling it AI for science?
00:30:49 Demis Hassabis: Well, look, I think there's one of the things I would recommend, I'm trying to think about and I think you mentioned this to me before.
00:30:55 Demis Hassabis: What would I do today myself if I was sitting in your place in Y Combinator, you know, looking at things.
00:31:01 Demis Hassabis: One thing you have to do is obviously intercept where the AI tech is going.
00:31:05 Demis Hassabis: So that's one hard part of it.
00:31:07 Demis Hassabis: But I do think there's huge, uh, scope for combining where AI is going with some other deep technology area.
00:31:14 Demis Hassabis: I just think that that sweet spot is is whether it's materials or medicine or other really hard areas of science.
00:31:22 Demis Hassabis: Um, I think that those kinds of interdisciplinary teams, especially if it involves the world of atoms as well.
00:31:27 Demis Hassabis: Um, there's not going to be a shortcut to that, uh, at least in the foreseeable future.
00:31:32 Demis Hassabis: Those are areas that are pretty safe from just getting swamped by whatever the next update is to the foundation models.
00:31:38 Demis Hassabis: So I think if you're looking for things like that, that's one of the more defensible areas, I would say.
00:31:44 Demis Hassabis: And I've always loved deep tech, so I'm kind of biased towards deep tech things.
00:31:50 Demis Hassabis: I think, um, nothing that's really long lasting and worthwhile is easy.
00:31:56 Demis Hassabis: And so I'm always been drawn to to deep technologies.
00:32:00 Demis Hassabis: Obviously AI was like that back in 2010 when we started out, right?
00:32:04 Demis Hassabis: It was it was thought to just, you know, we know it doesn't work kind of thing is what I was told by investors and even in academia, it was considered to be a very niche subject that we sort of tried in the 90s and we know doesn't work.
00:32:17 Demis Hassabis: But if you, you know, if you have belief and conviction in your idea, why it's different this time or what special combination from your background that you had, ideally you're expert in both those areas, both the machine learning and the other area you're applying it to, or you can create a founding team with that expertise.
00:32:31 Demis Hassabis: I think there's huge impact to be made there and huge value to be built there.
00:32:35 Garry Tan: That's a really important message.
00:32:37 Garry Tan: I mean, even, I mean, it's hard, it's easy to forget like basically once you've done it, you've done it, but before you've done it, people are arrayed against you.
00:32:44 Demis Hassabis: Oh, sure.
00:32:44 Demis Hassabis: I mean, no one believes in it, which is why I think you got to you've also got to work in things that you're genuinely passionate about.
00:32:51 Demis Hassabis: Like for me, I would have worked on AI no matter what happened.
00:32:55 Demis Hassabis: I just decided from a very young age, it was the thing that, um, could be the most consequential thing I could think of.
00:33:02 Demis Hassabis: It's turned out that way, but it might not have maybe we would have been 50 years too early.
00:33:05 Demis Hassabis: And it was also the most interesting thing I could think of working on.
00:33:10 Demis Hassabis: And so I would have still been working on AI today, even if we were still, you know, in a little garage somewhere and it still wasn't quite working.
00:33:19 Demis Hassabis: I would have still been trying to find maybe I would have been back in academia or something, but I would have found some way of of continuing to work on it.
00:33:24 Garry Tan: So, I mean, AlphaFold was like an example of a spike that you pursued and it worked.
00:33:30 Garry Tan: You know, what makes a scientific domain ripe for an AlphaFold style breakthrough?
00:33:33 Garry Tan: And is there a pattern, a certain objective function, like.
00:33:35 Demis Hassabis: The way I I should write this up at some point when I have five minutes spare, but the lesson I've learned from all the Alpha projects we've done, specifically AlphaGo and AlphaFold is, um, I think the techniques we have and the problems I look like to look for are great in if the if the situation can be described as massive combinatorial search space.
00:33:57 Demis Hassabis: The more massive the better in some ways.
00:33:59 Demis Hassabis: So no brute force or special case algorithm will will solve it.
00:34:04 Demis Hassabis: And that's true of Go moves and of, you know, different configurations of proteins, far more than the atoms in the universe, both of those.
00:34:10 Demis Hassabis: And then, um, you have a clear objective function.
00:34:14 Demis Hassabis: So, you know, you can think of it as minimizing the free energy in the proteins or, you know, the winning the game of Go.
00:34:20 Demis Hassabis: So you need to be able to specify your objective function clearly so you can hill climb.
00:34:24 Demis Hassabis: And then, um, enough data and or a simulator that can generate you, uh, lots of in distribution, uh, uh, synthetic data.
00:34:34 Demis Hassabis: If those things are true, then I think, um, with today's methods, you can go a long way into tackling and finding the kind of needle in the haystack that you need, uh, to for the solution that you're trying to look for.
00:34:45 Demis Hassabis: And I think of just drug discovery, by the way, in the same way, right?
00:34:47 Demis Hassabis: There is a compound out there that would solve this disease if one could find it, if one could only find it, right?
00:34:55 Demis Hassabis: And that wouldn't have any side effects and so on.
00:34:58 Demis Hassabis: And, uh, as long as the laws of physics allows it, then the only question is how do you find it in an efficient way, in a tractable way?
00:35:04 Demis Hassabis: I think we showed for the first time actually with AlphaGo that these systems could, uh, find those kinds of needles in a haystack, in that case, you know, the perfect Go move.
00:35:14 Garry Tan: I guess, uh, to get a little meta, I mean, we've been we're talking about humans using these methods to create AlphaFold, but then there's a meta level, which is humans using AI to explore the space of possible hypotheses.
00:35:27 Garry Tan: How close are we to AI systems that can do genuine scientific reasoning, not just pattern matching on data?
00:35:32 Demis Hassabis: I think we're close.
00:35:34 Demis Hassabis: Um, we're working on these general systems like that that like we have this system called co-scientist and we have other algorithms like AlphaFold that can go a little bit beyond what the basic Gemini will do.
00:35:47 Demis Hassabis: And obviously all the frontier labs are experimenting in this way.
00:35:50 Demis Hassabis: I've yet to seen anything so far, and we we all tinker with the same things, you know, some math problems that are a little bit harder than IMO and so on.
00:35:58 Demis Hassabis: I haven't seen anything yet, um, that is a true genuine, you know, massive discovery.
00:36:05 Demis Hassabis: That's my personal opinion.
00:36:06 Demis Hassabis: I think it's coming.
00:36:07 Demis Hassabis: I think it may be related to, uh, this earlier this thing we discussed about creativity and and actually going on beyond the bounds of what's known.
00:36:18 Demis Hassabis: So clearly that's just not pattern matching at that point because there's there is no pattern to match to.
00:36:21 Demis Hassabis: And it's a bit more than extrapolation.
00:36:23 Demis Hassabis: It's some kind of analogical reasoning.
00:36:25 Demis Hassabis: And I don't think these systems have that, or at least we're not using them in the in the right way to do that.
00:36:30 Demis Hassabis: So the way I often say that in science is, can it come up with a hypothesis that's really interesting, not just solve one.
00:36:38 Demis Hassabis: When I say just, we're now talking about just like solving the Riemann hypothesis or something.
00:36:42 Demis Hassabis: This would be obviously amazing or one of the millennium prize problems and maybe we're a couple of years out from doing that.
00:36:48 Demis Hassabis: Um, but I'd like to solve P equals NP, that's that's my favorite one.
00:36:52 Demis Hassabis: But can you, but even harder than that would be to come up with a new set of of millennium prize problems that were regarded by top mathematicians to be as, you know, as deep and meaningful and worthy of lifetime of study and effort to solve.
00:37:09 Demis Hassabis: Right?
00:37:10 Demis Hassabis: I think that's another level harder.
00:37:11 Demis Hassabis: And, uh, we don't have, um, you know, I still don't think we know how to do that.
00:37:15 Demis Hassabis: I don't think it's it's it's magical though.
00:37:17 Demis Hassabis: I do think these systems will be eventually able to do that.
00:37:20 Demis Hassabis: Maybe we're missing one or two things.
00:37:21 Demis Hassabis: And then the way we would test that is, you know, I sometimes call it my Einstein test, which is, you know, can you train a system with the knowledge of cutoff of 1901 and then will it come up with, you know, what Einstein did in 1905, including special relativity, you know, his Annus Mirabilis.
00:37:38 Demis Hassabis: Can can it do that, right?
00:37:40 Demis Hassabis: Uh, and then I think we could run that test.
00:37:43 Demis Hassabis: Maybe maybe we should just run that test and keep seeing if that's possible.
00:37:47 Demis Hassabis: And once that is, then I think we're on the verge of these systems being able to invent something new, truly novel.
00:37:53 Garry Tan: So last last question for the people who are deeply technical in this room, who want to work on something, you know, even close to the scale that what you have created with, you know, it's one of the largest AI efforts in the world and you've been a pioneer for all these years.
00:38:07 Garry Tan: So for that, I think everyone in this room thanks you and the folks at DeepMind very, very deeply from the bottom of our hearts.
00:38:13 Garry Tan: Thank you.
00:38:14 Garry Tan: What's the thing that you know now about building at the frontier that you wish you'd known at 25?
00:38:20 Demis Hassabis: I think we covered some of it in terms of actually you you work out that going off to hard problems and deep problems, um, is no more difficult in some ways than than going off to a shallower, simpler, more superficial problem.
00:38:34 Demis Hassabis: There there are just differently difficult.
00:38:36 Demis Hassabis: There's different things that are hard about each of those things.
00:38:38 Demis Hassabis: But I think given life's very short and you know, you only have so much time and energy, you might as well put your life force into something that will really make a a difference if you hadn't done it, if you hadn't been there to push it.
00:38:54 Demis Hassabis: So I would just think of it through that lens.
00:38:56 Demis Hassabis: And then the other thing is if you're if you are, you know, we talked about deep tech and I love interdisciplinary, uh, work and I think that's going to be even more prevalent in the next few years in combinations of fields and, uh, finding the the the connections between those fields.
00:39:12 Demis Hassabis: And it's going to be even easier to do that with AI.
00:39:14 Demis Hassabis: And then the only other thing I would say is if, you know, if you have your depending on what your AGI timeline is, you know, mine's like 2030 or something like this, then if you start off on a deep tech journey today, usually that you're talking about a 10-year journey for for true deep tech in my opinion.
00:39:31 Demis Hassabis: So then now you have to just consider AGI appearing in the middle of that journey.
00:39:37 Demis Hassabis: So what does that mean?
00:39:38 Demis Hassabis: It doesn't it's not bad necessarily, but you have to take that into account, right?
00:39:42 Demis Hassabis: To will it be able to leverage it?
00:39:45 Demis Hassabis: What will the AGI system do with it?
00:39:47 Demis Hassabis: And it goes a little bit back to what you said earlier about AlphaFold and general AI systems.
00:39:51 Demis Hassabis: So one thing I can think see happening is Gemini, Claude, or one of these general systems making use of AlphaFold like specialized systems as tools.
00:40:00 Demis Hassabis: I don't think we're going to have it just in one giant brain because it'll have too much regression in if I put all the proteins into, you know, our Gemini, that wouldn't make sense.
00:40:10 Demis Hassabis: We don't need Gemini to do protein folding.
00:40:12 Demis Hassabis: Going back to your information efficiency, it will definitely affect its language skills or something like that, right?
00:40:18 Demis Hassabis: In a bad way.
00:40:20 Demis Hassabis: So much better, I think, is to have really good general purpose tool usage models that will then maybe they could even train those specific tools, but they would be in a separate, uh, uh, system.
00:40:30 Demis Hassabis: So I think that's kind of interesting to think through the implications of that and then what you might build today.
00:40:35 Demis Hassabis: Also physical things too, like what kinds of factories would you build?
00:40:38 Demis Hassabis: What sorts of, um, you know, finance systems and so on.
00:40:42 Demis Hassabis: So I just think you need to really take that seriously in in in on the one hand is like and imagine what that world would look like and then build something that would be useful if that comes in halfway through.
00:40:53 Garry Tan: Demis Hassabis, everyone.
