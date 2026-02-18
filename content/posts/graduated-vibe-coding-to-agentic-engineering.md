---
date: '2026-02-17T16:00:00-07:00'
draft: false
title: "How I Graduated from Spec-Based Vibe Coding to Agentic Engineering"
tags: ['ai', 'agentic-engineering', 'claude-code', 'pai', 'context-engineering']
description: "From copy-pasting into ChatGPT to orchestrating self-improving AI systems. Here's the journey, the mistakes, and what I learned along the way."
---

In July of '25 there I sat, combing through the specs I generated with GitHub Copilot. I was working a contract for a real estate estimation company, and they needed my tool to scale their operations.

The idea was pretty simple: how do we take AI and generate estimation reports? Most inspection reports are 80-95% repetition. They only require about 20% of human intervention — the rest can be done by an intelligent LLM.

That was the goal anyway. LLM-based workflows were new, and people weren't sure what was possible. Most people were just starting to use ChatGPT like Google — looking up recipes, giving it their symptoms, trying to find out whether their sneezing poodle was allergic to its food or had somehow attracted lung cancer. The thinking was pretty simple: if AI is smart enough to tell me whether I need to take my $5,000 goldendoodle to the vet, I could probably use it to help me write an email at work.

We were only scratching the surface.

## The Vibe Coding Era

The thought behind LLM-based workflows was straightforward. Most tasks are pretty simple — you take a task, let the AI think about it, and make a decision. Plug your LLM into a code-based interface, make the decisions deterministic. Simple!

This was all the rage. Several AI companies were founded, went through Y Combinator, and got insane valuations. Cool, I guess — but it's just an LLM plugged into a system. How is that special?

There was this weird energy around "vibe coding" too. People were copy-pasting into ChatGPT like mad, making interesting progress. Suddenly tools launched — Cursor, Devin, GitHub Copilot. The idea was to put a harness around the LLM to get it to do coding tasks within an IDE interface. An Anthropic engineer saw this and just... built Claude Code, leveraging Anthropic's amazing models. It was all the rage, but very simple. There was no real reason to use it over GitHub Copilot, unless you just really liked the terminal.

## Building at the Speed of Thought

Around this time I started building the estimation tool. I was in the space. I saw how powerful AI coding was. I could build tools at the speed of thought — generating in days what took weeks previously. I shipped a deeply productive proof of concept within weeks, what would've normally taken months. All using spec-based coding.

The idea is pretty simple: you use AI to derive your specifications in a PRD document, then you use it to build the project from scratch, going one by one through each task. Then you test the code, verifying it works.

And it was working!

It wasn't simple usage either — it was a very advanced system. The entire application was done within two weeks, with advanced retries in case the LLM connection to OpenRouter broke, or our fallback on GitHub Models went down.

The system was also built from the ground up to persist logging across sessions, so we had full visibility into token usage, the requests and responses on the API, and every decision made by the AI system.

## The Discovery That Changed Everything

Funny part is, I didn't ask for most of this. I just needed the core functionality. The AI, with the PRDs and documentation, had a source of truth about how to proceed. However, consistently, each coding session the AI made decisions that didn't work. It would make isolated decisions that didn't account for the rest of the codebase, or the other tasks that needed to be created. It was like a brand new junior engineer — only thinking about accomplishing the task given, taking the path of least resistance to get the job done.

On a whim, as my documentation folder for all PRDs became rather large and the features grew in complexity, I created another folder: **"coding session summaries"** — where all the decisions made in each coding session were stored. This created a pattern that explained what decisions were made across sessions and why they were made.

Now every coding session, as the project progressed, I started doing this more and more. After every decision made by the AI, I told it to summarize and add it to a daily doc. This started to inform the AI about the broader patterns. It needed a way to solve these problems holistically.

It started thinking about the bigger picture — solving many problems, not just the ones I showed it initially. It started considering the broader context, decisions made previously, fixing those, and making them work with new features.

**It started to engineer, not just "vibe code."**

## Running a Business, Building in the Margins

I knew there was a way to track data across sessions and pull out insights on what worked and what didn't. But at this point I was caught up — completing contracts, finding new clients, running a business, figuring out sales and marketing and all the rest.

Running my own LLC taught me something: when you build tools for yourself, you build tools that actually work. No hypothetical users. No product-market fit guessing. Just: does this solve MY problem? If yes, ship it.

I knew even then there was a way to build out systems that automate everything. If I could "vibe-code" a self-improving AI system with markdown files, I could probably build AI solutions that did the same — or at least systems that elevated my skills as a human.

I started working on [Sales RPG](/posts/meet-jeff/) — a real-time AI coaching system that listens to sales calls, detects objections, and suggests responses live. I took my close percentage on sales calls from 5% to 25% within a month. The next month I did 30%, then 40%. I knew I was onto something.

## Enter PAI

Right around this time, December rolled in. Business slowed down as the holiday cheer arrived, so I started tinkering.

I watched Daniel Miessler's manifesto on Claude Code and PAI — Personal AI Infrastructure — as a way to elevate humans.

My documentation approach! Someone had built it into a system that works with Claude! The fact that it's self-improving, but it's all documentation-based, in text — just like markdown! I was hooked.

