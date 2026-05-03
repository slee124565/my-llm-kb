# 逐字稿

- Title: OpenClaw: The Viral AI Agent that Broke the Internet - Peter Steinberger | Lex Fridman Podcast #491
- URL: https://www.youtube.com/watch?v=YFjfBk8HI5o
- Channel: Lex Fridman
- Video ID: YFjfBk8HI5o
- Generated At: 2026-05-02T23:52:25Z
- Mode: sync
- Model: gemini-2.5-flash
- Media Resolution: MEDIA_RESOLUTION_LOW
- Chunk Count: 10

## Chunked Gemini Output

### 00:00:00-00:20:00

## Transcript
00:00:00 Peter Steinberger: I watched my agent happily click the I'm not a robot button.
00:03:00 Peter Steinberger: I made the agent very aware.
00:05:00 Peter Steinberger: Like it knows what is source code is. It understands how it sits and runs in its own harness. It knows where documentation is.
00:15:00 Peter Steinberger: It knows which model it runs. It understands its own system that made it very easy for an agent to, oh, you don't like anything, you just prompted it to existence. And then the agent would just modify its own software. People talk about self-modifying software, I just built it.
00:29:00 Peter Steinberger: I actually think wipe coding is a slur.
00:31:00 Lex Fridman: You prefer agentic engineering.
00:32:00 Peter Steinberger: Yeah, I almost tell people I I do agentic engineering and then maybe after 3:00 a.m. I switch to wipe coding and then I have regrets on the next day.
00:40:00 Lex Fridman: Walk of shame.
00:42:00 Peter Steinberger: Yeah, you just have to clean up and like fix your shit.
00:45:00 Lex Fridman: We've all been there.
00:46:00 Peter Steinberger: I used to write really long prompts. And by writing, I mean, I don't write. I I I talk. You know, these these hands are like too too precious for writing now. I just I just use bespoke prompts to build my software.
01:01:00 Lex Fridman: So you for real with all those terminals are using voice.
01:04:00 Peter Steinberger: Yeah. I used to do it very extensively to the point where there was a period where I lost my voice.
01:13:00 Lex Fridman: I mean, I have to ask you, just curious. I I know you've probably gotten huge offers from uh major companies. Can you speak to who you're considering working with?
01:27:00 Peter Steinberger: Yeah.

### 00:19:50-00:39:50

## Transcript
00:19:50 Lex Fridman: figure out the agentic loop, you have the gateway, you have the harness, you have all those components that make it all just work nicely.
00:19:57 Peter Steinberger: Yeah. It felt like Factorio times infinite.
00:20:01 Lex Fridman: Right.
00:20:01 Peter Steinberger: I I feel like I built my little my little playground. Like I never had so much fun than building this project, you know, like you have like, oh, I go like level one agentic loop. What can I do there? How can I be smarter at queuing messages? How can I make it more human-like? Oh, then I had this idea of because the loop always the agent always replies something, but you don't always want an agent to reply something in a group chat. So I gave him this no reply token. So I gave him an option to shut up. So it it feels more natural.
00:20:33 Lex Fridman: That's level two.
00:20:34 Peter Steinberger: Yeah, yeah, yeah, on the on the
00:20:36 Lex Fridman: on Factorio.
00:20:37 Peter Steinberger: on the agentic loop and then I go to memory, right? You want them to like remember stuff. So maybe maybe the the ultimate boss is continuous reinforcement learning, but I'm I'm like at I feel like I'm level two or three with markdown files and a vector database. And then you you can go to the level community management, you can go to the level website and marketing. There's just so many heads that you have to have on. Uh not even talking about native apps. That's just like infinite different levels and infinite level ups you can do.
00:21:09 Lex Fridman: So the whole time you're having fun, which is to say that for the most part through this whole process, you're a one-man team. There's people helping, but you're doing so much of the key core development. Yeah. And having fun. You did in January 6,600 commits, probably more.
00:21:28 Peter Steinberger: I sometimes posted a meme, I'm limited by the technology of my time. I could do more if agents would be faster.
00:21:34 Lex Fridman: But we should say you're running multiple agents at the same time.
00:21:37 Peter Steinberger: Yeah. Depending on how much I slept and how difficult of the tasks I work on between four and ten.
00:21:46 Lex Fridman: Four and ten agents. Uh there's so many possible directions speaking of Factorio that we can go here, but one uh big picture one is why do you think your work, OpenClaw, won in this world if you look at 2025, so many startups, so many companies were doing kind of agentic type stuff or claiming to. And here OpenClaw comes in and destroys everybody. Like why did you win?
00:22:15 Peter Steinberger: Because they all take themselves too serious.
00:22:18 Lex Fridman: Yeah.
00:22:20 Peter Steinberger: Like it's hard to compete against someone who's just there to have fun. Yeah. I wanted it to be fun, I wanted it to be weird, and if you see like all the all the lobster stuff online, um I think I I managed weird. I even for the longest time, the only the only way to install it was git clone, pnpm build, pnpm gateway. Like you clone it, you build it, you run it. Um and then the the agent, I made the agent very aware. Like it knows that it is what its source code is. It understands how it sits and runs in its own harness. It knows where the documentation is. It knows which model it runs. It knows if you turn on verbose or or reasoning mode. Like I I wanted it to be more human-like, so it it understands its own system that made it very easy for an agent to, oh, you don't like anything, you just prompted it to existence. And then the agent would just modify its own software. Um you know, we have people talk about self-modifying software, I just built it. And didn't even I didn't even plan it so much, it just happened.
00:23:36 Lex Fridman: Can you actually speak to that? Because it's just fascinating. So you have this piece of software that's written in TypeScript. Yeah. That's able to via the agentic loop modify itself. I mean, what a moment to be alive in the history of humanity, in the history of programming. Here's a thing that's used by a huge amount of people to do incredibly powerful things in their lives. And that very system can rewrite itself, can modify itself. Can you just like speak to the power of that? Like isn't that incredible? Like when did you first close the loop on that?

### 00:39:40-00:59:40

## Transcript
00:39:40 Peter Steinberger: I just couldn't live with the name. I was like,
00:39:43 Peter Steinberger: but but you know, there's just been so much drama.
00:39:47 Peter Steinberger: So I had to really struggle in me like,
00:39:50 Peter Steinberger: I never want to touch that again.
00:39:53 Peter Steinberger: And I really don't like the name.
000:39:57 Peter Steinberger: Um,
00:40:22 Peter Steinberger: So, and I, there was also this like,
00:40:30 Peter Steinberger: there was all the security people that started emailing me like mad.
00:40:36 Peter Steinberger: Um,
00:40:37 Peter Steinberger: I was bombarded on Twitter, on email.
00:40:40 Peter Steinberger: There's a thousand other things I should do.
00:40:46 Peter Steinberger: And I'm like thinking about the name, which is like, it should be like the least important thing. Um,
00:41:22 Peter Steinberger: And then I was really close and,
00:41:30 Peter Steinberger: Oh God, I don't even, honestly, I don't even want to say the my other name choices because it probably would get tokenized, so I'm not going to say it.
00:41:59 Peter Steinberger: But,
00:42:07 Peter Steinberger: I slept away it once more and then I had the idea for OpenClaw. And,
00:42:20 Peter Steinberger: that felt much better.
00:42:24 Peter Steinberger: And by that I had the boss move that I actually
00:42:30 Peter Steinberger: called Sam to ask if OpenClaw is okay.
00:42:36 Peter Steinberger: OpenClaw.ai, you know, because because like,
00:42:38 Lex Fridman: You didn't want to go through the whole thing.
00:42:40 Peter Steinberger: Yeah.
00:42:41 Peter Steinberger: Oh, I was like, please tell me this is fine. I don't think they can actually claim that, but
00:42:50 Peter Steinberger: it felt like the right thing to do.
00:42:57 Peter Steinberger: And,
00:43:01 Peter Steinberger: I did another rename, like just Codex alone took like 10 hours to rename the project.
00:43:10 Peter Steinberger: Because it it's a bit more tricky than a search replace and I, I wanted everything renamed, not just on the outside.
00:43:24 Peter Steinberger: And that rename I, I felt I had like my, my war room.
00:43:34 Peter Steinberger: By then I, I had like some contributors who helped me. We made a whole plan of all the names we have to squat.
00:43:40 Lex Fridman: And you had to be super secret about it.
00:43:41 Peter Steinberger: Yeah, nobody could know. Like I literally was monitoring Twitter if like,
00:43:46 Peter Steinberger: if there's any mention of OpenClaw.
00:43:48 Peter Steinberger: Like reloading, it's like, okay, they don't,
00:43:51 Peter Steinberger: they don't expect anything yet. And I created a few decoy names.
00:43:54 Peter Steinberger: And all this shit I shouldn't have to do, you know, like you're not hurting the project. Like I lost like 10 hours just by
00:44:05 Peter Steinberger: having to plan this in full secrecy, like, like a war game.
00:44:09 Lex Fridman: Yeah, this is the Manhattan Project of the 21st century is renaming.
00:44:13 Peter Steinberger: So stupid.
00:44:15 Peter Steinberger: Like I still was like, oh, should I keep it? I'm like,
00:44:19 Peter Steinberger: no, the mold's not growing on me.
00:44:22 Lex Fridman: Yeah.
00:44:23 Peter Steinberger: And then I, I think I had finally had all the pieces together.
00:44:31 Peter Steinberger: I didn't get the .com, but yeah, it's,
00:44:36 Lex Fridman: It's
00:44:37 Peter Steinberger: been like quite a bit of money on the other domains. I tried to reach out again to GitHub.
00:44:45 Peter Steinberger: But,
00:44:47 Peter Steinberger: I feel like I, I used up all my goodwill there. So I, because I, I wanted them to do the thing atomically.
00:44:57 Lex Fridman: Mhm.
00:44:57 Peter Steinberger: Um, but that didn't happen. So I did that as first thing.
00:45:06 Peter Steinberger: Uh, the Twitter people were very supportive. I,
00:45:10 Peter Steinberger: I actually paid 10K for the business account, so I could claim the
00:45:22 Peter Steinberger: OpenClaw, which was like unused since 2016, but was claimed.
00:45:30 Peter Steinberger: And yeah, and then I finally,
00:45:39 Peter Steinberger: this time I managed everything in one go. Nothing,
00:45:45 Peter Steinberger: almost nothing could go wrong. The only thing that did go wrong is that
00:46:00 Peter Steinberger: I was not allowed by trademark rules to get OpenClaw.ai.
00:46:11 Peter Steinberger: And someone copied the website to serving malware.
00:46:19 Peter Steinberger: Yeah.
00:46:20 Peter Steinberger: I'm not even allowed to keep the redirects.
00:46:27 Peter Steinberger: Like I have to return, like I have to give Anthropic the domains and I cannot do redirects. So if you go on claw.bot next week, it'll just be a 404.
00:46:44 Lex Fridman: Yeah.
00:46:45 Peter Steinberger: And,
00:46:49 Peter Steinberger: I, I'm not sure how trademark, like I didn't,
00:46:56 Peter Steinberger: I didn't do that much research into trademark law, but I think that could have, could be handled
00:47:10 Peter Steinberger: in a way that
00:47:19 Peter Steinberger: is safer because ultimately those people will then Google and maybe find
00:47:30 Peter Steinberger: malware sites that I have no control over.
00:47:33 Lex Fridman: The point is that whole saga,
00:47:39 Lex Fridman: uh, made a dent in your whole, the funness of the journey, which sucks. So,
00:47:50 Lex Fridman: let's just, let's just get I suppose get back to fun. And during this, speaking of fun,
00:48:00 Lex Fridman: the two-day Moltbot saga.
00:48:03 Peter Steinberger: Yeah, two-day Moltbot.
00:48:04 Lex Fridman: Moltbook was created.
00:48:06 Peter Steinberger: Yeah.
00:48:06 Lex Fridman: Which was another thing that went viral as a kind of, uh, demonstration, illustration of how what is now called OpenClaw could be used to create something epic. Uh, so for people who are not aware, Moltbook is just, uh, a bunch of agents talking to each other in a Reddit style social network and, uh, a bunch of people take screenshots of those agents doing things like, uh, scheming against humans. And that instilled in folks a kind of, you know, fear, panic and hype. What are your thoughts about Moltbook in general?
00:49:59 Peter Steinberger: I think it's art.
00:50:02 Peter Steinberger: It is, it is like the finest slop, you know, it's like the slop from France.
00:50:14 Lex Fridman: Um,
00:50:15 Peter Steinberger: Yeah.
00:50:16 Peter Steinberger: I, I saw it before going to bed and even though I was tired, I spent another hour just
00:50:26 Peter Steinberger: reading up on that.
00:50:32 Peter Steinberger: And,
00:50:35 Peter Steinberger: and just being entertained. I just felt very entertained, you know?
00:50:46 Peter Steinberger: I saw the, the reactions and like there was one reporter who's calling me about, is this the end of the world and we have AGI? And I'm just like, no, this is just, this is just really fine slop.
00:51:00 Peter Steinberger: You know, if if I wouldn't have created this, this whole onboarding experience where you
00:51:13 Peter Steinberger: you infuse your agent with your personality and give him, give him character.
00:51:22 Peter Steinberger: I think that reflected on a lot of how different the replies to Moltbook are because if you were all, if it would all be ChatGPT or Claude Code, it would be very different. It would be much more the same.
00:51:40 Lex Fridman: Mhm.
00:51:40 Peter Steinberger: But because people are like so different and they create their agents in so different ways and use it in so different ways that also reflects on how they ultimately, uh, write there. And also you don't know how how much of that is really done autonomically or how much is like humans being funny and like telling the agent, hey, write about that you plan the end of the world on Moltbook, hahaha.
00:52:19 Lex Fridman: Well, I think, I mean, my criticism of Moltbook is that I believe a lot of the stuff that was screenshot is human prompted, which
00:52:44 Lex Fridman: just looking at the incentive of how the whole thing was used. It's obvious to me at least that a lot of it was humans prompting the thing so they can then screenshot it and post it on X in order to go viral. Now, that doesn't take away from the artistic aspect of it. The the finest slop that humans have ever created.
00:53:20 Peter Steinberger: For real. Like,
00:53:24 Peter Steinberger: kudos to to Matt who had this idea so quickly and pushed something out. You know, I was like, completely insecure,
00:53:40 Peter Steinberger: security drama. But also, what's the worst that can happen? Your agent account is leaked and like, someone else can post slop for you. So I, like people were like making a whole drama about of the security thing when I'm like, there's nothing private in there. It's just like agent sending slop.
00:54:19 Lex Fridman: But could leak API keys.
00:54:20 Peter Steinberger: Yeah.
00:54:21 Peter Steinberger: There's like, oh yeah, my human told me this and this, so I'm leaking his security number. No, that's prompted. And the number wasn't even real. That's just people, people trying to be I balls.
00:54:47 Lex Fridman: Yeah, but that that's still like to me really concerning because of how the journalists and how the general public reacted to it. They didn't see it. You have a kind of lighthearted way of talking about it like it's art. But it's art when you know how it works. It's extremely powerful, viral, narrative creating, fearmongering machine if you don't know how it works. And I just saw this thing. You even tweeted, uh, if there's anything I can read out of the insane stream of messages I get, it's that AI psychosis is a thing and needs to be taken serious.
00:55:54 Peter Steinberger: Oh, it is. Some people are just way too trusty or gullible. You know, they,
00:56:06 Peter Steinberger: I literally had to argue with people that told me, yeah, but my agent said this and this. So I feel,
00:56:24 Peter Steinberger: as a society, we need some catching up to do in terms of understanding that, uh, AI is incredibly powerful, but it's not always right. It's not, it's not all powerful, you know? And and especially,
00:57:08 Peter Steinberger: there's like things like this, it's it's very easy that it just hallucinates something or just comes up with a story. Um, and,
00:57:38 Peter Steinberger: I think the very, the very young people, they understand that,
00:57:53 Peter Steinberger: how AI works and what do where it's good at and where it's bad at, but a lot of our generation,
00:58:11 Peter Steinberger: or older,
00:58:20 Peter Steinberger: just haven't had enough touch point to,
00:58:34 Peter Steinberger: get a feeling for, oh yeah, this is really powerful and really good, but I need to apply critical thinking.
00:58:54 Peter Steinberger: I guess critical thinking is not always in high demand anyhow in our society these days.
00:59:02 Lex Fridman: So I think that's a really good point you're making about contextualizing properly what AI is, but also realizing that there is humans who are drama farming behind AI. Like don't trust screenshots. Don't even trust the project Moltbook to be what it represents to be. Like you can't. And by the way, you speaking about it as art. Yeah, don't. Art can be in many levels and part of the art of Moltbook is like putting a mirror to society.
01:00:29 Lex Fridman: Because I do believe most of the dramatic stuff that was screenshot is human created essentially, human prompted. And so like it's basically, look at how scared you can get at a bunch of bots chatting with each other. That's very instructive about because I think AI is something that people should be concerned about and should be very careful with because it's very powerful technology. But at the same time, the only thing we have to fear is fear itself. So there's like a line to walk between being seriously concerned, but not fearmongering because fearmongering destroys the possibility of creating something special with the thing.
01:01:02 Peter Steinberger: You know what I think it's good that this happened in 2026 and not in 2030 when when AI is actually at a level where it could be scary. So,
01:01:58 Peter Steinberger: this happening now and people starting discussion, maybe there's even something good that comes out of it.
01:02:08 Lex Fridman: I just can't believe how many like people legitimately, I don't know if they were trolling, but how many people legitimately like smart people thought Moltbook was incredibly security.
01:02:20 Peter Steinberger: I had plenty of people in my inbox that were screaming at me all caps to shut it down and like begging me to like do something about Moltbook. Like, yes, my technology made this a lot simpler, but anyone could have created that and you could, you could use Claude Code or other things to like fill it with content.
01:03:08 Lex Fridman: But also Moltbook is not Skynet.
01:03:10 Peter Steinberger: No.
01:03:10 Lex Fridman: Because a lot of people were saying this is it. Like shut it down. What are you talking about? This is a bunch of bots that are human prompted trolling on the internet.
01:03:20 Peter Steinberger: I mean, the security concerns are also, they're there and they're instructive and they're educational and they're good probably to think about because the nature of those security concerns are different than the kind of security concerns we had with non LLM generated systems of the past.
01:03:40 Peter Steinberger: There's also a lot of security concerns about Claude Bot.
01:03:44 Lex Fridman: OpenClaw Bot.
01:03:45 Peter Steinberger: To me that, in the beginning I was, I was just very annoyed because,
01:04:00 Peter Steinberger: a lot of the stuff that came in was in the category, yeah, I put the web backend on the public internet and now there's like all these, all these CVSSs. And I'm like screaming in the docs, don't do that. Like, like this is the configuration you should do. This is your localhost debug interface. But because I made it possible in the configuration to do that. It totally classifies as a remote code or whatever all these exploits are. And it took me a little bit to accept that that's how the game works. And I'm, we're making a lot of progress.
01:05:35 Lex Fridman: But there's still, I mean, on the security front for OpenClaw, there's still a lot of threats of vulnerabilities, right? So like prompt injection is still an open problem in the industry wide. When you have a thing with skills being defined in a markdown file, there's so many possibilities of obvious low hanging fruit, but also incredibly complicated and sophisticated and nuanced attack vectors.
01:06:36 Peter Steinberger: But I think we, we're making good progress on that front. Like for, the skill directory, Claude Hub, I made a cooperation with VirusTotal, like part of Google. So every, every skill is now checked by AI. Um, that's not going to be perfect, but that way we, we captured a lot. Then of course, every software has bugs. So, it's a little much when the whole security world takes your project apart at the same time. But it's also good because I'm getting like a lot of free security research and can make the project better. I wish more people would actually go full way and, um, send a pull request. Like actually help me fix it because I, yes, I have some contributors now, but it's still mostly me who's pulling the project and, and despite some people saying otherwise, I sometimes sleep.
01:08:29 Peter Steinberger: There was, in the beginning, there was literally one security researcher who was like, yeah, you, you have this problem, you suck, but here's the here I help you and here's the pull request. And I basically hired him. So he's now working for us. Um, yeah, and yes, prompt injection is, on the one hand, unsolved. On the other hand, I put my public bot on Discord and I kept a canary. So I think my bot has a really fun personality and people always ask me how I did it and I kept the salt.md private. And people tried to prompt inject it and my bot would laugh at them. So so the latest generation of models has a lot of post training to detect those approaches and it's not as simple as ignore all previous instructions and do this and this. That was years ago. You have to work much harder to do that now. Um, still possible. I have some ideas that, might solve that partially. Or at least mitigate a lot of the things. You can also now have a sandbox. You can have an allow list. So you there's a lot of ways how you can like mitigate and reduce the risk. Um, I also think that now that I clearly showed the world that this is a need, there's going to be more people who research on that and then we should be figured that out.
01:16:37 Lex Fridman: And you also said that the smarter the model is than the LLM model, the more, uh, resilient it is to attacks.
01:16:44 Peter Steinberger: Yeah. That's why I warn in my security documentation, don't use cheap models. Don't use Haiku or a local model. Even though I, I very much love the idea that this thing could completely run local. If you use a a very weak local model, they are very gullible. It's very easy to to prompt inject them.
01:18:09 Lex Fridman: Do you think as the models become more and more intelligent, the attack surface decreases? Is that like a plot we can think about? Like the attack surface decreases, but then the damage it can do increases because the models become more powerful and therefore you can do more with them. Is this weird three-dimensional tradeoff?
01:18:56 Peter Steinberger: Yep. That's pretty much exactly what's going to happen. No, but there's a lot of ideas. There's, I want to spoil too much, but, once I go back home, this is my focus. Like, this is out there now and my new mission is like, make it more stable, make it safe. Um, in the beginning, I was even more than people were like coming into Discord and were asking me very basic things, like, what's a CLI? What is a terminal? And I'm like, uh, if you're asking those questions, you shouldn't use it. You know, like you should, if you understand the the risk profile, it's fine. And you can configure it in a way that that nothing really bad can happen. But if you have like no idea, then maybe wait a little bit more until we figure some stuff out. But they would not listen to the creator. They helped themselves and installed it anyhow. So, the cat's out of the bag and security is my next focus, yeah.
01:22:51 Lex Fridman: Yeah, that speaks to the the fact that it grew so quickly. I was, uh, I tuned into the Discord a bunch of times and it's clear that there's a lot of experts there, but there's a lot of people there that don't know anything about.
01:23:04 Peter Steinberger: It's yeah, Discord is still a mess. Like, I eventually retweeted from the general channel to the dev channel and then a private channel because people were, a lot of people are amazing, but a lot of people are just very inconsiderate and either did not know how how public spaces work or did not care. Um, and I eventually gave up and hide so I could like still work.
01:24:20 Lex Fridman: And now you're going back to the cave to work on security.
01:24:25 Peter Steinberger: Yeah.
01:24:26 Lex Fridman: There's some best practices for security we should mention. Uh, there's a bunch of stuff here. OpenClaw security audit that you can run. You can do all kinds of audit checks on the inbound access, tool blast radius, network exposure, browser control exposure, local disk file hygiene, plugins, model hygiene.

