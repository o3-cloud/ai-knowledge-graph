---
summary: Thariq Shihipar introduces the Claude Agent SDK—framework for autonomous agents with computer access—covering context gathering, action capabilities, verification patterns, and the gather-act-verify loop
event_type: blog_post
sources:
    - https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk
tags:
    - Claude-Agent-SDK
    - agentic-AI
    - agent-architecture
    - tool-design
    - MCP-integration
    - context-management
    - subagents
    - verification-patterns
    - autonomous-agents
---

# Building Agents with the Claude Agent SDK

**Author:** Thariq Shihipar
**Contributors:** Molly Vorwerck, Suzanne Wang, Alex Isken, Cat Wu, Keir Bradwell, Alexander Bricken, Ashwin Bhat
**Publication Date:** September 29, 2025
**Organization:** Anthropic

## Overview

Thariq Shihipar and the Anthropic team introduce the Claude Agent SDK—a comprehensive framework for building autonomous agents by giving Claude the tools programmers use every day. Rather than abstract agent concepts, the SDK provides concrete patterns for context gathering, action execution, and work verification in a continuous feedback loop.

The core philosophy: autonomous agents should have access to the same capabilities as developers—bash scripts, code execution, file system navigation, and external service integrations.

## Core Philosophy

### "Claude Needs the Same Tools That Programmers Use Every Day"

**Principle:**
To build capable agents, provide them with the tools that make humans productive.

**Implication:**
- File system access
- Script execution capability
- Code generation and execution
- External service integration

**Contrast:**
Instead of building agent-specific "AI-friendly" interfaces, provide real tools.

## The Agent Loop: Gather → Act → Verify → Repeat

### Architecture Overview

**Simple but powerful cycle:**

```
1. GATHER CONTEXT
   ↓
2. TAKE ACTION
   ↓
3. VERIFY WORK
   ↓
4. REPEAT (if needed)
```

**Each phase has specific responsibilities and techniques.**

## Phase 1: Context Gathering

### The Challenge

**Problem:**
Agents need to understand the current state (files, code, data, situation) before acting.

**Constraint:**
Context window is limited; can't load everything.

**Solution:**
Intelligent context gathering that retrieves only relevant information.

### Agentic Search: Bash-Based Navigation

**Approach:**
Use bash commands (grep, find, tail, cat, ls) for transparent, semantic-appropriate file system navigation.

**Why bash:**
- Developers know these commands
- Commands are deterministic and clear
- Outputs are predictable
- Errors are informative

**Typical search pattern:**

```bash
# Find all references to a variable
grep -r "variable_name" src/

# List files modified recently
find . -type f -mtime -1

# Examine end of log file
tail -100 debug.log

# Search for pattern with context
grep -B 2 -A 2 "error message" system.log
```

**Benefit:**
Agent's reasoning is transparent; humans understand what search returned and why.

### Semantic Search: When Bash Alone Isn't Enough

**Use case:**
Finding conceptually related information when exact keywords unknown.

**Implementation:**
Vector-based semantic search that complements bash queries.

**Pattern:**
```
Bash search for exact matches first
If results insufficient, semantic search for conceptual matches
Combine results intelligently
```

**Trade-offs:**

**Bash (agentic) search:**
- Transparent (you see exactly what was searched)
- Deterministic (same query = same result)
- Verifiable (can repeat manually)
- Less "magical"

**Semantic search:**
- Finds conceptually related content
- Requires less keyword precision
- Probabilistic (may vary)
- More powerful for understanding

**Recommendation:**
Start with bash/agentic search. Adopt semantic search when needed for speed or complexity.

### Subagents for Parallel Context Gathering

**Use case:**
Information-heavy tasks where context needs to come from multiple sources.

**Pattern:**

```
Main Agent:
- Needs to synthesize information from:
  - Document A
  - Document B
  - API response
  - Database query

Instead of:
- Loading all into one context (bloats window)

Do this:
- Spawn SubagentA → reads Document A → returns summary
- Spawn SubagentB → reads Document B → returns summary
- Spawn SubagentC → queries API → returns results
- Main agent receives three clean summaries
```

**Benefits:**
- Each subagent has focused, clean context
- Parallel execution (faster)
- Summaries are cleaner than raw data
- Main agent stays focused
- Scales to complex information needs

**Example: Research synthesis**

```
Task: "Summarize market trends across three industry reports"

SubagentA: "Read report1.pdf, summarize industry trends"
SubagentB: "Read report2.pdf, summarize industry trends"
SubagentC: "Read report3.pdf, summarize industry trends"

Main Agent: Receives three summaries, synthesizes comprehensive market analysis
```

