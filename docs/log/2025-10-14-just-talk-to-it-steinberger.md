---
summary: Peter Steinberger advocates for straightforward, intuition-based agentic engineering—rejecting complexity-heavy approaches and emphasizing direct communication, parallel agents, visual prompts, and developing practical intuition through consistent use
event_type: blog_post
sources:
    - https://steipete.me/posts/just-talk-to-it
tags:
    - agentic-engineering
    - agent-workflow
    - prompting-strategy
    - practical-guidance
    - intuition-building
    - code-generation
    - model-selection
    - agent-collaboration
---

# Just Talk To It: The No-BS Way of Agentic Engineering

**Author:** Peter Steinberger
**Publication Date:** October 14, 2025
**Type:** Practical Guidance and Experience Report

## Overview

Peter Steinberger cuts through the complexity and hype surrounding agentic engineering with a deliberately simple philosophy: just talk to it directly, develop intuition through consistent use, and avoid the elaborate frameworks and tools that most discourse emphasizes.

Rather than elaborate system prompts, subagents, architecture decision records, and specialized tool integrations, Steinberger's approach is refreshingly pragmatic—short visual prompts, parallel agent instances, atomic commits, and straightforward iteration.

His core message: the most effective agentic engineering isn't the most elaborate. It's the most direct.

## The Core Philosophy: Simplicity Over Sophistication

### The No-BS Approach

**Premise:**
Effective AI collaboration doesn't require complex frameworks, elaborate prompts, or sophisticated orchestration.

**What works:**
Straightforward communication. Direct requests. Visual context. Iterative refinement.

**The principle:**
"Just talk to it. Play with it. Develop intuition."

### Why Simplicity Wins

**Complexity overhead:**
- Elaborate system prompts add tokens
- Multi-stage planning delays execution
- Specialized agent personas restrict flexibility
- Infrastructure overhead slows iteration

**Simplicity benefits:**
- Direct communication is clear
- Fewer tokens wasted on framing
- Faster iteration cycles
- More flexibility to adjust mid-stream

**The reality:**
Most sophisticated approaches to agentic engineering add friction without meaningful benefit.

## Model Selection: GPT-5-Codex as Standard

### Why Codex?

**Steinberger's choice:**
GPT-5-Codex for approximately 100% of code generation tasks.

**Why not other models?**
- Speed (Codex is faster)
- Token efficiency (less wasteful)
- Code comprehension (reads before modifying)
- Practical reliability

### The Code-Reading Advantage

**Critical difference:**
Codex reads existing code carefully before making changes.

**Implication:**
Less chance of breaking hidden dependencies or introducing subtle bugs.

**Practical effect:**
You can trust Codex to understand context and make informed modifications.

### The Consistency Argument

**Why standardize:**
Rather than switching between models, develop deep intuition with one.

**Advantage:**
You learn how this specific model thinks, what it does well, what it struggles with.

**Result:**
Better prompting because you understand the tool deeply.

## The Workflow: Parallel Agents and Atomic Commits

### The Standard Setup

**Configuration:**
Running 3-8 parallel agent instances in the same folder simultaneously.

**Not:**
- Sequential agents waiting for each other
- Worktree-based approaches requiring file system coordination
- PR-based workflows adding review overhead

**What this enables:**
- Multiple directions explored simultaneously
- Faster iteration
- Easy rollback (commits are atomic)
- Simple comparison of approaches

### Atomic Commits as Integration Point

**How it works:**
Agents make their own commits as they work.

**Benefits:**
- Each change is atomic (reversible)
- Git history shows agent reasoning
- Easy to revert bad directions
- No waiting for human commit points

**Advantage over alternatives:**
- Worktrees: Require filesystem coordination, slow
- PRs: Add review overhead, delay feedback
- Uncommitted changes: Risk losing work, hard to compare

### The Parallel Processing Advantage

**Speed improvement:**
Multiple agents working simultaneously = multiple approaches tested in parallel.

