---
summary: Mark Kashef presents 20 agentic AI design patterns in practical detail—covering prompt chaining, routing, parallelization, reflection, tool use, planning, multi-agent collaboration, memory, learning, monitoring, exception handling, human-in-loop, RAG, and more with TL;DRs, visuals, and implementation resources
event_type: video
sources:
    - https://www.youtube.com/watch?v=e2zIr_2JMbE
tags:
    - agentic-AI
    - design-patterns
    - agent-architecture
    - prompt-chaining
    - routing
    - multi-agent
    - RAG
    - safety-guardrails
    - evaluation-monitoring
---

# Master ALL 20 Agentic AI Design Patterns [Complete Course]

**Speaker:** Mark Kashef
**Platform:** YouTube
**Duration:** ~63 minutes
**Publication Date:** September 17, 2025
**Community:** https://www.skool.com/earlyaidopters
**Free Resources:** Diagrams, ASCII flows, Mermaid files (available in video)

## Overview

Mark Kashef delivers a comprehensive, practical guide to 20 agentic AI design patterns used by professionals. Based on a Google engineer's work, the course translates complex patterns into plain English with concrete applications, tradeoffs, and combinations. Covers everything from basic prompt chaining through advanced safety guardrails, with emphasis on shipping production-ready agents faster while avoiding over-engineering.

## Core Philosophy

### Why Patterns Matter

**Reality:**
Separates professionals from beginners.

**Benefit:**
Understanding patterns enables faster, more reliable agent development.

**Approach:**
Learn when and why to use each, how to combine them, and what tradeoffs exist.

### What You Get

**TL;DRs:**
Concise summaries of each pattern.

**Visuals:**
Labeled diagrams showing architecture.

**Free repo:**
ASCII flows and Mermaid files for immediate implementation.

## The 20 Agentic AI Design Patterns

### Pattern 1: Prompt Chaining

**What it is:**
Assembly-line-like steps with validations between each.

**Use case:**
Multi-step processes where output of one step feeds into next.

**Benefits:**
- Clear workflow
- Easy validation
- Debugging simplified
- Reusable steps

**Tradeoffs:**
- Sequential execution (slower)
- Multiple API calls
- Context management

**When to use:**
Clear, linear workflows with validation requirements.

**Example:**
Write → Review → Revise → Finalize

### Pattern 2: Routing

**What it is:**
Smart triage directing work to specialist agents.

**Use case:**
Different types of work requiring different expertise.

**Benefits:**
- Specialist focus
- Cost optimization
- Better quality
- Scalable architecture

**Tradeoffs:**
- Routing overhead
- Multiple agents to manage
- Fallback handling needed

**When to use:**
Diverse tasks requiring different capabilities.

**Example:**
Customer inquiry → Route to Support/Sales/Technical agent

### Pattern 3: Parallelization

**What it is:**
Split work across agents, normalize results, merge.

**Use case:**
Independent tasks that can run simultaneously.

**Benefits:**
- Faster execution
- Better resource utilization
- Scalability
- Resilience

**Tradeoffs:**
- Synchronization complexity
- Resource costs
- Merging logic needed

**When to use:**
Tasks can be decomposed independently.

**Example:**
Analyze 100 documents in parallel, aggregate results.

### Pattern 4: Reflection

**What it is:**
Critic → revise → pass cycle.

**Use case:**
Quality assurance through self-evaluation.

**Benefits:**
- Better outputs
- Reduces hallucinations
- Self-improvement
- Quality gates

**Tradeoffs:**
- Additional API call
- Slower execution
- Requires good critic

**When to use:**
Quality critical; cost of errors high.

**Example:**
Generate → Critique → Revise → Accept or repeat

### Pattern 5: Tool Use

**What it is:**
Discover, authorize, execute, fallback.

**Use case:**
Extending agent capabilities with external tools.

**Benefits:**
- Access external data
- Execute actions
- Extend capabilities
- Ground in reality

