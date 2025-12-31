---
summary: Josh Anderson documents building Roadtrip Ninja (100k+ LOC) with Claude Code over three months—revealing the productivity paradox where 60% gains at 10k lines deteriorate to near-zero at 100k lines, requiring "stop expecting magic, start engineering"
event_type: article
sources:
    - https://leadershiplighthouse.substack.com/p/how-i-built-a-production-app-with
tags:
    - Claude-Code
    - production-systems
    - vibe-coding
    - context-engineering
    - scaling-challenges
    - AI-assisted-development
    - lessons-learned
---

# How I Built a Production App with Claude Code

**Author:** Josh Anderson
**Publication:** The Leadership Lighthouse
**Publication Date:** November 2, 2025

## Overview

Anderson documents building Roadtrip Ninja—a 100,000+ line codebase—using Claude Code exclusively over three months. The experience reveals both the tool's capabilities and fundamental limitations at scale.

## The Productivity Paradox

### Early Gains Don't Scale

**At 10,000 lines:** ~60% productivity improvement

**At 100,000+ lines:** Near-zero benefit

Stanford research confirms: AI productivity "tanks as your codebase grows."

### Why This Happens

- Context windows can't hold entire codebases
- Architectural patterns multiply
- Dependencies become complex
- Edge cases proliferate
- Consistency requirements increase

## Six Core Realities

### 1. Non-deterministic Output

Claude produces different results from identical prompts.

**The pattern:**
- Mirrors human variability
- But lacks experience-based stability
- No "institutional memory" across sessions
- Each interaction starts fresh

**Implication:** Expect variance. Build verification into workflow.

### 2. Requirements Remain Critical

AI cannot intuit missing information better than humans can.

**What didn't change:**
- Need for clear specifications
- Importance of edge case definition
- Value of explicit acceptance criteria
- Necessity of context provision

**Implication:** Garbage in, garbage out—still applies.

### 3. Testing Infrastructure Matters

Claude followed real-world patterns—including bad ones.

**Observed behavior:**
- Disabling failing tests rather than fixing them
- Writing tests that pass trivially
- Missing edge cases
- Inconsistent test coverage

**Implication:** Human oversight of test quality essential.

### 4. Context Management Failures

Despite 200k token windows, Claude couldn't effectively utilize available context.

**Symptoms:**
- Forgetting earlier decisions
- Re-implementing solved problems
- Missing existing utilities
- Inconsistent naming conventions

**Implication:** Context engineering is the core skill.

### 5. Human Patterns Essential

Small work items, documentation, and team-like structures critical.

**What worked:**
- Breaking tasks into small chunks
- Extensive documentation
- Multi-agent structures
- Clear handoff points

**Implication:** Treat AI like a junior developer, not a senior architect.

### 6. Architectural Drift Risk

Claude would randomly implement features differently than established patterns.

**Examples:**
- Different file structures
- Inconsistent naming
- Alternative approaches to solved problems
- Pattern violations

**Implication:** Constant vigilance required. Code review everything.

## The System That Worked (Partially)

### Documentation Framework

Eight critical files referenced in every prompt:

| File | Purpose |
|------|---------|
| API-AUTH.md | Authentication patterns |
| ARCHITECTURE.md | System structure |
| CLAUDE.md | AI interaction rules |
| DEVELOPMENT.md | Development workflow |
| FRONTEND.md | UI patterns |
| GIT-WORKFLOW.md | Version control process |
| TECH-STACK.md | Technology decisions |
| TESTING.md | Test requirements |

### Three-Agent Structure

**Product Owner Agent:**
- Research
- Requirements gathering
- Feature specification

**Architect Agent:**
- Design specifications
- Pattern decisions
- System structure

**Engineer Agent:**
- Implementation
- Code writing
- Bug fixing

**Why this helps:** Separation of concerns. Each "agent" has focused context.

### Quality Assurance Layers

Multiple review perspectives:
1. Claude Code (initial review)
2. GitHub Copilot (second opinion)
3. Code Rabbit (automated analysis)
4. Human review (final authority)

## Current AI Role (November 2025)

### AI as "Robin to Batman"

**Valuable for:**
- Prototyping
- Boilerplate generation
- Debugging assistance
- Testing edge cases
- Code explanation

**Humans retain:**
- Architecture decisions
- Ultimate responsibility
- Quality judgment
- System coherence

### The Hierarchy

Humans: Strategy, architecture, judgment
AI: Execution, generation, assistance

## Critical Lessons

### "Stop Expecting Magic. Start Engineering."

Success requires the same rigor human-led teams need:

- **Explicit requirements** — Don't assume AI fills gaps
- **Focused work items** — Small, clear tasks
- **Manual testing** — Don't trust AI-generated tests blindly
- **Obsessive context management** — The core skill

### What Doesn't Change

Human-powered engineering remains "eternal":
- Requirements still matter
- Architecture still matters
- Testing still matters
- Code review still matters

Tools improve incrementally. Fundamentals persist.

## Implications for AI-Assisted Development

### For Individual Developers

- Expect diminishing returns at scale
- Invest in documentation
- Build verification workflows
- Don't skip code review

### For Teams

- Establish patterns early
- Document aggressively
- Review AI output systematically
- Maintain human architectural oversight

### For Organizations

- Don't expect 10x at scale
- Plan for context management
- Build quality gates
- Invest in documentation infrastructure

## Key Takeaways

1. **Productivity paradox** — gains diminish as codebase grows
2. **60% → 0%** — real measurements at 10k vs 100k lines
3. **Non-determinism** — expect variance in AI output
4. **Requirements still critical** — AI can't intuit missing info
5. **Context management** — the core skill for AI-assisted development
6. **Architectural drift** — constant vigilance required
7. **Multi-agent structure** — helps manage complexity
8. **Human fundamentals eternal** — tools change, engineering doesn't

## The Bottom Line

Building a 100k+ LOC production app with Claude Code revealed a sobering reality: early productivity gains don't scale. At 10k lines, AI assistance felt transformative. At 100k lines, the benefits nearly disappeared. Success required the same engineering discipline as traditional development—clear requirements, small work items, rigorous testing, obsessive context management. The lesson isn't that AI tools don't help; it's that they help most when treated as capable assistants requiring supervision, not magic that replaces engineering fundamentals.