### Automatic Context Compaction

**Problem:**
Long-running agent operations accumulate context until window fills.

**Solution:**
Automatic compaction summarizes progress and resets context.

**Process:**

```
Agent operates normally
    ↓
Context approaches limit (80%)
    ↓
System identifies key information to retain
    ↓
Generate summary of progress
    ↓
Reset context with summary instead of full history
    ↓
Agent continues with clean window
```

**What gets retained:**
- Key facts discovered
- Decisions made
- Progress toward goal
- Not: every intermediate step

**Benefit:**
Agents can work on extended tasks without context explosion.

## Phase 2: Action Capabilities

### Custom Tools: Primary Building Block

**Principle:**
Custom tools are fundamental to agent capability.

**Design pattern:**

```python
@tool
def fetch_weather(location: str) -> str:
    """Get current weather for a location."""
    # Implementation fetches weather data
    return weather_report

@tool
def save_document(path: str, content: str) -> None:
    """Save content to file."""
    # Implementation writes file
    return result
```

**Characteristics:**
- Clear input/output contracts
- Single responsibility
- Well-documented behavior
- Predictable results

### Bash Scripting for Flexibility

**Use case:**
Complex operations not covered by specific tools.

**Approach:**
Agents can execute arbitrary bash commands within sandbox.

**Examples:**

```bash
# Build and test code
./build.sh && npm test

# Process files
find . -name "*.log" | xargs grep "ERROR"

# Data transformation
cat data.csv | cut -d',' -f1,3 | sort | uniq

# System operations
ps aux | grep process_name
```

**Benefit:**
Unlimited flexibility for complex operations.

### Code Generation for Reusable Solutions

**When to use:**
Operations complex enough to warrant actual code.

**Pattern:**
Agent generates Python/JavaScript/etc., then executes it.

**Advantage:**
- More maintainable than bash
- Better error handling
- Reusable across runs
- Easier to test and verify

**Example:**

```python
# Agent generates and executes:
import json

def process_customer_data(raw_data):
    customers = json.loads(raw_data)
    high_value = [c for c in customers if c['lifetime_value'] > 10000]
    return {
        'total': len(customers),
        'high_value_count': len(high_value),
        'high_value_customers': high_value
    }

result = process_customer_data(data)
```

### Model Context Protocol (MCP) Integration

**Purpose:**
Standardized tool integration with external services.

**Supported integrations:**
- **Slack:** Post messages, read channels, manage workflows
- **GitHub:** Manage repositories, pull requests, issues
- **Asana:** Create tasks, manage projects, track progress
- **Linear:** Manage issues and projects
- **Jira:** Integrate with issue tracking
- **Custom:** Build MCPs for any service

**Pattern:**

```
Agent needs to create GitHub issue
    ↓
Calls GitHub MCP tool
    ↓
MCP handles authentication, API calls, formatting
    ↓
Issue created, result returned to agent
```

**Benefit:**
Agents can integrate with enterprise systems without building custom integrations.

## Phase 3: Work Verification

### Rule-Based Feedback: Linting

**Use case:**
Verify generated code meets standards.

**Implementation:**
Run code linters/validators on generated output.

**Examples:**

```bash
# Verify Python code style
pylint generated_file.py

# Check TypeScript types
npx tsc --noEmit

# Lint HTML/CSS
stylelint generated.css

# Validate JSON
jq empty generated.json
```

**Benefit:**
Immediate feedback on code quality without human intervention.

### Visual Feedback: Screenshots and Renders

**Use case:**
Verify UI changes or visual output.

**Implementation:**
Capture screenshots of rendered output or generated visuals.

**Application:**
- Web UI changes
- Document rendering
- Design output
- Visual layouts

**Pattern:**

```
Agent generates HTML
    ↓
System renders to screenshot
    ↓
Agent sees visual result
    ↓
Can iterate if not matching requirements
```

### LLM-as-Judge: Secondary Model Evaluation

**Use case:**
Complex evaluation requiring semantic understanding.

**Pattern:**

```
Agent generates output
    ↓
Evaluation prompt: "Does this output meet requirements?"
    ↓
Secondary model evaluates
    ↓
Provides feedback or approval
    ↓
Agent receives evaluation and iterates if needed
```

**Examples:**

