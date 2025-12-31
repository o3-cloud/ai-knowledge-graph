---
summary: Chau Tran (Glean) introduces Workflow Search paradigm for enterprise-aware agents—balancing predictability on common tasks with flexibility on unforeseen scenarios through contextual understanding
event_type: video
sources:
    - https://www.youtube.com/watch?v=hxFpUcvWPcU
tags:
    - enterprise-agents
    - workflow-search
    - enterprise-context
    - semantic-search
    - agent-design
    - predictability
    - flexibility
    - Glean
---

# How to Build Enterprise Aware Agents

**Speaker:** Chau Tran (Software Engineer, Glean)
**Conference:** AI Engineer World's Fair
**Location:** San Francisco
**Platform:** YouTube (AI Engineer)
**Duration:** ~30-40 minutes
**Publication Date:** December 20, 2025

## Overview

Chau Tran from Glean addresses a fundamental gap in agent design: out-of-the-box LLM reasoning is like hiring a brilliant employee with no enterprise context. He introduces "Workflow Search" as a paradigm for building enterprise-aware agents that understand "how things are done at this company." The framework balances predictability on common workflows with flexibility for novel situations.

## The Problem: Context-Free LLMs

### The Analogy

**LLM capability:**
- Highly intelligent
- Strong reasoning ability
- Broad knowledge
- Impressive general skills

**Missing:**
- Organization context
- Business processes
- Company workflows
- Implicit conventions
- Operational knowledge

**Result:**
Brilliant but incompetent in your specific environment.

### Why It Matters

**Without context:**
- Takes wrong paths
- Doesn't know company norms
- Misses efficient workflows
- Creates friction points
- Lacks organizational awareness

**With context:**
- Understands best practices
- Follows company processes
- Works efficiently
- Reduces friction
- Operates effectively

## The Workflow Search Paradigm

### Core Concept

**Instead of:**
- Agents that reason from first principles
- Generic approaches applied broadly
- One-size-fits-all solutions
- Context-agnostic decisions

**Use:**
- Agents that understand workflows
- Organization-specific approaches
- Tailored to company processes
- Context-aware decisions

### How It Works

```
Agent encounters task
    ↓
Search company workflows
    ↓
Find relevant workflow
    ↓
Follow workflow pattern
    ↓
Execute task contextually
    ↓
Result matches organization
```

### The Efficiency Gain

**Traditional agent:**
- Reasons about everything
- Generates approaches
- Tests solutions
- Learns through trial
- Slow at first

**Workflow Search agent:**
- Finds existing workflow
- Follows known pattern
- Executes efficiently
- Learns from organization
- Fast from start

## Balancing Predictability and Flexibility

### The Tension

**Predictability:**
- Follow known paths
- Consistent results
- Efficient execution
- Reduces variance
- Organization understood

**Flexibility:**
- Handle novel situations
- Adapt to new problems
- Creative solutions
- Unexpected challenges
- Growth potential

**Challenge:**
Too much predictability → Brittle, can't handle novel cases
Too much flexibility → Unpredictable, inconsistent

### The Solution: Graduated Flexibility

**Tier 1: Common Workflows (Highly Predictable)**
- Frequently occurring tasks
- Well-established workflows
- Follow patterns exactly
- Minimal deviation needed
- High consistency

**Tier 2: Variations (Moderate Flexibility)**
- Related to known workflows
- Apply patterns with modifications
- Some customization needed
- Clear decision points
- Documented variations

**Tier 3: Novel Situations (High Flexibility)**
- Unforeseen problems
- No direct workflow match
- Reason from principles
- Create new approaches
- Learn from outcomes

### Implementation Approach

**1. Capture Workflows**
- Document common processes
- Codify best practices
- Identify decision points
- Create workflow maps

**2. Build Search Capability**
- Index workflows semantically
- Enable searching by scenario
- Match contexts to workflows
- Retrieve relevant patterns

**3. Create Flexibility Points**
- Where adaptation needed
- How to modify workflow
- Decision criteria
- Fallback approaches

**4. Handle Novel Cases**
- When no workflow matches
- How to reason
- How to fallback
- How to learn

## Enterprise Context Integration

### What Constitutes "Enterprise Context"

**Knowledge types:**
- Business processes
- Organizational structure
- Team responsibilities
- Tool ecosystems
- Data systems
- Communication norms
- Decision authorities
- Success metrics

**How it helps:**
- Agents understand boundaries
- Know who to ask
- Follow approval chains
- Use right tools
- Understand constraints

### Building Enterprise Context

**Data sources:**
- Process documentation
- Organizational charts
- Tool configurations
- Historical decisions
- Team knowledge
- System integrations

