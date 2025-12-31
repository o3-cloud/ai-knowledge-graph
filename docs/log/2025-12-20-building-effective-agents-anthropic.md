---
summary: Anthropic reveals that effective agent implementations use simple composable patterns over complex frameworks—emphasizing simplicity, transparency, and tool design as foundational principles
event_type: engineering-guide
sources:
    - https://www.anthropic.com/engineering/building-effective-agents
tags:
    - agent-architecture
    - agent-patterns
    - simplicity
    - tool-design
    - prompt-engineering
    - orchestration
    - LLM-agents
    - best-practices
---

# Building Effective Agents

**Organization:** Anthropic Engineering
**Publication Date:** December 20, 2025

## Overview

Anthropic's engineering guide on building effective agents reveals a counterintuitive finding: the most successful agent implementations rely on simple, composable patterns rather than complex frameworks. The guide emphasizes three foundational principles—simplicity, transparency, and documentation—and outlines six main architectural patterns for different use cases.

## The Core Philosophy

### Simplicity Over Complexity

**Key finding:**
"The most successful implementations weren't using complex frameworks or specialized libraries. Instead, they were building with simple, composable patterns."

**Implication:**
- Add complexity only when it demonstrably improves outcomes
- Start simple, optimize incrementally
- Frameworks often add overhead without benefit
- Direct LLM API calls often sufficient

**Practical approach:**
- Begin with basic prompt and tool
- Test and measure
- Add complexity only if needed
- Keep designs straightforward

## Three Foundational Principles

### 1. Simplicity

**Why it matters:**
- Easier to understand
- Easier to debug
- Easier to maintain
- Easier to modify

**Where it applies:**
- Agent design
- Prompt structure
- Tool definitions
- Architecture patterns

**How to achieve:**
- Start minimal
- Add only necessary complexity
- Question each component
- Prefer straightforward approaches

### 2. Transparency

**Why it matters:**
- Visible planning improves reliability
- Understand agent reasoning
- Debug failures
- Verify correctness

**What to make visible:**
- Planning steps
- Tool calls
- Decision points
- Reasoning traces

**How to implement:**
- Show agent thinking in outputs
- Log all decisions
- Trace tool usage
- Make reasoning explicit

### 3. Documentation and Testing

**Why it matters:**
- Tools are agent-computer interface
- Poor tools → poor agent behavior
- Detailed specs enable better performance
- Testing catches failures early

**What to document:**
- Tool purpose
- Parameters and constraints
- Return format and meaning
- Edge cases and errors

**Testing approach:**
- Sandboxed testing
- Diverse scenarios
- Edge cases
- Failure modes

## Six Architectural Patterns

### 1. Augmented LLM

**What it is:**
Base LLM with added capabilities: retrieval, tools, memory.

**Components:**
```
LLM Core
├─ Retrieval (context from documents)
├─ Tools (actions in external systems)
└─ Memory (conversation history)
```

**When to use:**
- Single-agent simple tasks
- Need for context and tools
- Information retrieval focus
- Conversational interface

**Strengths:**
- Simple to implement
- Familiar pattern
- Effective for many tasks
- Low overhead

**Limitations:**
- Single agent only
- Limited decomposition
- No specialization

### 2. Prompt Chaining

**What it is:**
Sequential LLM calls where output of one becomes input to next.

**Pattern:**
```
LLM Call 1 → Output
    ↓
LLM Call 2 → Output
    ↓
LLM Call 3 → Final Result
```

**When to use:**
- Multi-step tasks
- Complex reasoning
- Clear sequential workflow
- Each step has defined input/output

**Strengths:**
- Decompose complex tasks
- Better focus per step
- Easier to understand
- Simple to implement

**Limitations:**
- Sequential only (slower)
- Error propagation
- No dynamic branching
- Fixed workflow

**Example:**
```
Step 1: Analyze problem
Step 2: Research solutions
Step 3: Generate recommendation
Step 4: Format response
```

### 3. Routing

**What it is:**
Classify input to route to specialized downstream processes.

**Pattern:**
```
Input → Classifier LLM → Route to:
                        ├─ Handler A (specialized)
                        ├─ Handler B (specialized)
                        └─ Handler C (specialized)
```

**When to use:**
- Different task types need different handling
- Specialized handlers for domains
- Cost optimization (route to appropriate model)
- Quality specialization

**Strengths:**
- Optimize for specific task
- Cost efficiency
- Quality improvement
- Clear responsibility

**Limitations:**
- Must handle diverse inputs
- Routing errors propagate
- Multiple handlers needed
- Testing complexity

**Example:**
```
Customer inquiry → Routing LLM → Route to:
                                ├─ Support (problem)
                                ├─ Sales (inquiry)
                                └─ Technical (bug)
```

### 4. Parallelization

**What it is:**
Run independent subtasks simultaneously for efficiency.

**Pattern:**
```
Main Task
├─ Parallel Task 1 → Result A
├─ Parallel Task 2 → Result B
└─ Parallel Task 3 → Result C
    ↓
Combine Results
```

**When to use:**
- Independent subtasks
- Need faster results
- Multiple attempts for robustness
- Breadth-first exploration

**Strengths:**
- Speed (parallel execution)
- Robustness (multiple attempts)
- Efficiency
- Thoroughness

**Limitations:**
- Dependency management
- Result combination
- Cost (multiple calls)
- Complexity

**Example:**
```
Generate content
├─ Parallel: Generate headline
├─ Parallel: Generate body
└─ Parallel: Generate summary
    ↓
Combine into final output
```

### 5. Orchestrator-Workers

**What it is:**
Central LLM delegates dynamic subtasks to specialized worker agents.