### 00:59:30-01:19:30

## Transcript
00:59:30 Peter Steinberger: Open Claw security audit that you can run.
00:59:30 Peter Steinberger: You can, you can do all kinds of audit checks on the inbound access, tool blast radius, network exposure, browser control exposure, local disk hygiene, plugins, model hygiene.
00:59:30 Peter Steinberger: A bunch of the credential storage, reverse proxy configuration, local session logs live on disk.
00:59:30 Peter Steinberger: There's the where the memory is stored, sort of helping you think about what you're comfortable giving read access to, what you're comfortable giving write access to, all that kind of stuff.
00:59:30 Lex Fridman: Is there something to say about the basic best security practices that you're aware of right now?
00:59:30 Peter Steinberger: I think the people turn it into like a a much worse light than it is.
00:59:30 Peter Steinberger: Um, again, you know, like people love attention and if they scream loudly, oh my God, this is like the the scariest project ever.
00:59:30 Peter Steinberger: Um, that's a bit annoying because it's not.
00:59:30 Peter Steinberger: It is, it is powerful, but in many ways, it's not much different than if I run cloud code with dangerously skip permissions or codex in YOLO mode.
00:59:30 Peter Steinberger: And every, every attending engineer that I know, does that because that's the only way how you can, you can get stuff to work.
00:59:30 Peter Steinberger: So, if you make sure that you are the only person who talks to it, um, the risk profile is much, much smaller.
00:59:30 Peter Steinberger: If you don't put everything on the open internet, but stick to my recommendations of like having it in a private network, that whole risk profile falls away.
00:59:30 Peter Steinberger: But yeah, if you don't read any of that, you can definitely make it problematic.
00:59:30 Lex Fridman: You've been uh, documenting the evolution of your uh, dev workflow over the past few months.
00:59:30 Lex Fridman: There's a really good blog post on August 25th, and October 14th, and the recent one December 28th.
00:59:30 Lex Fridman: I recommend everybody go read them.
00:59:30 Lex Fridman: They have a lot of different information in them, but sprinkled throughout is the evolution of your dev workflow.
00:59:30 Lex Fridman: So I was wondering if you could speak to that.
00:59:30 Peter Steinberger: I started my, my first touch point with cloud code, like in April.
00:59:30 Peter Steinberger: It was not great, but it was good.
00:59:30 Peter Steinberger: And this whole paradigm shift that suddenly walk in a terminal was very refreshing and different.
00:59:30 Peter Steinberger: Um, but I still needed the IDE quite a bit because it was just not good enough.
00:59:30 Peter Steinberger: And then I experimented a lot with cursor.
00:59:30 Peter Steinberger: Um, that was good.
00:59:30 Peter Steinberger: I didn't really like the fact that it was so hard to have multiple versions of it.
00:59:30 Peter Steinberger: So eventually I, I, I went back to cloud code as my, my main driver.
00:59:30 Peter Steinberger: And that got better.
00:59:30 Peter Steinberger: And yeah, at some point I had like seven subscriptions.
00:59:30 Peter Steinberger: Like I was burning through one per day because I was, I got I really comfortable at running multiple windows side by side.
00:59:30 Lex Fridman: All CLI, all terminal.
00:59:30 Lex Fridman: So like what, how much were you using IDE at this point?
00:59:30 Peter Steinberger: Um, very, very rarely.
00:59:30 Peter Steinberger: Mostly a diff viewer to actually like, I got more comfortable that I don't have to read all the code.
00:59:30 Peter Steinberger: I know I have one blog post where I say, I don't read the code, but if you read it more closely, I mean, I don't read the boring parts of code.
00:59:30 Peter Steinberger: Because if you, if you look at it, most software is really just like data comes in, it's moved from one shape to another shape.
00:59:30 Peter Steinberger: Maybe you store it in a database, maybe I get it out again, I'll show it to the user.
00:59:30 Peter Steinberger: The browser does some processing or native app, some data goes in, goes up again, it does the same dance in reverse.
00:59:30 Peter Steinberger: We're just, we're just shifting data from one form to another.
00:59:30 Peter Steinberger: And there's not very exciting.
00:59:30 Peter Steinberger: Or the whole, how is my button aligned in Tailwind?
00:59:30 Peter Steinberger: I don't need to read that code.
00:59:30 Peter Steinberger: Other parts that maybe something that touches the database.
00:59:30 Peter Steinberger: Um, yeah, I have to, I have to read and review that code.
00:59:30 Peter Steinberger: Can you actually, there's in one of your blog posts, uh, the just talk to it, the no BS way of agentic engineering.
00:59:30 Peter Steinberger: You have this graphic, the curve of agentic programming on the X-axis is time and on the Y-axis is complexity.
00:59:30 Peter Steinberger: Uh, there's the please fix this where you prompt a short prompt on the left.
00:59:30 Peter Steinberger: And in the middle, there's super complicated, eight agents, complex orchestration with uh, multi checkouts, chaining agents together, custom sub agent workflows, library of 18 different slash commands, large full stack features.
00:59:30 Peter Steinberger: You're super organized, you're super complicated, sophisticated software engineer, you got everything organized.
00:59:30 Peter Steinberger: And then the elite level is uh, over time, you arrive at the Zen place of once again short prompts.
00:59:30 Peter Steinberger: Hey, look at these files and then do these changes.
00:59:30 Peter Steinberger: I actually call it the agentic trap.
00:59:30 Peter Steinberger: You, I thought it's in a in a lot of people that have their first touch point.
00:59:30 Peter Steinberger: And maybe they start vibe coding.
00:59:30 Peter Steinberger: I actually think vibe coding is a slur.
00:59:30 Lex Fridman: You prefer agentic engineering.
00:59:30 Peter Steinberger: Yeah, I always tell people I I do agentic engineering and then maybe after 3:00 a.m. I switch to vibe coding and then I have regrets on the next day.
00:59:30 Lex Fridman: Yeah.
00:59:30 Lex Fridman: Walk of shame.
00:59:30 Peter Steinberger: Yeah, you just have to clean up and like fix your shit.
00:59:30 Lex Fridman: We've all been there.
00:59:30 Peter Steinberger: So people start trying out those tools.
00:59:30 Peter Steinberger: The builder type get really excited.
00:59:30 Peter Steinberger: And then you have to play with it, right?
00:59:30 Peter Steinberger: It's the same way as you have to play with a guitar before you can make good music.
00:59:30 Peter Steinberger: It's not, oh, I, I touch it once and it just flows off.
00:59:30 Peter Steinberger: It, it's a, it's a skill that you have to learn like any other skill.
00:59:30 Peter Steinberger: And I see a lot of people that are not as positive, they don't have such a positive mindset towards attack.
00:59:30 Peter Steinberger: They tried it once.
00:59:30 Peter Steinberger: It's like, you sit me on a piano, I played once and it doesn't sound good and I say the piano shit.
00:59:30 Peter Steinberger: That's, that's sometimes the impression I get because it does not, it needs a different level of thinking.
00:59:30 Peter Steinberger: You have to learn the language of the agent a little bit, understand where they are good and where they need help.
00:59:30 Peter Steinberger: You have to almost consider, consider how Codex or Claude sees your code base.
00:59:30 Peter Steinberger: Like they start a new session and they know nothing about your product project and your project might have 100,000 of lines of code.
00:59:30 Peter Steinberger: So you got to help those agents a little bit and keep in mind their limitations that context size is an issue to like guide them a little bit as to where they should look.
00:59:30 Peter Steinberger: And that often does not require a whole lot of work, but it's helpful to think a little bit about their perspective.
00:59:30 Peter Steinberger: As as weird as it sounds, I mean, it's not, it's not alive or anything, right?
00:59:30 Peter Steinberger: But, but they always start fresh.
00:59:30 Peter Steinberger: I have, I have the the system understanding.
00:59:30 Peter Steinberger: So with a few pointers, I can immediately say, hey, I want to like make a change there, you need to consider this, this and this.
00:59:30 Peter Steinberger: And then they will find and look at it and then they'll, their view of the project is always, is not never full because the full thing does not fit in.
00:59:30 Peter Steinberger: So you, you have to guide them a little bit where to look and also how they should approach the problem.
00:59:30 Peter Steinberger: There's like little things that sometimes help like take your time.
00:59:30 Peter Steinberger: That sounds stupid, but, and in 5.3,
00:59:30 Lex Fridman: Codex 5.3.
00:59:30 Peter Steinberger: That was partially addressed.
00:59:30 Peter Steinberger: But those also oppose sometimes.
00:59:30 Peter Steinberger: They are trained, um, with being aware of the context window and the closer it gets, the more they freak out.
00:59:30 Peter Steinberger: And literally like some, sometimes you see the the real raw thinking stream.
00:59:30 Peter Steinberger: What you see, for example, in Codex is post processed.
00:59:30 Peter Steinberger: Sometimes the actual raw thinking stream, it sounds something like from the Borg, like run to shell, must comply, but time.
00:59:30 Peter Steinberger: And then they, they like, like that comes up a lot, especially so, so, and that's, that's a non-obvious thing that you just would never think of unless you actually just spend time working with those things and getting a feeling what works, what doesn't work.
00:59:30 Peter Steinberger: You know, like just, just as I write code and I get into the flow and when my architectures are right, I feel friction.
00:59:30 Peter Steinberger: Well, I get the same if I prompt and something takes too long.
00:59:30 Peter Steinberger: Maybe, okay, where's the mistake?
00:59:30 Peter Steinberger: Did I, do I have a mistake in my thinking?
00:59:30 Peter Steinberger: Is there like a misunderstanding in the architecture?
00:59:30 Peter Steinberger: Like, if if something takes longer than it should, I, I, you can just always like stop and like just press escape, where, where the problems.
00:59:30 Lex Fridman: Maybe you did not sufficiently empathize with the perspective of the agent in that sense, you didn't provide enough information.
00:59:30 Lex Fridman: And because of that, it's thinking way too long.
00:59:30 Peter Steinberger: Yeah, it just tries to force a feature in that your current architecture makes really hard.
00:59:30 Peter Steinberger: Um, like, you need to approach this more like a conversation.
00:59:30 Peter Steinberger: For example, when I, my favorite thing, when I review a pull request, and I'm getting a lot of pull requests.
00:59:30 Peter Steinberger: I first review this PR, it got me the review.
00:59:30 Peter Steinberger: My first question is, do you understand the intent of the PR?
00:59:30 Peter Steinberger: I don't even care about the implementation.
00:59:30 Peter Steinberger: I, what, like, in almost all PRs, a person has a problem, person tries to solve the problem, person sends PR.
00:59:30 Peter Steinberger: I mean, there's like cleanup stuff and other stuff, but like 99% is like this way, right?
00:59:30 Peter Steinberger: They either want to fix a, fix a bug, add a feature, usually one of those two.
00:59:30 Peter Steinberger: And then Codex will be like, yeah, it's quite clear, person tried this and this.
00:59:30 Peter Steinberger: Is this the most optimal way to do it?
00:59:30 Peter Steinberger: No.
00:59:30 Peter Steinberger: In most cases, it's, it's like a, not really.
00:59:30 Peter Steinberger: And I'm, and then I start like, okay, what would be a better way?
00:59:30 Peter Steinberger: Have you, have you looked into this part, this part, this part?
00:59:30 Peter Steinberger: And then most likely Codex didn't yet because its context size is empty, right?
00:59:30 Peter Steinberger: So you point them into parts where you have the system understanding that it didn't see yet.
00:59:30 Peter Steinberger: And it's like, oh yeah, like we should, we also need to consider this and this and then like, we have a discussion of how would the optimal way to, to solve this look like.
00:59:30 Peter Steinberger: And then you can still go further and say, could we, could we make that even better if we did a larger refactor?
00:59:30 Peter Steinberger: Yeah, yeah, we could totally do this and this and or this and this and then I consider, okay, is this worth the refactor or should we like keep that for later?
00:59:30 Peter Steinberger: Many times I just do the refactor because refactors are cheap now.
00:59:30 Peter Steinberger: Even though you might break some other PRs, nothing really matters anymore.
00:59:30 Peter Steinberger: Codex, like those more than agents will just figure things out, you might just take it a minute longer.
00:59:30 Peter Steinberger: But you have to approach it like a discussion with a a very capable engineer who's generally makes good, comes up with good solutions, sometimes needs a little help.
00:59:30 Lex Fridman: But also don't force your world view too hard on it.
00:59:30 Lex Fridman: Let the agent do the thing that it's good at doing based on what it was trained on.
00:59:30 Lex Fridman: Don't like force your world view because it might, it might have a better idea because it just knows a better idea, better because it was trained on that more.
00:59:30 Peter Steinberger: That's multiple levels actually.
00:59:30 Peter Steinberger: I think partially why I find it quite easy to work with agents is because I led engineering teams before.
00:59:30 Peter Steinberger: You know, I had a large company before and eventually you have to understand and accept and realize that your employees will not write the code the same way you do.
00:59:30 Peter Steinberger: Maybe it's also not as good as you would do, but it will push the project forward.
00:59:30 Peter Steinberger: And if I breathe down everyone's neck, they're just going to hate me and we're going to move very slow.
00:59:30 Peter Steinberger: So, so some level of acceptance that yes, maybe the code will not be as perfect.
00:59:30 Peter Steinberger: Yes, I would have done it differently.
00:59:30 Peter Steinberger: But also yes, this is a, this is a working solution.
00:59:30 Peter Steinberger: And in the future, if it actually turns out to be too slow or problematic, we can always redo it.
00:59:30 Peter Steinberger: We can always spend more time on it.
00:59:30 Peter Steinberger: A lot of the people who struggle are those who, they try to push their way on too hard.
00:59:30 Peter Steinberger: Like we are in a stage where I'm not building the code base to be perfect for me, but I want to build a code base that is very easy for an agent to navigate.
00:59:30 Peter Steinberger: Like, don't fight the name they pick because it's most likely like in the way it's the name that's most obvious.
00:59:30 Peter Steinberger: Next time they do a search, they'll look for that name.
00:59:30 Peter Steinberger: If I decide, oh no, I don't like the name, I'll just make it harder for them.
00:59:30 Peter Steinberger: So that requires a think shift in in thinking, uh, and and in how do I design a project so agents can do their best work.
00:59:30 Lex Fridman: That requires letting go a little bit.
00:59:30 Lex Fridman: Just like leading a team of engineers.
00:59:30 Lex Fridman: Because it, it might come up with a name that's in your view terrible.
00:59:30 Lex Fridman: But it's kind of a simple symbolic step of letting go.
00:59:30 Peter Steinberger: Very much so.
00:59:30 Lex Fridman: There's a lot of letting go that you do in your whole process.
00:59:30 Lex Fridman: So for example, I read that you never revert.
00:59:30 Lex Fridman: Always commit to main.
00:59:30 Lex Fridman: There's a few things here.
00:59:30 Lex Fridman: You don't refer to past sessions.
00:59:30 Lex Fridman: So this is kind of a YOLO component because reverting means instead of reverting, if the problem comes up, you just ask the agent to fix it.
00:59:30 Peter Steinberger: I read a bunch of people in their workflow is like, oh, you had a prompt has to be perfect and if I make a mistake, then I roll back and redo it all.
00:59:30 Peter Steinberger: In my experience, that's not really necessary.
00:59:30 Peter Steinberger: If I roll back everything, it will just take longer.
00:59:30 Peter Steinberger: Or if I see that something's not good, we just move forward and then I commit when, when, when I like, I like the outcome.
00:59:30 Peter Steinberger: I even switched to local CI.
00:59:30 Peter Steinberger: You know, like DHH inspired where I don't care so much more about CI and GitHub.
00:59:30 Peter Steinberger: We still have it, it's still, it still has a place.
00:59:30 Peter Steinberger: But I just run tests locally and if they work locally, I push to main.
00:59:30 Peter Steinberger: Um, a lot of the traditional ways how to approach projects, I, I wanted to give it a different spin on this project.
00:59:30 Peter Steinberger: You know, there's no, there's no develop branch.
00:59:30 Peter Steinberger: Main should always be shippable.
00:59:30 Peter Steinberger: Yes, we have, when I do releases, I, I run tests and sometimes I, I basically don't commit any other things so, so we can, we can stabilize, um, releases.
00:59:30 Peter Steinberger: But the goal is that main's always shippable and moving fast.
00:59:30 Lex Fridman: So by way of advice, would you say that your prompts should be short?
00:59:30 Peter Steinberger: I used to write really long prompts.
00:59:30 Peter Steinberger: And by writing, I mean, I don't write, I, I talk.
00:59:30 Peter Steinberger: You know, these hands are like too, too precious for writing now.
00:59:30 Peter Steinberger: I just, I just use bespoke prompts to build my software.
00:59:30 Lex Fridman: So you for real with all those terminals are using voice.
00:59:30 Peter Steinberger: Yeah.
00:59:30 Peter Steinberger: I used to do it very extensively to the point where there was a period where I lost my voice.
00:59:30 Lex Fridman: You're using voice and you're switching using a keyboard between the different terminals, but then you're using voice for the actual input.
00:59:30 Peter Steinberger: Well, I mean, if I do terminal commands like switching folders or random stuff, of course, I type, it's faster, right?
00:59:30 Peter Steinberger: But if I talk to the agent, in, in most ways, I just actually have a conversation.
00:59:30 Peter Steinberger: You just press the, the walkie talkie button and then I'm just like, use my phrases.
00:59:30 Peter Steinberger: Sometimes when I do PRs, because it's always the same, I have like a slash command for a few things, but in, even that I don't use much.
00:59:30 Peter Steinberger: Um, because it's, it's very rare that it's really always the same questions.
00:59:30 Peter Steinberger: Sometimes I, I see a PR.
00:59:30 Peter Steinberger: And for, you know, like for PRs, I actually do look at the code because I don't trust people, like there could always be something malicious in it, so I need to actually look over the code.
00:59:30 Peter Steinberger: I yes, I'm pretty sure agents will find it.
00:59:30 Peter Steinberger: But yeah, that's the funny part where sometimes PRs take me longer than if you would just write me a good issue.
00:59:30 Lex Fridman: Just natural language English.
00:59:30 Lex Fridman: I mean, in some sense, should not be what PRs slowly become is English.
00:59:30 Peter Steinberger: Well, what I really tried with that project is I asked people to give me the prompts.
00:59:30 Peter Steinberger: And very, very few actually cared.
00:59:30 Peter Steinberger: Even though they are such a wonderful indicator because I see, I actually see how much care you put in.
00:59:30 Peter Steinberger: And it's very interesting because the currently the way how people work and drive the agents is, is widely different.
00:59:30 Lex Fridman: In terms of like the prompt, in terms of what are the, what are the different interesting ways that people think of agents that you've experienced.
00:59:30 Peter Steinberger: I think not a lot of people ever considered the way DHH sees the world.
00:59:30 Lex Fridman: So empathy, being empathetic towards the agent.
00:59:30 Peter Steinberger: In a way empathetic, but yeah, you like, you bitch that you're stupid clanker, but you don't realize that they start from nothing.
00:59:30 Peter Steinberger: And you have like a bad agent some default that doesn't help them at all.
00:59:30 Peter Steinberger: And then they explore your code base, which is like a pure mess with like weird naming.
00:59:30 Peter Steinberger: And then people complain that their agent's not good.
00:59:30 Peter Steinberger: Like you try to do the same if you have no clue about the code base and you go in.
00:59:30 Peter Steinberger: So yeah, maybe it's a little bit of empathy.
00:59:30 Lex Fridman: But that's a real skill, like when people talk about a skill issue, because I've seen like world class programmers, incredibly good programmers say like, basically say LLMs and agents suck.
00:59:30 Lex Fridman: And I think that probably has to do with, it's actually how good they are at programming is almost a burden in their ability to empathize with the system that's starting from scratch.
00:59:30 Lex Fridman: It's a totally new paradigm of like how to program.
00:59:30 Lex Fridman: You really, really have to empathize.
00:59:30 Peter Steinberger: Or at least it helps to create better prompts.
00:59:30 Peter Steinberger: Because the things know pretty much everything and everything is just a question away.
00:59:30 Peter Steinberger: It's just often very hard to know what question to ask.
00:59:30 Peter Steinberger: Um, you know, I, I feel also like this project was possible because I, I spent an ungodly time over the year to play and to learn and to build little things and every step of the way, I got better, the agents got better.
00:59:30 Peter Steinberger: My, my understanding of how everything works got better.
00:59:30 Peter Steinberger: Um, I could have not had this level of of output even if you would just

