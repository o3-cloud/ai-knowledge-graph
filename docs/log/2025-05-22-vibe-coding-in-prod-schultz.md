---
summary: Erik Schultz (Anthropic) demonstrates vibe coding in production—rapid iteration and AI-driven development practices that blur boundaries between exploration and deployment
event_type: video
sources:
    - https://www.youtube.com/watch?v=fHWFF_pnqDk
tags:
    - vibe-coding
    - rapid-development
    - AI-driven-coding
    - production-workflow
    - iteration-patterns
    - code-generation
    - developer-experience
    - Claude
---

# Vibe Coding in Prod

**Speaker:** Erik Schultz (Member of Technical Staff, Anthropic)
**Conference:** Code w/ Claude
**Date:** May 22, 2025
**Location:** San Francisco, CA
**Platform:** YouTube (Anthropic)

## Overview

Erik Schultz presents "vibe coding in prod"—a development philosophy and practice pattern where rapid iteration, exploration, and deployment blur together using AI-assisted coding. Rather than traditional development cycles (plan → code → test → deploy), vibe coding emphasizes responsive iteration directly in production context with AI as co-developer.

## The Concept: Vibe Coding

### What Is Vibe Coding?

**Definition:**
Development approach where AI and human developer collaborate in tight feedback loops, allowing rapid exploration and iteration with minimal ceremony.

**Characteristics:**
- Fast iteration cycles
- AI as active collaborator
- Exploration over planning
- Feedback-driven development
- Production-adjacent thinking

### "Vibe" as Philosophy

**The term "vibe" implies:**
- Feel rather than specification
- Intuitive rather than formal
- Responsive rather than predetermined
- Collaborative rather than solo
- Rhythmic back-and-forth

**Not:**
- Sloppy or careless
- Without structure
- Unplanned
- Chaotic
- Irresponsible

## The Vibe Coding Workflow

### The Iteration Loop

```
Developer describes direction
    ↓
Claude generates code
    ↓
Developer feels direction
    ↓
Refine or suggest
    ↓
Claude adjusts
    ↓
Repeat until "vibe" is right
```

### Key Practices

#### 1. Rapid Feedback

**Speed matters:**
- Quick suggestion-refinement cycles
- Minutes, not hours per iteration
- Immediate feedback to AI
- Responsive collaboration

**Benefit:**
- Momentum maintained
- Exploration enabled
- Direction discovered
- Solutions emerge organically

#### 2. Feel-Based Direction

**Rather than:**
- Detailed specs
- Comprehensive PRDs
- Formal requirements
- Complete designs

**Use:**
- Rough direction
- Desired feel
- Example patterns
- Iterative feedback

**Advantage:**
- Faster to express
- AI catches intent
- Refinement through conversation
- Emerges through dialogue

#### 3. Production-Aware Development

**Thinking:**
- How will this work in production?
- Performance implications
- Reliability concerns
- Operational requirements

**Applied during:**
- Development phase
- Not as afterthought
- Influences design early
- Prevents rework

#### 4. AI as Collaborator

**Not:**
- Code generation tool
- Replacement for developer
- Deterministic process
- One-way direction

**Is:**
- Thinking partner
- Creative collaborator
- Pattern suggester
- Direction responder

**Relationship:**
- Developer leads direction
- AI suggests possibilities
- Developer refines
- Both improve output

## Advantages of Vibe Coding

### Speed

**Development accelerates:**
- No context switching
- Continuous flow state
- AI handles details
- Human provides direction
- Rapid iterations

### Exploration

**Possibilities emerge:**
- Try different approaches quickly
- Discover solutions through dialogue
- Explore design space efficiently
- Iterate on variations
- Find good patterns

### Quality

**Better outcomes:**
- Feedback loops catch issues early
- Multiple approaches evaluated
- Production thinking early
- AI suggests best practices
- Refinement iterative

### Enjoyment

**Development feels better:**
- Collaborative experience
- Flow state possible
- Creative process
- Problem-solving engaging
- Satisfying rhythm

## Challenges and Mitigations