**Tradeoffs:**
- Tool selection overhead
- Execution failures
- Authorization complexity

**When to use:**
Agents need capabilities beyond reasoning.

**Example:**
Agent uses web search, database queries, APIs

### Pattern 6: Planning

**What it is:**
Define milestones, dependencies, constraints.

**Use case:**
Complex projects with dependencies.

**Benefits:**
- Clear roadmap
- Dependency awareness
- Constraint handling
- Progress tracking

**Tradeoffs:**
- Planning overhead
- Re-planning when blocked
- Accuracy uncertainty

**When to use:**
Complex workflows with dependencies and constraints.

**Example:**
Project breakdown structure with task dependencies.

### Pattern 7: Multi-Agent Collaboration

**What it is:**
Manager + specialized roles + shared memory.

**Use case:**
Complex problems requiring multiple perspectives.

**Benefits:**
- Specialization
- Collaboration
- Knowledge sharing
- Robustness

**Tradeoffs:**
- Coordination complexity
- Communication overhead
- Consistency challenges

**When to use:**
Problems benefit from multiple specialized agents.

**Example:**
Manager coordinates Engineer + Researcher + Designer agents

### Pattern 8: Memory Management

**What it is:**
Short-term, episodic, and long-term memory with retrieval.

**Use case:**
Context preservation across interactions.

**Benefits:**
- Context awareness
- Learning over time
- Pattern recognition
- Personalization

**Tradeoffs:**
- Storage requirements
- Retrieval accuracy
- Privacy considerations

**When to use:**
Long-running agents needing historical context.

**Example:**
Conversation memory + learned preferences + patterns over time.

### Pattern 9: Learning & Adaptation

**What it is:**
Feedback → prompts/policies/tests adjustment.

**Use case:**
Continuous improvement through feedback.

**Benefits:**
- Improves over time
- Adapts to domain
- Personalizes behavior
- Reduces errors

**Tradeoffs:**
- Feedback collection needed
- Learning latency
- Stability vs. adaptation

**When to use:**
Long-term agents that improve with experience.

**Example:**
Collect user feedback, improve prompts accordingly.

### Pattern 10: Goal Setting & Monitoring

**What it is:**
Define KPIs, track drift, course-correct.

**Use case:**
Ensuring agents maintain performance.

**Benefits:**
- Performance visibility
- Drift detection
- Automated correction
- Accountability

**Tradeoffs:**
- Metric definition difficulty
- Correction overhead
- Threshold tuning

**When to use:**
Production agents requiring performance guarantees.

**Example:**
Track success rates, detect degradation, retrain if needed.

### Pattern 11: Exception Handling & Recovery

**What it is:**
Classify errors, backoff, fallbacks.

**Use case:**
Graceful degradation under failure.

**Benefits:**
- Robustness
- Recovery capability
- User experience
- Operational reliability

**Tradeoffs:**
- Complex logic
- Multiple paths
- Testing overhead

**When to use:**
Production systems requiring reliability.

**Example:**
API fails → retry with backoff → fallback to simpler method.

### Pattern 12: Human-in-the-Loop

**What it is:**
Review cues and approvals.

**Use case:**
High-stakes decisions requiring human oversight.

**Benefits:**
- Risk mitigation
- Quality assurance
- Compliance
- Trust

**Tradeoffs:**
- Workflow slowdown
- Human bottleneck
- Cost increase

**When to use:**
High-risk decisions or regulatory requirements.

**Example:**
Agent proposes action → human reviews → approves/rejects.

### Pattern 13: Retrieval-Augmented Generation (RAG)

**What it is:**
Parse, chunk, embed, rerank workflow.

**Use case:**
Grounding agent knowledge in documents.

**Benefits:**
- Current information
- Reduced hallucinations
- Knowledge grounding
- Scalable knowledge

**Tradeoffs:**
- Retrieval latency
- Chunk size tradeoffs
- Index maintenance

**When to use:**
Knowledge-intensive tasks; document-based reasoning.