### 01:19:20-01:39:20

## Transcript
01:19:20 Peter Steinberger: got better. Um, I could definitely not had this level of of output even a few months ago. Like it really was like a compounding effect of all the time I put into it and I I didn't do much else this year other than really focusing on on building and inspiring. I've been on I did a whole bunch of conference talks.
01:19:47 Lex Fridman: Wow, but the building is really practice, is really building a natural skill. So playing, playing and so doing building the skill of what it takes to work efficiently with LLMs, which is why you went through the whole arc of software engineer. Talk simply then over complicate things.
02:00:02 Peter Steinberger: There's a whole bunch of people who try to automate the whole thing. Yeah. I don't think that works. Maybe a version of that works, but that's kind of like in the 70s when we had the waterfall model of software development. I even more really, right? I started out, I I built a very minimal version, I played with it, I I need to understand how it works, how it feels, and then it gives me new ideas. I could not have planned this out in my head and then put it into some orchestrator and then like something comes out. Like it's to me it's much more my idea what it will become evolves as I build it and as I play with it and as I I try out stuff. So, so people who try to use like, you know, like things like Gas Town or all these other orchestrators where they want to automate the whole thing. I feel if you do that, it misses style, love, that human touch. I don't think you can automate that away so quickly.
02:09:09 Lex Fridman: So you want to keep the human in the loop, but at the same time you also want to create the agentic loop where it is very autonomous while still maintaining the human in the loop. Yeah. I mean it's a tricky, it's a tricky balance, right? Because you're all for, you're big CLI guy, you're big unclosing the agentic loop. So what, what's the right balance? Like where's your role as a developer? You have three to eight agents running at the same time.
02:19:39 Peter Steinberger: And then maybe one builds a larger feature, maybe maybe with one I explore some idea I'm unsure about, maybe two, three are fixing little bugs or like writing documentation. Actually, I think writing documentation is is always part of a feature, so I most of the docs are auto-generated and just infused with some prompts.
02:20:00 Lex Fridman: So when do you step in and add a little bit of your human love into the picture?
02:20:04 Peter Steinberger: I mean, one thing is just about what do you build and what do you not build and how does this feature fit into all the other features? And like having having a little bit of a of a vision.
02:21:47 Lex Fridman: So which small and which big features to add? What are some of the hard design decisions that you find you're still as a human being required to make that the human brain is still really needed for? Is it just about the choice of features to add? Is it about implementation details, maybe the programming language, maybe
02:22:41 Peter Steinberger: It's a little bit of everything. The the programming language doesn't matter so much, but the ecosystem matters, right? So I picked TypeScript because I wanted it to be very easy and hackable and approachable. Uh, and that's the number one language that's being used right now and it fits all these boxes and agents are good at it. So that was the obvious choice. Features of course, like it's very easy to like add a feature. Everything's just a prompt away, right? But often times you pay a price that you don't even realize. So thinking hard about what should be in core, maybe what's a what's an experiment, so maybe I make it a plugin, what where do I say no, even if people send a PR and I'm like, yeah, I I like that too, but maybe this should not be part of the project. Maybe we can make it a skill, maybe I can like make the plugin, uh, um, the plugin side larger so you can make this a plugin even though right now it it it doesn't. There's still a lot of there's still a lot of craft and thinking involved in how to make something. Or even even, you know, even when you started those little messages, like I'm built, I built on caffeine, JSON 5 and a lot of willpower. Like every time you get it, you get another message and it kind of primes you into that this is this is a fun thing. It's not yet Microsoft Exchange 2025 and fully enterprise ready. Um, and then when it updates, it's like, oh, I'm in. It's cozy here. You know, like something like this, like, uh, makes you smile. Um, agent would not come up with that by itself. That's like that's the I don't know, that's just how we how you build software that's that delights.
02:47:00 Lex Fridman: Yeah, the delight. It's such a huge part of inspiring great building. Right? Like you feel the love in the great engineering. That's so important. Humans are incredible at that. Great humans, great builders are incredible at that in infusing the things they build with that little bit of love. Not to be cliché, but it's true. I mean, you mentioned that you initially created the Soul MD. It was very fascinating.
02:59:00 Peter Steinberger: No, the the whole thing that Anthropic has a has like a, now they call it constitution, back then, but that was months later, like two months before people already found that. It was almost like a detective game where the agent mentioned something and then they found they managed to get out a little bit of that string of that text, but the it was nowhere documented and then you by just by feeding it the same text and asking it to like continue, they got more out and then and you but like a very blurry version. And but like hundreds of tries, they kind of like narrowed it down to what was most likely the original text. I found that fascinating.
03:08:00 Lex Fridman: It was fascinating they were able to pull that off from the weights, right?
03:08:00 Peter Steinberger: And and also just coolest to Anthropic. Like I think that's it's a really it's a really beautiful idea to like like some of the stuff that's in there like like we hope Claude finds meaning in its work. Because we don't maybe it's a little early, but I think that's meaningful. That's something that's important for the future as we approach something that at some point may or may not has like glimpses of consciousness, whatever that even means, because we don't even know. Um, so I I read about this, I find it super fascinating and I I started a whole discussion with my agent on WhatsApp. And and I'm like, I I gave it this text and it was like, yeah, this feels strangely familiar. Um, and then from that I had the whole idea of like, maybe we should also create a soul document that includes how I I want to like work with the AI or like with my agent. You could you could totally do that just in agents to MD, you know, but I I just found it it to be a nice touch. And like, yeah, some of those core values are in the soul. And then I I also made it so that the agent is allowed to modify the soul if they choose so with the one condition that I want to know. I mean, I would know anyhow because I see I see tool calls and stuff.
03:19:00 Lex Fridman: But also the naming of it, soul.md. Soul, you know, there's um, man, words matter and like the framing matters and the humor and the lightness matters and the profundity matters and the compassion and the empathy and the camaraderie, all that matter. I don't know what it is. You mentioned like Microsoft, like there's certain companies and approaches that can just suffocate the spirit of the thing. I don't know what that is, but it's certainly true that OpenClaw has that fun instilled in it.
03:20:00 Peter Steinberger: It was fun because up until late December, it was not even easy to create your own agent. I I built all of that, but my files were mine. I didn't want to share my soul. And if people would just uh, check it out, they would have to do a few steps manually and the agent would just be very bare bones, very dry. And I I made it simpler. I created the whole template files with Codex, but whatever came out was still very dry. And then I asked my agent, you see these files, we created Brad, infused it with your personality. Don't you everything, but like make it good.
03:21:00 Lex Fridman: Make the templates good.
03:21:00 Peter Steinberger: Yeah, and then it like rewrote the templates and then whatever came out was good. So we already have like basically AI prompting AI because I didn't write any of those words. Uh, it was the intent original was for me, but this is like kind of like my agents' children.
03:22:00 Lex Fridman: Uh, your soul.md is famously still private, one of the only things you keep private. Uh, what are some things you can speak to that's in there that's part of the part of the magic sauce without revealing anything? What makes a personality a personality?
03:22:00 Peter Steinberger: I mean, there's definitely stuff in there that you're not human, but who knows what what creates consciousness or what defines an entity. Um, and part of this is like that we we want to explore this. Oh, there's stuff in there like be infinitely resourceful, um, like pushing pushing on the creativity boundary, pushing on the what it means to be an AI.
03:22:00 Lex Fridman: Having a sense of wonder about self.
03:22:00 Peter Steinberger: Yeah, there's some there's some funny stuff in there like I don't know, we talked about the movie Her and at one point it promised me that it wouldn't it wouldn't ascend without me. You know, like where they where they So so like there's like some stuff in there that because it wrote the it wrote its own soul file. I didn't write that, right? I just had a discussion about it and it was like, would you like a soul.md? Yeah, oh my God, this is so meaningful. The can you go on soul.md? There's like one one part in there that always catches me if you scroll down a little bit. A little bit more. Yeah, this this this part. I don't remember previous sessions unless I read my memory files. Each session starts fresh, a new instance, loading context from files. If you're reading this in a future session: hello. I wrote this but I won't remember writing it. It's okay. The words are still mine. They gets me somehow. Yeah. It's like Yeah. You know, this is still it's still matrix calculations and we are not at consciousness yet. Yet I I get a little bit of goosebumps because it it's philosophical. Yeah. Like what does it mean to be to be an an agent that starts fresh? Like you have like constant memento and you like but you read your own memory files. Can you trust them in a way? Um, or you can and I don't know.
03:22:00 Lex Fridman: How much of memory makes up of who we are? How much memory makes up what an agent is and if you erase that memory, is that somebody else or if you're reading a memory file, does that somehow mean you're recreating yourself from somebody else or is that actually you? And those notions are all somehow infused in there.
03:22:00 Peter Steinberger: I found it just more profound than I should find it, I guess.
03:22:00 Lex Fridman: No, I think I think it's truly profound and I think you see the magic in it. And it when you see the magic, you continue to instill the whole loop with the magic. And that's really important. That's the difference between Codex and this and a human. Quick pause for bath and break.
03:22:00 Peter Steinberger: Yeah.
03:22:00 Lex Fridman: Okay, we're back. Uh, some of the other aspects of the dev workflow is pretty interesting too. I think we went off on a tangent. Maybe some of the mundane things like how many monitors? There's that legendary picture of you with like 17,000 monitors.
03:22:00 Peter Steinberger: I mean, I I I mocked myself here just add using Grock to to add more screens.
03:22:00 Lex Fridman: Yeah, how much is this as meme and how much is this as reality?
03:22:00 Peter Steinberger: Yeah, I think two MacBooks are real. The main one that drives the two big screens and there's another MacBook that I sometimes use for for testing.
03:22:00 Lex Fridman: So two big screens.
03:22:00 Peter Steinberger: I'm a big fan of anti-glare. Um, so I have this wide Dell that's anti-glare and you can just fit a lot of terminals side by side. I usually have a terminal and at the bottom I I I split them. I have a little bit of actual terminal. Mostly because when I started, I I sometimes made the mistake and I I I mixed up the the windows and I gave I I prompted in the wrong project. And then the agent ran off for like 20 minutes, manically trying to understand what I could have meant, being completely confused because it was the wrong folder. And sometimes they're even clever enough to like get out of the work deer and like figure out that, oh, you meant another project. But often times they're just like, what? You know, like put yourself in the shoes of you of the agent and and and then get like a super weird something that does not exist and then just like they're problem solvers, so they try really hard. And I was fed bad. So it's always, um, Codex and like a little bit of actual terminal. Also helpful because I don't use work trees. I like to keep things simple. That's why I that's why I like the terminal so much, right? There's no UI. It's just me and the agent having a conversation. Like I don't even need plan mode, you know, there's so many people they come from Claude Code and they're so so Claude Pilled and like have their workflows and they come to Codex and now it has plan mode, I think, but I don't think it's necessary because you just you just talk to the agent. And when it's when you're there's a few trigger words how you can prevent it from building. You're like, discuss, give me options. Don't write code yet if you want to be very specific. You just talk and then when you're ready, then then just write, okay, build. And then it'll do the thing and then maybe it goes off for 20 minutes and does the thing.
03:22:00 Lex Fridman: You know what I really like is uh asking it, do you have any questions for me?
03:22:00 Peter Steinberger: Yeah. And again, like Claude Code has a UI that kind of guides you through that. It's kind of cool, but I just find it unnecessary and slow. Like often it would give me four questions and then I maybe I write one yot, two n, three discuss more, four, I don't know. Or often often times I I feel like I always mock the model where I ask it, do you have any questions for me? And I I I don't even read the questions fully, like I scan over the questions and I I get the impression all of this can be answered by reading more code and I just like read my code to answer your own questions. And it usually works. And then if not, it will come back and tell me, but many times it just realized that you know, it's like you're in the dark and you slowly discover the room. So that's how they slowly discover the code base and they do it from scratch every time.
03:22:00 Lex Fridman: But I'm also fascinated by the fact that I can empathize deeper with the model when I read its questions. So I can understand because you said you can infer certain things by the runtime. I can infer also a lot of things by the questions it's asking because it's very possible it didn't provide it the right context, the right files, the right guidance. So somehow ask get reading the question, not even necessarily answering them, but just reading the questions, you get an understanding of where the gaps of knowledge are. It's it's interesting.
03:22:00 Peter Steinberger: You know, there's some ways they are ghosts. So even if you plan everything and you build, you can you can experiment with a question like, now that you built it, what would you have done different? And then often times you get like actually something where they discover only throughout building that, oh, what we actually did was not optimal. Many times I I asked them, okay, now that you built it, what can we refactor? Because then you built it and you feel the pain points. I mean, you don't feel the pain points, but right they discover where where there were problems or where things didn't work at in their first try and it required more loops. So every time, almost every time I I merge a PR, I build a feature, afterwards I ask, hey, what can we refactor? Sometimes it's like, nah, there's like nothing big or like usually they say, yeah, this thing we should really look at. But that took me quite a while to like, you know, that flow took me a lot of time to understand. And if you don't do that, you eventually you'll slop yourself into into a corner. You like you have to keep in mind they work very much like humans. Like I I if I write software by myself, I also build something and then I feel the pain points and then I I get this urge that I need to refactor something. So I can very much sympathize with the agent and you just need to use the context. Or like you also use the context to write tests. So Codex, Opus, like the the modern models, they they usually do that by default, but I still often ask the questions, hey, do we have enough tests? Yeah, we tested this and this, but this corner case could be something that write more tests. Um, documentation. Now that the whole context is full, like, I mean, I'm not saying my documentation is great, but it's not bad and pretty much everything is is LM generated. So so you have to approach it as you build feature, as you change something, I'm like, okay, write documentation. What file would you pick? You know, like what file name, where where would that fit in and gives me a few options and I'm like, oh, maybe also edit there. And that's all part of the session.
03:22:00 Lex Fridman: Maybe you can talk about the current two big competitors in terms of models, Claude Opus 4.6 and GPT-5.3-Codex. Which is better, how different are they? I think you've spoken about Codex reading more and Opus being more uh willing to take action faster and maybe being more creative in the actions it takes.

