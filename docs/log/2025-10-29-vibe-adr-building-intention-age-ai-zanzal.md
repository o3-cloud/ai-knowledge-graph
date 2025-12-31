---
summary: Owen Zanzal introduces Vibe ADR—a lightweight methodology combining conversational AI development with Architectural Decision Records to preserve intent, maintain context, and enable human-AI collaboration without losing architectural reasoning
event_type: blog_post
sources:
    - https://medium.com/devops-ai/vibe-adr-building-with-intention-in-the-age-of-ai-d01e93f36696
    - https://github.com/o3-cloud/vibe-adr
tags:
    - architectural-decision-records
    - AI-driven-development
    - decision-documentation
    - human-AI-collaboration
    - intentional-development
    - living-documentation
    - context-preservation
    - rapid-prototyping
    - development-methodology
    - code-with-purpose
---

# Vibe ADR: Building with Intention in the Age of AI

**Author:** Owen Zanzal
**Platform:** Medium (DevOps+AI)
**Publication Date:** October 29, 2025
**Type:** Framework and Methodology
**Repository:** https://github.com/o3-cloud/vibe-adr
**Key Problem:** Preserving architectural intent while leveraging AI speed

## Overview

Owen Zanzal introduces Vibe ADR, a lightweight but deeply intentional development methodology that solves a critical problem: how to move fast with AI coding tools without losing the architectural reasoning that keeps systems maintainable.

Vibe ADR combines conversational, AI-driven development (the "vibe") with Architectural Decision Records (ADRs)—lightweight markdown documents that capture decisions, their context, rationale, and consequences. The result is a development rhythm that preserves human intention while leveraging AI's execution speed, creating living documentation that both humans and future AI agents can understand and follow.

## The Core Problem: Speed Without Intention

### The AI Acceleration Paradox

**What's possible now:**
- Zero to prototype in minutes
- Hundreds of lines of working code from single prompt
- Entire features implemented in hours
- AI as capable code-generation tool

**What gets lost:**
- Why certain choices were made
- What assumptions guided the code
- How to safely evolve the system later
- Context for future changes
- Architectural reasoning

**The output:**
AI delivers code. But not intention.

### The Traditional Development Extremes

**Extreme 1: Code First, Figure It Out Later**
```
Immediate action
    ↓
Fast progress
    ↓
No documentation
    ↓
Systems drift quickly
    ↓
Unmaintainable chaos
```

**Problems:**
- Chaotic and brittle
- Silent design decisions
- Lost context
- Accumulation of technical debt

**Extreme 2: Spec First, Build Later**
```
Detailed planning
    ↓
Comprehensive specification
    ↓
Implementation phase
    ↓
Spec often outdated by first commit
    ↓
Waterfall rigidity
```

**Problems:**
- Rigid and slow
- Overhead-heavy
- Spec-code drift inevitable
- Requirements emerge during building
- Pre-emptive bureaucracy

### Why AI Amplifies the Problem

**Without explicit decision capture:**
- AI makes silent architectural choices
- Human collaborators can't follow reasoning
- "Quick experiments" accumulate
- System design drifts incrementally
- Future AI agents lack context

**Result:**
Speed becomes liability without intentional documentation.

## Vibe ADR: A New Development Rhythm

### The Core Concept

**Vibe ADR stands for:**

**Vibe** → Conversational, AI-driven, exploratory mode of development
- Dialogue-based
- Iterative
- Collaborative
- Responsive to discovery

**ADR** → Architectural (or Adaptive) Decision Record
- Lightweight markdown documentation
- Captures decision + context + rationale + consequences
- Living document, not static spec
- Version-controlled in repository

### The Unified Approach

```
Human intention (expressed in ADR)
    ↓
AI execution (implements ADR)
    ↓
Review and reflection (update ADR with learnings)
    ↓
Living documentation (decision graph in repository)
    ↓
Context for future work (humans and AI agents)
```

### The Development Heartbeat

**Vibe ADR creates iterative rhythm:**

```
Decide
    ↓
Build (with AI)
    ↓
Review
    ↓
Document
    ↓
Reset context
    ↓
Loop to next decision
```

Each cycle adds a node to growing decision constellation—the living architecture of the system.

## The Detailed Vibe ADR Workflow

### Step 1: Define the Vibe (High-Level README)

**Purpose:**
Capture project's north star—its purpose and philosophy before implementation details.

**What to include:**

**Project identification:**
- Project name
- Concise description
- Problem statement
- User goals

