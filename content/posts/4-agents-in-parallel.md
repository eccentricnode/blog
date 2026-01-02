---
date: '2026-01-01T22:00:00-07:00'
draft: false
title: 'I Ran 4 AI Agents in Parallel Tonight'
tags: ['ai', 'content-engine', 'automation', 'claude', 'pai']
description: 'What happens when you stop writing code and start directing systems.'
---

Tonight I orchestrated 4 AI agents working in parallel. They researched, compared, and updated documentation while I watched. It took about 60 seconds.

This is the story of how that happened.

## The Setup

I've been building what I call a Personal AI Infrastructure (inspired by [Daniel Miessler's work](https://danielmiessler.com/)). The idea: instead of doing everything yourself, you build systems that extend your capabilities. AI as a force multiplier, not a replacement.

The core of my system is Claude Code running in my terminal. No web UI. No copy-pasting. Just me talking to an AI that has access to my files, can run commands, and can spawn other AI agents.

## The Task

I was working on my Twitter agent (part of a larger content engine). Another instance of my AI assistant had built most of it earlier, but I wanted to verify the documentation was accurate.

Instead of manually checking the Twitter API docs, comparing them to my notes, and updating the discrepancies myself, I said:

> "Have an agent search my notes for Twitter agent content, another agent research the current API requirements online, compare the findings, and update anything that's wrong."

## What Happened Next

Four agents spun up:

**Agent 1: Note Searcher**
- Searched my Zettelkasten (note system) for Twitter-related content
- Found the project documentation
- Checked the setup guide and code comments

**Agent 2: Web Researcher**
- Searched for current Twitter/X API requirements
- Found that free tier limits changed (1,500 → 500 posts/month)
- Found that OAuth 1.0a is being deprecated

**Agent 3: Comparator**
- Received findings from both agents
- Identified 3 critical discrepancies
- Flagged OAuth deprecation as high priority

**Agent 4: Updater**
- Updated my project documentation with correct limits
- Added deprecation warnings to the code
- Fixed the setup guide

Total time: ~60 seconds.

## What I Actually Did

I described intent. That's it.

I didn't:
- Write a script
- Build a pipeline
- Manually coordinate the agents
- Copy-paste between windows

The system figured out how to parallelize the work. The first two agents ran simultaneously. The third waited for their results. The fourth executed the updates.

## The Insight

This is what "force multiplier" means in practice.

I didn't memorize the Twitter API changes. I didn't manually diff my notes against the docs. I didn't edit three files by hand.

I said what I wanted, validated the output, and moved on.

The agents handle volume. I handle judgment.

## The Stack

For those curious:

- **Runtime:** Claude Code (terminal-based AI assistant)
- **Orchestration:** Built-in Task tool that spawns subagents
- **Models:** Mix of Haiku (fast, cheap) and Sonnet (balanced)
- **Storage:** Local files, Zettelkasten for notes

No external services. No API orchestration layer. Just Claude Code and the file system.

## The Bigger Picture

This 4-agent demo was a small piece of a larger session. In the same evening:

- Migrated the Twitter agent from OAuth 1.0a to OAuth 2.0
- Wrote business plans for a consulting model
- Created a content strategy across LinkedIn, Blog, and Twitter
- Posted my first tweet from the new content engine

All without leaving my terminal.

The content engine is live. LinkedIn posts, blog automation, Twitter integration. Human-in-the-loop: AI drafts, I approve, system posts.

## What's Next

The same pattern that orchestrated 4 research agents can orchestrate:
- Content creation across platforms
- Code review and refactoring
- Infrastructure provisioning
- Client project delivery

You don't scale by doing more. You scale by building systems that do more for you.

---

*Built with Claude Code + Personal AI Infrastructure. The tweet about this post was also posted by the content engine.*
