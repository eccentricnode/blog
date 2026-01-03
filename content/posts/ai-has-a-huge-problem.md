---
title: "AI Has a Huge Problem (And a Man From 1920 Explains Why)"
date: 2026-01-03
draft: false
tags: ['ai', 'context-engineering', 'infrastructure', 'homelab']
description: "LLMs remember everything but understand nothing. Solomon Shereshevsky had the same problem. Here's why context engineering matters more than prompt engineering."
---

## AI Has a Huge Problem

LLMs have "infinite context"—trained on the entire internet. They've seen everything. Medical journals. Legal documents. Reddit threads. Stack Overflow. Poetry. Garbage.

And they hallucinate. Miss the point. Treat everything with equal weight.

They remember everything but understand nothing.

When you ask an LLM to "generate content," it pulls from everywhere. No filter. No priority. No sense of what matters for YOUR specific situation.

This is the fundamental problem with prompts.

A prompt says "do this thing." But it doesn't tell the AI what to ignore. What to prioritize. Where to focus. The AI has infinite options and no constraints—so it guesses. Sometimes it guesses well. Often it doesn't.

It reminds me of Solomon Shereshevsky.

## The Man Who Remembered Everything

Shereshevsky remembered everything.

Every conversation. Every face. Every day of his life in perfect detail. Neuropsychologist Alexander Luria studied him for decades.

His perfect memory was debilitating.

He couldn't abstract. Couldn't see patterns. Couldn't draw conclusions.

He missed the forest entirely, because he remembered every damn tree.

## Forgetting is a Human Superpower

Here's what Shereshevsky couldn't do that you can: forget.

Your brain has neurological mechanisms that FORCE you to prioritize. You forget most of what you experience—and that's not a bug. It's what lets you think clearly.

You see patterns because you've filtered out the noise.

You draw conclusions because you've discarded the irrelevant details.

You understand meaning because you're not drowning in data.

Forgetting is compression. It's prioritization. It's the difference between remembering everything and understanding anything.

## Context Engineering > Prompt Engineering

This is why context engineering matters more than prompt engineering.

Prompt engineering asks: "How do I phrase this request?"

Context engineering asks: "What should the AI be allowed to think about?"

Different question. Different results.

Build context for the AI. Tell it what you want, and why. Direct its focus. Provide boundaries for its thinking space.

By providing limitations, you enable creativity.

## The 5 Levels of Context

Dennis Richmond's "Context Engineering for Multiagent Systems" lays out a framework I've been testing:

**Level 1: Basic Prompt**
"Generate content."
→ Hallucinations. Clichés. Random outputs.

**Level 2: Linear Context**
"Here's some background. Now generate content."
→ Better, but still undirected.

**Level 3: Goal-Oriented Context**
"Your goal is X. Generate content that achieves X."
→ Starting to get directed.

**Level 4: Role-Based Context**
"You are a [role] with [expertise]. Your audience is [who]. Generate content."
→ Structured thinking.

**Level 5: Semantic Blueprint**
Defined participants. Relationships. Constraints. Output format. Success criteria.
→ Deterministic. Repeatable. Directed.

At Level 5, you're not asking the AI to guess. You're defining the exact space it can think within.

You're giving it the gift of forgetting everything else.

## What I Built Tonight

I set up a homelab server to test this.

Old PC. Ubuntu Server. Static IP. Zero networking knowledge going in. The infrastructure that scared me for months took 20 minutes once I actually tried.

But the infrastructure isn't the point.

The point is what runs on it: **an autonomous content system that uses context engineering to generate directed outputs.**

The architecture:

1. **Context Capture Layer** — Pulls my daily work. Session history. Project notes. What I'm learning, building, thinking about.

2. **Brand Planner Agent** — Reads the context. Decides what content to create. Has a semantic blueprint defining: "Position Austin as an AI force multiplier in the builder space."

3. **Platform Agents** — LinkedIn, Twitter, blog, YouTube. Each has its own blueprint. Different constraints. Different formats. Same underlying context.

4. **Feedback Loop** — Tracks what works. What gets engagement. What falls flat. Feeds back into the blueprints.

5. **Self-Improvement** — The system refines its own constraints based on results.

This isn't "AI writes my posts." This is: AI thinks within boundaries I define, generates outputs I can validate, and learns which boundaries produce the best results.

## PAI: Personal AI Infrastructure

I call the broader system PAI—Personal AI Infrastructure.

The insight: every session with AI generates signal. What worked. What didn't. What you're building. How you think. That signal usually disappears when you close the terminal.

PAI captures it.

Not everything. Not infinite context. The relevant context. Structured. Prioritized. Filtered.

Skills that define what the AI knows about specific domains.
Session history that tracks patterns over time.
Hooks that capture events as they happen.

It's the opposite of Shereshevsky. Instead of remembering everything, it remembers what matters.

## The Content Engine Test

Tonight's content engine is test #1.

The [Twitter thread](https://twitter.com/eccentric_node/status/2007418817710809191) I posted? Generated within constraints. 6 tweets, each under 280 characters, following a specific narrative arc, focused on one topic.

The [LinkedIn post](https://www.linkedin.com/posts/austin-b-johnson_ai-has-a-huge-problem-llms-have-infinite-activity-7413189644055547905-P9lB?utm_source=share&utm_medium=member_desktop&rcm=ACoAACNZGCsBShRq_ZZpkyQPxAPc1mXiN53xdIU)? Same context, different blueprint. Longer form. Professional tone. Different constraints.

Same underlying insight. Different boundaries. Different outputs.

That's the power of context engineering. You're not hoping the AI gets it right. You're defining what "right" means.

## What's Next

This is iteration one. The system will get better because it's designed to get better.

Sales AI RPG will be iteration two—deeper context, more agents, higher stakes.

The pattern scales. Context capture. Semantic blueprints. Directed outputs. Feedback loops. Self-improvement.

Building systems that build systems.

That's the bet.

---

## The Takeaway

Solomon Shereshevsky remembered everything and understood nothing.

AI has the same problem—infinite context, no filter, no priority.

The solution isn't better prompts. It's better constraints.

Build context for the AI. Tell it what to focus on. Define the boundaries of its thinking space.

By providing limitations, you enable creativity.

Context engineering > prompt engineering.
