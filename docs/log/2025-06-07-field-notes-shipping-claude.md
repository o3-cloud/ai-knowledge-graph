---
summary: Practical field notes on vibe coding with Claude—three development modes (playground, pair programming, production), CLAUDE.md as codebase constitution, anchor comments (AIDEV-NOTE), and the sacred rule that AI must never modify test files
event_type: article
sources:
    - https://diwank.space/field-notes-from-shipping-real-code-with-claude
tags:
    - Claude
    - vibe-coding
    - CLAUDE.md
    - production-systems
    - testing
    - AI-assisted-development
    - best-practices
    - git-workflow
---

# Field Notes From Shipping Real Code With Claude

**Author:** Diwank Singh Tomer
**Publication Date:** June 7, 2025

## Overview

Practical methodology for using Claude in real software development—not as fantasy but as disciplined practice. The core argument: good engineering practices become *more* critical when using AI, not less. Structure and human oversight remain essential.

## The Core Thesis

Vibe coding works, but requires:
- Discipline
- Structure
- Human oversight
- Clear boundaries

AI doesn't replace engineering rigor—it demands more of it.

## Three Development Modes

### 1. Playground Mode

**Context:** Personal projects, POCs, experiments

**Characteristics:**
- Maximum AI autonomy
- Speed trumps safety
- Learning and exploration
- Throwaway acceptable

**When to use:**
- Prototyping ideas
- Learning new technologies
- Personal tools
- Experiments

### 2. Pair Programming Mode

**Context:** Projects under ~5,000 lines

**Characteristics:**
- Collaborative approach
- Humans guide architecture
- AI handles implementation
- Regular check-ins

**When to use:**
- Small to medium projects
- Clear ownership
- Active development
- Moderate complexity

### 3. Production/Monorepo Scale

**Context:** Large, critical codebases

**Characteristics:**
- Heavily structured approach
- Clear boundaries required
- Extensive documentation
- Careful integration points

**When to use:**
- Production systems
- Team codebases
- High-stakes applications
- Complex architectures

## Key Infrastructure Elements

### CLAUDE.md Files

**Purpose:** "Constitution" for codebases

**Contents:**

| Section | Purpose |
|---------|---------|
| Architecture decisions | Why things are structured this way |
| Code style guidelines | How code should look |
| Domain glossary | What terms mean |
| Explicit restrictions | What AI must never do |

**Why it matters:**
- Provides persistent context
- Encodes team decisions
- Prevents repeated mistakes
- Guides AI behavior

### Anchor Comments

**Inline guidance using prefixes:**

```
AIDEV-NOTE: Explains why code is structured this way
AIDEV-TODO: Marks work for AI to complete
AIDEV-QUESTION: Flags uncertainty for human review
```

**Purpose:**
- Guide AI decision-making locally
- Document complex/performance-critical code
- Prevent locally suboptimal choices
- Preserve context at point of relevance

## The Sacred Rule

### AI Must Never Modify Test Files

**Why tests are sacred:**

Tests encode:
- Business intent and specifications
- Edge cases from production experience
- Domain-specific constraints
- Human understanding of requirements

**The problem with AI-generated tests:**

AI tests verify code behavior but miss:
- Production concerns (memory leaks, etc.)
- Business edge cases
- Domain knowledge
- Intent behind requirements

**Example:** Rate-limiter tests
- AI tests: Verify rate limiting works
- Human tests: Also check memory leaks, cleanup, edge cases

### The Never-Touch List

**Absolute boundaries for AI:**

| Category | Reason |
|----------|--------|
| Test files | Encode business intent |
| Database migrations | Irreversible, data-critical |
| Security-critical code | Risk too high |
| API contracts | Without versioning |
| Configuration/secrets | Security sensitive |

## Practical Techniques

### Git Workflows

**Worktrees for isolation:**
- Use git worktrees for AI experiments
- Keep experiments separate from main work
- Easy cleanup if experiments fail

**Commit tagging:**
- Tag commits with `[AI]` to indicate assistance level
- Helps reviewers focus appropriately
- Builds transparency

**Cherry-picking:**
- Keep main branch history clean
- Selective integration of AI work
- Maintain quality bar

### Token Economics

**Front-load context:**
- Provide comprehensive context upfront
- Reduces iteration cycles
- Better first-attempt results

**One task per session:**
- Focused sessions on distinct tasks
- Avoid context pollution
- Clear scope boundaries

**Avoid pollution:**
- Don't mix unrelated discussions
- Keep context relevant
- Fresh sessions for new topics

## Cultural Implications

### Transparency Over Concealment

**Recommendation:** Disclose AI assistance levels

**Benefits:**
- Builds trust
- Helps reviewers focus
- Honest about methodology
- Sets appropriate expectations

**Commit conventions:**
- `[AI-assisted]` — Human-guided, AI-implemented
- `[AI-generated]` — Primarily AI with human review
- `[Human]` — Traditional development

## Real-World Example

### Error Handling Refactor

**Task:** Refactor error handling across 500+ endpoints

**Division of labor:**

| Aspect | Owner |
|--------|-------|
| Error taxonomy | Human |
| Response format | Human |
| Architectural decisions | Human |
| Mechanical updates | AI |

**Result:**
- Traditional: 2 days
- AI-assisted: 4 hours
- Quality: Maintained through human architecture decisions

## Research Foundation

### Reference: "Accelerate"

By Forsgren, Humble, and Kim

**Key finding:** High-performing teams deploy 46x more frequently than low performers

**Implication:** Methodology matters more than tools

## Key Takeaways

1. **Three modes** — Playground, pair programming, production scale
2. **CLAUDE.md** — Codebase constitution with decisions and restrictions
3. **Anchor comments** — AIDEV-NOTE/TODO/QUESTION for local guidance
4. **Never touch tests** — Sacred rule; tests encode business intent
5. **Never-touch list** — Tests, migrations, security, API contracts, config
6. **Git discipline** — Worktrees, tagging, clean history
7. **Token economics** — Front-load context, one task per session
8. **Transparency** — Disclose AI assistance levels

## The Bottom Line

Shipping real code with Claude requires treating AI-assisted development as a discipline demanding the same rigor as traditional engineering—possibly more. The methodology centers on clear boundaries (never-touch lists), persistent context (CLAUDE.md), local guidance (anchor comments), and transparency (commit conventions). The sacred rule: AI must never modify test files, because tests encode business intent that AI cannot infer. Success comes from structure and oversight, not from expecting AI to operate autonomously. Documentation becomes code, boundaries become essential, and engineering practices become more critical, not less.