### Challenge 1: Lack of Structure

**Risk:**
- Without planning, miss requirements
- No clear direction
- Scope creep
- Unclear success

**Mitigation:**
- Start with clear direction
- Define "vibe" being sought
- Reference implementations
- Regular checkpoints

### Challenge 2: Responsibility

**Risk:**
- Who owns decisions?
- Where did this come from?
- Can we trust the code?
- Is this reviewed?

**Mitigation:**
- Developer remains responsible
- Code review still happens
- Testing still required
- Production caution
- Audit trail maintained

### Challenge 3: Production Risk

**Risk:**
- Iteration in production unsafe
- Changes could break things
- Users affected by experiments
- Operational concerns

**Mitigation:**
- Feature flags
- Canary deployments
- Gradual rollout
- Monitoring and alerts
- Rollback capability

## Tools and Environment

### What Enables Vibe Coding

**AI capability:**
- Claude understanding intent
- Code generation quality
- Rapid interaction
- Suggestion variety

**Developer tools:**
- IDE with AI integration
- Version control
- Testing framework
- Feature flag systems
- Monitoring

### Practical Setup

**For vibe coding:**
- AI-powered editor (like Claude Code)
- Feature flags enabled
- Comprehensive monitoring
- Quick test suite
- Monitoring dashboards
- Gradual deployment

## When Vibe Coding Works

### Good Fits

- Exploration phase
- New feature prototyping
- Iteration on design
- Problem-solving
- Quick experiments
- Small changes

### Less Suitable

- Critical systems
- Major architectural decisions
- Security-sensitive code
- Compliance requirements
- High-stakes changes
- Team coordination needed

### Balanced Approach

**Optimal:**
- Use vibe coding where appropriate
- Combine with formal process where needed
- Feature flags for safety
- Production monitoring
- Team communication
- Clear ownership

## The Development Evolution

### Traditional Development

```
Plan → Code → Test → Deploy
 ↓      ↓      ↓       ↓
Weeks   Days   Hours  Risky
```

**Challenges:**
- Long cycle times
- Delayed feedback
- Testing bottleneck
- Deployment risk

### Vibe Coding Development

```
Vibe direction → AI collaboration → Iterate → Deploy (with flags)
      ↓              ↓                ↓          ↓
    Minutes       Minutes          Minutes    Minimal risk
```

**Advantages:**
- Rapid cycles
- Continuous feedback
- Early testing
- Managed risk

## Key Takeaways

1. **Vibe coding is rapid iteration** — Tight feedback loops with AI
2. **Feel over specs** — Intuitive direction rather than formal requirements
3. **Production-aware** — Think operations during development
4. **AI as collaborator** — Suggestor and shaper, not executor
5. **Speed is feature** — Fast iteration enables exploration
6. **Developer leads** — AI supports human direction
7. **Requires foundation** — Feature flags, monitoring, testing
8. **Risk managed** — Gradual rollout and canary deployment
9. **Not always appropriate** — Use where exploration valuable
10. **Emerging practice** — Changing how development works

## The Bottom Line

Erik Schultz's presentation of vibe coding in prod represents an emerging development practice enabled by advanced AI coding assistants. Rather than formal specification and planning, vibe coding emphasizes rapid iteration, intuitive direction, and collaborative problem-solving between developer and AI.

The approach works because:
- Tight feedback loops enable fast iteration
- AI can respond to feel and direction
- Production thinking happens during development
- Changes are small and safe
- Exploration becomes efficient

Vibe coding isn't irresponsible development—it's development with different tradeoffs. It trades formal specification for rapid iteration, extensive planning for emergent design, and formal testing for continuous feedback. Where appropriate (feature development, exploration, iteration), this enables faster, more enjoyable development with quality outcomes.

The future likely combines approaches: vibe coding for exploration and iteration, formal process for critical decisions, feature flags for safe deployment, and comprehensive monitoring for production confidence. The shift is from "lock in requirements early, execute carefully" to "start with direction, iterate rapidly, deploy safely"—enabled by AI as thinking partner and developer tools as enablers.
