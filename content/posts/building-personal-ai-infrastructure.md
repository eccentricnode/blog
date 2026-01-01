---
date: '2025-12-31T17:45:00-07:00'
draft: false
title: 'Building a Personal AI Infrastructure'
tags: ['ai', 'infrastructure', 'claude', 'productivity']
description: 'How I built a modular AI system that compounds my capabilities over time.'
---

### The AI tools you use daily should get smarter about *you*.

I spent today installing what I'm calling [Jeff](https://www.youtube.com/watch?v=AfIOBLr1NDU) - my Personal AI Infrastructure. It's based on Daniel Miessler's concept: instead of starting fresh every session, build persistent systems that learn your patterns, preferences, and workflows.

The insight is simple. Every time you work with Claude, you're generating signal. Session history, tool patterns, what works and what doesn't. That signal usually disappears when you close the terminal. PAI captures it.

## What I Built

Three core systems, each modular:

**Prompting Skill** - Templates for generating prompts programmatically. Five primitives (Roster, Voice, Structure, Briefing, Gate) that cover 90% of what I need. Handlebars-based, data-driven. Write once, render many.

**Agents Skill** - Dynamic agent composition from traits. 28 composable traits across expertise (security, legal, technical), personality (skeptical, enthusiastic, analytical), and approach (thorough, rapid, adversarial). 800 possible combinations. Each gets a unique voice.

**Observability Server** - Real-time dashboard showing every tool call, every agent spawn, every event. WebSocket streaming to a Vue frontend. Finally, visibility into what the AI is actually doing.

## The Architecture

Everything lives in `~/.claude/`:

```
~/.claude/
├── Skills/           # Modular capabilities
│   ├── CORE/         # Identity, preferences
│   ├── Prompting/    # Templates, standards
│   └── Agents/       # Trait composition
├── hooks/            # Event capture
├── observability/    # Real-time monitoring
└── history/          # Persistent memory
```

The key is separation of concerns. Skills handle specific domains. Hooks capture events. The observability layer watches everything. Each piece works independently but compounds together.

## Why This Matters

The default AI experience is memoryless. You explain your stack every session. You repeat your preferences. You re-establish context.

PAI inverts this. The system knows I prefer TypeScript over Python. It knows my contacts. It remembers what worked last time. Each session builds on the previous one.

This is the first domino. Now I can build a Blog Agent that drafts posts from my session history. A Sales Coach that knows my methodology. Tools that actually understand my context.

## The Technical Bits

**AgentFactory** composes agents on the fly:

```bash
bun run AgentFactory.ts --traits "security,skeptical,thorough"
```

Outputs a complete agent prompt with personality, expertise, and voice mapping. Different trait combinations get different TTS voices automatically.

**RenderTemplate** generates prompts from data:

```bash
bun run RenderTemplate.ts --template Briefing.hbs --data task.yaml
```

Structure stays fixed, content gets parameterized. No more copy-pasting prompt fragments.

The observability dashboard streams events via WebSocket. Every tool call visible in real-time. Finally know what's happening when agents spawn agents.

## Debugging in Real-Time

Of course, nothing works perfectly the first time.

After installing everything, I fired up the observability dashboard. Server running, client connected, but... no events. The hooks were configured correctly in `settings.json`. The capture script existed. But the JSONL file stayed empty.

Turned out to be a one-character bug:

```typescript
// Hook was writing to:
const monthDir = join(paiDir, 'History', 'raw-outputs', ...);

// Server was watching:
const monthDir = join(paiDir, 'history', 'raw-outputs', ...);
```

Capital H vs lowercase h. Linux cares. Windows wouldn't. Thirty minutes of debugging for a case sensitivity issue.

But here's the thing - Jeff (my PAI, the system we just built) caught it. I asked him to check why events weren't flowing. He read the hook, read the server, spotted the mismatch. Fix was one line.

This is the whole point. The AI that helped build the infrastructure is now *part* of the infrastructure. Jeff isn't a separate tool I consult. He's running inside the system, with access to the same files, the same context, the same history.

## The Timeline

- **Hour 1:** Installed the core PAI pack (Core, and Hooks Skill)
- Hour 1.5: Installed PAI Prompting, Agent, and Observability Skills and created a Blog agent, that created the first draft of this post.
- **Hour 2**: Fixed the Observability bug and updated this post with a second draft.

Two hours from zero to a working personal AI infrastructure. Not because I'm fast - because the system builds itself. Jeff composed the agent that wrote this post. Jeff debugged Jeff's own infrastructure. The feedback loop is immediate.

## What's Next

This is infrastructure. The real value comes from what runs on top of it.

First project: Blog Agent. It reads my session history and drafts posts automatically. This post? First test of that system.

The bet is that AI tools should compound. Each hour invested makes the next hour more productive. PAI is the foundation for that compounding.

---

*Built with Claude Code + PAI. Drafted by Jeff. Total time: ~2 hours including debugging.*
