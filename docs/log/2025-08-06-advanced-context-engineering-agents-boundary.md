---
summary: Boundary explores advanced context engineering for coding agents—demonstrating three-phase pipeline (research-planning-implementation), sub-agent decomposition, context compaction, naming alignment, and markdown review to systematize AI-assisted development
event_type: video
sources:
    - https://www.youtube.com/watch?v=42AzKZRNhsk
    - https://github.com/hellovai/ai-that-works/tree/main/2025-08-05-advanced-context-engineering-for-coding-agents
tags:
    - context-engineering
    - coding-agents
    - AI-development
    - prompt-engineering
    - agent-decomposition
    - code-generation
    - systematic-development
    - human-AI-collaboration
---

# Advanced Context Engineering for Coding Agents

**Creator/Host:** Boundary (AI That Works #17)
**Platform:** YouTube
**Duration:** ~72 minutes
**Publication Date:** August 6, 2025
**Code Repository:** https://github.com/hellovai/ai-that-works/tree/main/2025-08-05-advanced-context-engineering-for-coding-agents

## Overview

Boundary demonstrates how to systematize AI-assisted software development through advanced context engineering. Rather than "vibes-coding"—where developers throw prompts at agents and hope for results—the approach provides a disciplined three-phase pipeline combining research, planning, and implementation with strategic context management, sub-agent decomposition, and markdown review methodology.

## The Core Insight

### Context Engineering Philosophy

**Common misconception:**
More information in prompts = better results.

**Reality:**
Deliberate structuring, compacting, and aligning information matters far more than volume.

**Principle:**
"Context engineering isn't just about cramming more stuff into the prompt; it's a deliberate practice of structuring, compacting, and aligning information to make your AI agent a more effective partner."

### Why It Matters

**Without context engineering:**
- Agents get confused
- Results inconsistent
- Implementation takes many iterations
- Errors compound

**With context engineering:**
- Agents understand problem clearly
- Results more reliable
- Implementation faster
- Fewer iterations needed

### The Shift

**From:** Exploratory "vibes-coding"
**To:** Systematic AI-assisted development
**Requires:** Discipline and deliberate structure

## The Three-Phase Pipeline

### Phase 1: Research

**Objective:**
Understand the problem and existing system structure.

**What the agent explores:**
- Problem requirements
- Existing codebase architecture
- File structure and organization
- How components relate
- Naming conventions
- Design patterns in use

**Process:**
1. Agent reads relevant documentation
2. Agent explores codebase structure
3. Agent identifies key files and relationships
4. Agent maps how system works
5. Agent documents findings

**Key focus:**
Critical details like filenames and structural relationships.

**Output:**
Understanding of:
- What needs to be built
- Where it fits in system
- What exists that can be reused
- Dependencies and constraints

### Phase 2: Planning

**Objective:**
Create step-by-step implementation outline before coding.

**What emerges:**
Detailed plan mapping necessary changes.

**Process:**
1. Agent reviews research findings
2. Agent designs approach
3. Agent identifies files to create/modify
4. Agent outlines steps in sequence
5. Agent documents decision rationale

**Characteristics:**
- Explicit step-by-step breakdown
- Clear dependencies
- Identified decision points
- Documented assumptions
- Contingency plans

**Key benefit:**
Catch problems before writing code.

**Human role:**
Review plan with agent, provide feedback, align on approach.

### Phase 3: Implementation

**Objective:**
Execute plan while adapting to surprises.

**Process:**
1. Agent implements first step
2. Agent runs tests
3. Agent observes results
4. Agent adapts if needed
5. Repeat for each step

**Flexibility:**
Plan provides direction; agent adapts when reality differs.

**Integration:**
- Tests run continuously
- Feedback guides adjustments
- Unexpected issues addressed
- Plan updated if needed

**Success criteria:**
- Plan executed
- Tests pass
- Code meets requirements
- Implementation complete

## Sub-Agent Decomposition

### The Challenge

**Problem:**
Complex tasks in single monolithic prompt lead to:
- Confused agents
- Inconsistent results
- Missing considerations
- Lower quality output

### The Solution

**Decompose complex tasks into specialized agents:**

```
Complex Task
    ↓
├── Researcher Agent
│   (understands problem space)
│   ↓
├── Planner Agent
│   (creates implementation outline)
│   ↓
├── File Identifier Agent
│   (finds affected files)
│   ↓
└── Implementer Agent
    (writes code)
```

### How It Works

**Researcher Agent:**
- Single focus: understand problem
- Explores codebase
- Identifies patterns
- Documents findings
- Specialized context: architecture docs, file structure

**Planner Agent:**
- Single focus: design approach
- Takes researcher's findings
- Creates step-by-step plan
- Identifies decision points
- Specialized context: requirements, design patterns

**File Identifier Agent:**
- Single focus: find affected files
- Searches codebase
- Maps relationships
- Identifies dependencies
- Specialized context: existing code, file locations

**Implementer Agent:**
- Single focus: write code
- Receives research, plan, file list
- Implements per plan
- Integrates with tests
- Specialized context: code style, frameworks in use

### Benefits

**Focused expertise:**
Each agent excels at its narrow task.

**Reduced cognitive load:**
Not trying to do everything at once.

**Better outputs:**
Specialization enables higher quality.

**Parallel execution:**
Some agents can work simultaneously.

**Quality gates:**
Output from each phase reviewed before next.

## Context Compaction Techniques

### The Goal

**Objective:**
Maintain focus on essential information.

**Challenge:**
Too much context overloads agent; too little causes mistakes.

### Techniques

#### 1. Information Staging

**Concept:**
Provide information when needed.

**Pattern:**
```
Research phase: Provide full codebase context
Planning phase: Provide requirements and design docs
Implementation phase: Provide code files being modified
```

**Benefit:**
Agent focused on relevant information for current phase.

#### 2. Selective Context

**Approach:**
Include what matters, exclude what doesn't.

**Example:**
- Studying file structure? Include tree, not full files
- Implementing feature? Include only relevant code sections
- Writing tests? Include test patterns, not all production code

**Mechanism:**
Structure information by relevance to current task.

#### 3. Summarization

**Technique:**
Summarize complex information.

**Example:**
Instead of entire 1000-line file, summarize:
- What it does
- Key functions
- Dependencies
- How it fits

**Benefit:**
Agent understands big picture without being overwhelmed.

#### 4. Hierarchical Organization

**Structure:**
Organize from broad to specific.

**Pattern:**
```
System overview
  ↓
Relevant subsystem
  ↓
Specific component
  ↓
Particular function/class
```

**Benefit:**
Agent can navigate to right level of detail.

#### 5. Reference Systems

**Approach:**
Use references instead of including everything.

**Example:**
Rather than embedding full files:
```
See: src/components/Form.tsx (handles input validation)
See: src/utils/api.ts (manages API calls)
```

**Benefit:**
Context concise; agent can reference as needed.

## Naming and Language Alignment

### The Principle

**Concept:**
Consistent naming helps agents recognize relationships.

**Why it matters:**
Agents identify patterns through language and naming.

**Effect:**
Better understanding = better code generation.

### Examples

#### Naming Conventions

**Consistent:**
```
├── useUserData.ts (React hook)
├── useUserAPI.ts (API layer)
├── useUserValidation.ts (Validation hook)
├── useUserLoading.ts (Loading state)
```

**Agent understanding:**
"useX.ts files are React hooks; they handle different aspects."

**Inconsistent:**
```
├── getUserData.ts
├── userApi.ts
├── validateUser.ts
├── userLoading.ts
```

**Agent confusion:**
Mix of naming patterns; unclear relationships.

#### Language Patterns

**Consistent:**
```
const getUserById = (id: string) => {}
const getProductById = (id: string) => {}
const getOrderById = (id: string) => {}
```

**Agent pattern recognition:**
"Functions follow `get[Entity]ById` pattern."

### Application

**During Planning:**
Agent plans following existing conventions.

**During Implementation:**
Agent generates code matching established patterns.

**Result:**
Code feels cohesive; consistent with existing style.

## Markdown Review Methodology

### The Practice

**Process:**
Review research and plan agent creates before implementation.

**Timing:**
After research complete, before coding begins.

**Participants:**
Human developer + AI agent (collaborative review).

### What to Review

#### Research Review

**Check:**
- Did agent understand the problem?
- Are key components identified?
- Are relationships clear?
- Anything important missing?

**Action:**
- Clarify misunderstandings
- Add missing context
- Validate understanding

#### Plan Review

**Check:**
- Does plan make sense?
- Are steps in right order?
- Are dependencies clear?
- Any concerns about approach?

**Action:**
- Approve if solid
- Suggest changes if issues
- Add constraints or considerations

### Benefits

**Catches errors early:**
Before coding starts.

**Mental alignment:**
Developer and agent on same page.

**Shared understanding:**
Explicit documentation of approach.

**Prevents false starts:**
Wrong approaches identified before implementation.

**Builds confidence:**
Both parties understand what's happening.

### Format

**Markdown in context:**
```markdown
# Research Findings

## Problem
[Agent's understanding of what needs to be built]

## Existing System
[Agent's understanding of current architecture]

## Key Files
[Files that will be affected/created]

## Relationships
[How components relate]

---

# Implementation Plan

## Step 1
[What will be done]
- Affects: [files]
- Dependencies: [what must be done first]

## Step 2
[Next action]
...
```

**Human review:**
Read markdown, provide feedback, iterate if needed.

## Practical Development Workflow

### Starting a Feature

**1. Brief Agent on Context**
Share requirements, existing code, constraints.

**2. Research Phase**
Agent explores codebase, documents findings.

**3. Review Research**
Verify understanding, clarify if needed.

**4. Planning Phase**
Agent creates step-by-step plan.

**5. Review Plan**
Approve approach or suggest changes.

**6. Implementation Phase**
Agent writes code following plan.

**7. Integrated Testing**
Tests run; agent adapts as needed.

**8. Iterate**
Refine implementation based on test results.

### When to Intervene

**Provide guidance:**
- When agent confused
- When plan questionable
- When tests fail unexpectedly
- When assumptions wrong

**Let agent work:**
- Following clear plan
- Tests passing
- No blockers
- Code generation straightforward

## Key Practices

### 1. Mental Alignment First

**Before coding:**
Ensure human and agent understand approach.

**Mechanism:**
Markdown review of research and plan.

**Result:**
Smoother implementation.

### 2. Systematic Decomposition

**Complex tasks:**
Break into specialized sub-agents.

**Benefit:**
Better focus, higher quality.

### 3. Context Intentionality

**Every context inclusion:**
Ask "Is this needed right now?"

**Filter:**
Include only relevant information.

**Result:**
Agent less confused, more effective.

### 4. Naming Discipline

**Establish conventions:**
Consistent naming helps agents understand.

**Maintain:**
Enforce in code review.

**Payoff:**
Better generated code.

### 5. Test-Driven Development

**With agents:**
Clear tests guide implementation.

**Benefit:**
Agent knows success criteria.

**Process:**
Tests run continuously; agent adapts.

## Exploration and Intuition Building

### The Balance

**Systematic engineering:**
Needed for consistency and quality.

**Exploratory coding:**
Needed to build intuition about problem.

**Together:**
Understand what agents are good at vs. need guidance on.

### Learning Process

**1. Exploratory phase:**
Manually explore the problem.

**2. Build understanding:**
Learn how system works.

**3. Systematic phase:**
Leverage understanding for agent guidance.

**4. Refine process:**
Improve based on what worked.

**Outcome:**
Better guidance for agents based on deep understanding.

## Key Takeaways

1. **Structure beats volume** — Organized context better than large context
2. **Three-phase pipeline works** — Research, plan, implement systematizes development
3. **Sub-agents for complexity** — Decompose tasks for better results
4. **Compaction is deliberate** — Actively manage what agent sees
5. **Naming matters** — Conventions help agents understand
6. **Review before coding** — Catch issues early via markdown review
7. **Systematic not vibes** — Move from exploratory to disciplined approach
8. **Testing guides implementation** — Tests provide success criteria for agent
9. **Human-AI partnership** — Collaboration, not replacement
10. **Intuition still needed** — Explore problems to guide agent effectively
11. **Phase-appropriate context** — Different context for different phases
12. **Agent specialization effective** — Focused agents outperform generalists

## The Bottom Line

Boundary's advanced context engineering demonstrates that effective AI-assisted development isn't about prompting skill—it's about systematic information architecture. The three-phase pipeline (research-planning-implementation) provides structure. Sub-agent decomposition focuses effort. Context compaction maintains clarity. Naming alignment enables understanding. Markdown review ensures alignment.

The shift from "vibes-coding" (prompt, hope for results) to systematic engineering (deliberate structure, review, then execute) transforms AI assistance from hit-or-miss to reliably effective.

The methodology doesn't eliminate the need for human judgment and exploration—it enhances it. Developers still need deep understanding of problems and systems. But that understanding, captured in systematic structure and shared with specialized agents, enables far more effective collaboration.

For developers adopting AI agents for coding, the key insight is that engineering excellence applies to prompting and context as much as to code. Strategic structuring, deliberate focus, and systematic review of AI-generated plans before implementation dramatically improves results. This is how development with AI agents becomes productively systematic rather than creatively chaotic.
