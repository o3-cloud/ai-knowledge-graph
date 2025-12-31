---
summary: Documents successful reverse-engineering of Nintendo 64 games through one-shot decompilation with Claude, accelerating matching code completion from 25% to 45% through strategic function prioritization and Claude Code optimization
event_type: article
sources:
    - https://simonwillison.net/2025/Dec/6/one-shot-decompilation/
tags:
    - reverse-engineering
    - decompilation
    - Claude-Code
    - MIPS-assembly
    - workflow-optimization
    - N64-games
    - AI-specialization
---

# The Unexpected Effectiveness of One-Shot Decompilation with Claude

**Author:** Chris Lewis (documented by Simon Willison)
**Publication:** simonwillison.net
**Publication Date:** December 6, 2025

## Overview

Chris Lewis is engaged in "matching decompilation" of Nintendo 64 games, particularly Snowboard Kids 2. This specialized reverse-engineering challenge requires analyzing MIPS assembly code and writing C code that, when compiled identically, reproduces the exact binary—while maintaining simple, idiomatic control flow plausible for 1990s developers.

By switching to Claude Code with Opus 4.5 and implementing strategic workflow optimization, Lewis dramatically accelerated progress from ~25% matching code (mid-November) to ~45% (early December).

## The Decompilation Challenge

### What is Matching Decompilation?

**Goal:** Transform binary executable back into human-readable C source code such that:
- Compiled code produces identical binary output (bit-perfect match)
- Control flow is simple and idiomatic for the era
- Data structures resemble what original developers would write
- Code is understandable and maintainable

This differs from "non-matching" decompilation, which produces functional but not identical binaries. Matching requires understanding original developer intent and writing code that compiles to exact same machine instructions.

### Why It's Hard

**MIPS Assembly Complexity**
- Reverse-engineering requires deep assembly knowledge
- Must understand compiler optimizations and patterns
- Control flow reconstruction non-trivial
- Function boundaries and calling conventions matter

**Plausibility Constraint**
- Code must look like 1990s C, not modern code
- Idiomatic patterns for that era required
- Data structures should be sensible choices
- Comments and variable names should match era

**Scale**
- Snowboard Kids 2 contains many functions
- Each function must match exactly
- Small mistakes break the entire binary
- Iterative refinement required

## Initial Approach: Interactive Mode

Lewis initially used Claude Code in interactive mode, making incremental progress. However, this approach was:
- Time-consuming per function
- Inefficient for larger-scale work
- Limited by session management
- Slow compared to potential

**Initial results:** ~25% of functions matched by mid-November

## Strategic Innovation: Lowest Hanging Fruit

Rather than attacking functions randomly, Lewis implemented **strategic prioritization**:

### Function Scoring System

Developed `score_functions.py` that analyzes functions and scores them by complexity:
- Simpler functions have lower scores
- Complex functions have higher scores
- Prioritizes "lowest hanging fruit"

**Scoring criteria might include:**
- Number of basic blocks
- Control flow complexity
- Assembly instruction count
- References to other functions
- Data structure complexity

### Automated Workflow

Created Bash script that:
1. Runs `score_functions.py` to identify next simplest unmatched function
2. Generates one-shot prompt for Claude
3. Submits to Claude Code (non-interactive mode)
4. Validates if new code matches binary
5. Iterates to next function

This workflow enables **systematic, high-throughput decompilation**.

## One-Shot Prompting Effectiveness

**Key finding:** One-shot prompting proved surprisingly effective for this domain.

Rather than:
- Interactive dialogue about each function
- Iterative refinement back-and-forth
- Asking Claude to explain reasoning

Lewis found success with:
- Single, comprehensive prompt per function
- Clear context about patterns observed so far
- Constraints about era-appropriate code
- Validation through binary comparison

**Advantages:**
- Non-interactive mode faster than interactive
- No session management overhead
- Systematic, reproducible process
- Enables parallel batch processing
- Clear success criteria (binary match)

## Results and Scaling

**Progress trajectory:**
- Mid-November: ~25% matching code
- Early December: ~45% matching code
- **20 percentage point improvement in 2-3 weeks**

**At current pace:**
- Continued progress toward 60-70%+
- Remaining functions likely require more manual analysis
- Diminishing returns as hardest functions remain

## Why This Works

### Claude Strengths for This Task

1. **Specialized Knowledge:** Understanding MIPS, compilation, binary formats
2. **Code Generation:** Producing syntactically correct, compilable C code
3. **Iterative Refinement:** Can be told "this doesn't match, try different approach"
4. **Attention to Detail:** Producing exact binary matches requires precision

### Workflow Design Matters More Than Complexity

Key insight: **One-shot decompilation outperformed interactive approaches not because one-shot is inherently better, but because:**
- Workflow design prioritizes low-hanging fruit
- Validation is automated (binary comparison)
- Process is systematic and reproducible
- No cognitive overhead from interaction
- Batching enables scaling

### Constraint-Driven Prompting

Prompts include constraints that guide output:
- "Must compile to identical binary"
- "Use era-appropriate C idioms"
- "Keep control flow simple and readable"
- "Match calling conventions exactly"

These constraints narrow solution space, making one-shot more effective.

## Lessons for AI-Assisted Specialized Work

### 1. Domain Expertise + AI
Lewis brings deep reverse-engineering expertise. Claude provides:
- Assembly understanding
- C code generation
- Quick iteration
- Validation support

Neither alone sufficient; together powerful.

### 2. Workflow Design > Prompting Sophistication
Systematic prioritization (lowest hanging fruit) and clear validation beats clever prompting.

### 3. Constraints Enable Precision
Constraint-driven prompting (binary match requirement, era-appropriate code) produces better results than open-ended requests.

### 4. Batch Processing at Scale
Non-interactive, systematic processing enables handling hundreds of functions efficiently.

### 5. Validation is Critical
Binary comparison provides objective success criteria. No guessing if output is correct.

## Broader Implications

This work demonstrates that Claude excels at:
- Specialized technical tasks with clear constraints
- Domain-specific code generation
- Reverse-engineering and analysis
- Batch processing with validation
- Translating between code representations

And shows that **workflow optimization matters as much as raw model capability**—systematic function prioritization achieved more impact than attempting all functions randomly.

## The Bigger Picture

Matching decompilation of classic games represents a niche application, but the patterns apply broadly:

- **Constraint-driven work:** When outputs have objective validation criteria
- **Specialized domains:** Where knowledge is deep but learnable
- **Batch processing:** Where similar tasks repeat
- **Incremental progress:** Where partial solutions compound

These conditions appear across many professional domains—not just reverse-engineering.

## Timeline

- **Mid-November:** ~25% matching completion
- **December 6, 2025:** ~45% matching completion
- **Continued:** Progress toward higher completion rates

The dramatic acceleration suggests the approach is sustainable and could potentially achieve 70-80%+ completion on Snowboard Kids 2, with remaining functions requiring specialized manual analysis or different approaches.
