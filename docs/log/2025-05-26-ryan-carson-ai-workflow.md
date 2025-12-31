---
summary: Five-time founder Ryan Carson shares a three-file system (PRD, task list, context) that transforms chaotic vibe coding into structured AI development—demonstrating how slowing down for proper context speeds up overall development
event_type: video
sources:
    - https://www.youtube.com/watch?v=fD4ktSkNCw4
    - https://github.com/snarktank/ai-dev-tasks
tags:
    - AI-workflow
    - solo-founders
    - Cursor
    - MCP
    - PRD
    - task-management
    - vibe-coding
    - context-engineering
---

# A 3-Step AI Coding Workflow for Solo Founders

**Speaker:** Ryan Carson (5x Founder)
**Interviewer:** Claire Vo
**Publication:** How I AI
**Date:** May 26, 2025
**Duration:** ~35 minutes

## Overview

Ryan Carson shares his playbook for turning "vibe coding" into a structured, scalable approach. The method centers on a three-file system that transforms chaotic AI coding into reliable, repeatable development—potentially replacing full engineering teams for solo founders.

## The Three-File System

### The Structure

```
1. PRD (Product Requirements Document)
2. Task List (Generated from PRD)
3. Context (Codebase understanding)
```

### Why Three Files

**Problem with vibe coding:**
- Chaotic, unrepeatable
- Context gets lost
- AI goes off track
- Technical debt accumulates

**Solution:**
- Structured inputs
- Clear progression
- Maintained context
- Systematic execution

## Step 1: AI-Generated PRD

### Creating the PRD with Cursor

**Process:**
1. Describe the feature/product to AI
2. AI generates structured PRD
3. Review and refine
4. PRD becomes source of truth

### What the PRD Contains

- Feature description
- User stories
- Acceptance criteria
- Technical considerations
- Edge cases

## Step 2: Task List Generation

### From PRD to Tasks

**Process:**
1. Feed PRD to AI
2. AI generates task list
3. Tasks are granular and ordered
4. Dependencies identified

### Task Characteristics

- Small, manageable scope
- Clear completion criteria
- Logical sequence
- Independent where possible

### Tools Referenced

- **Task Master** — Claude-based task generation
- **ChatPRD** — PRD creation tool

## Step 3: Systematic Execution

### Working Through Tasks with Cursor

**Process:**
1. Pick task from list
2. Provide relevant context
3. AI implements
4. Review and commit
5. Move to next task

### The Key Insight

**"Slowing down to provide proper context is the secret to speeding up."**

Paradox: Taking time upfront for context reduces overall development time.

## Context Management

### Why Context Matters

LLMs perform dramatically better with:
- Codebase understanding
- File relationships
- Existing patterns
- Project conventions

### Tools for Context

**Repo Prompt:**
- Precise control over context
- Select relevant files
- Exclude noise
- Optimize token usage

## MCPs: Extending AI Capabilities

### What MCPs Enable

Model Context Protocols extend AI beyond coding:
- Database access
- Browser testing
- External APIs
- System integration

### Specific MCPs Demonstrated

**Browserbase/Stagehand:**
- Front-end testing
- Visual verification
- Browser automation
- QA workflows

### MCP Philosophy

Don't limit AI to code generation—extend it to:
- Test the code
- Verify the output
- Interact with systems
- Complete workflows

## Common Mistakes to Avoid

### Mistake 1: Skipping PRD

**Problem:** Jumping straight to coding
**Result:** Misaligned output, wasted iterations

### Mistake 2: Large Tasks

**Problem:** Tasks too big for AI context
**Result:** Incomplete implementations, drift

### Mistake 3: Ignoring Context

**Problem:** Not providing codebase context
**Result:** Inconsistent patterns, duplication

### Mistake 4: No Change Management

**Problem:** Not tracking what changed
**Result:** Lost work, merge conflicts

## Time Savings for Product Managers

### Traditional Flow

```
PM writes PRD → Engineer interprets → Back and forth → Implementation
```

### AI-Assisted Flow

```
PM + AI writes PRD → AI generates tasks → AI implements → PM reviews
```

**Result:** PM can ship features directly in many cases.

## Key Timestamps

| Time | Topic |
|------|-------|
| 00:00 | Introduction and Ryan's AI projects |
| 03:25 | Demo: Creating a PRD with Cursor |
| 05:00 | Open source links |
| 09:53 | Common mistakes to avoid |
| 11:00 | Demo: Generating task list from PRD |
| 15:31 | Importance of context |
| 18:07 | Demo: Working through tasks systematically |
| 18:56 | Change management |
| 20:00 | Task lists for product managers |
| 21:50 | Demo: MCPs for front-end testing |
| 24:50 | Specific MCPs and use cases |
| 26:45 | Demo: Repo Prompt for context control |
| 31:23 | Music in development |
| 32:10 | Lightning round |

## Tools Referenced

| Tool | Purpose |
|------|---------|
| Cursor | AI-powered code editor |
| ChatGPT/Claude/Gemini | LLM backends |
| Repo Prompt | Context control |
| Task Master | Task generation |
| Browserbase | Browser automation |
| Stagehand | MCP for testing |
| ChatPRD | PRD generation |

## Open Source Resources

**GitHub Repository:**
https://github.com/snarktank/ai-dev-tasks

Contains Ryan's workflow templates and examples.

## Key Takeaways

1. **Three-file system** — PRD, task list, context
2. **PRD first** — Don't skip requirements
3. **Granular tasks** — Small, manageable scope
4. **Context is key** — Slow down to speed up
5. **MCPs extend AI** — Beyond just coding
6. **Repo Prompt** — Precise context control
7. **Change management** — Track what changed
8. **PM empowerment** — Ship features directly

## The Bottom Line

Ryan Carson's three-file system offers solo founders a structured alternative to chaotic vibe coding. The approach—PRD to task list to systematic execution—transforms AI coding from unreliable experimentation into repeatable process. The counterintuitive insight: slowing down to provide proper context speeds up overall development. MCPs extend AI capabilities beyond code generation into testing and system interaction. For founders building with minimal teams, this workflow demonstrates how AI can replace traditional engineering capacity when properly structured.
