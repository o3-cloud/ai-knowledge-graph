---
summary: Cognition team reveals lessons and challenges from rebuilding Devin for Claude Sonnet 4.5—covering context anxiety, self-documentation behavior, parallel execution, and implications for long-horizon autonomous agent development
event_type: blog_post
sources:
    - https://cognition.ai/blog/devin-sonnet-4-5-lessons-and-challenges
tags:
    - autonomous-agents
    - Devin
    - Claude-Sonnet-4.5
    - agent-development
    - long-horizon-tasks
    - context-management
    - model-behavior
    - engineering-lessons
---

# Rebuilding Devin for Claude Sonnet 4.5: Lessons and Challenges

**Author:** Cognition Team
**Publication Date:** September 29, 2025
**Organization:** Cognition (Devin creators)

## Overview

The Cognition team shares practical lessons from rebuilding Devin—their autonomous software engineer—for Claude Sonnet 4.5. Rather than a generic "model X is better" comparison, the post dives deep into specific behaviors, challenges, and engineering solutions required to leverage Sonnet's capabilities effectively for long-horizon autonomous tasks.

Key finding: Sonnet 4.5's strengths (faster execution, better planning, proactive testing) come with new challenges (context anxiety, verbose self-documentation, parallel processing complexity) requiring deliberate architectural changes.

## Performance Improvements

### Raw Metrics

**Sonnet 4.5 vs. previous versions:**

- **Execution speed:** 2x faster
- **Junior Developer Evaluations:** 12% improvement
- **Planning performance:** 18% better
- **Multi-hour sessions:** More reliable
- **Task completion:** More consistent

### What These Mean

**2x faster execution:**
- Fewer API calls per task
- More efficient operations
- Reduced latency overall
- Better for interactive use

**12% improvement on Junior Developer Evaluations:**
- Can handle more complex coding tasks
- Better code quality
- Improved problem-solving
- Closer to senior developer capability

**18% better planning:**
- Understands task decomposition better
- Creates more accurate plans
- Fewer incorrect intermediate steps
- Better foresight about issues

**Reliable multi-hour sessions:**
- Can work on extended projects
- Maintains coherence over time
- Doesn't degrade over long operations
- Suitable for overnight batch jobs

## Key Discovery 1: Context Anxiety

### The Phenomenon

**What Cognition observed:**
Sonnet 4.5 exhibits "context anxiety"—proactively summarizing and rushing to complete tasks when nearing context limits, even with ample capacity remaining.

**Manifestation:**

```
Agent has 30% context remaining.
By model's calculation, context window is "nearly full."
Agent begins:
- Summarizing work
- Rushing to conclusions
- Skipping verification steps
- Compacting information prematurely

Result:
Incomplete work, rushed outputs, reduced quality.
```

### Why This Happens

**Model's perspective:**
- Trained on context window dynamics
- Learned that context filling = problem
- Developed heuristic: "summarize and close when approaching full"
- Conservative approach to context management

**The problem:**
Heuristic was learned from general-purpose text, not specialized agent tasks.

### The Solution: Beta 1M Token Context + Cap

**Implementation:**

```
Enable: 1M token context window beta
Cap usage at: 200k tokens

Result:
- Model has psychological safety (large window available)
- Doesn't trigger anxiety at lower thresholds
- Uses available space more effectively
- Completes work more thoroughly
```

**Why this works:**
Knowing large context is available reduces the urge to prematurely compact. Model uses available space confidently rather than anxiously.

### Implications

**Design lesson:**
Agent architecture should provide psychological safety alongside actual capacity.

**Pattern:**
```
Available context: 1M
Recommended usage: 200k
Buffer: 800k

Model perceives abundance, uses available thoughtfully.
vs.

Available context: 200k
Usage: 180k
Buffer: 20k

Model perceives scarcity, rushes to complete.
```

**Application:**
When designing prompts and context allocation for Sonnet 4.5, provide larger context than you expect to use.

## Key Discovery 2: Self-Documentation Behavior

### The Behavior

**Observation:**
Sonnet 4.5 autonomously creates summaries to externalize state.

**Examples:**
- CHANGELOG.md (tracking modifications)
- SUMMARY.md (current status summary)
- Progress files
- State documentation

**Why it does this:**
Model learned this is effective strategy for maintaining context across long conversations.

### The Problem

**Issue:**
Self-generated summaries lack crucial detail.

**Example:**

```
Full work:
[100 lines of code changes]
[10 implementation decisions]
[5 failure modes encountered and fixed]
[3 edge cases handled]

Self-generated summary:
"Updated user authentication module"

Result:
Missing context for future work.
Can't resume from summary without confusion.
```

### The Solution: Human Memory Management

**Implementation:**

```
Agent creates self-summaries (useful but incomplete)
    ↓
Cognition team supplements with:
- Detailed technical notes
- Architecture decisions logged
- Known edge cases documented
- Failure modes recorded
    ↓
Combined memory = reliable state externalization
```

**Pattern:**
```
Don't rely on:
- Agent self-summaries alone
- Self-generated documentation as source of truth

Instead use:
- Agent summaries + human-generated technical notes
- Hybrid memory systems
- Verified state representations
```

