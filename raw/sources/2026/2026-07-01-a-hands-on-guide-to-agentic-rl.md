# A Hands-On Guide to Agentic RL

Source: https://theneuralmaze.substack.com/p/a-hands-on-guide-to-agentic-rl
Author: Miguel Otero Pedrido
Publisher: The Neural Maze
Published: 2026-07-01
Captured: 2026-07-03
Tags: AI Systems Engineer Journey
Subtitle: Issue #06 — How RL actually trains an agent, when it's worth the cost, and the real Prime Intellect environments behind the open models

Markdown Content:

Hey friends! 👋

Welcome to Issue #06 of the [AI Systems Engineer Journey](https://theneuralmaze.substack.com/t/ai-systems-engineer-journey).

I won't open with a definition. I'll open with one game of [Wordle](https://www.nytimes.com/games/wordle/index.html), played by a small AI model, because the whole issue lives inside it.

If you've somehow missed it, Wordle is a word game that took over the internet a few years back. There's a secret five-letter word, and you get six guesses to find it. Each guess has to be a real word, and after every guess the board colours each letter to tell you how close you were:

- 🟩 green — right letter, right position;
- 🟨 yellow — that letter is in the word, but somewhere else;
- ⬛ grey — that letter isn't in the word at all.

> The whole game is that feedback loop.

A single guess in isolation is a coin flip; what makes you good at Wordle is using what the earlier guesses told you — keeping the greens, moving the yellows, dropping the greys. Which is exactly why it's such a sharp little test for an agent: it's not one question with one answer, it's a short series of moves where each one should build on the feedback from the last. Get one move right and then ignore what it taught you, and you lose.

So here's how our small model did. The secret word was CRANE (hidden from the model, shown here just so you can follow along):

```text
guess 1:  TRAIN   →   T⬛  R🟨  A🟨  I⬛  N🟨      (R, A, N are in the word)
guess 2:  RANCH   →   R🟨  A🟨  N🟨  C🟨  H⬛      (now R, A, N, C all confirmed)
guess 3:  CLEAN   →   C🟩  L⬛  E🟨  A🟨  N🟨      (?!  it just dropped the R)

   ...six guesses used, never solved.     WIN: ❌     REWARD ≈ 0.2
```

Look at guess 3. The board had told the model, twice, that the answer contains an R. And then it guessed a word with no R in it at all. It threw away the one thing it had proven. A base small model wins roughly 0% of these games — not because it can't read the feedback, but because it never learned to act on it.

You have produced thousands of transcripts like this — your own agent, taking turns, getting feedback, fumbling it. And here's what almost nobody does with them: learn from them. We read the failure, sigh, go edit the prompt, and throw the transcript away.

This issue is about the world where you stop throwing them away — where a transcript like that, score and all, becomes the thing that makes the agent better. And the best part: the Wordle environment above is real, it's public, and by the end of this you'll have run it yourself.

![a white cell phone](https://images.unsplash.com/photo-1652451764453-eff80b50f736?fm=jpg&q=60&w=3000&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D)

## Everything we've built so far leaves the model untouched

Look at what this series has actually been doing.

In [Issue #03](https://theneuralmaze.substack.com/p/dont-marry-your-llm-provider) we put a reverse proxy in front of the model so we could swap providers freely. In [Issue #04](https://theneuralmaze.substack.com/p/building-agent-memory-with-knowledge) we gave the agent a memory it could reason over. Good work, both. But notice where it happened: around the model. We changed the inputs and the tools. The model in the middle stayed exactly as the lab shipped it.

That's true of every lever we normally pull:

- Prompting changes the question we ask.
- Tools change what the model can reach.
- Memory changes what it can recall.

Three good levers.

> Not one of them changes what the model has actually learned to do, like the Wordle player's habit of ignoring the feedback sitting right in front of it.

Go back to that game. No prompt was going to fix guess 3. You could write "pay attention to confirmed letters" into the system prompt, and it would help sometimes and quietly fail other times, because you'd be coaching from the sideline a player who can't change how he plays.

> The habit lives in the model's weights — the numbers inside the network that decide what it does next. And there's exactly one lever that reaches the weights.

That lever is reinforcement learning.

The idea is simple: let the model play, score the game, then adjust the weights so the moves from the good games become more likely and the moves from the bad ones less likely. Repeat a lot. Nobody hands the model the answer word. Across thousands of its own games, it discovers that the trajectories where it respected the feedback tend to win — so it slowly becomes a player that respects the feedback.

Prompting moves the goalposts. RL moves the player.

> 🙋 If finetuning and RL are your thing, the [Finetuning Sessions](https://theneuralmaze.substack.com/t/finetuning-sessions) are for you — pretraining, LoRA, QLoRA, GRPO, and the rest, taught step by step.

## Why training an agent is harder than training a chatbot

This is the one piece of theory I really want to land, because it's what makes "RL for agents" different from the RL you've heard about.

Picture how a chatbot gets trained: it writes one answer, a scorer gives that answer one number, and you update. One reply, one score. Clean.

Now look at our Wordle game. The model didn't produce one answer … it produced a sequence — guess, feedback, guess, feedback, guess.

> That sequence is called a trajectory, and it creates a problem the chatbot case never has.

The score lands at the very end: the game was lost.

But which move was the mistake? Guesses 1 and 2 were fine — they gathered real information. The blunder was guess 3, throwing away the confirmed R. The reward is a single number stuck on the end of the whole game, while the move that actually cost it was in the middle.

> Figuring out which step deserves the blame (or the credit) is the central challenge of training agents. It even has a name: credit assignment.

![](https://substackcdn.com/image/fetch/$s_!gj9S!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1a90cffe-780c-4325-b8ed-6ecd3d950738_1280x401.png)

So the difference is this. A chatbot is judged on what it says. An agent is judged on what it does — over several turns, with feedback or tools, inside something that reacts to it. You can't capture that with a prompt and a score.

> You need something that can actually run the agent, let it take its turns, and judge the whole run.

The industry has a word for that something. The surprising part is that it's the same word we already use for testing agents.

## The simple idea at the center of Prime Intellect

For years, two things lived in separate worlds: evals (the tests you run to see how good your agent is) and RL environments (the simulators you train it in). Different tools, different teams.

[Prime Intellect](https://www.primeintellect.ai/)'s key idea is that they’re the same thing. Both need exactly three parts:

- a dataset of tasks — the puzzles, questions, or goals (for Wordle, the list of target words);
- a harness — the machinery that lets the model act: the turn-by-turn loop, the feedback after each guess, any tools;
- a rubric — a way to score what happened (did it solve the word? in how many guesses?).

Give those three to a frozen model and you've run an eval: you measured it. Give the same three to a model that's learning, and feed the score back into its weights, and you've run RL: you improved it. The thing itself doesn't change.

Only what you do with the final number changes.

That Wordle transcript from the top? It's an eval result. It's also, with nothing altered, a training example. Same object, two uses.

There's one more piece that makes this work well for agents, and it's why games, math, and coding went first. To score a chatbot's reply you need a second AI trained to imitate human taste (i.e. fuzzy and fragile).

> But to score an agent doing a concrete task, you can often just check the result. Did it guess the word? Did the tests pass?

That's not a matter of taste; it's a function that returns a clear number. The rubric is plain code, and code doesn't get tired or play favorites. People call this RL with verifiable rewards, and it's the honest, cheap core the whole thing is built on.

![](https://substackcdn.com/image/fetch/$s_!UZIN!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb0acc4ad-fb37-4e6a-b95f-3836bdc47630_999x474.png)

Prime Intellect ships this as three open pieces you'll use in a minute: [verifiers](https://github.com/PrimeIntellect-ai/verifiers), the library for writing one of these environments (originally by Will Brown — whose Wordle environment we've been staring at); the [Environments Hub](https://app.primeintellect.ai/dashboard/environments?ex_sort=by_sections), a public registry with 2,500+ of them, like a package registry where every "package" is a world you can train an agent in; and [prime-rl](https://github.com/PrimeIntellect-ai/prime-rl), the trainer that runs the loop at scale. Their open INTELLECT models are the proof it works — INTELLECT-2 was a 32B model trained with RL across compute spread around the world, and the newer INTELLECT-3 is an open agentic-and-coding model trained on exactly these community environments.

## How the "nudge" actually works, in one minute

You can run everything below without this section, but here's the engine in plain words so it doesn't feel like magic.

The method almost everyone uses is [GRPO](https://theneuralmaze.substack.com/p/the-rl-algorithm-behind-deepseeks). The name is scarier than the idea.

![](https://substackcdn.com/image/fetch/$s_!KeXH!,w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F30cc8be2-6597-4947-8a42-b4a1544b56d1_2404x1204.png)

Older methods needed a second neural network whose only job was to judge how good an attempt was — an extra model to train and keep from breaking. GRPO drops it and uses a simpler trick: let the model attempt the same task several times, and compare the attempts to each other.

The loop:

1. Take one puzzle. Let the agent play it eight times (with a little randomness so the games differ).
2. Score all eight.
3. Some beat the group's average, some fall below it.
4. Nudge the model toward the above-average games and away from the below-average ones.
5. Next puzzle.

That's it. The batch of attempts is its own measuring stick — no judge network needed. Simple to run, stable enough to scale, which is why the open community settled on it.

And here's why this is our job and not just the research team's. Making those eight attempts means running inference — slow, turn-by-turn generation. Updating the weights means running training — heavy, GPU-hungry math. If you make one wait for the other, half your expensive hardware sits idle.

So `prime-rl` runs them asynchronously: a pool of workers generates games non-stop while a separate trainer keeps updating the model. Add the sandboxes to safely run model-written code, the harness, the provider abstraction — and agentic RL turns out to be mostly a distributed-systems problem with a thin layer of math on top. That substrate is the AI Systems Engineer's job.

## You probably shouldn't do this yet

I'm not going to hand you a neat decision table, because the honest answer is a ladder, and most people reading this are on a lower rung than they think.

> RL is the heaviest, priciest, least forgiving lever in the stack.

Before you take one training step you've spent real money on GPUs, built a reward you actually trust, and accepted that a bug in that reward won't crash — it'll quietly teach your model to do the wrong thing. Most "my agent is dumb" problems die one or two rungs lower — at prompting, better tools, or the memory we built last issue — for a fraction of the cost. Climb to RL only when you've truly run out of room below.

How do you know you've run out of room? These are the real signals you've hit the prompting ceiling:

- You've stopped finding wins in prompts, tools, and memory — the model already has what it needs and still fails a whole class of tasks the same way every time. (Our Wordle player is this: the feedback was right there, and it ignored it anyway.)
- Success is verifiable — you can write a function that scores an attempt honestly. If you can't, RL has nothing real to optimize.
- The failure is in the behavior across a trajectory, not in one weak sentence — exactly what prompting can't reach.
- You have (or can generate) lots of varied tasks to practice on, plus GPUs — your own or hosted.

All four? You've got a real case. Two of four, and you're about to spend a fortune learning something a better prompt would've told you for free.

One thing to burn in before we run anything, because it's the failure that bites people:

> 👉 RL optimizes exactly what you reward, never what you meant.

Hand out points for making a guess and you'll train an agent that guesses endlessly. Leave a loophole that scores higher than solving the task, and the model will find it — reliably, at scale, without a shred of guilt. Your reward function is the most dangerous code in the whole pipeline. We'll see exactly where that danger lives when we read one.

## Run a real one: Wordle, off the Hub