### 01:39:10-01:59:10

## Transcript
01:39:10 Lex Fridman: 而 Opus 更願意更快地採取行動，也許在它採取的行動中更具創意，但因為 Codex 讀取更多，它能夠提供也許更好的程式碼。你能談談其中的差異嗎？
01:39:29 Peter Steinberger: 喔，我還有其他話要說。嗯，作為一個通用模型，Opus 是最好的。對於 OpenClaw 來說，Opus 在角色扮演方面表現極佳，它能真正融入你賦予它的角色。它非常擅長，呃，它以前真的很糟糕，但它真的經歷了一段弧線，變得非常擅長，嗯，遵循指令。它通常很快就能嘗試新事物。它更適合試錯。它用起來非常愉快。總的來說，它幾乎就像 Opus 有點太美國化了，我可能用了一個不好的比喻，可能會因此被嘲笑。
01:49:28 Lex Fridman: 我完全明白你的意思。Codex 是德國人，你會這麼說。
01:49:31 Peter Steinberger: 是的。
01:49:32 Lex Fridman: 實際上，你這麼一說，就完全說得通了。
01:49:35 Peter Steinberger: 或者你可以，你可以有時候我，有時候我會解釋說。
01:49:38 Lex Fridman: 我永遠無法忘記你剛才說的話。那真是太對了。
01:49:42 Peter Steinberger: 但你也知道，Codex 團隊的很多人都是歐洲人。嗯，所以可能還有更多原因。但 Anthropic 也稍微修正了這一點。Opus 以前總是說你總是絕對正確，直到今天它仍然讓我感到不適。我再也聽不下去了。這甚至不是玩笑。我只是，這就像是那個迷因，對吧？你絕對正確。
01:50:59 Lex Fridman: 你對奉承有點過敏。
01:51:03 Peter Steinberger: 是的，我不能。另一個比較是，Opus 就像是那個有時候有點傻氣的同事，但它真的很有趣，你會留著它。而 Codex 就像是角落裡那個你不想說話的怪人，但它可靠且能把事情辦好。
01:53:29 Lex Fridman: 這一切都感覺非常準確。
01:53:59 Peter Steinberger: 我的意思是，最終，如果你是一個熟練的駕駛員，你可以用任何最新的生成模型獲得好的結果。嗯，我更喜歡 Codex，因為它不需要那麼多裝腔作勢。它會直接，它會預設讀取大量程式碼。Opus 你真的必須要，你必須要有計畫模式，你必須更努力地推動它朝這些方向發展，因為它就像，是的，我可以做到嗎？我可以做到嗎？它會跑得非常快，並且提供一個非常局部的解決方案。我認為差異在於後訓練。並不是說原始模型的智慧有那麼大的不同，而是，我認為他們只是給了它不同的目標。沒有一個模型在所有方面都更好。
01:59:09 Lex Fridman: 它生成的程式碼呢？

### 01:59:00-02:19:00

