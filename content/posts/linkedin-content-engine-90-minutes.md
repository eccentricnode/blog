---
date: '2026-01-01T18:30:00-07:00'
draft: false
title: 'I Built a LinkedIn Posting Agent in 90 Minutes'
tags: ['ai', 'content-engine', 'linkedin', 'claude', 'automation']
description: 'From zero to live post on LinkedIn using Claude Code and my Personal AI Infrastructure.'
---

### The best demo is a working system.

I have a principal engineer interview next week. Instead of preparing slides, I decided to build something. The result: a LinkedIn Content Engine that went from idea to live post in about 90 minutes.

[Here's the actual post it created.](https://www.linkedin.com/feed/update/urn:li:activity:7412668096982736897/)

## The Idea

I wanted autonomous content creation with human oversight. Not fully automated (LinkedIn's ToS prohibits that anyway), but an AI collaborator that:

1. Helps develop and refine ideas
2. Drafts content with proper formatting
3. Shows a dry-run for approval
4. Posts on my command

Buffer and Hootsuite do this, but I wanted to own the infrastructure. And I wanted to prove I could build it fast.

## What We Built

Three TypeScript files. ~150 lines total.

**oauth-server.ts** (~70 lines)
- Spins up local server on localhost:3000
- Opens browser to LinkedIn OAuth
- Catches callback, exchanges code for tokens
- Extracts user ID from JWT id_token
- Saves everything to .env

**test-connection.ts** (~25 lines)
- Verifies token works before posting
- Validates auth is configured correctly

**post.ts** (~55 lines)
- Takes content as argument
- Supports `--dry-run` for testing
- Posts to LinkedIn's ugcPosts API
- Returns post ID on success

That's it. The rest is prompt engineering - Jeff (my PAI) handles drafting, formatting, and the approval workflow.

## The Architecture

```
┌─────────────────────────────────────────────────────┐
│ Me: "I want to post about X"                        │
└─────────────────────┬───────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────┐
│ Jeff: Drafts content, adds structure, formatting    │
└─────────────────────┬───────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────┐
│ Dry Run: Shows exactly what will be posted          │
└─────────────────────┬───────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────┐
│ Me: "Looks good"                                    │
└─────────────────────┬───────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────┐
│ post.ts → LinkedIn API → Live on my feed            │
└─────────────────────────────────────────────────────┘
```

Human-in-the-loop. ToS compliant. Still 10x faster than doing it manually.

## The Timeline

Here's what actually happened:

**0:00** - Started with the idea. Jeff helped document the architecture.

**0:15** - OAuth server written. First attempt failed - redirect URI mismatch.

**0:25** - Fixed redirect URI in LinkedIn Developer Portal. Second attempt failed - "unauthorized_scope_error".

**0:35** - Realized I needed to add "Share on LinkedIn" product to my app. Requested access, got approved instantly.

**0:45** - Third OAuth attempt. Still failing - was requesting `openid profile email` scopes that weren't available yet.

**0:50** - Fixed scopes to just `w_member_social`. OAuth worked! But couldn't read my profile to get my member ID.

**0:55** - Added "Sign In with LinkedIn using OpenID Connect" product. Re-ran OAuth with `openid profile w_member_social`.

**1:00** - Success! Extracted user ID from the JWT id_token. But posting failed - wrong author URN format.

**1:10** - Fixed URN from `urn:li:member:` to `urn:li:person:`. Dry run worked.

**1:15** - Asked Jeff to help draft a Happy New Year post. He cleaned up my rambling into structured bullet points.

**1:20** - Approved the dry run. Hit post.

**1:21** - Live on LinkedIn.

~90 minutes. Most of that was fighting LinkedIn's OAuth setup, not writing code.

## The Code That Matters

The actual posting logic is dead simple:

```typescript
const postBody = {
  author: `urn:li:person:${USER_SUB}`,
  lifecycleState: "PUBLISHED",
  specificContent: {
    "com.linkedin.ugc.ShareContent": {
      shareCommentary: { text: content },
      shareMediaCategory: "NONE",
    },
  },
  visibility: {
    "com.linkedin.ugc.MemberNetworkVisibility": "PUBLIC",
  },
};

await fetch("https://api.linkedin.com/v2/ugcPosts", {
  method: "POST",
  headers: {
    Authorization: `Bearer ${ACCESS_TOKEN}`,
    "Content-Type": "application/json",
    "X-Restli-Protocol-Version": "2.0.0",
  },
  body: JSON.stringify(postBody),
});
```

The complexity isn't in the posting - it's in the OAuth dance and knowing the right URN format. Once you have a valid token and user ID, it's one API call.

## Why This Matters

This is infrastructure for a larger Content Engine:

- **LinkedIn Agent** ✅ (today)
- **Blog Agent** ✅ (already had this - it's writing this post)
- **Trend Aggregator** (next - what's working in my niche)
- **Zettelkasten → Content Pipeline** (turn my notes into posts)
- **YouTube/X Agents** (same pattern, different APIs)

The pattern is the same for all of them:
1. AI helps develop the idea
2. AI drafts the content
3. Human approves
4. System posts

I'm not trying to remove myself from the loop. I'm trying to remove the friction. The ideas are mine. The refinement is collaborative. The execution is automated.

## The Interview Angle

When I walk into that principal engineer interview, I'm not bringing slides. I'm bringing this:

"I built an autonomous content engine in a day. Here's the architecture. Here's it running live. Here's the LinkedIn post it created. Here's the blog post it wrote about itself."

That's the demo. That's the proof. Systems that build systems.

## What I Learned

1. **OAuth is always the hard part.** The actual API calls are trivial once you're authenticated.

2. **LinkedIn's URN format is weird.** The `sub` from OpenID Connect uses `urn:li:person:`, not `urn:li:member:`. Documentation is scattered.

3. **Human-in-the-loop is a feature, not a limitation.** ToS compliance aside, I *want* to approve posts before they go live. The AI is a collaborator, not a replacement.

4. **Speed compounds.** This took 90 minutes because I already had PAI infrastructure. The Blog Agent that's writing this post was already built. Each tool makes the next tool faster.

## Try It Yourself

The code is simple enough to recreate in an afternoon:

1. Create a LinkedIn app at developers.linkedin.com
2. Add "Share on LinkedIn" and "Sign In with LinkedIn using OpenID Connect" products
3. Set redirect URI to `http://localhost:3000/callback`
4. Write an OAuth server that catches the callback and exchanges the code
5. Extract user ID from the id_token JWT
6. POST to `/v2/ugcPosts` with the right headers

Or just ask your AI to help you build it. That's what I did.

---

*Built with Claude Code + PAI. Drafted by Jeff. Total time: ~90 minutes for the LinkedIn agent, ~20 minutes for this post.*
