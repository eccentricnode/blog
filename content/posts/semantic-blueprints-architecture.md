---
title: "Semantic Blueprints: Separating Domain Knowledge from AI Orchestration"
date: 2026-01-17
tags: [ai, architecture, python, multi-agent, blueprints]
draft: false
---

# Semantic Blueprints: Separating Domain Knowledge from AI Orchestration

I just shipped Phase 3 of ContentEngine, a terminal-based AI content generation system. The breakthrough wasn't the code—it was the architecture pattern.

## The Problem with Hardcoded Prompts

Most AI systems hardcode domain knowledge in Python files:

```python
def generate_post(topic):
    prompt = f"""
    Generate a LinkedIn post about {topic}.
    Use storytelling format.
    Keep it under 1200 characters.
    """
    return llm.generate(prompt)
```

**This doesn't scale.**

Want to change your content strategy? Touch the code.
Want to A/B test frameworks? Touch the code.
Want a non-technical person to edit brand voice? Good luck.

## The Solution: Semantic Blueprints

**Semantic blueprints = domain knowledge as declarative YAML files, separate from the Python orchestration engine.**

### Example Blueprint

```yaml
# blueprints/frameworks/linkedin/STF.yaml
name: STF
platform: linkedin
description: Storytelling Framework - Problem/Tried/Worked/Lesson

structure:
  sections:
    - name: Problem
      description: What challenge did you face?
    - name: Tried
      description: What approaches did you attempt?
    - name: Worked
      description: What solution actually worked?
    - name: Lesson
      description: Universal insight for the reader

validation:
  min_sections: 4
  min_chars: 600
  max_chars: 1500

compatible_pillars:
  - what_building
  - what_learning
  - problem_solution
```

### How It Works

The engine composes at runtime:

```
Context (from my daily work) +
Framework (STF blueprint) +
Constraints (BrandVoice blueprint) +
Template (Handlebars) =
Generated LinkedIn post
```

Each piece is YAML. The orchestration is Python. Clean separation.

## ContentEngine Architecture (Current State)

**All CLI-based. No GUI.**

### Phase 1: LinkedIn OAuth + Posting
```bash
# Create draft
uv run content-engine draft "Your content here"

# List drafts
uv run content-engine list --status draft

# Approve and post
uv run content-engine approve 1

# Schedule for later
uv run content-engine schedule 1 "2026-01-20 09:00"
```

### Phase 2: Context Capture
```bash
# Capture daily context from session history
uv run content-engine capture-context

# Outputs to context/2026-01-17.json
{
  "themes": ["semantic blueprints", "YAML vs JSON"],
  "decisions": ["chose YAML for readability"],
  "progress": ["Phase 3 complete, 26 stories shipped"]
}
```

Uses Ollama (llama3:8b) locally to synthesize themes from:
- PAI session history (~/.claude/History/Sessions/)
- Project notes (~/Documents/Folio/1-Projects/)

### Phase 3: Semantic Blueprints

**Blueprint Infrastructure:**
```bash
# List all blueprints
uv run content-engine blueprints list

# Output:
# CONSTRAINTS:
#   • BrandVoice
#   • ContentPillars
#   • ContentStrategy
#   • PlatformRules
#
# FRAMEWORKS:
#   • linkedin/STF
#   • linkedin/MRS
#   • linkedin/SLA
#   • linkedin/PIF
#
# WORKFLOWS:
#   • SundayPowerHour
#   • Repurposing1to10

# Show blueprint details
uv run content-engine blueprints show STF
```

**Content Generation:**
```bash
# Generate post using blueprints
uv run content-engine generate \
  --pillar what_building \
  --framework STF \
  --date 2026-01-17
```

**Validation:**
```bash
# Validate post against constraints
uv run content-engine validate <post_id>

# Checks:
# - Framework structure (4 sections for STF?)
# - Brand voice (forbidden phrases, tone)
# - Platform rules (800-1200 chars, line breaks)
```