**What you learn:**
- Different agents find different solutions
- Can compare approaches in real time
- Can adopt best from each
- Fast directional feedback

**Example:**
- Agent 1: Aggressive refactoring approach
- Agent 2: Conservative, minimal-change approach
- Agent 3: Novel architecture approach

Compare results after 30 minutes; choose best direction; merge insights.

## Prompting Strategy: Short, Visual, Direct

### What Works

**Effective prompts:**
- Short and specific
- Visual (screenshots)
- Direct (no elaborate framing)
- Focused on one concern per prompt

**Why short works:**
- Models read faster
- Token efficiency
- Clearer intent
- Less ambiguity

### Screenshots as Primary Context

**Usage:**
Approximately 50% of prompts are visual.

**Why:**
- Shows exactly what you mean
- Faster than describing UI
- Eliminates ambiguity
- Models excel at visual understanding

**Example:**
Instead of: "Change the button color in the settings panel to blue"
Better: Screenshot showing current button + text "Make this blue"

### The One-Concern-Per-Prompt Rule

**Principle:**
Queue messages for larger tasks rather than bundling.

**Anti-pattern:**
"Refactor this module, add error handling, update tests, and optimize performance"

**Better approach:**
1. First prompt: "Refactor this module for clarity"
2. Wait for result
3. Second prompt: "Add error handling here"
4. Wait for result
5. Third prompt: "Update tests to match"

**Benefit:**
- Easier to debug failures
- Can stop/adjust mid-stream
- Better results on each step
- Clearer reasoning trail

## Understanding Blast Radius

### The Critical Concept

**Definition:**
How many files will this change touch? How deep is the impact?

**Why it matters:**
- Affects risk assessment
- Determines verification requirements
- Indicates complexity level
- Shapes how you queue prompts

### Examples

**Small blast radius:**
"Add validation to this single function"
- 1-2 files affected
- Clear impact zone
- Safe to run autonomously
- Easy to verify

**Medium blast radius:**
"Refactor authentication module"
- 5-10 files potentially affected
- Multiple subsystems touched
- Need verification steps
- Monitor for regressions

**Large blast radius:**
"Migrate database schema and update all queries"
- Dozens of files affected
- System-wide impact
- Requires careful verification
- May need human oversight
- Consider breaking into smaller pieces

### Using Blast Radius in Planning

**Before prompting agent:**
- Estimate files affected
- Assess risk level
- Plan verification
- Queue related messages carefully

**If blast radius too large:**
- Break into smaller changes
- Verify early steps before continuing
- Use feature flags for larger changes
- Consider phased rollout

## What Doesn't Work: Misconceptions and Overhead

### Subagents

**The idea:**
Decompose work into specialized subagents that coordinate.

**Reality:**
- Adds coordination overhead
- Requires message passing
- Slows down simple tasks
- More failure points
- Harder to debug

**Better approach:**
Single agent with clear context does simpler work faster.

### Elaborate Planning Documents

**The idea:**
Create detailed plans before agents execute.

**Reality:**
- Plans become outdated quickly
- Agents often find better approaches
- Adds token overhead
- Slows iteration
- Reduces flexibility

**Better approach:**
Quick sketches of direction; let agent explore.

### Model Context Protocol (MCP) Integration

**The idea:**
Standardized tool interfaces enable sophisticated orchestration.

**Reality:**
- Adds complexity overhead
- Requires tool maintenance
- Slows simple operations
- Limited benefit for most tasks

**Better approach:**
Direct tool calls for what you need; simple and direct.

### Specialized Agent Personas

**The idea:**
Give agents detailed role descriptions and personality traits.

**Reality:**
- Wastes tokens on framing
- Restricts flexibility
- Agents still make same mistakes
- Adds cognitive overhead

**Better approach:**
Clear task description beats elaborate persona.

## The Misconception Audit

### What People Think Works But Doesn't