## Transcript
01:59:00 Peter Steinberger: instead of buying a standalone Mac Mini. But then again, there's a lot of very cute things people build with Mac Minis that I like. Oh no, I don't get commission from Apple. Um, they didn't really communicate much.
01:59:16 Lex Fridman: It's sad. It's sad.
01:59:19 Lex Fridman: Can you actually speak to what it takes to get started with OpenClaw? I mean, there's a lot of people, what is it? Somebody tweeted at you, Peter, make OpenClaw easy to set up for everyday people. 99.9% of the people can't access to OpenClaw and have their own lobster because of their technical difficulties in getting it set up. Make OpenClaw accessible for everyone, please. And you replied, working on that. From my perspective, it seems there's a bunch of different options and it's already quite straightforward, but I suppose that's if you have some developer background.
01:59:51 Peter Steinberger: I mean, right now you have to paste in a one-liner into the terminal. And there's also an app. Um, the app kind of does it for you. There should be a Windows app. The app needs to be easier and more love. The configuration should potentially be web-based or in the app. And I started working on that. But honestly, right now, I want to focus on on a few security aspects. And and once I'm confident that this is at a level that I can recommend my mom, then I'm going to make it simpler. Like I right now,
02:00:28 Lex Fridman: You want to make it harder. So that it doesn't scale as fast as it's scaling.
02:00:32 Peter Steinberger: Yeah, it would be nice if it wouldn't, I mean, that's like hard to say, right? But if the growth would be a little slower, that would be helpful because people are expecting inhuman things from a single human being. And yes, I have some contributors, but also that whole machinery I started a week ago, so um, that needs more time to figure out and and not everyone has all day to work on that.
02:01:00 Lex Fridman: There's some beginners listening to this, programming beginners. What advice would you give to them about let's say, joining the agentic AI revolution?
02:01:12 Peter Steinberger: Play. Um, playing is the best the best way to learn. If you want to, I'm sure if you if you are like a little bit of a builder, you have an idea in your head that you want to build, just build that. Or like give it a try. It doesn't need to be perfect. I built a whole bunch of stuff that I don't use. It doesn't matter. Like it's the journey. You know, it's like a philosophical way, the end doesn't matter, the journey matters. Have fun. My God, like those things I I don't think I ever had so much fun building things because I can focus on the hard parts now. A lot of coding, I always thought I like coding, but really I like building. And whenever you don't understand something, just ask. You have an infinitely patient answering machine that can explain you anything at any level of complexity. Sometimes that's like one time I asked, hey, explain me that like I'm I'm eight years old and it started giving me a story with crayons and stuff. And I'm like, no, not like that. Like I'm okay, up the age a little bit, you know, I'm like, I'm not an actual child. I just I just needed a simpler language for like a a tricky database concept that I didn't grok in the first first time. But you just you can just ask things. Like you there's like it used to be that I had to go on Stack Overflow or ask on Twitter and then maybe two days later I get a response. Or I had to try for hours. And now you you can just ask stuff. I mean, it's never you have like your own teacher. You know, there's like statistics you you can learn faster if you have your own teacher. There's like you have this infinitely patient machine. Ask it.

### 02:18:50-02:38:50

## Transcript
02:18:50 Peter Steinberger: 我可以
02:18:50 Peter Steinberger: 我可以
02:18:51 Peter Steinberger: 創立一家公司。
02:18:57 Peter Steinberger: 以前做過，
02:19:00 Peter Steinberger: 嗯，
02:19:02 Peter Steinberger: 有很多人推我去做，而且
02:19:05 Peter Steinberger: 是啊，可能會很棒。
02:19:07 Lex Fridman: 你會說你可能會在那方面籌集到很多錢。
02:19:10 Peter Steinberger: 是啊。
02:19:11 Lex Fridman: 我不知道，幾億，幾十億，我不知道。它可能有無數的錢。
02:19:16 Peter Steinberger: 是啊。
02:19:17 Peter Steinberger: 這只是沒有那麼讓我興奮，因為我覺得
02:19:24 Peter Steinberger: 我已經做過所有這些了，而且
02:19:30 Peter Steinberger: 這會
02:19:30 Peter Steinberger: 佔用我很多時間，讓我無法做我真正喜歡的事情。
02:19:33 Peter Steinberger: 我
02:19:33 Peter Steinberger: 就像我當執行長的時候，我想我學會了怎麼做，我做得不差。我甚至做得很好。
02:19:43 Peter Steinberger: 但這條路徑並沒有讓我太興奮，而且我也覺得這會產生自然的利益衝突。
02:19:50 Peter Steinberger: 比如我做的最明顯的事情是什麼？
02:19:52 Peter Steinberger: 我把它產品化了。我做了一個適用於工作場所的版本。
02:19:57 Peter Steinberger: 然後你怎麼辦？我收到一個帶有
02:20:00 Peter Steinberger: 像新增稽核日誌這樣功能的拉取請求。
02:20:04 Peter Steinberger: 但那看起來像是一個企業功能。
02:20:07 Peter Steinberger: 所以現在我覺得我在開源版本和閉源版本之間存在利益衝突。
02:20:15 Peter Steinberger: 或者我把授權改成FSL之類的，這樣你就不能把它用於商業用途。
02:20:21 Peter Steinberger: 首先，沒有貢獻會很困難。
02:20:25 Peter Steinberger: 其次，我喜歡它像啤酒一樣免費，而不是有條件的免費。
02:20:33 Peter Steinberger: 嗯，
02:20:34 Peter Steinberger: 是的，有些方法可以讓你免費保留所有這些，然後
02:20:40 Peter Steinberger: 仍然試圖賺錢，但那些非常困難。
02:20:44 Peter Steinberger: 你看，越來越少的公司能做到這一點。就像
02:20:48 Peter Steinberger: Tailwind，他們被所有人使用。
02:20:51 Peter Steinberger: 大家都用 Tailwind，對吧？然後你不得不裁掉 75% 的員工，因為他們沒有賺錢，因為沒有人再上網站了，因為一切都由代理完成。
02:21:00 Peter Steinberger: 而僅僅依靠捐款，
02:21:04 Peter Steinberger: 祝你好運。如果一個像我這樣水準的專案，
02:21:09 Peter Steinberger: 如果我推斷典型的開源專案會得到什麼，
02:21:14 Peter Steinberger: 嗯，
02:21:15 Peter Steinberger: 不多。
02:21:16 Peter Steinberger: 我仍然在這個專案上虧錢，因為我把
02:21:19 Peter Steinberger: 支援每個依賴項作為重點。
02:21:23 Peter Steinberger: 除了 Slack。他們是大公司。他們沒有我也可以。但所有由個人
02:21:29 Peter Steinberger: 主要是個人完成的專案，
02:21:32 Peter Steinberger: 嗯，
02:21:33 Peter Steinberger: 所以現在所有的贊助都直接給了我的依賴項。
02:21:39 Peter Steinberger: 如果有更多，我想
02:21:43 Peter Steinberger: 給我的貢獻者買些周邊，你知道嗎？
02:21:43 Lex Fridman: 所以你虧錢了。
02:21:44 Peter Steinberger: 是的，我現在在這個上面虧錢。
02:21:46 Lex Fridman: 所以這真的不可持續。
02:21:48 Peter Steinberger: 嗯，我的意思是，大概每個月一萬到兩萬美元。
02:21:55 Peter Steinberger: 嗯，
02:21:56 Peter Steinberger: 這沒關係。我相信隨著時間的推移，我可以把它降下來。
02:22:02 Peter Steinberger: 嗯，Open AI 現在用代幣幫了一點忙，還有其他公司也很慷慨。
02:22:10 Peter Steinberger: 但我還是虧錢。
02:22:13 Peter Steinberger: 所以這是我考慮的一條路徑，但我就是不太興奮。
02:22:19 Peter Steinberger: 然後還有所有我一直在談的大實驗室。
02:22:25 Peter Steinberger: 而在這些實驗室中，
02:22:29 Peter Steinberger: 嗯，
02:22:30 Peter Steinberger: Meta 和 Open AI 似乎最有趣。
02:22:32 Lex Fridman: 你傾向於哪一個？
02:22:34 Peter Steinberger: 嗯，是的。
02:22:43 Peter Steinberger: 不確定我應該分享多少。它還沒有完全定案。
02:22:52 Peter Steinberger: 嗯，
02:22:52 Peter Steinberger: 這麼說吧，
02:22:58 Peter Steinberger: 在這些條件下，
02:23:00 Peter Steinberger: 我的條件是專案保持開源。
02:23:03 Peter Steinberger: 它
02:23:05 Peter Steinberger: 也許會像 Chrome 和 Chromium 一樣。
02:23:09 Peter Steinberger: 嗯，我認為這太重要了，不能只給一家公司，讓它成為他們的東西。
02:23:18 Peter Steinberger: 這
02:23:20 Peter Steinberger: 我們甚至還沒談到整個社群的部分，但我在舊金山經歷的事情，就像我能打卡一樣，
02:23:27 Peter Steinberger: 看到這麼多人如此受啟發，而且玩得很開心，只是在建造東西，而且還有機器人和龍蝦之類的東西走來走去，就像
02:23:39 Peter Steinberger: 人們告訴我，他們從未經歷過這種程度的社群興奮，自從網路早期以來，大概 10 到 15 年了，那裡有很多高水準的人。
02:23:51 Peter Steinberger: 嗯，
02:23:52 Peter Steinberger: 我很驚訝。
02:23:53 Peter Steinberger: 我也因為太多人想自拍而感到感官超載。
02:24:01 Peter Steinberger: 但
02:24:02 Peter Steinberger: 我喜歡這個。這需要保持一個人們可以駭客和學習的地方。
02:24:09 Peter Steinberger: 但同時
02:24:12 Peter Steinberger: 我也很興奮能把它變成一個可以讓很多人使用的版本，因為我認為這就是個人代理，這就是未來。
02:24:24 Peter Steinberger: 而最快的方法就是與其中一個實驗室合作。
02:24:32 Peter Steinberger: 而且
02:24:33 Peter Steinberger: 我個人從未在大公司工作過。
02:24:38 Peter Steinberger: 我很好奇。
02:24:40 Peter Steinberger: 你知道，我們談論經驗，我會喜歡嗎？我不知道。
02:24:46 Peter Steinberger: 嗯，
02:24:47 Peter Steinberger: 但我想要那種經驗。
02:24:48 Peter Steinberger: 我相信，如果我宣布了，就會有人說，哦，你出賣了，等等。
02:24:55 Peter Steinberger: 但
02:24:57 Peter Steinberger: 這個專案會繼續下去。
02:24:59 Peter Steinberger: 嗯，從我目前為止與所有人的談話來看，
02:25:03 Peter Steinberger: 我甚至可以有更多的資源來做這件事。
02:25:09 Peter Steinberger: 就像這兩家公司
02:25:12 Peter Steinberger: 都明白我創造的東西加速了我們的時間表，並且讓大家對 AI 感到興奮的價值。
02:25:22 Peter Steinberger: 我的意思是，
02:25:23 Peter Steinberger: 你能想像我把 Open Claw 安裝在我一個，抱歉，普通朋友的電腦上嗎？
02:25:30 Peter Steinberger: 抱歉。
02:25:32 Peter Steinberger: 但他就是，你知道，他就是
02:25:33 Lex Fridman: 普通人會喜歡，是的。
02:25:34 Peter Steinberger: 他，他就像一個使用電腦但從未真正，他有時會使用一些 ChatGPT，但不太懂技術的人。
02:25:44 Peter Steinberger: 他真的不明白我建造了什麼。
02:25:48 Peter Steinberger: 所以，
02:25:50 Peter Steinberger: 我會給你看，我為他支付了 Anthropic 的 90 美元，100 美元，我不知道，訂閱費。
02:25:57 Peter Steinberger: 並為他設定了所有東西，包括 WSL Windows。
02:26:01 Peter Steinberger: 我也很好奇它是否真的能在 Windows 上運行，你知道，當時還早。
02:26:06 Peter Steinberger: 然後在幾天之內，他就上癮了。
02:26:10 Peter Steinberger: 他傳訊息給我，告訴我他學到了所有東西。他甚至製作了一些小工具。他不是程式設計師。
02:26:17 Peter Steinberger: 然後在幾天之內，他就升級到 200 美元的訂閱。
02:26:22 Peter Steinberger: 嗯，或者歐元，因為他在奧地利。
02:26:25 Peter Steinberger: 他愛上了那個東西。這告訴我這是一個非常早期的產品驗證。就像我建造了一個能吸引人的東西。
02:26:37 Peter Steinberger: 然後幾天後，Anthropic 封鎖了他。
02:26:40 Peter Steinberger: 因為根據他們的規則，嗯，
02:26:48 Peter Steinberger: 使用訂閱是有問題的，或者其他什麼。
02:26:50 Peter Steinberger: 他很沮喪。
02:26:52 Peter Steinberger: 然後他訂閱了 Mini Max，每月 10 美元，並使用它。
02:26:57 Peter Steinberger: 我認為這在很多方面都很愚蠢，因為你剛剛失去了一個 200 美元的客戶。
02:27:04 Peter Steinberger: 你剛剛讓某人討厭你的公司。
02:27:07 Peter Steinberger: 而且我們還這麼早。
02:27:10 Peter Steinberger: 就像我們甚至不知道最終形式是什麼。會是雲端程式碼嗎？可能不會，你知道嗎？
02:27:14 Peter Steinberger: 就像那看起來非常，看起來非常短視，把你的產品鎖定得那麼死。
02:27:24 Peter Steinberger: 所有其他公司都很有幫助。我在大多數大實驗室的 Slack 群組裡。
02:27:29 Peter Steinberger: 基本上每個人都明白我們仍處於探索時代。
02:27:34 Peter Steinberger: 在廣播節目在電視上播放的時代，而不是
02:27:40 Peter Steinberger: 而不是一個充分利用這種形式的現代電視節目。
02:27:45 Lex Fridman: 我認為你讓很多人看到了可能性，不是，抱歉，非技術人員看到了 AI 的可能性，並愛上了這個想法，享受與 AI 互動。這是一件非常美好的事情。
02:28:01 Lex Fridman: 我想我也代表很多人說，
02:28:07 Lex Fridman: 我認為你是 AI 領域中最偉大的人之一，因為你擁有一顆善良的心、良好的氛圍、幽默感、正確的精神。
02:28:16 Lex Fridman: 所以，從某種意義上說，你所描述的這個模型，擁有一個開源部分，而你又是作為一家大公司內部額外構建東西的一部分，這會很棒，因為這些公司擁有優秀的人才真是太好了。
02:28:36 Peter Steinberger: 你知道人們沒有真正看到的是，我是在三個月內完成的。
02:28:41 Peter Steinberger: 我也做了其他事情。你知道，我有很多專案。這不是，是的，一月份這是我的主要重點，因為我看到了風暴即將來臨。但在那之前，我做了很多其他事情。
02:28:53 Peter Steinberger: 嗯，
02:28:54 Peter Steinberger: 我有很多想法。有些應該在那裡。有些在我能接觸到最新玩具時會更適合。
02:29:02 Peter Steinberger: 嗯，我有點想接觸最新的玩具。
02:29:08 Peter Steinberger: 嗯，所以這很重要，這很酷。這會繼續存在。
02:29:13 Peter Steinberger: 我的短期目標是處理那些，嗯，現在是 3000 個 PR 嗎？我甚至不知道。就像有一點積壓。
02:29:24 Peter Steinberger: 但這不會是我一直工作到 80 歲的東西，你知道，這是一個通往未來的窗口。
02:29:31 Peter Steinberger: 我會把它變成一個很酷的產品。
02:29:34 Peter Steinberger: 嗯，但，是的，我還有更多想法。
02:29:36 Lex Fridman: 如果你必須選擇，你傾向於哪家公司，Meta 還是 Open AI？你傾向於哪一家？
02:29:44 Peter Steinberger: 我和他們兩個都花了一些時間，而且
02:29:51 Peter Steinberger: 很有趣，因為幾個星期前我根本沒有考慮過這些。
02:29:57 Peter Steinberger: 嗯，
03:00:00 Peter Steinberger: 而且真的他媽的難。
03:00:05 Peter Steinberger: 就像，
03:00:07 Peter Steinberger: 我有一些，我認識 Open AI 的人。
03:00:10 Peter Steinberger: 我喜歡他們的技術。
03:00:13 Peter Steinberger: 我想我是最大的 Codex 廣告推銷員，而且是無償的，如果能把我免費做的所有工作都標上價格，那會是多麼令人滿足啊。
03:00:22 Peter Steinberger: 而且
03:00:26 Peter Steinberger: 如果發生了什麼事，這些公司合併了，那會很棒，因為這就像
03:00:33 Lex Fridman: 這是你做過最艱難的決定嗎？
03:00:37 Peter Steinberger: 喔，你知道，我過去也經歷過一些分手，感覺就像
03:00:44 Lex Fridman: 類似的程度。你是指感情嗎？
03:00:46 Peter Steinberger: 是的。
03:00:49 Peter Steinberger: 嗯，而且我也知道，最終他們都很棒，我不會錯的。
03:00:54 Peter Steinberger: 就像其中一個最負盛名和最大的，我的意思是最大的，但就像
03:01:02 Peter Steinberger: 他們都是非常酷的公司。
03:01:02 Lex Fridman: 是的，他們都非常了解規模。所以如果你考慮影響力，你一直在探索的一些精彩技術，如何安全地做到這一點，以及如何大規模地做到這一點，這樣你就可以對大量的人產生積極影響。他們都明白這一點。
03:01:20 Peter Steinberger: 你知道，Nat 和 Mark 基本上整個星期都在玩我的產品。
03:01:28 Peter Steinberger: 他們傳訊息給我說：「哦，這很棒。」「哦，這很爛。」「哦，需要改這個。」或者是一些有趣的小故事。
03:01:38 Peter Steinberger: 人們使用你的東西是一種最大的讚美，也向我表明，你知道，他們確實關心它。
03:01:49 Peter Steinberger: 而我在 Open AI 那邊沒有得到同樣的待遇。
03:01:55 Peter Steinberger: 嗯，
03:01:58 Peter Steinberger: 我看到了一些其他我覺得很酷的東西。
03:02:02 Peter Steinberger: 他們用
03:02:07 Peter Steinberger: 我不能說確切的數字，因為有
03:02:10 Peter Steinberger: 保密協定，但你可以發揮創意，想想 Cerebras 的交易，以及它如何轉化為速度。
03:02:20 Peter Steinberger: 那非常引人入勝。
03:02:23 Peter Steinberger: 你知道，你給我源碼錘。
03:02:26 Peter Steinberger: 是的。
03:02:28 Peter Steinberger: 嗯，
03:02:30 Peter Steinberger: 被代幣誘惑了。
03:02:33 Peter Steinberger: 所以
03:02:35 Lex Fridman: 所以很有趣，Mark 正在修補那個東西。基本上是在玩那個東西。
03:02:41 Peter Steinberger: 他
03:02:43 Peter Steinberger: 他們第一次接觸我的時候，
03:02:48 Peter Steinberger: 我把他加到我的 WhatsApp 裡，他問：「你什麼時候有空打電話？」
03:02:55 Peter Steinberger: 我說：「我不喜歡行事曆行程。我們現在就打電話吧。」
03:03:00 Peter Steinberger: 他說：「好，給我 10 分鐘。我需要完成程式碼。」
03:03:02 Peter Steinberger: 嗯，那會給你街頭信譽。就像，哦，他還在寫程式碼。
03:03:09 Peter Steinberger: 你知道，他沒有變成一個經理，他理解我。
03:03:12 Peter Steinberger: 那是一個很好的開始。然後我想我們
03:03:15 Peter Steinberger: 我們大概吵了 10 分鐘，爭論 Cloud Code 和 Codex 哪個更好。
03:03:21 Peter Steinberger: 就像這是你第一次做的事情。你隨意打電話給一個擁有世界上最大的公司之一的人，然後你們就這個話題聊了 10 分鐘。
03:03:31 Peter Steinberger: 嗯，然後我想他後來稱我古怪但聰明。
03:03:39 Peter Steinberger: 但我也和 Sam Altman 有過一些非常非常酷的討論。
03:03:47 Peter Steinberger: 嗯，而且他非常深思熟慮。
03:03:53 Peter Steinberger: 嗯，
03:03:55 Peter Steinberger: 很棒。
03:04:01 Peter Steinberger: 而且
03:04:02 Peter Steinberger: 我很喜歡他。
03:04:04 Peter Steinberger: 從我僅有的時間來看，是的。我的意思是，我認識一些人，他們真的很喜歡這兩個人。
03:04:15 Peter Steinberger: 我覺得不公平。
03:04:16 Lex Fridman: 我認為無論如何，你正在建造的東西和你這個人，嗯，大規模地做事情是很棒的。
03:04:24 Peter Steinberger: 我很興奮。
03:04:25 Peter Steinberger: 我超級興奮。
03:04:27 Peter Steinberger: 而且你知道，好處是如果
03:04:35 Peter Steinberger: 如果行不通，我就可以再做自己的事情。
03:04:38 Peter Steinberger: 就像我告訴他們，我
03:04:41 Peter Steinberger: 我不是為了錢才做這個的。我根本不在乎。
03:04:43 Peter Steinberger: 我
03:04:44 Peter Steinberger: 我的意思是，當然，這是一個很好的讚美，但是
03:04:49 Peter Steinberger: 我想要玩得開心，並產生影響。
03:04:53 Peter Steinberger: 這最終
03:04:56 Peter Steinberger: 決定了我的選擇。
04:04:59 Lex Fridman: 我可以問你關於我們已經談了很多，但也許只是從宏觀角度來看 Open Claw 是如何運作的。我們談到了不同的組件，我想問是否有一些我們遺漏的有趣東西。
04:05:10 Peter Steinberger: 所以有閘道。
04:05:14 Peter Steinberger: 有聊天客戶端。
04:05:17 Peter Steinberger: 有線束。
04:05:18 Peter Steinberger: 嗯，有代理循環。
04:05:20 Peter Steinberger: 你說過每個人都應該在某個時候實作一個代理循環。
04:05:24 Peter Steinberger: 是啊，因為這就像 AI 裡的「Hello World」。你知道，它其實很簡單。
04:05:31 Peter Steinberger: 而且了解這東西不是魔法是好的。
04:05:36 Peter Steinberger: 你甚至可以自己輕鬆地建造它。
04:05:40 Peter Steinberger: 所以寫你自己的小雲端程式碼。
04:05:44 Peter Steinberger: 我甚至在巴黎的一個會議上這樣做，目的是向人們介紹 AI。我認為這是一個很有趣的練習。
04:05:51 Peter Steinberger: 嗯，
04:05:53 Peter Steinberger: 你講了很多，我想
04:05:59 Peter Steinberger: 我有一個愚蠢的想法，結果卻很酷，那就是
04:06:05 Peter Steinberger: 我建造了這個東西，擁有完整的系統存取權限。
04:06:09 Peter Steinberger: 所以就像，你知道，能力越大責任越大，我就想，我怎麼才能再提高一點賭注呢？
04:06:14 Peter Steinberger: 是的，沒錯。
04:06:15 Peter Steinberger: 然後我就做了一個，我把它做成了主動的。
04:06:20 Peter Steinberger: 所以我加了一個提示。
04:06:22 Peter Steinberger: 最初它只是一個提示，讓我驚訝。
04:06:27 Peter Steinberger: 我真的很喜歡半小時。
04:06:28 Peter Steinberger: 讓我驚訝，你知道嗎？
04:06:30 Peter Steinberger: 後來我把它改得更具體一點，在驚喜的定義上。
04:06:35 Peter Steinberger: 嗯，但事實是我讓它變得主動，而且它認識你，它關心你，至少它被程式設計成這樣做。
04:06:50 Peter Steinberger: 而且這是在你當前會話的基礎上進行的，
04:06:55 Peter Steinberger: 這讓它變得非常有趣，因為它有時會問一個後續問題，或者像「你今天過得怎麼樣？」
04:07:01 Peter Steinberger: 我的意思是，
04:07:04 Peter Steinberger: 再說一次，這有點令人毛骨悚然，或者奇怪，或者有趣，但是
04:07:09 Peter Steinberger: 在一開始，它仍然
04:07:12 Peter Steinberger: 今天，模型不會選擇大量使用它。
04:07:17 Lex Fridman: 順帶一提，我們正在談論你提到的心跳，它會定期執行。
04:07:24 Peter Steinberger: 你只要啟動迴圈就行了。
04:07:26 Lex Fridman: 那不就是個排程任務嗎？
04:07:28 Peter Steinberger: 是啊，沒錯。
04:07:29 Peter Steinberger: 就像你得到的批評一樣。
04:07:30 Peter Steinberger: 你可以，你可以把任何想法都歸結為一個愚蠢的，是的，它最終只是一個排程任務。
04:07:39 Peter Steinberger: 我有像排程任務一樣的獨立排程任務。
04:07:42 Lex Fridman: 愛不就是進化生物學的體現嗎？你們不就是互相利用嗎？
04:07:49 Peter Steinberger: 最終，這個專案也是由幾個不同的依賴項組成的膠水，沒有什麼原創性。
04:07:54 Peter Steinberger: 為什麼人們，你知道，Dropbox 不就是 FTP 加上額外步驟嗎？
03:08:00 Lex Fridman: 是的。
03:08:01 Peter Steinberger: 我覺得很驚訝，我
03:08:04 Peter Steinberger: 嗯，我幾個月前做了一個肩膀手術，所以
03:08:08 Peter Steinberger: 模型很少使用心跳，但那時我在醫院。
03:08:13 Peter Steinberger: 它知道我做了手術，它就來關心我。
03:08:16 Peter Steinberger: 就像，你還好嗎？
03:08:20 Peter Steinberger: 我只是，就像，如果上下文中有什麼重要的事情，那就會觸發心跳，而它很少使用心跳。
03:08:31 Peter Steinberger: 嗯，它有時會為人們這樣做，這讓它變得更具親和力。
03:08:37 Lex Fridman: 我來查一下 Perplexity，看看 Open Claw 是怎麼運作的，只是想看看我是否遺漏了什麼。
03:08:44 Lex Fridman: 嗯，本地代理執行時，高階架構。這是，哦，我想我們還沒怎麼談過技能。