**Example:**
User query → retrieve relevant documents → generate answer.

### Pattern 14: Inter-Agent Communication

**What it is:**
Protocols, agent IDs, message expiry.

**Use case:**
Multi-agent systems requiring coordination.

**Benefits:**
- Structured coordination
- Message routing
- Timeout handling
- State management

**Tradeoffs:**
- Protocol complexity
- Message overhead
- Debugging difficulty

**When to use:**
Complex multi-agent systems.

**Example:**
Agents exchange structured messages with protocol definitions.

### Pattern 15: Resource-Aware Optimization

**What it is:**
Route by cost/complexity/latency.

**Use case:**
Cost-effective agent execution.

**Benefits:**
- Lower costs
- Faster execution
- Resource efficiency
- Scalability

**Tradeoffs:**
- Routing logic
- Quality variation
- Complexity

**When to use:**
Cost or latency sensitive applications.

**Example:**
Simple queries to fast model, complex to powerful model.

### Pattern 16: Reasoning Techniques

**What it is:**
Chain-of-Thought, Tree-of-Thought, self-consistency, debate.

**Use case:**
Improving reasoning quality.

**Benefits:**
- Better reasoning
- Error reduction
- Transparency
- Multiple perspectives

**Tradeoffs:**
- Computational cost
- Latency increase
- Output volume

**When to use:**
Complex reasoning tasks.

**Examples:**
- CoT: Show reasoning steps
- ToT: Explore multiple reasoning paths
- Debate: Multiple perspectives

### Pattern 17: Evaluation & Monitoring

**What it is:**
Golden sets, SLAs, drift detection.

**Use case:**
Production quality assurance.

**Benefits:**
- Performance visibility
- Issue detection
- Trend analysis
- Decision support

**Tradeoffs:**
- Metric definition
- Evaluation cost
- Baseline maintenance

**When to use:**
All production systems.

**Example:**
Track accuracy against golden test set; alert on degradation.

### Pattern 18: Guardrails & Safety

**What it is:**
PII protection, injection defense, sandboxing.

**Use case:**
Security and safety requirements.

**Benefits:**
- Data protection
- Attack prevention
- Regulatory compliance
- Trust

**Tradeoffs:**
- Performance impact
- False positives
- Complexity

**When to use:**
Any production system handling sensitive data.

**Example:**
Detect PII, block prompt injection, sandbox execution.

### Pattern 19: Prioritization

**What it is:**
Score by value × effort × urgency × risk, reorder.

**Use case:**
Resource allocation and task ordering.

**Benefits:**
- Optimal allocation
- Clear priorities
- Fairness
- Efficiency

**Tradeoffs:**
- Scoring complexity
- Dynamic reordering
- User expectations

**When to use:**
Systems with limited resources or multiple requests.

**Example:**
Queue requests, prioritize high-value/low-effort items first.

### Pattern 20: Exploration & Discovery

**What it is:**
Map space, cluster, probe.

**Use case:**
Discovering solution spaces and patterns.

**Benefits:**
- Novel solutions
- Pattern discovery
- Optimization
- Innovation

**Tradeoffs:**
- Exploration cost
- Convergence uncertainty
- Unfamiliar territory

**When to use:**
Novel problems or optimization tasks.

**Example:**
Agent explores problem space, clusters solutions, probes promising areas.

## Pattern Combinations for Robust Systems

### Quick Recipes

**Content Generation:**
Chaining + Reflection + Learning

**Customer Support:**
Routing + Tool Use + Human-in-loop + Exception Handling

**Data Analysis:**
Parallelization + Reflection + Evaluation + Monitoring

**Knowledge Q&A:**
RAG + Routing + Evaluation

**Autonomous Systems:**
Planning + Tool Use + Multi-Agent + Goal Monitoring

## Key Tradeoffs Summary

### Cost vs. Quality
**Cost-optimized:**
Resource-aware routing, tool selection.

**Quality-optimized:**
Reflection, multiple reasoning techniques, human-in-loop.

