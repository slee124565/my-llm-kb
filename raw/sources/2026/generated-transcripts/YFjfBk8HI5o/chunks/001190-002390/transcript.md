# Chunk 0001: 00:19:50-00:39:50

- Title: OpenClaw: The Viral AI Agent that Broke the Internet - Peter Steinberger | Lex Fridman Podcast #491
- URL: https://www.youtube.com/watch?v=YFjfBk8HI5o
- Video ID: YFjfBk8HI5o
- Start: 00:19:50
- End: 00:39:50

## Gemini Output

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