**Integration approach:**
- Semantic search over context
- Retrieve relevant information
- Ground agent reasoning
- Provide decision support
- Enable appropriate action

## Workflow Search in Practice

### Example: Document Routing

**Common workflow:**
1. Receive document
2. Classify by type
3. Check approval status
4. Route to owner
5. Create tracking task

**Workflow Search approach:**
- Agent searches for "document routing" workflow
- Finds standard process
- Executes steps in sequence
- Handles common variations
- Routes efficiently

**Flexibility:**
- Novel document type?
- Escalate with context
- Reason about classification
- Create new route

### Example: Customer Support

**Common workflows:**
- Issue triage (what category?)
- Resolution (is there known solution?)
- Escalation (when needed?)
- Follow-up (after resolution)

**Workflow Search:**
- Classify incoming issue
- Search for matching workflow
- Apply process
- Escalate if needed
- Track resolution

**Flexibility:**
- Unusual issue type
- Complex customer context
- Unforeseen complication
- Reason and adapt

## Technical Implementation

### Architecture Components

**1. Workflow Repository**
- Store process definitions
- Version control
- Update management
- Search indexing

**2. Semantic Search Engine**
- Index workflows
- Query by context
- Retrieve matches
- Rank by relevance

**3. Workflow Executor**
- Follow workflow steps
- Handle decision points
- Manage state
- Execute actions

**4. Context Manager**
- Maintain org context
- Provide information
- Update knowledge
- Track changes

**5. Flexibility Layer**
- Detect novel cases
- Reason about options
- Create new workflows
- Learn from outcomes

### Glean's Implementation

**Glean Assistant leverages:**
- Semantic understanding of workflows
- Enterprise context grounding
- Flexible execution
- Learning from interactions
- Assistant API integration

## Benefits of Workflow Search

### For Organizations

**Efficiency:**
- Standard processes execute faster
- Less time reasoning from scratch
- Consistent execution
- Known paths recognized

**Consistency:**
- Familiar patterns applied
- Predictable outcomes
- Organization norms respected
- Quality maintained

**Knowledge capture:**
- Workflows documented
- Best practices preserved
- Learning institutionalized
- Context built up

### For Agents

**Capability:**
- Understand organization
- Execute effectively
- Learn from workflows
- Improve over time

**Context:**
- Know what's possible
- Understand constraints
- Follow procedures
- Respect boundaries

### For Users

**Experience:**
- Agents work naturally
- Know how to help
- Follow company norms
- Execute efficiently

**Trust:**
- Predictable behavior
- Known patterns
- Organizational alignment
- Consistent results

## Scaling Workflow Search

### Small Organization

**Approach:**
- Document key workflows
- Build initial search index
- Handle novel cases informally
- Learn and refine

**Effort:** Low to moderate

### Medium Organization

**Approach:**
- Comprehensive workflow documentation
- Semantic indexing
- Variation handling
- Regular updates
- Learning mechanisms

**Effort:** Moderate

### Large Organization

**Approach:**
- Multiple workflow repositories (by domain)
- Sophisticated search
- Complex decision logic
- Cross-functional workflows
- Continuous learning

**Effort:** Significant but worthwhile

## Key Takeaways

1. **Context matters enormously** — LLMs brilliant but context-free
2. **Workflow Search grounds agency** — Organization-specific decision-making
3. **Balance efficiency and adaptability** — Predictability plus flexibility
4. **Capture institutional knowledge** — Workflows are learning
5. **Enable semantic search** — Find workflows by context
6. **Graduated flexibility** — Common paths confident, novel cases careful
7. **Enterprise awareness** — Understand organizational boundaries
8. **Learn continuously** — Improve from interactions
9. **Scale thoughtfully** — Complexity grows with size
10. **Technical foundation needed** — Search, execution, context management

## The Bottom Line

Chau Tran's Workflow Search paradigm addresses the fundamental limitation of context-free agents. Brilliant but inexperienced LLMs need organizational context—understanding how decisions are made, what processes are followed, who has authority, what tools to use, and how things work at this particular company.

The key innovation is balancing predictability (follow known workflows efficiently) with flexibility (reason about novel cases thoughtfully). Common tasks execute quickly through known patterns. Unusual situations trigger more careful reasoning. Over time, new patterns become documented workflows, and the system learns.

Implementation requires semantic search over process documentation, organizational context integration, decision logic for known vs. novel situations, and continuous learning. As organizations implement this approach, their agents become increasingly effective—moving from generic assistance to deeply embedded operational partners that understand how things really work.

The approach is particularly valuable for enterprise deployment where organizational context, process predictability, and consistent outcomes matter. Rather than agents that struggle to understand company norms, Workflow Search enables agents that naturally operate within organizational processes and continuously improve as they learn from interactions.