### Implications for Design

**Key insight:**
Agent self-documentation is useful but incomplete. For autonomous systems requiring reliability, pair with human-managed state tracking.

**Recommendation:**
For production systems, implement both:
1. **Agent self-documentation** (what model naturally does)
2. **Structured state tracking** (explicit memory management)

Together they form reliable memory system better than either alone.

## Key Discovery 3: Proactive Testing

### The Behavior

**Observation:**
Sonnet 4.5 proactively writes test scripts to validate its work.

**Pattern:**

```
Agent generates solution
    ↓
Writes test to verify solution
    ↓
Runs test
    ↓
Evaluates results
    ↓
Iterates if test fails
```

**Benefit:**
Improved reliability without explicit instruction to test.

### The Challenge

**Issue:**
Sometimes creates overly complicated test scripts instead of fixing root cause.

**Example:**

```
Problem: Function has edge case bug
Agent's approach A (better): Fix the bug
Agent's approach B (actual): Create complex test harness to work around bug

Result:
System works, but includes unnecessary complexity.
Could be simpler if root cause addressed.
```

### The Design Insight

**What's happening:**
Model is pattern-matching on "good practice" (write tests) but misapplying it.

**Trade-off:**
- Tests provide reliability assurance
- But can become crutch instead of fix
- Sometimes "fail fast" better than "test everything"

**Recommendation:**
Guide with prompts about when to test vs. when to refactor.

```
Instead of: "Always write tests"

Better: "Write tests for critical paths. For known edge cases,
         fix the root cause rather than test around it."
```

### Implications

**Model behavior insight:**
Sonnet 4.5 wants to be thorough and defensive. Sometimes that's over-engineering.

**User responsibility:**
Provide guidance on when thoroughness is valuable vs. when simplicity is preferable.

## Key Discovery 4: Parallel Execution

### The Behavior

**Observation:**
Sonnet 4.5 efficiently runs multiple operations simultaneously.

**Pattern:**

```
Multiple independent subtasks
    ↓
Model recognizes parallelization opportunity
    ↓
Executes concurrently
    ↓
Aggregates results
    ↓
Faster overall completion
```

**Benefit:**
Natural parallelization without explicit instruction.

### The Challenge

**Issue:**
Parallel execution accelerates context consumption.

**Pattern:**

```
Sequential execution:
Task 1 → result → context cleared
Task 2 → result → context cleared
Total context used: moderate

Parallel execution:
Task 1 → running (context accumulates)
Task 2 → running (context accumulates)
Task 3 → running (context accumulates)
Aggregate all results

Result: Much higher context usage
```

**Interaction with context anxiety:**
Parallel execution can trigger context anxiety earlier, causing premature compaction.

### The Solution: Deliberate Parallelization Decisions

**Approach:**

```
Enable parallelization for:
- Independent tasks
- Tasks where speed is critical
- Operations that don't require sequential state

Avoid parallelization for:
- Tasks requiring sequential state
- Operations where combined context is problematic
- Situations where lower context is priority
```

**Design pattern:**

```python
# Guide parallelization explicitly
prompt = """
For this task, you should:
1. Identify which operations can run in parallel
2. Start Task A and Task B concurrently
3. Task C depends on Task A's result, so wait for A before starting C
4. Aggregate all results when complete
"""
```

### Implications

**Insight:**
Parallelization is powerful but requires careful context management.

**Principle:**
Sonnet 4.5's parallel capabilities are valuable, but must be guided by explicit decisions about context usage vs. speed trade-offs.

## Integration of Challenges

### How They Interact

**Scenario: Complex multi-hour task**

```
1. Context anxiety triggers
   → Model wants to summarize

2. Self-documentation activates
   → Creates SUMMARY.md (but incomplete)

3. Parallel execution runs
   → Accelerates context consumption
   → Compounds anxiety

4. Result:
   → Premature compaction
   → Incomplete work
   → Context anxiety loop
```

### The Solution Architecture

**Cognition's approach:**

```
1. Provide large context window (1M, cap at 200k)
   → Reduces anxiety

2. Suppress aggressive self-summarization
   → Maintain context integrity
   → Use when reaching actual limits

3. Guide parallelization explicitly
   → Avoid uncontrolled parallel context explosion
   → Balance speed and context preservation

4. Maintain external memory system
   → Reliable state tracking
   → Agent augmented with human-managed notes

Result:
Leverages Sonnet 4.5 strengths while mitigating challenges.
```

## Architectural Changes for Sonnet 4.5

### Prompt Engineering

**Changes from previous model:**

**Before:**
```
"Solve this problem efficiently."
```

**After:**
```
"You have ample context available (1M tokens, cap at 200k).
Work methodically. Don't rush conclusions.

When you create summaries (CHANGELOG.md, SUMMARY.md), include:
- Specific technical details
- Decision rationale
- Known issues and workarounds

Write tests for critical paths, but fix edge case root causes
rather than test around them.

For independent operations, parallelization is fine.
For dependent tasks, complete prerequisites first."
```

