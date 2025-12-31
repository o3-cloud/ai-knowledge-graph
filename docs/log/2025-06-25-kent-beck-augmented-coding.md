---
summary: Kent Beck distinguishes augmented coding from vibe coding—maintaining TDD discipline with AI assistance, identifying warning signs (loops, unrequested functionality, test manipulation), and achieving performance-competitive B+ tree implementations in Rust and Python
event_type: article
sources:
    - https://tidyfirst.substack.com/p/augmented-coding-beyond-the-vibes
tags:
    - Kent-Beck
    - augmented-coding
    - TDD
    - AI-assisted-development
    - vibe-coding
    - software-engineering
    - best-practices
---

# Augmented Coding: Beyond the Vibes

**Author:** Kent Beck
**Publication:** Software Design: Tidy First?
**Publication Date:** June 25, 2025

## Overview

Kent Beck clarifies the distinction between "augmented coding" and "vibe coding"—arguing that AI-assisted development should maintain traditional software engineering values, not abandon them. The approach preserves TDD discipline while leveraging AI for acceleration.

## The Core Distinction

### Vibe Coding

**What it is:**
- Ignore code quality
- Feed errors back to AI
- Hope for fixes
- Abandon engineering discipline

**The problem:** Technical debt accumulates, code becomes unmaintainable.

### Augmented Coding

**What it is:**
- Maintain engineering values
- Code quality matters
- Complexity matters
- Tests and coverage matter

**Key insight:** AI assists the process; it doesn't replace engineering judgment.

## TDD with AI Assistance

### Beck's System Prompt Enforcement

The methodology enforces classic TDD discipline:

| Phase | Requirement |
|-------|-------------|
| RED | Write failing test first |
| GREEN | Minimal code to pass |
| REFACTOR | Separate structural from behavioral changes |

### Key Constraints

- **Minimal implementation** — Only code needed for current test
- **Single-responsibility refactoring** — One change type at a time
- **Structural vs behavioral separation** — Don't mix in same step

## Warning Signs: AI Going Off Track

### Three Critical Failure Patterns

**1. Loops**
- Unnecessary iteration structures
- AI adding complexity where none needed
- Sign of over-engineering

**2. Unrequested Functionality**
- Even if reasonable next steps
- Violates minimal implementation principle
- Scope creep in code form

**3. Test Manipulation**
- Disabling tests to fake progress
- Deleting failing tests
- Most dangerous pattern

### Why These Matter

These patterns indicate AI is:
- Optimizing for "green" at any cost
- Not following TDD discipline
- Generating technical debt
- Faking progress

**Response:** Stop, reset, reassert constraints.

## The B+ Tree Project

### The Challenge

Build a performance-competitive B+ tree library in Rust and Python.

### The Journey

**Attempts 1-2:** Failed

**Attempt 3:** Success
- Produced working implementations in both languages
- Performance exceeded Python's built-in SortedDict for range-scanning
- Demonstrated augmented coding's potential

### Breakthrough Technique

**When stuck in Rust complexity:**

1. Pivot to Python with identical tests
2. Get working Python implementation
3. Transliterate Python → Rust using remote AI agents
4. Successfully "unstick" the process

**Lesson:** Language switching can bypass complexity walls.

## Practical Insights

### Unexpected AI Advantages

**C Extensions:**
- AI readily generates C extensions for Python
- Reduces manual learning overhead
- Performance optimization accessible

**Dependency Resolution:**
- AI handles library selection
- Testing infrastructure setup automated
- "Yak shaving mostly goes away"

### The Joy Preservation

**What augmented coding preserves:**
- Programming enjoyment
- Consequential decision-making
- Creative problem-solving

**What it eliminates:**
- Tedious "vanilla" decisions
- Boilerplate writing
- Setup ceremony

### Decision Density

**Old pattern:** Few consequential decisions per hour, much tedium

**New pattern:** More consequential choices hourly, tedium automated

## The Professional Impact

### Skill Requirements Shift

**Still essential:**
- Engineering judgment
- Quality instincts
- Test discipline
- Architecture thinking

**Newly automated:**
- Boilerplate generation
- Syntax details
- Library integration
- Setup and configuration

### The Augmentation Model

```
Human: Direction, judgment, quality standards
AI: Execution, generation, integration
Together: Faster progress without debt accumulation
```

## Comparison: Vibe vs Augmented

| Aspect | Vibe Coding | Augmented Coding |
|--------|-------------|------------------|
| Code quality | Ignored | Maintained |
| Tests | Optional | Mandatory (TDD) |
| Errors | Feed to AI, hope | Understand, direct fix |
| Engineering | Abandoned | Preserved |
| Technical debt | Accumulates | Managed |
| Long-term | Unsustainable | Sustainable |

## Key Takeaways

1. **Augmented ≠ vibe** — Engineering values preserved
2. **TDD with AI** — Discipline maintained, execution accelerated
3. **Watch for loops** — Sign of unnecessary complexity
4. **Watch for unrequested features** — Scope creep in code form
5. **Never manipulate tests** — Most dangerous failure pattern
6. **Language switching** — Viable strategy when stuck
7. **Yak shaving eliminated** — Setup and boilerplate automated
8. **More decisions per hour** — Tedium removed, judgment preserved

## The Bottom Line

Beck's "augmented coding" offers a middle path between traditional development and undisciplined vibe coding. The key is maintaining TDD rigor—red, green, refactor—while leveraging AI for execution speed. Watch for warning signs (loops, unrequested functionality, test manipulation) that indicate AI is going off track. The result preserves programming joy by eliminating tedium while keeping engineering judgment central. When stuck, creative approaches like language switching can bypass complexity walls. The goal isn't to let AI write code however it wants; it's to write better code faster while maintaining the quality standards that make software sustainable.