**Elaborate system prompts:**
- Longer ≠ better
- Shorter, focused prompts perform better
- Keep system prompt minimal

**Multi-stage pipelines:**
- Orchestration complexity > benefit
- Direct approach is faster
- Simpler failure modes

**Specialized reasoning techniques:**
- Chain-of-thought, tree-of-thought, etc.
- For most code tasks: overkill
- Direct prompting works better

**Optimized infrastructure:**
- Fancy agent frameworks
- Sophisticated tool chains
- Most add friction, not value

**Pre-planning everything:**
- Detailed requirements upfront
- Actual code uncovers real requirements
- Better to prototype quickly

## Practical Guidance: How to Actually Work

### Developing Intuition

**The core skill:**
Learning how a specific model thinks, what it does well, what it struggles with.

**How to develop it:**
- Consistent use (daily)
- Pay attention to patterns
- Note what works and doesn't
- Adjust approach based on results
- Build mental models of agent behavior

**Time required:**
Weeks of consistent use to develop strong intuition.

**Benefit:**
Once developed, you can work 5-10x faster because you know exactly how to communicate.

### The Refactoring Investment

**Recommended allocation:**
Approximately 20% of development time on refactoring.

**Why agents excel at refactoring:**
- Clear intent (improve code without changing behavior)
- Tests validate correctness
- Can run many iterations quickly
- Technical debt compounds less

**Practical approach:**
- Generate features (70%)
- Refactor aggressively (20%)
- Review and verification (10%)

### Status Checks Without Waiting

**Principle:**
Don't wait passively for agents to finish.

**What to do:**
- Check on progress periodically
- Stop mid-execution for status
- Adjust direction if needed
- Interrupt and pivot quickly

**Advantage:**
- Faster feedback loops
- Can course-correct immediately
- Less wasted work
- Better parallelization

### The Agents File

**Instead of:**
- Bloated system prompts
- Elaborate configuration files
- Complex tool definitions

**Use:**
- Focused agents file
- Clear role definition
- Minimal framing
- Easy to understand

**Benefit:**
- Easier to maintain
- Less token overhead
- Clearer communication
- More flexible

## Real-World Patterns

### Pattern 1: Parallel Exploration

```
Start: One folder, 3-8 agents, related but different approaches
Parallel: All agents working simultaneously for 30 minutes
Evaluation: Compare results; pick best direction
Integration: Merge insights from best approaches
Commit: Move forward with winning approach
```

**Timeline:** 1 hour to explore 3-8 approaches
**Traditional timeline:** Several days for same exploration

### Pattern 2: Blast-Radius-Aware Queuing

```
Large change needed affecting many files

Estimate blast radius:
- Phase 1: 5 files
- Phase 2: 10 files
- Phase 3: 8 files
- Total: 23 files (large)

Execute:
Queue Phase 1 → Verify → Queue Phase 2 → Verify → Queue Phase 3
Test after each phase
Can stop if issues found
```

**Advantage:** Contained risk; can roll back at phase boundaries

### Pattern 3: Rapid Iteration Cycles

```
Task: Implement new feature

Cycle 1: Agent generates basic implementation (30 min)
Check: Does it work? Are there obvious issues?
Cycle 2: Refine based on findings (20 min)
Check: Better? Production-ready?
Cycle 3: Optimize and polish (15 min)
Done: Ship

Total time: ~65 minutes
Traditional timeline: Several days of meetings, planning, development
```

### Pattern 4: Opportunistic Refactoring

```
While generating features:
- 70% time: Feature development
- 20% time: Refactor adjacent code
- 10% time: Verification

Agent can: Clean up technical debt while building
Result: Code improves over time rather than degrading
```

## The Intuition-Building Process

### Stage 1: Early Exploration (Weeks 1-2)

**What you do:**
- Use agent for simple tasks
- See what works and doesn't
- Notice patterns in responses
- Learn communication preferences

