---
summary: A reference CLAUDE.md implementation (v3.0.0) emphasizing mandatory TDD, functional programming, strict TypeScript, and a modular architecture splitting core philosophy (~100 lines) from on-demand skills and verification agents
event_type: github_file
sources:
    - https://github.com/citypaul/.dotfiles/blob/main/claude/.claude/CLAUDE.md
tags:
    - CLAUDE.md
    - TDD
    - TypeScript
    - functional-programming
    - best-practices
    - context-engineering
    - testing
---

# Reference CLAUDE.md: TDD-First Development Guidelines

**Author:** citypaul
**Version:** 3.0.0
**Type:** CLAUDE.md configuration file

## Overview

A lean, context-efficient CLAUDE.md optimized for TDD-driven TypeScript development. The architecture splits guidance into three layers: core philosophy (always loaded), skills (on-demand), and agents (specialized verification).

## Architecture

### Three-Layer Structure

```
CLAUDE.md (~100 lines)     ← Core philosophy, always loaded
    ↓
Skills (on-demand)          ← Detailed patterns when needed
    ↓
Agents (subprocesses)       ← Specialized verification
```

**Why this structure:**
- Core file stays small (~100 lines)
- Detailed patterns loaded only when relevant
- Reduces context usage
- Maintains comprehensive guidance

## Core Philosophy

### The Foundation: Mandatory TDD

**Non-negotiable:** Every production code line must be written responding to a failing test.

This enables all other principles:
- Behavior-driven testing
- Functional programming
- Incremental changes
- Working state throughout development

## Quick Reference Principles

### Testing & Development

| Principle | Implementation |
|-----------|---------------|
| TDD mandatory | Write tests first, always |
| Test behavior | Not implementation details |
| Factory functions | For test data creation |
| No 1:1 mapping | Tests organized by behavior, not files |
| 100% coverage | Through business behavior testing |

### TypeScript Requirements

| Requirement | Rationale |
|-------------|-----------|
| Strict mode | Catch errors at compile time |
| Never `any` | Type safety throughout |
| `type` over `interface` | For data structures |
| `interface` for behavior | Contracts and implementations |
| No type assertions | Without documented justification |
| Schema-first | Zod/Standard Schema → derive types |
| Schemas at boundaries | Plain types internally |

### Code Style

| Pattern | Instead Of |
|---------|------------|
| Immutable data | Mutations |
| Pure functions | Side effects |
| Early returns | Nested conditionals |
| Self-documenting code | Comments |
| Options objects | Positional parameters |
| Array methods | Loops |

## Development Workflow

### RED-GREEN-REFACTOR Cycle

```
1. RED      → Write failing test first
2. GREEN    → Minimum code to pass
3. REFACTOR → Assess (only if value-adding)
4. APPROVAL → Wait for commit approval
5. STATE    → Each increment leaves codebase working
6. LEARNING → Capture insights, merge at completion
```

### Key Behaviors

**Production code only follows failing test:**
- No speculative code
- No "I'll test it later"
- Test drives implementation

**Assess refactoring after every green:**
- Not automatic
- Only if adding value
- Avoid premature optimization

**Update CLAUDE.md for meaningful changes:**
- Document gotchas
- Capture patterns
- Record decisions
- Note edge cases

## Working with Claude

### Mandatory Practices

1. **Always follow TDD** — No exceptions
2. **Assess refactoring** — After every green phase
3. **Update CLAUDE.md** — When introducing meaningful changes
4. **Ask reflective questions** — "What do I wish I'd known at the start?"
5. **Document while fresh** — Capture context before it fades

### The Learning Loop

After significant work:
- What patterns emerged?
- What gotchas did we hit?
- What decisions did we make and why?
- What edge cases appeared?

Document these while context is fresh.

## Available Skills (On-Demand)

| Skill | Purpose |
|-------|---------|
| `tdd` | Complete TDD workflow, red-green-refactor patterns |
| `testing` | Detailed test patterns and examples |
| `typescript-strict` | TypeScript patterns, strict mode rationale |
| `functional` | Functional programming patterns with examples |
| `refactoring` | Refactoring methodology |
| `expectations` | Guidance on expectations and documentation |
| `planning` | Three-document model (PLAN.md, WIP.md, LEARNINGS.md) |

### Loading Skills

Reference a skill when entering relevant domain—detailed patterns load without bloating core context.

## Planning Documents

### Three-Document Model

**PLAN.md:**
- Overall approach
- Key decisions
- Success criteria

**WIP.md:**
- Current state
- Next steps
- Blockers

**LEARNINGS.md:**
- Insights gained
- Patterns discovered
- Future considerations

## Key Principles Summary

### Simplicity Over Complexity

When uncertain:
- Favor simplicity
- Favor readability
- Avoid over-engineering
- Let tests guide design

### Test-Driven Everything

Tests are not an afterthought:
- They drive design
- They document behavior
- They enable refactoring
- They catch regressions

### Functional First

Pure functions and immutable data:
- Easier to test
- Easier to reason about
- Fewer bugs
- Better for AI collaboration

## Key Takeaways

1. **TDD is mandatory** — Non-negotiable foundation
2. **Modular architecture** — Core + skills + agents
3. **~100 lines core** — Context-efficient design
4. **Strict TypeScript** — No `any`, schema-first
5. **Functional patterns** — Pure functions, immutable data
6. **RED-GREEN-REFACTOR** — Disciplined cycle
7. **Document while fresh** — Capture learnings immediately
8. **Skills on-demand** — Load detailed patterns when needed

## The Bottom Line

This CLAUDE.md exemplifies a disciplined, TDD-first approach to AI-assisted development. The three-layer architecture (core, skills, agents) keeps the always-loaded context small (~100 lines) while providing comprehensive guidance on demand. The foundation is simple but strict: every line of production code must respond to a failing test. This enables everything else—functional programming, strict TypeScript, incremental development. The approach treats AI collaboration as a disciplined practice, not casual assistance.