**Customer support response:**
```
Agent generates response to customer complaint
LLM-as-Judge evaluates: "Is this empathetic and solution-focused?"
If not, agent revises
```

**Code review:**
```
Agent generates code
LLM-as-Judge evaluates: "Is this code clean, readable, and efficient?"
Provides specific feedback for improvement
```

**Content generation:**
```
Agent writes article
LLM-as-Judge evaluates: "Does this match brand voice and address user needs?"
Returns suggestions for revision
```

## Use Case Patterns

### Finance Agent: Portfolio Analysis

**Flow:**

```
1. GATHER
   - Access portfolio data (CSV, API)
   - Fetch current market prices
   - Retrieve economic indicators

2. ACT
   - Analyze portfolio allocation
   - Calculate performance metrics
   - Identify rebalancing opportunities
   - Generate recommendations

3. VERIFY
   - Check calculation accuracy (rule-based)
   - LLM-as-judge: "Are recommendations sound?"
   - Ensure compliance with constraints

4. REPORT
   - Generate visualization
   - Create recommendation summary
```

### Personal Assistant Agent: Calendar and Travel

**Flow:**

```
1. GATHER
   - Check calendar availability
   - Search flight prices
   - Get hotel options
   - Retrieve user preferences

2. ACT
   - Find optimal travel dates
   - Book flights
   - Reserve hotel
   - Update calendar

3. VERIFY
   - Confirm bookings (check emails)
   - Verify calendar updates
   - LLM-as-judge: "Are reservations aligned with preferences?"

4. NOTIFY
   - Send confirmation summary
```

### Customer Support Agent: Ticket Resolution

**Flow:**

```
1. GATHER
   - Read customer ticket
   - Search knowledge base
   - Retrieve customer history
   - Check system status

2. ACT
   - Diagnose issue
   - Generate solution
   - Create support response
   - Escalate if needed

3. VERIFY
   - Rule-based: Check response quality
   - LLM-as-judge: "Is solution complete and helpful?"
   - Human review if uncertain

4. DELIVER
   - Send response to customer
```

### Research Agent: Document Synthesis

**Flow:**

```
1. GATHER (using subagents)
   - SubagentA → reads paper 1 → summary
   - SubagentB → reads paper 2 → summary
   - SubagentC → reads paper 3 → summary

2. ACT
   - Synthesize summaries
   - Identify common themes
   - Note contradictions
   - Extract key insights

3. VERIFY
   - LLM-as-judge: "Is synthesis accurate and well-reasoned?"
   - Check citations are correct

4. REPORT
   - Generate comprehensive synthesis document
```

## Implementation Recommendations

### Start with Agentic Search

**Why:**
- Transparent and verifiable
- Developers understand bash commands
- Results are predictable
- Easier to debug

**Progression:**
```
Phase 1: Bash/agentic search for file system navigation
    ↓
Phase 2: Add semantic search where agentic search insufficient
    ↓
Phase 3: Optimize search strategy based on task type
```

### Use Subagents for Information-Heavy Tasks

**Indicator:**
Multiple sources of information needed for context.

**Solution:**
Spawn subagents for parallel information gathering.

**Example:**
```
If task needs information from:
- Document 1
- Document 2
- API endpoint
- Database
→ Use subagents instead of loading everything into context
```

### Build Representative Test Sets

**Critical for success:**
Comprehensive testing of agent behavior.

**Components:**
- Typical use cases
- Edge cases
- Error scenarios
- Performance requirements

**Evaluation:**
- Accuracy metrics
- Latency measurements
- Cost tracking
- User satisfaction

### Verification Strategy Selection

**Agentic search results:**
→ Rule-based verification (lint, validate format)

**Generated code:**
→ Rule-based (lint, type check) + visual (screenshots)

**Complex decisions:**
→ LLM-as-judge evaluation

**Human-critical operations:**
→ Human review + approval

## Key Principles

### 1. Transparency Over Magic

**Principle:**
Use bash and explicit tools over hidden "AI magic."

**Benefit:**
Humans can understand and verify what agent does.

### 2. Real Tools Over AI-Specific Ones

**Principle:**
Give agents tools developers use, not special "agent-friendly" interfaces.

**Benefit:**
Agents are useful for real tasks immediately.

### 3. Modular Task Decomposition

**Principle:**
Break complex tasks into discrete gather-act-verify cycles.

**Benefit:**
Each cycle is verifiable; overall progress is trackable.

### 4. Graduated Verification Complexity

**Principle:**
Match verification method to task complexity.