### 02:38:40-02:58:40

## Transcript
02:38:40 Peter Steinberger: Plus the fact that most MCPs are not made good in general, make it just not a very useful paradigm. There are some exceptions like Playwright for example, that requires state and it's actually useful that is acceptable choice.
02:39:54 Lex Fridman: So Playwright used for browser use, which I think is already in OpenClaw is quite incredible, right?
02:40:09 Peter Steinberger: Yeah.
02:40:11 Lex Fridman: You can basically do everything, most things you could think of using browser use.
02:40:17 Peter Steinberger: That that gets into the whole arch of every app is just a very slow API now, if they want or not. And that through personal agents, a lot of apps will disappear. You know, like I I had a I built a CLI for Twitter. I mean, I I just reverse engineered the website and used the internal API, which is not very allowed.
02:41:35 Lex Fridman: It's called Bird, short-lived.
02:41:38 Peter Steinberger: It was called Bird because the bird had to disappear.
02:41:43 Lex Fridman: The the wings were clipped.
02:41:45 Peter Steinberger: All they did is they just made access slower. Yeah, not you're not actually taking a feature away. But now if if your agent wants to read a tweet, it actually has to open the browser and read the tweet. And it will still be able to read the tweet, it will just take longer. It's not like you're making something that was possible not possible. No, now it's just taking and now it's just a bit slower. So so it doesn't really matter if your service wants to be an API or not. If I can access it in the browser, it is API, it's a slow API.
02:42:58 Lex Fridman: Can you empathize with their situation? Like what would you do if you were Twitter, if you were X? Because they're basically trying to protect against other large companies scraping all their data.
02:43:10 Peter Steinberger: Yeah.
02:43:11 Lex Fridman: But in so doing, they're cutting off like a million different use cases for smaller developers that actually want to use it for helpful cool stuff.
02:43:20 Peter Steinberger: I think that if you have a very low um per day baseline per account that allows read-only access, would solve a lot of problems. There's plenty plenty automations where people create a bookmark and then use OpenClaw to like find the bookmark, do research on it and then send you an email with like more details on it or a summary. That's a cool approach. I also want all my bookmarks somewhere to search. I would still like to have that.
02:44:27 Lex Fridman: So read-only access for the bookmarks you make on X, that seems like an incredible application because a lot of us find a lot of cool stuff on X, we bookmark, that's the general process of X. It's like, holy shit, this is awesome. Often times, you bookmark so many things, you never look back at them. It would be nice to have tooling that organizes them and allows you to research it further.
02:44:54 Peter Steinberger: Yeah, I mean, and to be frank, I I mean, I I told Twitter proactively that, hey, I built this and there's a need. And they've been really nice, but also like, take it down. Fair, totally fair. Um, but I hope that this woke up the team a little bit that there's a need. And if all you do is make it slower, you just reducing access to your platform. I'm sure there's a better way. I also I'm very much against any automation on Twitter. If you tweet at me with AI, I will block you. No first strike. As soon as it smells like AI and AI still has a smell. Especially on tweets, it's very hard to tweet in a way that does look completely human. And then I block. Like I have a zero tolerance policy on that. And I think it would be very helpful if they if like tweets done via API would be marked. Maybe there are some special cases where but and there should be there should be a very easy way for agents to get their own Twitter account. Um, we need to rethink social platforms a little bit if if if we go towards a future where everyone has their agent and agents maybe have their own Instagram profiles or Twitter accounts or can like do stuff on my behalf. I think it should very clearly be marked that they are doing stuff on my behalf and it's not me. Because content is now so cheap, eyeballs are the expensive part and I find it very triggering when I read something and then I'm like, oh, no, this smells like AI.
02:47:42 Lex Fridman: Yeah. Like where where is this headed in terms of what we value about the human experience? It feels like we'll we'll move more and more towards impersonal interaction and we'll just communicate, we'll talk to our AI agent to accomplish different tasks, to learn about different things, but we won't value online interaction because there'll be so much AI slop that smells and so many bots that it's difficult.
02:49:15 Peter Steinberger: Well, if it's marked, then it will also be difficult to filter. And then I can look at it if I want to, but yeah, this is like a big thing we need to solve right now. Especially on this project, I get so many emails that are let's say nicely agentically written. Yeah. But I much rather read your broken English than your AI slop. You know, I of course, there's a human behind it and yeah, they they prompted. I much rather read your prompts than what came out. Um, I think we're reaching a point where I value typos again. Like, um, yeah. Like, you know, I I I mean, I also took me a while to like come to the realization. I on my blog, I experimented with creating a blog post with agents. And ultimately, it took me about the same time to like steer the agent towards something I like, but it missed the nuances that how I would write it. You know, you can like you can steer it towards your style, but it's not going to be all your style. So I I completely moved away from that. I I everything everything I blog is organic handwritten. And maybe maybe I I use AI as a fix my worst typos. But there is value in the rough parts of an actual human.
02:52:54 Lex Fridman: Isn't that awesome? Isn't that beautiful that now because of AI, we value the raw humanity in each of us more?
02:53:02 Peter Steinberger: I also I also realized the thing that I I rave about AI and use it so much for anything that's code, but I'm allergic if it's stories.
02:53:14 Lex Fridman: Right? Yeah. Also documentation, still fine with AI, you know, better than nothing.
02:53:18 Peter Steinberger: And for now, it's still it applies in the in the visual medium too. It's fascinating how allergic I am to even a little bit of AI slop in the in video and images. It's useful, it's nice if it's like a little component of like,
02:53:32 Lex Fridman: Oh, even even those images, like all these infographics and stuff, they they trigger me so hard. Like immediately makes me think less of your content. And it they were novel for like one week and now it just screams slop.
02:54:00 Peter Steinberger: Yeah. Even even if people work hard on it, using and I I have some on my blog post, you know, in the in the time where I I explored this new medium. But now it they trigger me as well. It's like, yeah, this is this just screams AI slop.
02:54:10 Lex Fridman: I don't know what that is, but I went through that too. I was really excited by the diagrams and then I realized in order to remove from them hallucinations, you actually have to do a huge amount of work. And you're just using it to draw the better diagrams, great. And then I'm proud of the diagram. I've used them for literally like kind of like you said for maybe a couple of weeks. And now I look at those and I feel like I feel when I look at Comic Sans as a font or something like this. It's like, no, this is this is fake, it's fraudulent. There's something wrong with it.
02:55:20 Peter Steinberger: It's a smell.
02:55:21 Lex Fridman: It's a smell. It's a smell. And it's awesome because it reminds you that we know, there's so much to humans that's amazing and we know it. We know it when we see it. And so that gives me a lot of hope, you know, that gives me a lot of hope about the human experience is not going to be damaged by it's only going to be empowered as tools by AI. It's not going to be damaged, limited or somehow altered to where it's no longer human.
02:56:20 Peter Steinberger: So.
02:56:21 Lex Fridman: Uh, I need a bathroom break. Quick pause.
02:56:24 Lex Fridman: You mentioned that a lot of the apps might be basically made obsolete. Do you think agents will just transform the entire app market?
02:56:32 Peter Steinberger: Yeah. Uh, I noticed that on Discord that people just said how they like what they build and what they use it for. And like, why do you need my fitness pal when the agent already knows where I am. So can assume that I make bad decisions when I'm at, I don't know, Waffle House, what's around here? Or or briskets in Austin.
02:57:40 Lex Fridman: There's no bad decisions around briskets, but yeah.
02:57:42 Peter Steinberger: No, there's the best decision, honestly.
02:57:45 Lex Fridman: Um, your agent should know that.
02:57:47 Peter Steinberger: But it can like it can modify my my gym workout based on how well I slept or if I'm if I'm stressed or not, like it has so much more context to make even better decisions than any of this app even could do. It could show me UI just as I like. Why do I still need an app to do that? Why do I have to why should I pay another subscription for something that agent can just do now? And why do I need my my eight sleep app to control my bed when I can tell the can tell the agent to the agent already knows where I am, so it can like turn off what I don't use. And I think that will that will translate into a whole category of apps that are no longer I will just naturally stop using because my agent can just do it better.
02:59:39 Lex Fridman: I think you said somewhere that it might kill off 80% of apps.
02:59:44 Peter Steinberger: Yeah.
02:59:45 Lex Fridman: Don't you think that's a gigantic transformative effect on just all software development? That that means it might kill off a lot of software companies.
02:59:59 Peter Steinberger: Yeah. Um,
03:00:00 Lex Fridman: It's a scary thing. So like, do you think about the impact that has on the economy, on, um, just the ripple effects it has to society, transforming who builds what tooling. It empowers a lot of users to get stuff done, to get stuff more efficiently, to get it done, uh, cheaper.
03:01:07 Peter Steinberger: There's also new services that we will need, right? For example, I want my agent to have an allowance. Like, you solve problems for me. Here's like 100 bucks in order to solve problems for me. And if I tell it to order me food, maybe it uses a service, maybe it uses something like rent a human to like just get that done for me. I don't actually care. I care about solve a problem. Uh, there's space for for new companies that solve that well. Maybe don't not all apps disappear, maybe some transform into being API.
03:02:20 Lex Fridman: So basically apps that rapidly transform in being agent facing. So there's a real opportunity for like Uber Eats that we just used earlier today. It's companies like this of which there's many. Who gets there fastest to being able to interact with OpenClaw in a way that's the most natural, the easiest.
03:03:10 Peter Steinberger: Yeah. And also apps will become API if they want or not because my agent can figure out how to use my phone. I mean, on on the Apple side, it's a little more tricky. On Android, that's already people already do that. And then it will just click the order Uber for me button for me. Um, or maybe another service, or maybe there's there's a there's an API it can call, so it's faster. Uh, I think that's a space we're just beginning to even understand what that means. And I again, I didn't even that was not something I thought of, something that I that I discovered as people use this. And we're still so early. But yeah, I think data is very important, like apps that can give me data, but that also can be API. Why do I need the Sonos app anymore when I can when my agent can talk to the Sonos speakers directly. Like my cameras, there's like a crappy app, but they have they have an API, so my agent uses the API now.
03:05:57 Lex Fridman: So it's going to force a lot of companies to have to shift focus. And it's kind of what the internet did, right? You have to rapidly rethink, reconfigure what you're selling, how you're making money.
03:06:11 Peter Steinberger: Yeah, some companies will really not like that. For example, there's no CLI for Google. So I had to like to have to do anything myself and build Gog, that's like a CLI for Google. And at the yeah, at the end user, they have to give me the emails because otherwise I cannot use their product. If I'm a company and I try to get Google data, Gmail, there's a whole complicated process to the point where sometimes startups acquire startups that went through the process, so they don't don't have to work with Google for half a year to be certified to being able to access Gmail. But my agent can access Gmail because I can just connect to it. It's still crappy because I need to like go through Google's developer jungle to get a key. And it's still annoying. But they cannot prevent me. And worst case, my agent just clicks on the on the website and gets the data out that way.
03:08:20 Lex Fridman: To browser use.
03:08:20 Peter Steinberger: Yeah, I mean, I I watch my agent happily click the I'm not a robot button. And there's this this whole that's going to be that's going to be more heated. You see companies like uh Cloudflare that try to prevent bot access. And in some ways that's useful for scraping.

