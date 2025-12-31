---
summary: Documents large-scale AI-assisted code migration of 6000 React tests from Testing Library v13 to v14, demonstrating effective strategies for structuring automation with ASTs, iterative improvement, and human oversight
event_type: article
sources:
    - https://eliocapella.com/blog/ai-library-migration-guide/
tags:
    - code-migration
    - AI-assisted-automation
    - AST-codemods
    - React-testing
    - jscodeshift
    - automation-strategy
    - human-AI-collaboration
---

# Migrating 6000 React Tests Using AI Agents and ASTs

**Author:** Elio Capella (Filestage)
**Publication:** eliocapella.com
**Publication Date:** November 21, 2025

## Overview

Large-scale code migrations are tedious, repetitive, and error-prone. This article documents a successful migration of 6000+ React tests from Testing Library v13 to v14 using AI agents paired with Abstract Syntax Tree (AST) automation. The approach demonstrates that breaking large tasks into manageable chunks with clear validation yields better results than attempting end-to-end automation.

## The Challenge

**React Testing Library v14** introduced breaking changes:
- All APIs became asynchronous
- New setup patterns required
- 970 test files affected
- 6000+ individual test cases
- Massive scope for manual refactoring

Traditional approach: Manually update all tests. Alternative: Systematize the migration through AI-assisted automation.

## Three-Part Strategy

### Part 1: Research Phase

Before automating, **understand the problem deeply**:

- Researched React Testing Library v14 migration requirements
- Identified what actually changed in the library
- Documented patterns that needed transformation
- Built mental model of scope and complexity

Claude's research capabilities proved valuable for this phase—scanning documentation, understanding patterns, and building comprehensive understanding.

### Part 2: Strategic Splitting with Dual Package Installation

Rather than migrating all 970 files at once, implement **safe parallel work**:

**Key insight:** Install both package versions simultaneously using npm aliasing.

```
npm install react-testing-library-v13@npm:react-testing-library@13
npm install react-testing-library@14
```

This enables:
- Different team members working on different migrations without conflicts
- Safe, independent PR creation
- Team contributions don't interfere with automation
- Flexibility to catch missed edge cases
- Incremental validation and rollout

Migrated across **50 PRs**, each approximately 30 minutes of work.

### Part 3: AST-Based Automation with jscodeshift

**Abstract Syntax Trees** enable programmatic code transformation:

jscodeshift parses code into tree structure representing syntax, enabling:
- Precise pattern matching without regex brittleness
- Reliable refactoring at scale
- Built-in testing mechanisms
- Validation through test execution

**Migration codemod evolution:**
- Initial version: 271 lines
- Final version: 992 lines
- 14 test cases covering edge cases
- Expanded as new patterns discovered

**What the codemod handles:**
- Transforming sync APIs to async equivalents
- Adding await keywords where needed
- Updating setup/cleanup patterns
- Modifying assertion patterns
- Handling special cases and edge cases

## AI's Role in Automation

AI agents contributed to:

1. **Initial transformation logic** — Claude suggested codemod structure and transformation patterns
2. **Iteration and refinement** — Handling edge cases discovered during testing
3. **Documentation** — Creating migration guides for team
4. **Validation** — Running tests and identifying failures

## Critical AI Limitations Discovered

The article identifies honest shortcomings that appeared:

### Context Window Constraints
Optimal batch size: **10 tests per session**. Beyond this, AI lost context and performance degraded.

### Tendency to Skip Hard Problems
AI agents chose workarounds over solving difficult patterns thoroughly:
- Detected unsolvable edge cases but didn't invest in proper solutions
- Used suboptimal patterns when elegant solution existed
- Relied on partial automation rather than complete coverage

### Service Reliability Issues
Service outages during heavy usage periods disrupted workflow and required workarounds.

### Incomplete Understanding
AI applied transformations without full mechanical understanding, sometimes producing code that "worked" but wasn't optimal.

## Migration by the Numbers

**Scale:**
- 970 test files
- 6000+ test cases
- 50 separate PRs

**Codemod statistics:**
- Initial: 271 lines, 0 test cases
- Final: 992 lines, 14 test cases
- Growth: Iterative expansion as edge cases emerged

**Migration guide:**
- Initial: 4,532 words
- Final: 7,517 words
- Expanded as edge cases and patterns documented

**Timeline:**
- One week total
- ~30 minutes per PR
- Incremental, manageable chunks

## Practical Principles for AI-Assisted Migration

### 1. Prepare Thoroughly
Research the migration deeply before automating. Understand what's changing and why.

### 2. Chunk Strategically
Don't attempt monolithic migration. Use dual-package installation and divide work into 50-100 small PRs.

### 3. Use ASTs, Not Regex
Regex-based transformations brittle and unreliable at scale. AST-based codemods far more robust.

### 4. Test Everything
Build comprehensive test cases into codemod. Validate each transformation.

### 5. Batch for Context
Work in small batches (10 tests) to stay within AI context window effectiveness.

### 6. Maintain Human Oversight
- Review edge cases that automation missed
- Validate patterns weren't handled
- Run full test suites frequently
- Don't assume automation is 100% correct

### 7. Iterate, Don't Aim for Perfect
Codemod grew from 271 to 992 lines through iteration. Each PR revealed new patterns.

### 8. Document as You Go
Migration guide evolved alongside codemod. Document patterns, edge cases, solutions.

## Key Insight: "Small Changes Iteratively"

The author emphasizes: **"Small changes iteratively" with "good automated validation" remains essential, even with AI assistance.**

This means:
- Not betting the entire migration on one massive AI run
- Small, reviewable PRs catch problems early
- Automated tests validate each transformation
- Human review focuses on edge cases
- Incremental confidence builds with each PR

## Lessons for Large-Scale AI-Assisted Code Work

1. **Structured automation beats naive prompting.** AST-based codemods more reliable than asking Claude to rewrite entire test files.

2. **AI is tool for implementation, not design.** Humans design strategy, splitting, and validation; AI executes transformations.

3. **Context matters.** Small batches stay within AI effectiveness window.

4. **Validation is critical.** Automated tests catch ~95% of issues; humans catch the remaining edge cases.

5. **Documentation compounds value.** Migration guide becomes institutional knowledge for next library upgrade.

6. **Service reliability impacts workflow.** Be prepared for AI service interruptions during large initiatives.

## Comparison: AI-Assisted vs. Pure Manual

**Manual approach:** 970 files × 30 minutes = 485 hours of human effort

**AI-assisted approach:**
- Automation codemod development: 20 hours
- Running codemod on all files: 1 hour
- Edge case handling: 10 hours
- Testing and validation: 10 hours
- **Total: 41 hours** (90% reduction)

Result: One week of focused effort vs. several weeks of manual refactoring.

## Why This Matters

This migration demonstrates that **AI excels at:
- Executing well-defined transformations at scale
- Handling repetitive patterns
- Discovering edge cases through testing
- Generating documentation
- Freeing human effort for high-value decisions

And **struggles with:**
- Completely novel, unstructured problems
- Deep mechanical understanding
- Context beyond ~10-20 examples
- Service interruptions

## Conclusion

AI-assisted code migration isn't "let Claude rewrite your codebase." Rather, it's:
1. Humans design the strategy and define transformations
2. Machines execute programmatic transformations reliably
3. Humans validate results and handle edge cases
4. Iterate until complete

This collaboration model—humans for strategy/validation, machines for execution—enables handling migrations at scales previously requiring months of effort in just one week.