PAI is a self-improving AI system built on Claude Code — it remembers what works, loads your context every session, and gets better the more you use it. I named mine Jeff. ([Here's the full introduction](/posts/meet-jeff/) and [the architecture behind it](/posts/building-personal-ai-infrastructure/).)

I hadn't really used Claude Code before this, just found it annoying — pulling up code files in the IDE, then typing in my coding assistant in the terminal. But if it's self-improving? I'm sold.

I started by setting it up. Just the fact that memory persisted across sessions blew my mind.

I started tinkering, and started shipping 2x faster than I was with spec-driven development. My mind was blown. How was this possible?

## The Agentic Explosion

Next thing you know, Ralph Wiggum popped off. Everyone was talking about it, using it. Then Beads appeared. Gastown. What the heck is all this?

Everyone was talking about coding harnesses, improving systems, agentic coding, and spec-driven development — ***together***.

Something started changing. Anthropic shipped a plugin system for Claude Code. Then when they saw engineers were wiring up business work, taxes, and everything else to the system, they shipped Claude Cowork. Not months after they saw this shift. Not weeks. At most, two weeks — and more likely, days.

These agentic coding tasks are taking off like crazy. Anthropic, seeing this agentic storm, people subscribing to Claude Code 5 or 6 times to have long-running sessions — they released agentic swarms on the API.

Now there are agentic systems recreating C compilers, SaaS features, entire product surfaces. Most of the big SaaS companies like HubSpot took a nosedive in the stock market.

Guys like Geoffrey Huntley are recreating features with Claude Code simply by looking at a website or app, showing it to Claude, and getting 80% of the way there in hours — then adding to their own stack.

## The Economics Are Insane

Claude Code + PAI + long-running sessions with Ralph or Gastown or multiple subscriptions or agentic swarms... you can create anything, at half the cost of money and time.

Let's say you need an entire drop-in replacement for HubSpot, customized to your own use case. You could pay Anthropic $300 for Claude Code and your engineer $65-72/hr to create your custom app in two weeks — or use an agentic swarm for maybe $10K total.

Within a weekend, you can create the same system you were paying $500/seat for, potentially saving $5K-10K a month.

If you're a CTO, where are you going to spend your monthly budget? Are there security concerns? Obviously. But you could deploy another swarm at your security vulnerabilities, or hire a company to fix them. Run the system on your own server, for your own people. Any issue, problem, or feature that's needed — just spawn a new session with a PAI-based Claude Code instance or an agentic swarm.

You still need engineers. They push the AI along on existing codebases, whether brownfield or barely-greenfield. But even then, AI can grok it. Opus 4.6 has a 200K token context window — enough to hold entire features in memory and understand the broader architecture.

## Where This Is All Going: Context Engineering

Now that I've been using PAI for almost 2.5 months, I've learned the value of a self-improving system. The question became: how do you do this at scale?

I was introduced to the concept of context engineering in the AI Native Engineer community, where Zen Van Riel did an interview with Denis Rothman, referencing the *Context Engineering* book. I deep-dived into it. It solved the problem.

Here's the formula:

**PAI + LLM = productive Digital Assistant.**

**LLMs + Context Engineering = self-improving systems that scale. No black box.**

This is what I'm learning and building toward.

RAG is important — that's why I use it. Proper prompts, important. Understanding business problems deeply, vital. That's why the context engineering framework matters: it combines all these high-level concepts so you can create feedback loops for AI systems. The system can retrieve not only the priorities of the company — the how, the why — but over time, as it accrues data, it can pull the *context* on what worked and what didn't.

This is incredibly valuable to an LLM. As the big labs keep pushing the boundaries on context limits and reasoning capabilities, as long as these models have a system to remember what works, you can take a Haiku-level model and it will compete with Opus 4.6 — and leave it in the dust, if Opus has no memory.

## The Papertrail of Trust

The trick now is nailing this scalable architecture. That's what I've been testing with my Sales RPG project and ContentEngine. How do you provide feedback systems into the core functionality? How do you get human involvement so the AI isn't just "improving" and going off the rails, but rather moving towards a specific goal with purpose?

No black box. No wondering what it's doing. Every decision, every input, every output — monitored, logged, and analyzed.

This creates a **papertrail of trust**. This gives the CEO certainty that we're not creating a system that goes "full Terminator" and wipes out the database. (Unless you gave it full access to your production database... then you have bigger problems.)

The idea is this: you set up the entire infrastructure not only to intake the data that informs the LLM's decision-making — you program in the layers that analyze your agent's decisions and create the feedback loops.

Now your engineers and your business people can look at what the system is generating and whether it's in line with the goals laid out originally. If not, you optimize the inputs, changing the outputs, ensuring the system is always aligned.

This is how the big labs do it with ChatGPT, Claude, and the rest. The difference is: now you can do it too.

---

Eight months ago I was combing through specs, line by line, hoping the AI didn't break something I couldn't see. Now I have a self-improving AI system that persists memory across sessions, orchestrates parallel agents, and builds in a weekend what used to take a quarter.

I graduated from vibe coding. And I'm not going back.