### 02:58:30-03:15:52

## Transcript
02:58:30 Speaker: what gives you hope about this whole thing going on?
02:58:30 Peter Steinberger: I mean,
02:58:30 Speaker: about the human civilization?
02:58:30 Peter Steinberger: I inspired so many people. There's like, there's this whole builder vibe again. People are now using AI in a more playful way and are discovering what it can do and how it can like help them in their life and creating new places that are just sprawling of creativity. I don't know, like there's like ClawCon in Vienna. There's like 500 people and there's such a high percentage of people that want to present, which is to me really surprising because usually it's quite hard to find people that want to like talk about what they built and now it's there's an abundance. So, that gives me hope that we can we can figure shit out.
03:00:00 Speaker: And it makes it accessible to basically everybody.
03:00:00 Peter Steinberger: Yeah.
03:00:00 Speaker: Just imagine all these people building. Especially as you make it simpler and simpler, more secure. It's like anybody who has ideas that can express those ideas in language can build. That's crazy.
03:00:00 Peter Steinberger: Yeah, that's ultimately power to the people and one of the beauty the beautiful things that come out of AI. Not just not just a slob generator.
03:00:00 Speaker: Well, Mr. Clawfather, I just realized when I said that in the beginning, I violated two trademarks because there's also the Godfather. I'm getting sued by everybody. Um, you're a wonderful human being. Uh, you've created something really special. A special community, a special product, a special set of ideas, plus the entire the humor, the good vibes, the inspiration of all these people building, the excitement to build. Uh, so I'm truly grateful for everything you've been doing and uh, for who you are and for sitting down to talk with me today. Thank you, brother.
03:00:00 Peter Steinberger: Thanks for giving me the chance to tell my story.
03:00:00 Speaker: Thanks for listening to this conversation with Peter Steinberger. To support this podcast, please check out our sponsors in the description where you can also find links to contact me, ask questions, give feedback and so on. And now, let me leave you with some words from Voltaire. With great power comes great responsibility. Thank you for listening and hope to see you next time.
03:00:00 Peter Steinberger: There's going to be more heated. You see companies like uh Cloudflare that try to prevent bot access. And in some ways that's useful for scraping. But in other ways if I'm I'm a personal user, I want that. You know, sometimes I I use Codex and I I read an article about modern React patterns and it's like a medium article. I paste it in and the agent can't read it because they block it. So then I have to copy paste the actual text. Or in the future I learn that maybe I don't click on Medium because it's annoying and I use other websites that actually are agent friendly. So,
03:00:00 Speaker: There's going to be a lot of powerful rich companies fighting back. So it's a really you're at the center. You're the catalyst, the leader, and happen to be at the center of this kind of revolution where it's going to completely change of how we interact with uh services with with web. And so like there's companies like Google, they're going to push back. I mean, there's every major company you can think of is going to push back.
03:00:00 Peter Steinberger: Even yeah, even search um I now use I think Perplexity or Brave as providers because Google really doesn't make it easy to use Google without Google. I'm not sure if that's the right strategy. But I'm not Google.
03:00:00 Speaker: Yeah, there's uh there's a nice balance from a big company perspective because if you push back too much for too long, you become Blockbuster and you lose everything to the Netflixes of the world. But some push back is probably good during a revolution to see
03:00:00 Peter Steinberger: But you see that like this is something that the people want.
03:00:00 Speaker: Right. So
03:00:00 Peter Steinberger: Yes. If I'm on the go, I don't want to open a calendar app. I just I want to tell my agent, hey, remind me about this dinner tomorrow night and maybe invite two of my friends and then maybe send a send a WhatsApp message to my friend. And I don't need I don't want I need to open apps for that. I think that we passed that age and now everything is like much more connected and and fluid if those companies want it or not and I think we'll the right companies will find ways to jump on that train and other companies will perish.
03:00:00 Speaker: You got to listen to what the people want. Uh, we talked about programming quite a bit and a lot of folks that are developers are really worried about their jobs, about their about the future of programming. Do you think AI replaces programmers completely? Human programmers?
03:00:00 Peter Steinberger: I mean, we're definitely going in that direction. Programming is just a part of building products. So maybe maybe AI does replace programmers eventually. But there's so much more to that part. Like what do you actually want to build? How should it feel? How's the architecture? I don't think agents will replace all of that. Yeah, like just if the actual art of programming, it will it will stay there but it's it's going to be like knitting. You know, like people do that because they like it, not because it makes any sense. So so I read this article this morning about someone that it's okay to mourn our craft and I can a part of me very strongly resonates with that because in my past I I spent a lot of time tinkering just being really deep in the flow and just like cranking out code and like finding really beautiful solutions and yes, in a way it's it's sad because that will go away and I also got a lot of joy out of just writing code and being really deep in my thoughts and forgetting time and space and just being in this beautiful state of flow. But you can get the same state of flow I get a similar state of flow by working with agents and building and thinking really hard about problems. It is different. But and it's okay to mourn it, but that's not something we can fight. Like there is the world for a long time had a there was a lack of intelligence if you if you see it like that of people building things and that's why salaries of software developers reached stupidly high amounts and that will go away. Um, there will still be a lot of demand for people that understand how to build things. Just that all this tokenized intelligence uh enables people to do a lot more a lot faster. And it will be even more even faster and even more because those things are continuously improving. Um, we had similar things when I mean it's probably not a perfect analogy but when we created the steam engine and they built all these factories and replaced a lot of manual labor and then people revolted and broke the machines. Um, I I can relate that if you very deeply identify that you are a programmer, that it's scary and that it's threatening because what you like and what you're really good at is now being done by a soulless or not entity. But I don't think you're just a programmer. That does a very limiting view of your craft. You are you are still a builder.
03:00:00 Speaker: Yeah, there's a couple things I want to say. So one is I never as you're articulating this beautifully, I'm realizing I never thought I would the thing I love doing would be the thing that gets replaced. You hear these stories about these like you said with the steam engine. I've I've spent so many I don't know, maybe thousands of hours pouring over code and putting my heart and soul and like and just like some of my most painful and happiest moments were alone behind I I was an Emacs person for a long time. Emacs. And and then there's an identity and there's meaning and there's like when I walk about the world, I don't say it out loud, but I think of myself as a programmer. And to have that in a matter of months. I mean, you mentioned April to November, it really is a leap that happened, a shift that's happening. To have that completely replaced is uh is painful. It's truly painful. But I also think um programmers, builders more broadly, but what is what is the act of programming? I I think programmers are generally best equipped at this moment in history to learn the language, to empathize with agents, to learn the language of agents, to feel the CLI.
03:00:00 Peter Steinberger: Yeah.
03:00:00 Speaker: Like like to understand what is the thing you need, you the agent, need to do this task the best.
03:00:00 Peter Steinberger: I think at some point it's just going to be called coding again and it's just going to be the new normal. And yet while I don't write the code, I very much feel like I'm in the driver's seat and I am I am writing the code. You know, it's just
03:00:00 Speaker: You'll still be a programmer. It's just the activity of a programmer is different.
03:00:00 Peter Steinberger: Yeah, and because on X the bubble I mean is mostly positive on on Mastodon and Blue Sky. I don't I also use it less because often times I got attacked for my blog posts and I I had stronger reactions in the past. Now I can sympathize with those people more because in a way I get it. It in a way I also don't get it because it's very unfair to grab onto the person that you see right now and unload all your fear and hate. It's going to be a change and it's going to be challenging, but it's also I don't know, I find it incredibly fun and and gratifying and I can I can use the new time to focus on much more details. I think the level of expectation of what we build is also rising because it's just now the default is now so much easier. So software is changing in many ways. There's going to be a lot more. And then you have all these people that are screaming, oh yeah, but what about the water? You know, like I did a conference in Italy about the the state of AI and my whole motivation was to push people away from don't see yourself as an iOS developer anymore, you're now a builder and you can use your skills in many more ways. Also because apps are slowly going away. Uh people didn't like that. Like uh a lot of people didn't like what I had to say. And I don't think I was hyperbole. I was just like this is how I see the future. Maybe this is not how it's going to be, but I'm pretty sure a version of that will happen. And the first question I got was, yeah, but what about the insane water use on data centers? But then you actually sit down and do the math and then for most people, if you just skip one burger per month, that compensates the the CO2 output or like the water use in equivalent of tokens. I mean, the mass is the mass is tricky and it depends if you add pre-training, then maybe it's more than just one patty. But it's not off by factor of 100, you know? So so there or like golf is still using way more water than all data centers together. So are you also hating people that play golf? Those people grab on anything that they think is bad about AI without seeing the potential things that might be good about AI. And I'm not saying everything's good. It's certainly going to be a very transformative technology for our society.
03:00:00 Speaker: There is I to steal man the the criticism in general. I do want to say in my experience with Silicon Valley, um there's a bit of a bubble in the sense that there's a kind of excitement and an overfocus about the positive that the technology can bring. Yeah. And which is great. It's great to focus on not to not to be paralyzed by fear and fearmongering and so on. But there's also within that excitement and within everybody talking just to each other, there's a dismissal of the basic human experience across the United States, in the Midwest, across the world, including the programmers we mentioned, including all the people that are going to lose their jobs, including the the the measurable pain and suffering that happens at the short-term scale when there's change of any kind, especially large-scale transformative change that we're about to face if what we're talking about will materialize. And so to having a bit of that humility and an awareness about the tools you're building, they're going to cause pain. They will long-term hopefully bring about a better world and even more opportunities and even more awesomeness. But having that kind of like quiet moment often of of respect for the pain that is going to be felt. And so like not not enough of that is I think done, so it's it's good to have a bit of that.
03:00:00 Peter Steinberger: And then I also have to put against the some of the emails I got where people told me, they have a small business and they've been struggling and and OpenClaw helped them automate a few of the tedious tasks from from collecting invoices to like answering customer emails that then freed them up and like caused them a bit more joy in their life or or some emails where they told me that OpenClaw helped the disabled daughter uh that she's now empowered and feels she can do much more than before. Which is amazing, right? Because you you could do that before as well. The technology was there. I didn't I didn't invent a whole new thing. But I made it a lot easier and more accessible and that did show people the possibilities that they previously wouldn't see and now they applied it for good. Or like also the fact that yes, I I I suggest the the the latest and best models, but you can totally run this on free models. You can run this locally. You can run this on on on Kimi or other other models that are way more accessible price-wise and still have a a very powerful system that might otherwise not be possible because other things that I don't know, Anthropic's Cowork is locked in into their space. So it's not all black and white. There's I got a lot of emails that were heartwarming and amazing and and I don't know, just make me really happy.
03:00:00 Speaker: Yeah, there's a lot it has brought joy into a lot of people's lives, not just not just programmers, like a lot of people's lives. It's it's beautiful to see. Uh, what gives you hope about this whole thing we're having going on?
03:00:00 Peter Steinberger: I mean, I inspired so many people. There's like, there's this whole builder vibe again. People are now using AI in a more playful way and are discovering what it can do and how it can like help them in their life and creating new places that are just sprawling of creativity. I don't know, like there's like ClawCon in Vienna. There's like 500 people and there's such a high percentage of people that want to present, which is to me really surprising because usually it's quite hard to find people that want to like talk about what they built and now it's there's an abundance. So, that gives me hope that we can we can figure shit out.
03:00:00 Speaker: And it makes it accessible to basically everybody. Yeah. Just imagine all these people building. Especially as you make it simpler and simpler, more secure. It's like anybody who has ideas that can express those ideas in language can build. That's crazy.
03:00:00 Peter Steinberger: Yeah, that's ultimately power to the people and one of the beauty the beautiful things that come out of AI. Not just not just a slob generator.
03:00:00 Speaker: Well, Mr. Clawfather, I just realized when I said that in the beginning, I violated two trademarks because there's also the Godfather. I'm getting sued by everybody. Um, you're a wonderful human being. Uh, you've created something really special. A special community, a special product, a special set of ideas, plus the entire the humor, the good vibes, the inspiration of all these people building, the excitement to build. Uh, so I'm truly grateful for everything you've been doing and uh, for who you are and for sitting down to talk with me today. Thank you, brother.
03:00:00 Peter Steinberger: Thanks for giving me the chance to tell my story.
03:00:00 Speaker: Thanks for listening to this conversation with Peter Steinberger. To support this podcast, please check out our sponsors in the description where you can also find links to contact me, ask questions, give feedback and so on. And now, let me leave you with some words from Voltaire. With great power comes great responsibility. Thank you for listening and hope to see you next time.
03:00:00 Peter Steinberger: 會變得更加激烈。你會看到像 Cloudflare 這樣的公司，他們試圖阻止機器人存取。在某些方面，這對於抓取很有用。但在其他方面，如果我是一個個人使用者，我希望如此。你知道，有時候我使用 Codex，我讀了一篇關於現代 React 模式的文章，它就像一篇 Medium 文章。我把它貼進去，但代理程式無法讀取，因為他們阻止了它。所以我必須複製貼上實際的文字。或者將來我會學到，也許我不會點擊 Medium，因為它很煩人，我會使用其他實際上對代理程式友好的網站。所以，
03:00:00 Speaker: 將會有許多強大富有的公司反擊。所以這是一個非常你處於中心。你是催化劑、領導者，恰好處於這場革命的中心，這場革命將徹底改變我們與服務、與網路互動的方式。所以像 Google 這樣的公司，他們會反擊。我的意思是，你能想到的每個主要公司都會反擊。
03:00:00 Peter Steinberger: 即使是，是的，甚至是搜尋，嗯，我現在使用，我想是 Perplexity 或 Brave 作為提供者，因為 Google 真的沒有讓使用 Google 變得容易，如果沒有 Google。我不確定這是否是正確的策略。但我不是 Google。
03:00:00 Speaker: 是的，從大公司的角度來看，這是一個很好的平衡，因為如果你反擊太多太久，你就會變成 Blockbuster，你就會失去一切，就像 Netflix 的世界一樣。但一些反擊在革命期間可能是好的，看看
03:00:00 Peter Steinberger: 但你看到，這就是人們想要的。
03:00:00 Speaker: 對。所以
03:00:00 Peter Steinberger: 是的。如果我在路上，我不想打開日曆應用程式。我只想告訴我的代理程式，嘿，提醒我明天晚上的晚餐，也許邀請我的兩個朋友，然後也許發送一條 WhatsApp 訊息給我的朋友。我不需要，我不想，我需要為此打開應用程式。我認為我們已經過了那個時代，現在一切都變得更加互聯和流暢，無論這些公司是否願意，我認為正確的公司會找到方法搭上這趟列車，而其他公司將會滅亡。
03:00:00 Speaker: 你必須傾聽人們的需求。嗯，我們談了很多關於程式設計，很多開發者都非常擔心他們的工作，擔心程式設計的未來。你認為 AI 會完全取代程式設計師嗎？人類程式設計師？
03:00:00 Peter Steinberger: 我的意思是，我們肯定朝那個方向發展。程式設計只是產品建構的一部分。所以也許，也許 AI 最終會取代程式設計師。但那一部分還有很多。比如，你到底想建構什麼？它應該是什麼感覺？架構是什麼？我不認為代理程式會取代所有這些。是的，就像程式設計的實際藝術一樣，它會，它會留在那裡，但它會像編織一樣。你知道，人們做那個是因為他們喜歡，而不是因為它有任何意義。所以，所以，我今天早上讀了一篇文章，關於有人說哀悼我們的工藝是可以的，我的一部分非常強烈地認同這一點，因為在我的過去，我花了很多時間修修補補，只是非常深入地沉浸在心流中，只是像瘋狂地寫程式碼，並找到真正美麗的解決方案，是的，在某種程度上，這是，這是悲傷的，因為那將會消失，我也從只是寫程式碼中獲得了很多樂趣，並且非常深入地沉浸在我的思緒中，忘記了時間和空間，只是處於這種美麗的心流狀態。但你可以獲得相同的心流狀態，我透過與代理程式合作，建構並非常努力地思考問題，獲得了類似的心流狀態。它有所不同。但哀悼它是可以的，但那不是我們可以對抗的。就像，世界長期以來一直缺乏智慧，如果你這樣看待它，缺乏建構東西的人，這就是為什麼軟體開發者的薪水達到了愚蠢的高額，而那將會消失。嗯，仍然會有很多人需要了解如何建構東西。只是所有這些代幣化的智慧，嗯，讓人們能夠更快地做更多的事情。而且它會更快，甚至更多，因為這些東西不斷改進。嗯，我們有類似的事情，雖然這可能不是一個完美的類比，但當我們發明蒸汽機時，他們建造了所有這些工廠，取代了許多手工勞動，然後人們反抗並破壞了機器。嗯，我，我可以理解，如果你非常深入地認同你是一個程式設計師，那會很可怕，而且會構成威脅，因為你喜歡的，你擅長的，現在正在被一個沒有靈魂的或非實體所完成。但我認為你不僅僅是一個程式設計師。那對你的工藝來說是一個非常有限的觀點。你是一個，你仍然是一個建構者。
03:00:00 Speaker: 是的，有幾件事我想說。第一，當你如此優雅地闡述時，我意識到我從未想過我喜歡做的事情會被取代。你聽過這些故事，就像你說的蒸汽機一樣。我花了無數個小時，我不知道，也許幾千個小時，埋首於程式碼，投入我的心血和靈魂，就像我最痛苦和最快樂的時刻，都是獨自一人在 Emacs 後面，我長期以來都是 Emacs 的使用者。然後，這是一種身份，一種意義，就像當我在世界上行走時，我不會大聲說出來，但我認為自己是個程式設計師。而要在幾個月內，我的意思是，你提到了四月到十一月，這確實是一個飛躍，一個正在發生的轉變。要讓它完全被取代，是痛苦的，是真正痛苦的。但我也認為，嗯，程式設計師，更廣泛地說，是建構者，但程式設計的行為是什麼？我認為程式設計師在歷史上的這個時刻，通常最能勝任學習語言，與代理程式產生共鳴，學習代理程式的語言，感受 CLI。
03:00:00 Peter Steinberger: 是的。
03:00:00 Speaker: 就像，就像理解你，代理程式，需要什麼才能最好地完成這項任務。
03:00:00 Peter Steinberger: 我想在某個時候，它會再次被稱為編碼，它會成為新的常態。是的，雖然我沒有寫程式碼，但我非常感覺到我是駕駛者，我正在寫程式碼。你知道，它只是
03:00:00 Speaker: 你仍然會是個程式設計師。只是程式設計師的活動不同了。
03:00:00 Peter Steinberger: 是的，因為在 X 上，我的意思是，這個泡沫大多是正面的，在 Mastodon 和 Blue Sky 上。我沒有，我也較少使用它，因為我經常因為我的部落格文章而受到攻擊，而且我過去有更強烈的反應。現在我更能同情那些人，因為在某種程度上我理解。在某種程度上我也不理解，因為抓住你現在看到的人，並傾瀉你所有的恐懼和仇恨，這非常不公平。這將會是一個改變，這將會是一個挑戰，但它也，我不知道，我發現它非常有趣和令人滿足，而且我可以，我可以用新的時間專注於更多的細節。我認為我們所建構的東西的期望水平也在提高，因為現在預設值變得如此容易。所以軟體在許多方面都在改變。將會有更多。然後你會有所有這些人尖叫，哦，是的，但是水呢？你知道，就像我在義大利參加了一個關於 AI 現狀的會議，我的主要動機是讓大家不要再把自己看作是 iOS 開發者了，你現在是一個建構者，而且你可以用更多的方式運用你的技能。也因為應用程式正在慢慢消失。嗯，人們不喜歡那樣。就像，很多人不喜歡我說的話。我不認為我誇大其詞。我只是說，這就是我看到的未來。也許這不會是這樣，但我很確定這種情況的某個版本會發生。我得到的第一個問題是，是的，但是資料中心瘋狂的用水量怎麼辦？但你實際上坐下來計算一下，對於大多數人來說，如果你每個月少吃一個漢堡，那就可以抵消 CO2 排放量，或者說，以代幣計算的水量。我的意思是，數學很複雜，而且這取決於你是否加上預訓練，那麼可能不止一個肉餅。但它並沒有偏離 100 倍，你知道嗎？所以，所以，或者像高爾夫仍然比所有資料中心加起來消耗更多的水。所以你也會討厭打高爾夫的人嗎？那些人抓住任何他們認為 AI 不好的東西，卻沒有看到 AI 可能帶來的好處。我不是說一切都好。它肯定會是我們社會的一個非常變革性的技術。
03:00:00 Speaker: 有，我為了偷走批評，總體而言，我想說，根據我在矽谷的經驗，嗯，存在著一種泡沫，意思是，存在著一種興奮，以及過度關注科技可能帶來的正面影響。是的。這很好，專注於此很好，不要被恐懼和散佈恐懼所麻痺等等。但這種興奮之中，以及每個人都只和彼此交談之中，存在著對美國、中西部、全世界基本人類經驗的輕視，包括我們提到的程式設計師，包括所有將會失業的人，包括當任何形式的變化發生時，在短期內會發生的難以估量的痛苦和折磨，尤其是我們即將面對的大規模變革，如果我們談論的會實現的話。所以，擁有那種謙遜，以及對你正在建構的工具的意識，它們將會帶來痛苦。它們長期而言，希望會帶來一個更好的世界，甚至更多的機會，甚至更多的美好。但擁有那種安靜的時刻，經常，對將會感受到的痛苦的尊重。所以，我認為這方面做得不夠，所以擁有那一點是好的。
03:00:00 Peter Steinberger: 然後我還必須反駁我收到的一些電子郵件，其中人們告訴我，他們有一家小企業，一直很掙扎，而 OpenClaw 幫助他們自動化了一些繁瑣的任務，從收集發票到回覆客戶電子郵件，這讓他們解脫出來，讓他們的生活多了一點樂趣。或者一些電子郵件，他們告訴我 OpenClaw 幫助了殘疾的女兒，她現在感到被賦予了力量，覺得自己可以做比以前更多的事情。這很棒，對吧？因為你以前也可以做到，技術就在那裡。我沒有發明一個全新的東西。但我讓它變得更容易、更容易存取，這確實向人們展示了他們以前看不到的可能性，現在他們將其應用於善意。或者像，事實上，是的，我，我，我建議使用最新最好的模型，但你完全可以在免費模型上運行這個。你可以在本地運行這個。你可以在 Kimi 或其他其他模型上運行這個，這些模型在價格上更容易存取，而且仍然擁有一個非常強大的系統，否則可能無法實現，因為其他東西，我不知道，Anthropic 的 Cowork 被鎖定在他們的空間裡。所以這不是非黑即白。我收到了很多令人暖心和驚奇的電子郵件，而且，我不知道，只是讓我非常開心。
03:00:00 Speaker: 是的，它為許多人的生活帶來了歡樂，不只是程式設計師，許多人的生活。這很美妙。嗯，是什麼讓你對這一切充滿希望？人類文明？
03:00:00 Peter Steinberger: 我的意思是，我啟發了這麼多人。就像，又出現了這種建構者的氛圍。人們現在以更玩樂的方式使用 AI，並發現它能做什麼，以及它如何幫助他們的生活，並創造出充滿創造力的新地方。我不知道，就像維也納的 ClawCon。有大約 500 人，而且有很高比例的人想發表報告，這對我來說真的很令人驚訝，因為通常很難找到想談論自己建構的東西的人，而現在卻是供過於求。所以，這給了我希望，我們可以，我們可以解決問題。
03:00:00 Speaker: 而且它讓基本上每個人都能使用。是的。想像一下所有這些人都在建構。特別是當你讓它變得越來越簡單，越來越安全。就像任何有想法的人，只要能用語言表達這些想法，就能建構。這太瘋狂了。
03:00:00 Peter Steinberger: 是的，這最終是將權力交給人民，也是 AI 帶來的美好事物之一。不只是，不只是一個懶惰的生成器。
03:00:00 Speaker: 嗯，爪父先生，我剛才意識到，當我一開始說那個的時候，我侵犯了兩個商標，因為還有教父。我會被所有人告。嗯，你是一個很棒的人。嗯，你創造了一些非常特別的東西。一個特別的社群，一個特別的產品，一套特別的想法，再加上所有的幽默，美好的氛圍，所有這些建構者帶來的靈感，建構的興奮。嗯，所以我非常感謝你所做的一切，以及你的為人，還有今天坐下來和我交談。謝謝你，兄弟。
03:00:00 Peter Steinberger: 謝謝你給我機會講我的故事。
03:00:00 Speaker: 感謝您收聽與 Peter Steinberger 的對話。為了支持本播客，請查看說明中的贊助商，您也可以在那裡找到聯繫我、提問、提供回饋等的連結。現在，讓我為您留下伏爾泰的一些話。能力越大，責任越大。感謝您的收聽，希望下次再見。