**Simple output:** Rule-based validation
**Complex output:** LLM-as-judge
**High-stakes:** Human review

### 5. Parallel Information Gathering

**Principle:**
Use subagents for parallel context collection.

**Benefit:**
Faster, cleaner, more scalable than serial loading.

## Architectural Patterns

### The Gather-Act-Verify Loop

```
GATHER CONTEXT
    ↓
    Agentic search (bash)
    Semantic search (if needed)
    Tool calls for data
    Subagents for parallelization
    ↓
TAKE ACTION
    ↓
    Custom tools
    Bash scripts
    Code generation
    MCP integrations
    ↓
VERIFY WORK
    ↓
    Rule-based validation
    Visual verification
    LLM-as-judge evaluation
    Human review (if needed)
    ↓
NEXT ITERATION
```

### Context Management in Long-Running Agents

```
Normal operation
    ↓
Context accumulates
    ↓
Approaches 80% full
    ↓
Automatic compaction:
  - Summarize progress
  - Extract key facts
  - Discard intermediate steps
    ↓
Reset context with summary
    ↓
Continue operation
```

## Key Takeaways

1. **Claude Agent SDK provides structured framework** — Gather-Act-Verify loop for reliable agents
2. **Philosophy: Real tools, not AI-specific ones** — Bash, code, APIs that developers know
3. **Agentic search precedes semantic search** — Start transparent, add semantic when needed
4. **Subagents enable parallel context gathering** — Better for information-heavy tasks
5. **Context compaction handles long operations** — Automatic summarization prevents overflow
6. **Custom tools are fundamental building blocks** — Clear contracts, single responsibility
7. **Bash flexibility enables complex operations** — Unlimited capability within sandbox
8. **Code generation for maintainable solutions** — Better than bash for complex logic
9. **MCP integration connects external services** — Slack, GitHub, Asana, etc. without custom code
10. **Rule-based verification catches obvious issues** — Linting, validation, format checking
11. **Visual verification confirms UI changes** — Screenshots and renders for visual output
12. **LLM-as-judge evaluates complex output** — Secondary model provides semantic evaluation
13. **Human review for high-stakes operations** — Critical decisions require human approval
14. **Verification strategy matches task complexity** — Right tool for right verification need
15. **Test sets drive quality** — Representative tests across typical, edge, and error cases
16. **Transparency enables debugging** — Visible actions easier to understand and fix
17. **Modular decomposition improves reliability** — Each gather-act-verify cycle is independent
18. **Parallel execution improves speed** — Subagents handle multiple information sources
19. **Clean context improves reasoning** — Compaction and subagents keep reasoning space clear
20. **Graduated complexity supports different needs** — Simple tasks use simple verification; complex tasks use complex verification

## Implementation Checklist

**Before deploying agent:**

- [ ] Define clear agent mission and success criteria
- [ ] Implement gather phase with agentic search
- [ ] Build necessary custom tools
- [ ] Set up action execution (bash, code, MCP)
- [ ] Implement rule-based verification
- [ ] Add visual verification (if relevant)
- [ ] Implement LLM-as-judge evaluation (if needed)
- [ ] Create representative test cases
- [ ] Test edge cases and error scenarios
- [ ] Set up context compaction for long tasks
- [ ] Design subagent architecture (if relevant)
- [ ] Document tool contracts clearly
- [ ] Set up monitoring and logging
- [ ] Plan human review workflow (if high-stakes)
- [ ] Iterate based on test results

## The Bottom Line

The Claude Agent SDK embodies a practical philosophy: give Claude the same tools that make developers productive, then structure agent work around a simple but powerful loop—gather context, take action, verify work, repeat.

Key distinctions from other agent frameworks:

1. **Transparency over abstraction** — Use bash and explicit tools, not hidden AI magic
2. **Real tools over simplified ones** — Developers recognize and understand actions
3. **Structured verification** — Not just "does it look right?" but systematic checks
4. **Scalable context management** — Subagents and compaction handle complexity
5. **Multiple verification strategies** — Right tool for right situation

**For teams building agents:**

Start with simple gather-act-verify cycles on well-defined tasks. Verify work systematically—rule-based first, LLM-judge for complexity, human review for critical decisions. As tasks become more complex, add subagents for parallel context gathering and automatic compaction for long operations.

The SDK provides the framework; the discipline comes from implementing solid patterns for context gathering, clear tool design, and appropriate verification.

The result: agents that are capable, understandable, and reliable—not black-box solutions, but systems where humans can see what agents do and why.

