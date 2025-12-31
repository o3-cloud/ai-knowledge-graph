---
summary: Proposes 12-Factor Agents—engineering principles for building reliable, production-grade LLM-powered software that prioritizes deterministic code with strategic LLM integration over monolithic agent frameworks
event_type: video
sources:
    - https://www.youtube.com/watch?v=8kMaTybvDUw
tags:
    - agent-patterns
    - LLM-reliability
    - production-agents
    - engineering-principles
    - software-architecture
    - HumanLayer
    - agent-frameworks
---

# 12-Factor Agents: Patterns of Reliable LLM Applications

**Speaker:** Dex Horthy (HumanLayer)
**Platform:** AI Engineer
**Upload Date:** July 3, 2025

## Core Insight

Most "AI Agent" products aren't actually agentic. Rather, they're **mostly deterministic code with LLM steps strategically sprinkled in at critical points** to create magical user experiences. Good agents don't follow the "here's your prompt, here's a bag of tools, loop until you hit the goal" pattern—they're primarily software engineering.

## The Problem with Agent Frameworks

After trying every major framework (CrewAI, LangChain, smolagents, LangGraph, Griptape), Dex found a critical gap:

- Most frameworks assume you want a general-purpose "loop forever" agent
- Limited consideration for real production requirements
- Frameworks don't address deployment, monitoring, human oversight
- Few deployed customer-facing agents actually use these off-the-shelf solutions
- Strong founders building impressive things typically **roll their own stack**

The real question: **What are the principles for building LLM-powered software good enough for production customers?**

## 12-Factor Agents Framework

Inspired by 12-factor methodology for cloud applications, these principles apply to LLM systems regardless of model capability advances.

### Factor 1: Natural Language to Tool Calls

Map natural language understanding into **structured tool invocations**, not free-form reasoning. This introduces determinism where it matters:

- Parse user intent into specific, bounded actions
- Explicit tool selection rather than open-ended reasoning
- Clear contract between natural language input and tool execution
- Easier to test, debug, and audit than free-form prompting

### Factor 2: Own Your Prompts

**Never rely on framework defaults or library prompts.** Your prompts encode domain knowledge and operational requirements:

- Version control prompts like code
- Iterate based on real production feedback
- Tailor to your specific domain and context
- Framework generic prompts won't capture your requirements
- Own the prompt—it's core business logic

### Factor 3: Own Your Context Window

Treat token budget as scarce resource requiring deliberate management:

- Don't let framework automatically stuff "everything" into context
- Implement strategic context selection—what's actually relevant?
- Balance completeness with efficiency
- Monitor context usage patterns
- Optimize for cost and latency, not comprehensiveness

### Factor 4: Tools Are Just Structured Outputs

Reconceptualize tools as **structured output specifications**, not separate "tool-calling" subsystem:

- Tools define what the model should output (and when)
- Schema drives model behavior toward valid, executable outputs
- Separates intent (what model should do) from execution (what framework does)
- Enables cleaner separation between LLM reasoning and software execution

### Factor 5: Unify Execution State and Business State

Single source of truth for system state:

- Don't maintain separate "agent state," "business state," "execution context"
- Unified state model that encompasses everything system tracks
- Prevents divergence between what model thinks state is vs. actual state
- Simplifies debugging—single state to inspect and reason about
- Critical for multi-turn interactions and resumption

### Factor 6: Launch/Pause/Resume with Simple APIs

Agents should support **stateless execution patterns**:

- Launch: Start agent with given input
- Pause: Suspend when awaiting external input (human, API result, etc.)
- Resume: Continue from paused state with new information
- Simple APIs hide complexity while maintaining full visibility
- Enables human-in-the-loop workflows naturally

### Factor 7: Contact Humans with Tool Calls

Use the same tool-calling mechanism for **human interaction** as for external services:

- Human review/approval is a "tool" invocation
- Same structured approach as calling APIs
- Natural integration of human oversight
- Makes human-in-the-loop a first-class pattern
- Auditable—all human interactions logged like tool calls

### Factor 8: Own Your Control Flow

Explicit, verifiable control flow rather than framework-driven loops:

- Your code controls what happens next, not framework defaults
- Clear decision points—when to call model, when to call tool, when to ask human
- Testable control flow
- Easier to reason about and debug
- Supports custom orchestration specific to your domain

### Factor 9: Compact Errors into Context Window

**Errors are informative context**, not exceptions to suppress:

- When failures occur, extract learning and include in context
- Structured error representation that fits in token budget
- Models learn what went wrong and can adapt approach
- Don't lose valuable signal by treating errors as stops
- Enables sophisticated error recovery strategies

### Factor 10: Small, Focused Agents

Keep individual agents **narrow in scope and responsibility**:

- Single, clear purpose rather than monolithic "do everything" agent
- Easier to test, deploy, and reason about
- Failures isolated to narrow scope
- Composable—multiple agents coordinate on complex problems
- Aligns with software architecture best practices

### Factor 11: Trigger from Anywhere, Meet Users Where They Are

Agents should be **location-agnostic and triggerable from any context**:

- Call agents from web apps, APIs, scheduled jobs, webhooks
- Don't require special framework scaffolding to invoke
- Standard function/method interface
- Flexible integration into existing systems
- Users interact through familiar channels (chat, dashboards, etc.)

### Factor 12: Make Your Agent a Stateless Reducer

Embrace **functional programming patterns** for agent logic:

- Agent = pure function taking state + input → state + output
- No hidden state or side effects within agent
- Composition and testing straightforward
- Aligns with cloud-native patterns (Lambda, serverless)
- Enables horizontal scaling, parallelization, recovery

## Architectural Philosophy

These factors encode principles for **software-first agent design**:

1. **Determinism matters** where it matters
2. **Control flow is explicit** not implicit
3. **State is unified** not scattered
4. **Humans are first-class** not afterthoughts
5. **Agents are small** not monolithic
6. **Integration is simple** not complex

## Key Distinctions

### Not This:
```
Prompt + Tools → Loop Forever → Magic
```

### But This:
```
Deterministic Code + Strategic LLM Calls + Human Oversight = Production Agent
```

## Why This Matters

Even if LLMs become exponentially more powerful:
- These principles remain valuable
- Core engineering discipline doesn't change
- Reliability comes from architecture, not just model capability
- Maintainability improves with explicit patterns
- Production deployment requires these considerations

## Implementation

Dex emphasizes: **Don't use frameworks that force you to violate these principles.** The 12-factor approach often means minimal scaffolding and rolling custom orchestration.

Resources:
- **Twitter:** https://x.com/dexhorthy/
- **GitHub:** https://github.com/humanlayer/12-factor-agents
- **Discussion:** https://news.ycombinator.com/item?id=43699271

## Implications for Teams

For organizations building agent systems:
- Prioritize software engineering discipline over framework conveniences
- Own your prompts, context, and control flow
- Make agents small and focused
- Embed human oversight through tool calls
- Treat agent logic as pure functions where possible
- Plan for launch/pause/resume workflows from the start
- Don't assume off-the-shelf frameworks fit production requirements

## The Real Insight

**LLM integration is just software engineering** applied to a new tool. The principles that made software reliable for decades still apply—they just need to be consciously applied to LLM-powered systems.