**Workflows:**
```bash
# Sunday Power Hour: Generate 10 posts from weekly work
uv run content-engine sunday-power-hour

# Process:
# 1. Context mining (last 7 days)
# 2. Pillar categorization (35/30/20/15 distribution)
# 3. Strategy selection (traffic vs building in public)
# 4. Framework assignment
# 5. Batch generation
# 6. Validation + polish
```

### What's Implemented

**Files Ralph built (Phase 3):**
- `lib/blueprint_loader.py` - Load and cache YAML blueprints
- `lib/blueprint_engine.py` - Validation and workflow execution
- `lib/template_renderer.py` - Handlebars template rendering
- `agents/linkedin/content_generator.py` - Blueprint-driven generation
- `agents/linkedin/post_validator.py` - Multi-constraint validation

**Blueprints created:**
- 4 frameworks (STF, MRS, SLA, PIF)
- 4 constraints (BrandVoice, ContentPillars, ContentStrategy, PlatformRules)
- 2 workflows (SundayPowerHour, Repurposing1to10)

**Test coverage:**
- 403 tests passing
- mypy typed (strict mode)
- ruff compliant (100%)

## Why Semantic Blueprints Work

### 1. Maintainability
Non-engineers can edit YAML files. No code changes required to adjust:
- Content frameworks
- Brand voice characteristics
- Platform-specific rules
- Multi-step workflows

### 2. Version Control
Git shows exactly what changed in your strategy:
```bash
git diff blueprints/constraints/BrandVoice.yaml

- forbidden_phrases: ["leverage synergy"]
+ forbidden_phrases: ["leverage synergy", "circle back"]
```

### 3. A/B Testing
Create blueprint variants, test performance:
```bash
git checkout -b test/stf-v2
# Edit blueprints/frameworks/linkedin/STF.yaml
git commit -m "test: shorter STF structure (3 sections)"

# Run for 2 weeks, measure engagement
# Keep winner, discard loser
```

### 4. Composability
Blueprints compose at runtime:

```python
# Simplified pseudocode
def generate_post(pillar, framework_name, date):
    context = capture_context(date)
    framework = load_blueprint(f"frameworks/{framework_name}")
    constraints = [
        load_blueprint("constraints/BrandVoice"),
        load_blueprint("constraints/PlatformRules")
    ]

    prompt = render_template("LinkedInPost.hbs", {
        "context": context,
        "framework": framework,
        "constraints": constraints
    })

    draft = llm.generate(prompt)
    validation = validate(draft, framework, constraints)

    if validation.passed:
        return draft
    else:
        return refine(draft, validation.violations)
```

## The YAML vs JSON Decision

I chose YAML over JSON for blueprints. Here's why:

**YAML advantages:**
- More readable (less punctuation noise)
- Claude Code formats it perfectly
- Comments supported natively
- Better for human-AI collaboration

**JSON disadvantages:**
- Harder to read (braces, quotes everywhere)
- No comments (have to use hacky workarounds)
- Token-heavy (encourages "toon" compression hacks)

**Example comparison:**

```json
{
  "name": "STF",
  "structure": {
    "sections": [
      {"name": "Problem", "description": "What challenge?"},
      {"name": "Tried", "description": "What approaches?"}
    ]
  }
}
```

vs

```yaml
name: STF
structure:
  sections:
    - name: Problem
      description: What challenge?
    - name: Tried
      description: What approaches?
```

YAML wins for readability. And I hate token-saving strategies like "toon" - premature optimization that makes configs unreadable.

## ContentStrategy Blueprint: Traffic vs Building in Public

Phase 3 includes a meta-blueprint that encodes content strategy itself.

**The insight:** Content has two modes—

**Traffic (optimize for discovery):**
- Hook-first: "I spent 20min per post. Now 15 seconds. Here's how:"
- No assumed context
- Universal insights anyone can use
- Goal: Get found by hiring managers

**Building in Public (document your work):**
- Context-first: "ContentEngine Phase 3 complete. Here's what I learned:"
- Assume followers know the project
- Transparent about struggles
- Goal: Attract collaborators, show consistent shipping