**What you learn:**
- How long things take
- What kinds of prompts work
- Basic capabilities and limitations
- Failure modes

### Stage 2: Confidence Building (Weeks 3-4)

**What you do:**
- Try more complex tasks
- Run parallel agents more often
- Experiment with different prompting styles
- Build faster feedback loops

**What you learn:**
- How to break down problems
- Effective prompt structures
- When to use multiple agents
- Risk assessment intuition

### Stage 3: Fluency (Weeks 5+)

**What you do:**
- Work almost entirely through agents
- Complex tasks decomposed naturally
- Parallel exploration as default
- Refactoring becomes routine

**What you learn:**
- Deep understanding of agent capabilities
- When to intervene and when to let run
- How to shape solutions
- Blast radius estimation becomes automatic

## Key Takeaways

1. **Simplicity beats sophistication** — Direct communication more effective than elaborate frameworks
2. **GPT-5-Codex is the workhorse** — Speed, efficiency, code comprehension justify standardization
3. **Parallel agents explore faster** — Running 3-8 simultaneously tests multiple approaches
4. **Atomic commits enable exploration** — Easy to compare and revert directions
5. **Short visual prompts work best** — Screenshots eliminate ambiguity; brevity reduces tokens
6. **One concern per prompt** — Queue messages for larger tasks; easier to debug
7. **Understand blast radius** — Estimate files affected; shape verification accordingly
8. **Subagents add overhead** — Single agent with clear context faster and simpler
9. **Elaborate planning doesn't work** — Agents find better approaches; plans become outdated
10. **MCPs are overkill** — Direct tool calls work fine; less complexity overhead
11. **Agent personas don't help** — Clear task beats elaborate role description
12. **20% refactoring pays dividends** — Technical debt improves over time instead of accumulating
13. **Intuition is the real skill** — Takes weeks of consistent use to develop
14. **Status checks don't require waiting** — Interrupt and adjust mid-execution
15. **Blast-radius-aware queuing reduces risk** — Phase large changes; verify at boundaries
16. **Parallel exploration compresses decision time** — Hours instead of days
17. **Rapid iteration cycles accelerate feature development** — Compare after each cycle
18. **Code reveals requirements better than planning** — Prototype quickly; plan from reality
19. **Refactoring as part of development** — Clean up as you build; debt doesn't accumulate
20. **Develop intuition through consistent use** — The leverage point for 5-10x productivity gain

## The Bottom Line

Peter Steinberger's "Just Talk To It" philosophy represents a necessary counterpoint to the increasingly elaborate and complex approaches to agentic engineering.

**The core insight:**
More complexity doesn't equal better results. In fact, most sophisticated approaches add overhead that slows you down.

**What actually works:**
- Straightforward communication
- Clear context (often visual)
- Direct iteration
- Consistent use to build intuition
- Atomic changes you can evaluate and adjust

**The misconceptions he debunks:**
- Subagents add value (they don't; overhead exceeds benefit)
- Elaborate planning helps (it doesn't; gets outdated)
- MCPs enable sophistication (they add complexity)
- Complex personas improve results (they waste tokens)
- Longer prompts are better (they're not; shorter is clearer)

**The surprising findings:**
- 3-8 parallel agents > sophisticated orchestration
- Screenshots > verbose descriptions
- One concern per prompt > bundled requests
- Short, focused agent instances > elaborate system prompts
- Atomic commits > PRs and worktrees

**The opportunity:**
Once you develop intuition about how an AI model thinks—which takes weeks of consistent use—you can work 5-10x faster than traditional development because iteration becomes instant and directional feedback immediate.

**The practical approach:**
Start simple. Use one model. Develop deep intuition. Add parallel agents for exploration. Allocate 20% time to refactoring. Build intuition through consistent use, not elaborate frameworks.

The future of agentic engineering isn't more tools, more MCPs, more specialized agents. It's simpler, more direct, built on deep intuition about how the model works.

Just talk to it.