### Latency vs. Reliability
**Low latency:**
Parallelization, streaming, early termination.

**High reliability:**
Exception handling, recovery, monitoring.

### Automation vs. Control
**Autonomous:**
Goal-setting, learning, planning.

**Human-controlled:**
Human-in-loop, guardrails, approval workflows.

## Implementation Approach

### Start Simple
**Begin with:**
Prompt chaining + tool use + basic error handling.

**Validate:**
Does basic pattern solve problem?

### Add Sophistication
**Layer 2:**
Add reflection, monitoring, evaluation.

**Layer 3:**
Add learning, multi-agent, advanced reasoning.

### Optimize Production
**When ready:**
Add resource optimization, guardrails, human-in-loop.

## Key Insights

### Patterns Are Building Blocks
**Reality:**
Most agents combine multiple patterns.

**Strategy:**
Understand individual patterns, combine strategically.

### Know Your Tradeoffs
**Principle:**
Every pattern involves cost/latency/quality tradeoffs.

**Practice:**
Understand tradeoffs; make deliberate choices.

### Avoid Over-Engineering
**Temptation:**
Use all 20 patterns.

**Reality:**
Most problems solved with 3-5 patterns.

**Discipline:**
Add complexity only when needed.

### Production Readiness Checklist
Before production, ensure:
- [ ] Error handling & recovery
- [ ] Monitoring & evaluation
- [ ] Guardrails & safety
- [ ] Human-in-loop where needed
- [ ] Cost optimization
- [ ] Fallback strategies

## Key Takeaways

1. **20 patterns exist for good reason** — Each solves specific problems
2. **Prompt chaining is foundation** — Most agents start here
3. **Routing enables specialization** — Specialists outperform generalists
4. **Parallelization speeds execution** — Use when tasks independent
5. **Reflection improves quality** — Reduces hallucinations
6. **Tool use extends capability** — Grounds agents in reality
7. **Planning handles complexity** — Dependencies and constraints essential
8. **Multi-agent collaboration powerful** — Specialization + coordination
9. **Memory critical for context** — Short, episodic, long-term
10. **Learning enables improvement** — Feedback drives better behavior
11. **Monitoring detects problems** — Essential for production
12. **Human-in-loop for high stakes** — Risk mitigation
13. **RAG grounds knowledge** — Reduces hallucinations
14. **Safety guardrails non-negotiable** — Production requirement
15. **Evaluation essential** — Can't manage what you don't measure
16. **Combine patterns strategically** — Don't use all 20
17. **Know your tradeoffs** — Cost vs. quality, latency vs. reliability
18. **Start simple, add sophistication** — Avoid premature complexity
19. **TL;DRs help fast learning** — Quick reference key
20. **Free resources available** — Diagrams and Mermaid files provided

## The Bottom Line

Mark Kashef's 20 agentic AI design patterns course provides the professional's playbook for building reliable, production-grade agents. Rather than abstract concepts, each pattern shows when to use it, why it works, what tradeoffs exist, and how to implement it.

Key insight: most agents combine 3-5 patterns, not all 20. Understanding individual patterns enables strategic combination. The course disciplines against over-engineering—a common mistake where developers add complexity before proving it's needed.

The most important patterns for production readiness:
1. Prompt chaining (foundation)
2. Tool use (capability extension)
3. Exception handling (reliability)
4. Evaluation & monitoring (visibility)
5. Guardrails & safety (protection)
6. Reflection (quality)

Add more patterns as the use case requires: routing for specialization, multi-agent for complexity, learning for improvement, human-in-loop for high-stakes decisions.

For developers building production agents, this course provides both learning and reference material. Study the individual patterns, understand the tradeoffs, apply strategically, and avoid unnecessary complexity. The free repo with diagrams and Mermaid files enables quick implementation of any pattern.

The discipline is: know your problem, choose minimal patterns that solve it, combine strategically, and add complexity only when justified by requirements, not preferences.