**Pattern:**
```
Orchestrator LLM
├─ Analyze task
├─ Create plan
└─ Delegate to:
    ├─ Worker 1 (specialized)
    ├─ Worker 2 (specialized)
    └─ Worker 3 (specialized)
        ↓
    Results → Synthesize
```

**When to use:**
- Complex tasks needing specialization
- Dynamic task decomposition
- Coordination needed
- Hierarchical workflow

**Strengths:**
- Handle complexity
- Dynamic adaptation
- Specialization
- Flexible workflow

**Limitations:**
- Complex orchestration
- Difficult to debug
- More expensive
- Higher overhead

**Example:**
```
Research task
├─ Orchestrator analyzes scope
└─ Dispatches to:
    ├─ Literature searcher
    ├─ Data analyst
    ├─ Expert consulter
    └─ Synthesis writer
        ↓
    Final research report
```

### 6. Evaluator-Optimizer

**What it is:**
Iterative refinement where evaluator assesses outputs and optimizer improves them.

**Pattern:**
```
Initial Output
    ↓
Evaluator LLM → Assessment
    ↓
Poor? → Optimizer LLM → Improved Output
    ↓
Good? → Final Result
```

**When to use:**
- High-quality output needed
- Quality is measurable
- Iterative improvement beneficial
- Can afford multiple passes

**Strengths:**
- Improve output quality
- Handle complex requirements
- Catch errors
- Refine results

**Limitations:**
- More expensive (multiple calls)
- Slower
- Requires clear evaluation criteria
- May not converge

**Example:**
```
Generate article
    ↓
Evaluate quality
    ↓
Identified issues → Improve
    ↓
Re-evaluate → Accept/repeat
```

## Tool Design as Critical Interface

### Treating Tools Like UI

**Philosophy:**
Tools are the agent-computer interface. Poor tools → poor agent behavior.

**Principles:**
- Clear purpose
- Explicit parameters
- Documented constraints
- Error handling
- Edge case handling

### Tool Specification

**What to define:**
```
Tool: search_documents
Purpose: Find relevant documents
Parameters:
  - query (string, max 100 chars)
  - max_results (int, 1-100)
  - filters (optional, predefined list)
Returns:
  - documents (array)
    - id (string)
    - score (0-1)
    - excerpt (string)
Errors:
  - no_results: query returned nothing
  - invalid_filter: filter not recognized
```

**Why it matters:**
- Agent understand exactly what tool does
- Clear error handling
- Proper parameter usage
- Predictable behavior

## Testing and Validation

### Sandboxed Testing

**What to test:**
- Tool outputs correct results
- Error handling works
- Edge cases handled
- Performance acceptable
- Safety guardrails effective

### Diverse Scenarios

**Test coverage:**
- Happy path (typical use)
- Edge cases
- Error conditions
- Boundary conditions
- Malicious inputs

### Guardrails for Autonomy

**For autonomous agents:**
- Cost limits
- Action rate limits
- Approval requirements
- Rollback capability
- Monitoring and alerts

## Practical Implementation Approach

### Start Simple

**Phase 1: Basic agent**
- Simple prompt
- One or two tools
- Minimal orchestration
- Test thoroughly

**Phase 2: Evaluate**
- Measure performance
- Identify gaps
- Assess complexity ROI
- Determine improvements

**Phase 3: Add complexity**
- Add only if beneficial
- Measure impact
- Keep designs simple
- Document patterns

### Use LLM APIs Directly

**Not frameworks initially:**
- Understand fundamentals
- Build custom patterns
- Optimize for use case
- Avoid framework overhead

**When frameworks make sense:**
- Building production systems
- Team needs patterns
- Sufficient maturity
- Clear benefits

## Key Recommendations

1. **Start simple** — Basic prompt + tools sufficient for many tasks
2. **Test extensively** — Sandboxed testing catches issues
3. **Make tools explicit** — Clear specs enable better agent behavior
4. **Measure before optimizing** — Only add complexity with evidence
5. **Keep transparent** — Visible reasoning easier to debug
6. **Document thoroughly** — Tool specs critical for agent success
7. **Use direct APIs** — Understand patterns before frameworks
8. **Choose pattern purposefully** — Match pattern to task requirements
9. **Invest in tool design** — Agent-computer interface critical
10. **Iterate incrementally** — Add complexity gradually with evidence

## Key Takeaways

1. **Simplicity wins** — Complex frameworks often unnecessary
2. **Six patterns cover most cases** — Augmented LLM, chaining, routing, parallelization, orchestration, evaluation
3. **Tools are interface** — Invest in clear tool design
4. **Transparency matters** — Make agent reasoning visible
5. **Testing essential** — Sandboxed testing and guardrails
6. **Start with basics** — Use LLM APIs directly
7. **Measure complexity** — Only add if demonstrable improvement
8. **Pattern selection** — Choose pattern matching task
9. **Documentation critical** — Tool specs enable agent success
10. **Iterate carefully** — Add complexity with evidence

## The Bottom Line

Anthropic's engineering guide on building effective agents emphasizes that success comes from simplicity and clear thinking, not complex frameworks. The most effective implementations use straightforward patterns: augmented LLM for single-agent tasks, prompt chaining for sequential workflows, routing for specialization, parallelization for speed, orchestrator-workers for complex coordination, and evaluator-optimizer for iterative refinement.

The key insight is treating tool design as critical: just as user interface matters for human-computer interaction, tool specification matters for agent-computer interaction. Clear, well-documented tools enable agents to behave more reliably and effectively.

The practical recommendation is to start simple—basic prompt plus one or two tools, tested thoroughly. Only add architectural complexity when you have evidence it improves outcomes. Invest in understanding these patterns directly through LLM APIs rather than jumping to frameworks. The path to effective agents isn't revolutionary architecture—it's thoughtful simplicity, clear tool design, and incremental improvement based on measurement.
