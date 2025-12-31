---
summary: Analysis of how AI transforms software engineering workflows by accelerating feedback loops while preserving fundamental engineering principles. Identifies what AI changes versus what remains constant.
event_type: research
sources:
    - https://sarshah.bearblog.dev/what-ai-changes-about-software-engineering-and-what-it-doesnt/
tags:
    - ai-engineering
    - software-development
    - engineering-principles
    - ai-workflows
    - feedback-loops
    - human-oversight
---

# What AI Changes About Software Engineering (And What It Doesn't)

**Author:** Sar Shah
**Source:** Bear Blog
**Topic:** Reframing AI's role in development through the lens of engineering fundamentals

## Core Thesis

AI doesn't change what software engineering fundamentally is—it changes *how fast we can iterate through engineering loops*. The engineering loop (Research → Plan → Implement → Verify) remains intact; AI accelerates the feedback latency within and between these stages.

## The Engineering Loop (Unchanged)

Software engineering has never been primarily about writing code. The actual work involves:

1. **Research** - Understanding the problem, exploring solutions, gathering context
2. **Plan** - Designing architecture, defining approach, clarifying intent
3. **Implement** - Writing code that matches the plan
4. **Verify** - Testing, validation, confidence building

This cycle is fundamental. AI doesn't eliminate or reorder these stages.

## What AI Changes: Feedback Loop Acceleration

**The Insight:** "AI lets us run more high-quality loops per unit time."

Rather than waiting days/weeks between stages, AI compresses latency:

| Stage | Traditional Latency | AI-Assisted Latency |
|-------|-------------------|-------------------|
| Research (exploring possibilities) | Hours/days | Minutes |
| Planning (generating design alternatives) | Days | Hours |
| Implementation (writing code) | Days/weeks | Hours |
| Verification (running tests, analyzing failures) | Hours | Minutes |

The quality of each loop remains engineer-dependent, but the **quantity of loops possible per unit time** increases dramatically.

## Three Essential Building Blocks

For reliable AI-assisted development, Shah identifies three foundational elements:

### 1. Context
- Relevant codebase knowledge
- Understanding existing architecture
- Familiarity with project history and constraints
- System-level thinking, not just local changes

**Why it matters:** AI responds to what you ask, but context determines the quality of what you ask. Poor context → poor outputs regardless of model quality.

### 2. Intent
- Clearly defined goals and success metrics
- Explicit problem statement
- Tradeoff understanding (speed vs. quality vs. maintainability)
- What "done" looks like

**Why it matters:** Intent disambiguates when multiple valid approaches exist. AI can generate many options; intent helps select the right one.

### 3. Mode
- Operational stance appropriate to each stage
- Research mode = explore broadly
- Planning mode = narrow and clarify
- Implementation mode = execute against plan
- Verification mode = validate and challenge

**Why it matters:** Using the same prompting approach for research and verification produces worse results than mode-specific strategies.

## The Critical Role of Human Checkpoints

Shah advocates for **explicit human oversight at stage endings**, not throughout:

```
Research Phase
    ↓ [HUMAN REVIEW OF RESEARCH BRIEF]
Planning Phase
    ↓ [HUMAN REVIEW OF IMPLEMENTATION PLAN]
Implementation Phase
    ↓ [HUMAN REVIEW OF CODE STRUCTURE]
Verification Phase
    ↓ [HUMAN REVIEW OF TEST RESULTS & CONFIDENCE]
Ship
```

**Key principle:** Don't just increase code generation speed. Use AI to accelerate *understanding*, then verify before proceeding.

### Where Human Review Matters Most

1. **Research findings** - Did we understand the problem correctly?
2. **Plan viability** - Is the approach sound? Are tradeoffs acceptable?
3. **Implementation alignment** - Does code match plan? Is quality acceptable?
4. **Verification adequacy** - Are tests sufficient? Do results justify shipping?

Humans don't need to review every line; they need to verify every stage's conclusions.

## What Remains Fundamentally Human

