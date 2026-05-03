# Chunk 0003: 00:59:30-01:19:30

- Title: OpenClaw: The Viral AI Agent that Broke the Internet - Peter Steinberger | Lex Fridman Podcast #491
- URL: https://www.youtube.com/watch?v=YFjfBk8HI5o
- Video ID: YFjfBk8HI5o
- Start: 00:59:30
- End: 01:19:30

## Gemini Output

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