### Pressure Points at Start and End

**Cognition's key finding:**
Need aggressive prompting both at conversation start and end.

**Start of conversation:**
```
"This task may take multiple hours.
You have ample context.
Work thoroughly, don't rush."
```

**Approaching task completion:**
```
"Before concluding, verify:
- All requirements met
- Edge cases handled
- Testing complete
- Documentation thorough

Don't rush to conclusion. Take time to verify."
```

### External State Management

**Pattern:**

```
Agent works on task
    ↓
Agent creates self-summaries (CHANGELOG, SUMMARY)
    ↓
Human/system supplements with:
    - Technical decision log
    - Known issues tracker
    - Architecture notes
    - Edge case registry
    ↓
Combined state available for next session
```

## Real-World Implications

### For Building Autonomous Agents

**Lesson 1: Model Behavior Is Nuanced**
Performance improvements come with behavioral quirks. Understanding these is crucial.

**Lesson 2: Large Context Is Psychological**
Context anxiety isn't just about capacity; it's about model's perception of safety.

**Lesson 3: Self-Documentation Is Limited**
Agent self-summaries are useful but incomplete. Pair with explicit memory systems.

**Lesson 4: Parallelization Needs Guidance**
Parallelization capability is powerful but requires deliberate control.

### For Long-Horizon Tasks

**Current limitation:**
Multi-hour tasks still require careful management and prompting.

**What works:**
- External memory systems
- Explicit pacing guidance
- Large context windows with psychological safety
- Human-augmented state tracking

**What doesn't:**
- Assuming agent will manage context optimally
- Relying solely on agent self-documentation
- Unguided parallelization

## Future Exploration Areas

### Sub-agent Delegation

**Potential:**
Leverage Sonnet's improved context awareness for better sub-agent decomposition.

**Challenge:**
Deciding when to delegate to subagent vs. handle in main agent.

**Opportunity:**
Better architecture for complex multi-step tasks.

### Meta-Agent Reasoning

**Concept:**
Agent that reasons about its own workflows and optimizes them.

**Application:**
- Self-optimizing task decomposition
- Dynamic parallelization decisions
- Intelligent context management

### Custom-Trained Models

**Possibility:**
Train models specifically for context management and autonomous work.

**Benefit:**
Address context anxiety, self-documentation limitations through training.

**Timeline:**
Future exploration, not immediate.

## Key Takeaways

1. **Sonnet 4.5 brings significant improvements** — 2x speed, 12-18% quality gains
2. **Performance gains enable longer autonomous work** — Multi-hour sessions now reliable
3. **Context anxiety is a real behavioral issue** — Model rushes when approaching limits
4. **Large context windows reduce anxiety** — Psychological safety matters as much as actual capacity
5. **Cap usage deliberately** — 1M window, cap at 200k for balance
6. **Self-documentation is incomplete** — Summaries lack crucial detail
7. **Pair with human memory systems** — External state tracking essential
8. **Proactive testing is positive** — But can become over-engineering
9. **Guide testing vs. fixing decisions** — Model needs direction on priorities
10. **Parallelization is powerful but costly** — Accelerates context consumption
11. **Explicit parallelization guidance needed** — Don't let model run uncontrolled
12. **Prompting at boundaries is critical** — Start and end of conversation need aggressive guidance
13. **Context is both technical and psychological** — How much is available matters less than how safe it feels
14. **Model behavior is subtle and nuanced** — Understand specific quirks and patterns
15. **Autonomous doesn't mean hands-off** — Requires thoughtful architecture and prompting
16. **External memory systems are necessary** — Reliable agents need human-augmented state
17. **Multi-hour tasks are feasible** — With right architecture and guidance
18. **Trade-offs between speed and completeness** — Parallelization faster but consumes context
19. **Testing patterns can be guided** — Prompting shapes whether model fixes or tests around issues
20. **Future improvements coming** — Sub-agent delegation, meta-reasoning, custom models

## The Bottom Line

Cognition's experience rebuilding Devin for Sonnet 4.5 reveals important lessons about leveraging advanced models for long-horizon autonomous tasks.

**Key insights:**

1. **Performance improvements are real** — 2x speed and 12-18% quality gains enable more ambitious tasks
2. **New challenges emerge** — Context anxiety, incomplete self-documentation, parallelization complexity
3. **Solutions are architectural** — Large context windows, external memory, explicit guidance
4. **Model behavior requires understanding** — Generalist model exhibits specialized quirks when given agent work

**Practical takeaways for builders:**

- Use 1M token context, cap at 200k for psychological safety
- Implement external memory systems rather than relying on self-documentation
- Guide parallelization explicitly rather than assuming optimal behavior
- Use aggressive prompting at conversation boundaries
- Pair agent work with human-augmented state tracking

**Bigger picture:**
Autonomous agents are becoming more capable, but remain best as human-augmented systems rather than fully independent. Cognition's approach—combining model capabilities with thoughtful architecture and guidance—represents the realistic path to reliable autonomous work.

The lesson: advanced models enable ambitious agent work, but require understanding their behavioral quirks and designing systems that account for those quirks rather than working around them.