AI cannot do (without human oversight):
- **Tradeoff judgment** - Choosing between competing values
- **Context integration** - Understanding the system holistically
- **Intent clarification** - What problem are we actually solving?
- **Confidence building** - The emotional/organizational stake in quality
- **Responsibility** - Owning the decision to ship

These aren't tasks AI can't assist with—they're decisions that retain human accountability.

## Connecting to the Engineering Principles

This aligns with what software engineering actually requires:

- **Systems thinking** - Understanding interactions and dependencies (AI doesn't replace this)
- **Tradeoff analysis** - Balancing competing concerns (AI can help explore, not decide)
- **Risk management** - Understanding what could go wrong (AI can amplify, human judgment directs)
- **Quality ownership** - Taking responsibility for shipped code (cannot be delegated to AI)

## Comparison to Code-Generation-First Approaches

**Naive approach:** "Just use ChatGPT to write code faster"
- Result: More code, same understanding
- Outcome: False sense of velocity without confidence

**Informed approach:** "Use AI to accelerate research, planning, and verification"
- Result: Better understanding, appropriate code, higher confidence
- Outcome: Sustainable velocity with maintainability

## Practical Implementation Strategy

### For Individual Developers
1. Use AI in research phase to explore solutions faster
2. Draft architectural plans, refine with AI, review yourself
3. Use AI for implementation, review code against plan
4. Use AI to generate tests, review test coverage yourself
5. Verify results match original intent before shipping

### For Teams
1. Establish clear documentation of context (codebase, architecture, constraints)
2. Define intent explicitly in tickets/issues (what success looks like)
3. Create stage-specific review processes (not continuous review)
4. Build confidence metrics (test coverage, performance, reliability)
5. Maintain human accountability for stage decisions

### Against Common Pitfalls
- Don't skip research phase to "just code faster"
- Don't lose intent in pursuit of throughput
- Don't confuse code generation speed with engineering speed
- Don't eliminate human judgment to automate everything
- Don't treat AI as a substitute for understanding

## Key Metrics for Success

**Instead of measuring:**
- Lines of code generated per hour
- Time from ticket to PR

**Measure:**
- Quality of research outputs (problem understanding)
- Plan viability (architectural soundness)
- Implementation alignment (code matches plan)
- Verification adequacy (test coverage + confidence)
- Post-ship outcomes (bugs found, performance, maintainability)

## The Real Productivity Gain

Shah's insight reframes productivity:
- **Traditional view:** More code = more productivity
- **Informed view:** Better understanding = sustainable productivity

AI's actual contribution: "Run more high-quality loops per unit time" = faster iteration through the same engineering discipline that's always been necessary.

## Related Concepts

This research directly connects to:
- `2025-12-27-death-and-rebirth-of-programming.md` - Understanding and complexity management becoming the scarce resource
- `2025-12-27-agent-readiness-framework.md` - Systems designed for agent collaboration also amplify human understanding
- `2025-12-27-llm-coding-workflow-best-practices.md` - Intentional workflows that preserve human judgment
- `2025-12-27-how-chatgpt-influences-language.md` - Awareness that tools shape thinking non-neutrally

## Critical Insight

AI doesn't change software engineering fundamentally because software engineering was never about fast code-writing. It was always about:
- Understanding problems deeply
- Making sound architectural choices
- Building confidence in complex systems
- Taking responsibility for shipped quality

AI accelerates the feedback loops within this discipline, but doesn't replace the discipline itself. Teams that treat AI as a "code generator" miss the actual opportunity: using AI to run more research/planning/verification cycles while maintaining human judgment at decision points.

## Open Questions

1. How do we train engineers to use AI for stage acceleration rather than code speed maximization?
2. What metrics should teams optimize for to maintain engineering discipline while using AI?
3. How does "running more loops" change the quality of early-stage decisions (research/planning)?
4. Can distributed teams maintain the context needed for effective AI-assisted development?
5. How do we avoid the trap of "faster bad decisions" vs. "slower good decisions"?