**The blueprint encodes this decision:**

```yaml
# blueprints/constraints/ContentStrategy.yaml
name: ContentStrategy
current_goal: get_hired  # or build_community

platforms:
  twitter:
    default_game: traffic
    why: Discovery platform. Hook or die.

  linkedin:
    default_game: both  # STF framework = story + insight
    why: Professional audience expects depth.

  blog:
    default_game: building_in_public
    why: Deep technical content for already-interested readers.

decision_tree:
  - question: Which platform?
    answer_mapping:
      twitter: Traffic unless major milestone
      linkedin: Both (use STF framework)
      blog: Building in public

  - question: Which pillar?
    answer_mapping:
      what_building: Can be either (use STF)
      what_learning: Traffic (universal insights)
      sales_tech: Traffic (unique expertise attracts)
      problem_solution: Traffic (specific solutions)
```

**SundayPowerHour workflow uses this to decide framing per post.**

## Applications Beyond ContentEngine

This pattern isn't just for content systems. Same approach works for:

### Sales Coaching Systems
```yaml
# blueprints/frameworks/sales/SPIN.yaml
name: SPIN
description: Situation-Problem-Implication-Need framework

questions:
  situation:
    - "Tell me about your current sales process"
    - "How are you tracking leads today?"
  problem:
    - "What challenges are you facing with conversion?"
    - "Where are deals falling through?"
  implication:
    - "How does this impact your revenue goals?"
    - "What happens if this continues?"
  need_payoff:
    - "How would solving this change your business?"
    - "What would 2x conversion mean for your team?"
```

### Customer Support Templates
```yaml
# blueprints/workflows/support/RefundRequest.yaml
name: RefundRequest
steps:
  - acknowledge_issue
  - verify_eligibility
  - offer_alternatives
  - process_refund

constraints:
  tone: empathetic
  response_time: under_2_hours
  escalation_triggers:
    - abusive_language
    - legal_threat
    - high_value_customer
```

### Any Domain Expertise Encoding
If you have experts who need to iterate on strategy without touching code, semantic blueprints work.

## Tech Stack

**Language:** Python 3.11+
**Package Manager:** uv (fast, modern Python tooling)
**AI:**
- Ollama (llama3:8b) for local dev/context synthesis
- AWS Bedrock (Claude Haiku + Llama 3.3 70B) for production

**Database:** SQLite (dev) → PostgreSQL (prod)
**Blueprints:** PyYAML for parsing
**Templates:** pybars3 (Handlebars)
**Testing:** pytest, mypy (strict), ruff

**Cost:** ~$0.004/post on Bedrock ($0.12/month for 30 posts)

## What's Next

**Phase 4: Brand Planner Agent**
- Auto-decides pillar distribution
- Suggests optimal posting times
- You review the plan, not every post

**Phase 5: Autonomous Generation**
- Runs on schedule (every Sunday)
- Auto-approves posts that pass validation
- You only intervene on edge cases

**Phase 6: Engagement Feedback Loops**
- Learns from performance data
- Adjusts frameworks based on what works
- Self-improving system

## The Lesson

**Declarative > Imperative for AI systems.**

Stop hardcoding domain knowledge in Python. Encode it as blueprints instead.

When domain expertise lives in YAML:
- Non-engineers can iterate on strategy
- Version control shows what changed
- A/B testing doesn't require code changes
- Your system becomes maintainable at scale

**This is the pattern AI engineering teams use in production.**

---

## Source Code

ContentEngine is currently private (portfolio project). Planning to open-source the semantic blueprints library once I validate the pattern with engagement data.

**Tech demos available for interviews.**

Built with Python for superior AI/ML ecosystem (LangChain, Anthropic SDK, etc.).

---

**Status:** Phase 3 complete (26/26 stories shipped). All CLI-based. 403 tests passing. Ready to run semi-autonomous for 2-4 weeks and collect performance data.

Building in public. Feedback welcome.