**Guiding principles:**
- Key constraints and philosophy
- Technical preferences ("favor simplicity over performance")
- Operational requirements ("runs offline first")
- Quality attributes

**Cultural tone:**
- Emotional character ("should feel playful")
- Trust and reliability signals ("should feel trustworthy")
- Design values ("user-centric," "privacy-first")
- Team culture ("experimentation encouraged")

**Why this matters:**
This README is living intention. It guides both humans and AI toward aligned choices. It's not instructions; it's philosophy.

### Step 2: Draft Your First ADR

**Purpose:**
Capture one significant decision with full context and reasoning.

**File naming:**
- Location: `docs/decisions/`
- Format: `0001-decision-name.md`, `0002-next-decision.md`
- Sequential numbering with zero-padding
- Discoverable and reviewable in version control

**What decisions ADRs capture:**

Not limited to architecture:
- Language or framework selection
- API or UX patterns
- Testing strategies
- Tooling choices
- Infrastructure setups
- Workflow or process decisions
- Tool preferences ("Use Claude Code for unit generation")

**Standard ADR sections:**

**Context and Problem Statement**
- What problem led to this decision?
- What was the situation that made decision necessary?
- Background that matters

**Vibe Context**
- Emotional or cultural tone guiding this decision
- How does this fit the project's vibe?
- What principles apply here?

**Decision Drivers**
- What factors motivated the choice?
- What constraints matter?
- What trade-offs were considered?
- What's non-negotiable?

**Considered Options**
- What alternatives were evaluated?
- Why were alternatives rejected?
- What would choosing differently have meant?

**Decision Outcome**
- The chosen option
- Explicit rationale
- Why this over others
- What we're committing to

**Consequences**
- Trade-offs (what we gain, what we sacrifice)
- Pros and cons
- Future implications
- Dependencies created

**Confirmation**
- Tests or validation proving alignment
- How to verify decision was correct
- Success criteria

**AI-Specific Sections**
- Guidance level for AI assistant
- Tool preferences
- Test expectations
- Context the AI needs

**Feedback Log**
- Post-implementation reflections
- Learnings discovered during building
- Adjustments needed
- What surprised us

**Dynamic Documentation Metadata**
- YAML front-matter for automation
- Status (active, superseded, deprecated)
- Related ADRs
- Links to commits

**Important principle:**
The VIBE_ADR_TEMPLATE is a guide, not law. Every project differs. Trim unused sections aggressively.

### Step 3: Implement the ADR (with AI)

**Process:**
Hand the ADR and README to your AI coding agent (Claude Code, Devin, etc.)

**Example prompt:**
```
Based on ADR #1 and the project README, generate the initial codebase
in Go, create a service for session tracking, include tests for
concurrent sessions, and stage in branch adr-001-init.
```

**Best practices:**

**Plan before coding:**
- Ask AI to plan the implementation
- Generate code based on plan
- Write tests to validate

**Feed full context:**
- Include README
- Include relevant ADRs
- Provide any existing code patterns
- Share constraints and preferences

**Keep scope focused:**
- Implementation scoped only to what ADR covers
- Don't let implementation drift to unrelated decisions
- One ADR = one focused implementation

**Make assumptions explicit:**
- Have AI generate test stubs showing its assumptions
- Review and verify assumptions
- Correct if assumptions are wrong

**Explore options when uncertain:**

```
"When uncertain, parallelize insight"

Multiple plausible approaches?
    ↓
Have AI implement all three in parallel branches
    ↓
Compare performance, clarity, maintainability
    ↓
Decide based on concrete comparison
    ↓
Record that decision in next ADR
```

### Step 4: Review, Reflect, and Update

**After implementation:**

**Validate:**
- Run the generated tests
- Verify implementation works
- Check against success criteria

**Reflect with AI:**
Ask the AI for ADR review:
- Did implementation match decision?
- What changed during building?
- Why did those changes happen?
- What assumptions proved wrong?
- What surprised you?

**Update the ADR:**
- Record actual outcomes
- Document insights in Feedback Log
- Capture learnings about the decision
- Note if assumptions changed

