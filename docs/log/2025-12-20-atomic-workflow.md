---
summary: Introduces Atomic—a system for scalable AI coding infrastructure combining persistent memory via specifications with active working memory through progress tracking, enabling agents to compound knowledge across sessions
event_type: article
sources:
    - https://alexlavaee.me/blog/atomic-workflow/
tags:
    - AI-coding-agents
    - persistent-memory
    - specifications
    - workflow-automation
    - agent-architecture
    - scalability
    - human-in-the-loop
---

# Atomic: Automated Procedures and Memory for AI Coding Agents

**Author:** Alex Lavaee
**Publication:** Personal Blog (alexlavaee.me)
**Publication Date:** 2025

## Core Problem

Scaling AI coding infrastructure faces two critical challenges:

1. **Scale paradox:** More subagents doesn't equal better performance. Initial approach with 114+ specialized subagents created confusion rather than capability.

2. **Memory loss:** Without persistent storage, insights and decisions vanish when context windows reset. Agents repeat research, lose architectural context, and rebuild understanding across sessions.

## Key Innovation: Atomic System

**Atomic** addresses scalability through two interconnected mechanisms:

### Persistent Memory: Specifications
Store architectural decisions, research findings, and domain knowledge in version-controlled `specs/` directories that **survive across sessions** and context window resets.

- Specifications preserve compound knowledge
- Not just documentation—operational artifacts that guide agent behavior
- Enables agents to build on previous research rather than starting fresh
- Architectural decisions captured as source of truth

### Active Working Memory: Progress Tracking
Track what agents accomplish in real-time, creating observable execution state that informs next steps.

- Current progress visible to all agents in the pipeline
- Prevents redundant work and conflicting changes
- Guides which subagents to invoke next
- Foundation for human oversight and decision-making

## Three Core Primitives

**Commands** orchestrate workflows
- Entry points that coordinate execution
- Trigger sequences of subagents
- Manage phase transitions
- Human-controllable workflow orchestration

**Subagents** execute specialized tasks
- Narrow, focused responsibilities
- Execute within defined phases
- Produce artifacts (specs, code, tests)
- Not monolithic "do everything" agents

**Skills** inject domain expertise
- Reusable procedural knowledge
- Applied by agents during execution
- Patterns, best practices, architectural guidance
- Accumulate over time

## Five-Phase Workflow

Atomic structures development as five sequential phases:

### Phase 1: Research (Parallel)
Multiple subagents explore problem space in parallel:
- Analyze requirements and constraints
- Research existing approaches
- Identify dependencies and risks
- Gather domain knowledge

Outputs inform specifications.

### Phase 2: Specification
Consolidate research into formal specifications:
- Architecture decisions documented
- API contracts defined
- Algorithm approaches selected
- Edge cases identified

Specifications stored persistently in `specs/` directory.

### Phase 3: Feature Decomposition
Break specifications into implementable features:
- Parse requirements into discrete features
- Identify feature dependencies
- Sequence implementation order
- Define acceptance criteria

Feature list becomes contract for implementation phase.

### Phase 4: Atomic Implementation (Sequential)
Implement features sequentially, each as atomic unit:
- Each feature completes fully before next starts
- Agents focus on one feature at a time
- Minimize context switching
- Progressive buildup of functionality

Atomic execution prevents half-finished states.

### Phase 5: Quality Gates
Verify completeness and correctness:
- Run comprehensive tests
- Verify against specifications
- Check for regressions
- Validate architectural constraints

Quality gates ensure deliverable quality before completion.

## The "40-60%" Insight

Critical finding: **Agents deliver 40-60% on complex features, not 100%.**

This means:
- Perfect automation is unrealistic goal
- Human judgment needed for remaining 20-60%
- Edge cases, optimization, architectural decisions require human expertise
- System designed for human-in-the-loop, not full autonomy

### Human Oversight Points
1. **Specification review:** Engineers validate architecture and approach
2. **Feature decomposition review:** Engineers confirm feature breakdown makes sense
3. **Implementation review:** Engineers handle edge cases and optimization
4. **Quality validation:** Engineers verify against specifications

## Focused Composition Over Scale

Key lesson: **114+ subagents is worse than carefully curated set.**

Effective systems:
- Compose cohesive, specialized agents
- Each has clear, narrow purpose
- Agents communicate through persistent specifications
- Quality over quantity
- Easier to reason about and debug

## Architecture Benefits

### Knowledge Compound
- Specifications survive context resets
- Each session builds on previous findings
- Research accumulates rather than repeating
- System becomes more capable over time

### Deterministic Orchestration
- Phase-based workflow is explicit and predictable
- No chaotic looping or uncertainty
- Human can intervene at phase boundaries
- Clear progress visibility

### Scalable Human Oversight
- Humans don't manage 114 agents
- Humans review high-value decision points
- Progress tracking enables efficient review
- Agents handle execution details

### Composable Agents
- Agents work on different phases independently
- Specifications provide coordination mechanism
- No need for complex inter-agent communication
- Easy to add/remove/modify agents

## Specification-Driven Design

Specifications serve as:
- **Source of truth** for architecture
- **Contract** between agents
- **Persistence mechanism** for knowledge
- **Guidance** for implementation
- **Verification basis** for quality gates

Rather than prompt-driven or framework-driven, specification-driven ensures architectural coherence across sessions.

## Workflow Orchestration

Commands provide human control points:
- Initiate workflows
- Transition between phases
- Inject human decisions
- Modify specifications mid-workflow
- Pause/resume execution

This hybrid model enables:
- Automation where it adds value
- Human intervention where needed
- Observable, auditable progress
- Flexible adaptation to new information

## Key Insights

1. **Persistent memory matters** more than agent count. Specifications enable compounding knowledge.

2. **Phases structure complexity.** Sequential phase workflow is easier to reason about and oversee.

3. **Agents aren't magic.** Realistic 40-60% delivery requires human contribution for remaining work.

4. **Focused is better.** Curated agents with clear specialization beat generic multi-agent chaos.

5. **Specifications are operations.** Not documentation—living artifacts that guide agent execution.

6. **Human-in-the-loop is feature.** Designed into architecture, not retrofitted.

## Practical Implications

For teams implementing AI-assisted coding:

- Design workflows as explicit phases
- Store architectural decisions in persistent format (specs)
- Use agents for well-defined tasks, not end-to-end autonomy
- Plan for human review at architecture/design phases
- Track progress visibly for coordination and oversight
- Curate agents carefully—fewer, more specialized is better
- Treat specifications as operational artifacts, not documentation

## The Broader Vision

Atomic points toward **specification-driven AI development**:
- Agents as execution engines for specifications
- Humans as architects and decision-makers
- Persistent memory enabling learning and compound knowledge
- Scalable systems through focus rather than scale
- Reliable delivery through human-agent collaboration

Rather than asking "How do we get agents to do everything?", ask "How do we use agents to execute specifications that humans design?"