**Link to commits:**
- Record commits that implement ADR
- Enable traceability (Commit #f21a8b implements ADR-001)
- Enable rollback if needed
- Create decision-code connection

**Result:**
Every meaningful code change anchored to decision record explaining its origin and intent.

### Step 5: Commit, Clear Context, and Loop

**Finalization:**

**Commit together:**
- Code + ADR committed together
- Both are part of decision node

**Tag repository (optional):**
- Tag like `vibe-adr-001`
- Enables easy reference
- Links history to decisions

**Clear AI context:**
- End the AI session
- Start fresh session for next ADR
- Prevents assumption bleed-over
- Keeps context clean

**Loop to next decision:**
- Start next ADR for following decision
- Each cycle adds to constellation
- Growing architecture visible in decisions

## Bootstrap with llms.txt

### Accelerating Onboarding

**What is llms.txt:**
A file that lists core documents, setup checklist, and workflow expectations.

**How to use:**
```
https://raw.githubusercontent.com/o3-cloud/vibe-adr/refs/heads/main/llms.txt
```

Paste that URL into agent session or use as context attachment.

**What it enables:**
- Agent understands Vibe ADR immediately
- Agent knows which documents to load
- Agent understands workflow expectations
- Instant architectural context
- Faster alignment on first prompt

**Bootstrapping effect:**
New AI sessions can start with full context without manual setup.

## Turning ADRs into Living Documentation

### From Decision Records to System Understanding

**Over time:**
ADRs accumulate into your system's architecture.

**Combination of ADRs + llms.txt creates:**
- Self-documenting system
- Living architecture
- Evolutionary history
- Human-readable design rationale

### Advanced Practices

**Generate Dynamic README:**
Synthesize short summary from latest ADRs:
```
Current architecture summary:
- Backend: Go
- Database: PostgreSQL
- Async: NATS message queue
- Testing strategy: Property-based + integration
- Key principles: Offline-first, fault-tolerant
```

**Build Decision Timelines:**
Scripts that visualize ADR evolution over time:
- When decisions were made
- How decisions evolved
- Supersessions and deprecations
- Architectural trajectory

**Enable AI Rehydration:**
- Feed past ADRs to Claude Code
- Restore full architectural context instantly
- Future sessions inherit all prior reasoning
- No need to re-establish context

**Empower New Developers:**
- Learn entire system by reading ADRs
- No need to dig through chat history
- Understand reasoning, not just code
- Quick ramp-up on architecture

**Standardize Agent Onboarding:**
- Point agents to llms.txt
- Bootstrap context automatically
- Consistent onboarding every time
- Self-service for future agents

**Result:**
Project becomes self-documenting, agent-friendly, developer-friendly system.

## Vibe ADR vs. Traditional Approaches

### Spec-Driven Development: Problems and Solutions

| Problem | How Vibe ADR Solves It |
|---------|----------------------|
| Up-front overhead | Documentation created incrementally, not all at once |
| Rigidity/Waterfall | Each ADR can be replaced, branched, superseded anytime |
| Unknown requirements | Decisions made and captured as they emerge |
| Spec-code drift | Each ADR reviewed right after implementation |
| Low developer engagement | Developers still "vibe" with AI; feels natural, lightweight |

**Key difference:**
Vibe ADR turns specification into moment-of-decision reflection, not pre-emptive bureaucracy.

### What Vibe ADR Learns from Spec-Driven Development

**Borrows these strengths:**

**Clarity of Purpose**
- Concise list of user stories in README
- Success criteria explicit
- Goals always visible

**Structured Breakdown**
- Ask AI to generate task plan from ADRs
- Dependency mapping
- Organized decision graph

**Testing Discipline**
- Every ADR tied to specific tests
- No decision complete without verification
- Quality built into decision process

**Traceability**
- Link commits, PRs, CI to ADR IDs
- Enable auditability
- Historical record of decisions

**Governance at Scale**
- Review ADRs in sprint retrospectives
- Maintain decision logs in version control
- Scale team decisions
- Organizational learning

**Result:**
Vibe ADR gets reliability of spec-driven workflows without the overhead.

## Repository Structure in Practice

### Typical Project Layout

```
/project-root
│
├── README.md
│   (Project vision, vibe, principles)
│
├── docs/
│   └── decisions/
│       ├── 0001-adopt-vibe-adr.md
│       ├── 0002-define-llms-txt.md
│       ├── 0003-backend-language-choice.md
│       ├── VIBE_ADR_TEMPLATE.md
│       └── index.md (auto-generated summary)
│
├── src/
│   (Implementation from ADRs)
│
└── tests/
    (Tests validating ADRs)
```

### Living Documentation Pipeline

**Process:**
```
Write ADRs in version control
    ↓
Implement from ADRs
    ↓
Review with AI
    ↓
Update ADRs with learnings
    ↓
Run summarizer script
    ↓
Generate updated README from ADRs
    ↓
Living documentation = current reality
```

**Result:**
Not aspirational spec that went stale. Living documentation generated from actual decisions.

## Practical Implementation Tips

### Getting Started

**1. Start small**
- Pick one feature
- Practice one ADR loop
- Learn rhythm before scaling

**2. Use version control from day one**
- Store ADRs under `/decisions/`
- Every ADR is a commit
- History is visible

**3. Feed AI context**
- Always include README
- Always include relevant ADRs
- Provide existing patterns
- Share constraints

**4. Link everything**
- Each commit references its ADR
- Each ADR links back to commits
- Decision-code connection visible
- Traceability maintained

**5. Review weekly**
- Generate ADR status summaries
- Track active vs. deprecated
- Visualize architecture
- Keep momentum visible

**6. Automate reflection**
- Have AI update "Feedback & AI Notes"
- Run post-commit review
- Capture learnings automatically
- Reduce manual overhead

**7. Encourage branching**
- Torn between solutions?
- Implement all three
- Compare concrete implementations
- Decide based on evidence

**8. Automate the README**
- Script regenerates from ADR metadata
- Always current
- Reduces maintenance
- Single source of truth

**9. Keep ADRs short**
- One decision per file
- 1-2 pages maximum
- Dense with signal
- Easy to read

**10. Reset often**
- Clear AI context between loops
- Prevents architectural drift
- Keeps assumptions explicit
- Each ADR is fresh start

## Key Takeaways

1. **AI speed needs intention anchor** — Capture reasoning, not just code
2. **ADR captures decision context** — Not just "what" but "why"
3. **Vibe sets cultural tone** — README guides human and AI choices
4. **Five-step workflow creates rhythm** — Define → Build → Review → Document → Loop
5. **ADRs are executable intent** — Feed to AI for implementation
6. **Assumptions made explicit** — AI generates test stubs showing them
7. **Parallel implementation when uncertain** — Implement alternatives; decide empirically
8. **Review immediately after building** — Capture learnings while fresh
9. **Link code to decisions** — Traceability between commits and ADRs
10. **Clear context between loops** — Prevent assumption bleed-over
11. **ADRs form decision graph** — Together they become system architecture
12. **Living documentation** — Generated from reality, not aspirational spec
13. **llms.txt bootstraps context** — New sessions start with full architectural context
14. **Dynamic README from ADRs** — Always current summary
15. **Decision timelines visualize evolution** — See how architecture emerged
16. **New developers learn from ADRs** — Reasoning visible, not hidden
17. **Agents understand context** — Self-documenting for future AI
18. **Spec-driven + adaptive approach** — Reliability without bureaucracy
19. **Testing tied to decisions** — Verification baked into process
20. **Scalable governance** — Works for individuals and teams

## The Bottom Line

Owen Zanzal's Vibe ADR methodology solves the critical problem of modern AI development: how to move fast while preserving architectural reasoning and enabling true human-AI collaboration.

**The core insight:**
AI can generate code faster than ever, but without explicit decision capture, the reasoning gets lost. ADRs preserve that reasoning as living documentation that both humans and future AI agents can understand.

**The methodology:**
Five-step rhythm (Define → Build → Review → Document → Loop) that balances speed with intentionality. Each cycle adds a node to your system's decision graph.

**The key innovation:**
ADRs are not post-hoc documentation—they're executable specifications for AI. Feed an ADR to Claude Code and get implementation that matches your intent.

**What gets preserved:**
- Why decisions were made
- What assumptions guided choices
- How to safely evolve the system
- Context for future changes
- Architectural reasoning

**What gets enabled:**
- Fast prototyping without losing intent
- True collaboration between human and AI
- Self-documenting systems
- Rapid onboarding (new developers and AI agents)
- Evolutionary architecture with full history

**For practitioners:**
Vibe ADR is immediately applicable. Pick one feature, practice one loop, learn the rhythm. The template is a guide; adapt to your project.

**For teams:**
This scales. Use ADRs in retrospectives. Maintain decision logs. Build organizational memory. Archive architectural reasoning.

**For the future:**
As AI agents become more capable, having full decision context in ADRs enables them to inherit architectural understanding instantly. Your Vibe ADR repository becomes the constitution for future AI collaborators.

**The philosophy:**
Decide with clarity. Build with speed. Document with soul.

That's what Vibe ADR makes possible.

