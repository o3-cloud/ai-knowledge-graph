---
summary: Arize introduces Dev-Agent-Lens—an open-source observability proxy layer that adds comprehensive tracing to Claude Code deployments, enabling visibility into tool reliability, latency, token consumption, costs, and failure patterns through OpenTelemetry and OpenInference standards
event_type: blog_post
sources:
    - https://arize.com/blog/claude-code-observability-and-tracing-introducing-dev-agent-lens/
    - https://github.com/Teraflop-Inc/dev-agent-lens
tags:
    - observability
    - Claude-Code
    - tracing
    - DevOps
    - monitoring
    - OpenTelemetry
    - OpenInference
    - tool-observability
    - cost-management
    - production-AI
---

# Dev-Agent-Lens: Claude Code Observability and Tracing

**Authors:** Adam Mischke (Founder, AM2), Alex Owen (Founder, Stealth Startup), Jason Lopatecki (Co-founder and CEO, Arize AI)

**Platform:** Arize Blog
**Publication Date:** August 22, 2025
**Type:** Technical Infrastructure and Tools
**Repository:** https://github.com/Teraflop-Inc/dev-agent-lens
**Key Concept:** Open-source observability for AI agent deployments

## Overview

Arize introduces Dev-Agent-Lens, an open-source proxy layer that solves a critical infrastructure gap: comprehensive observability for Claude Code deployments. While Claude Code excels at code generation and analysis, production workflows require visibility into what's actually happening: which tools are being invoked, why they fail, where latency accumulates, and what costs are being incurred.

Dev-Agent-Lens routes Claude Code requests through LiteLLM, which emits OpenTelemetry and OpenInference spans that integrate with observability platforms (Arize AX cloud or Phoenix open-source), enabling teams to debug, optimize, and monitor production AI agent workflows.

## The Critical Gap

### What Production Needs But Conventional Monitoring Provides

**Production AI agent deployments require visibility into:**

```
Tool invocations and reliability rates
├── Which tools are called?
├── How often do they fail?
├── What's the success rate?
└── What's causing failures?

Latency breakdown
├── Model response time (pure)
├── Tool execution time
├── End-to-end latency
└── Where are bottlenecks?

Token and cost metrics
├── Tokens consumed per prompt
├── Tokens consumed per completion
├── Where do tokens accumulate?
└── What's driving costs?

Failure patterns
├── Why did this tool call fail?
├── What's the error pattern?
├── How frequent are failures?
└── How do we prevent them?
```

### Why Conventional Logging Falls Short

**Problem:**
Standard logging and monitoring tools don't capture:

```
Streaming responses
├── Hard to log streaming data
├── Incomplete visibility
└── Missing intermediate states

Nested tool invocations
├── Tool calls other tools
├── Relationships not visible
└── Dependencies hidden

Internal calls
├── Model internal prompts
├── Tool construction logic
├── Token accumulation points
└── Not captured in standard logs
```

**Result:**
Production blind spots even with logging in place.

## The Solution: Dev-Agent-Lens Architecture

### High-Level Design

**Request flow:**

```
Claude Code Client
    ↓
Dev-Agent-Lens Proxy
    ├── Request routing
    ├── Authentication
    ├── Rate limiting
    └── Cost tracking
    ↓
LiteLLM
    ├── Emits OpenTelemetry spans
    ├── Captures trace data
    └── Forwards to observability layer
    ↓
Observability Platform
    ├── Arize AX (cloud)
    └── Phoenix (open-source)
    ↓
Visualization & Analysis
    ├── Dashboards
    ├── Trace inspection
    ├── Cost analysis
    └── Alerting
```

### Core Components

**1. Proxy Control (LiteLLM)**

**Responsibilities:**
- Centralized routing of requests
- Authentication management
- Rate limiting enforcement
- Cost tracking and aggregation

**Benefits:**
- Single point of control
- Consistent telemetry collection
- Easy policy enforcement
- Transparent cost visibility

**2. Observability Standard (OpenTelemetry + OpenInference)**

**Why these standards:**
- OpenTelemetry: industry standard for tracing
- OpenInference: AI-specific tracing format
- Not proprietary
- Works with multiple backends
- Widely supported

**What they capture:**
- Detailed span information
- Timing and latency
- Token counts
- Success/failure status
- Tool invocations and results
- Nested relationships

**3. Storage and Backend**

**Options:**
- **Arize AX:** Cloud-hosted observability
- **Phoenix:** Open-source, self-hosted

**Benefits of both:**
- Complete trace visibility
- Historical analysis
- Cost trending
- Alerting capabilities

**4. Evaluation Framework**

**Trace-level evaluations:**
- Did tool call succeed?
- Was response accurate?
- Did model reason correctly?

**Session-level evaluations:**
- Did workflow complete?
- Was outcome correct?
- Did it meet SLAs?

**5. Production Monitors**

**Alert on:**
- Span properties (latency, error rates)
- Evaluation metrics (correctness, success rate)
- Cost thresholds
- Tool reliability

## Span Types Generated

### Five Distinct Span Categories

**1. LLM/raw_gen_ai_request**

**Purpose:**
Captures initial model request.

**Includes:**
- Input prompt
- Model parameters
- Request metadata

**Use:**
Understanding initial request structure.

**2. LLM/Claude_Code_Internal_Prompt**

**Purpose:**
Tracks prompt construction and token metrics.

**Includes:**
- Constructed prompt
- Token count breakdown
- Prompt assembly details

**Use:**
Identifying where prompts grow, token bloat.

**3. TOOL/Claude_Code_Internal_Tool**

**Purpose:**
Records internal tool operations.

**Includes:**
- Tool execution details
- Operation timing
- Internal state changes

**Use:**
Debugging tool behavior.

**4. TOOL/Claude_Code_Tool**

**Purpose:**
Tracks external tool calls.

**Includes:**
- Tool name and parameters
- Execution duration
- Success/failure status
- Error details

**Use:**
Understanding tool reliability and failures.

**5. LLM/Claude_Code_Final_Output**

**Purpose:**
Captures assembled final response.

**Includes:**
- Final output
- Output assembly details
- Completion metadata

**Use:**
Validating final results.

### Why This Span Hierarchy Matters

**Complete visibility:**
```
Every step of execution captured
    ↓
From initial prompt to final output
    ↓
Including all tool calls and their results
    ↓
Token consumption visible at each point
```

**Debugging power:**
Can trace exactly where:
- Latency accumulates
- Tokens are consumed
- Failures occur
- Unexpected behavior happens

## Cost Management Use Case

### The Cost Challenge

**Problem:**
Unexpected cost escalation in production.

**Symptoms:**
```
Token usage spikes
    ↓
No visibility into why
    ↓
Can't identify which operations caused it
    ↓
No way to prevent recurrence
```

### How Dev-Agent-Lens Helps

**Visibility:**

```
Token usage per prompt
├── See exactly what prompted sent
├── Identify bloated prompts
└── Spot accumulating context

Token usage per completion
├── See what model generated
├── Identify verbose outputs
└── Spot runaway tool responses

Token usage per tool call
├── See what each tool costs
├── Identify expensive tools
└── Spot inefficient tool usage
```

**Actionable insights:**

```
Sudden spikes signal:
├── Bloated prompts
├── Runaway tool outputs
├── Inefficient tool chains
└── Context accumulation
```

### Recommended Cost Controls

**1. Trim Prompts**
- Remove unnecessary context
- Deduplicate information
- Use structured inputs (not prose)

**2. Deduplicate Retrieved Text**
- Don't send same information twice
- Combine similar results
- Compress retrieved context

**3. Cap Tool Payloads**
- Limit tool response sizes
- Implement response trimming
- Truncate large outputs

**4. Set Token Limits**
- Max tokens per request
- Max tokens per completion
- Max tokens per session

**5. Implement Project Budgets**
- Monthly spend caps
- Per-agent limits
- Alert thresholds

## Real-World Examples

### Example 1: Security Analysis Agent

**Purpose:**
Detect vulnerable code.

**SLA:**
3-second latency requirement.

**What visibility provides:**
- Latency breakdown (model vs. tool time)
- Which tools are invoked
- Success/failure rates
- Token consumption
- Cost per analysis

**Monitoring:**
Alerts if latency exceeds SLA.

### Example 2: Incident Response Agent

**Purpose:**
Chain database lookups, reasoning, notifications.

**Workflow:**
```
Detect incident
    ↓
Query database for context
    ↓
Analyze with Claude Code
    ↓
Determine response
    ↓
Post to Slack
```

**Visibility:**
See latency at each step.

**Optimization:**
Identify where to parallelize, cache, or optimize.

### Example 3: Code Review PR Bot

**Purpose:**
Automated PR analysis and feedback.

**Implementation:**
TypeScript SDK with telemetry.

**Visibility:**
Complete trace of review process.

**Quality:**
Measure review accuracy and usefulness.

## Getting Started

### Setup Process

**Step 1: Clone and Configure**

```bash
git clone https://github.com/Teraflop-Inc/dev-agent-lens
cd dev-agent-lens
```

**Environment variables:**
- ANTHROPIC_API_KEY (Claude API access)
- ARIZE_API_KEY (cloud observability)
- ARIZE_SPACE_KEY (workspace identifier)

**Step 2: Launch Infrastructure**

```bash
docker-compose up
```

**What starts:**
- Dev-Agent-Lens proxy
- LiteLLM server
- Observability infrastructure
- Local storage

**Step 3: Execute Examples**

```bash
# Run security analysis agent
python examples/security_agent.py

# Run incident response agent
python examples/incident_agent.py

# Run PR review bot
npm run bot:pr-review
```

**Step 4: Visualize**

Access Arize dashboard to see:
- Live traces
- Latency analysis
- Token consumption
- Tool reliability
- Cost metrics

## Architecture Benefits

### 1. Standards-Based

**Uses:**
- OpenTelemetry (industry standard)
- OpenInference (AI standard)
- LiteLLM (standard proxy)

**Benefits:**
- Not proprietary
- Works with multiple backends
- Future-proof
- Community support

### 2. Transparent

**What you get:**
- Full trace visibility
- No black boxes
- Complete data ownership
- Can export anywhere

### 3. Flexible

**Options:**
- Cloud (Arize AX) or self-hosted (Phoenix)
- Open-source core
- Customizable spans
- Extensible architecture

### 4. Production-Ready

**Includes:**
- Rate limiting
- Authentication
- Cost tracking
- Alerting
- SLA monitoring

## Comparison with Alternatives

### vs. Basic Logging

| Aspect | Logging | Dev-Agent-Lens |
|--------|---------|-----------------|
| **Streaming capture** | No | Yes |
| **Nested calls** | No | Yes |
| **Token tracking** | Manual | Automatic |
| **Tool visibility** | Limited | Complete |
| **Cost analysis** | No | Yes |
| **Alerting** | Manual | Automated |

### vs. Ad Hoc Instrumentation

| Aspect | Custom | Dev-Agent-Lens |
|--------|--------|-----------------|
| **Implementation time** | Weeks | Hours |
| **Maintenance** | High | Low |
| **Standards** | Custom | Industry standard |
| **Integration** | Manual | Automatic |
| **Tools included** | None | Multiple |

### vs. General Observability

| Aspect | Generic | Dev-Agent-Lens |
|--------|---------|-----------------|
| **AI-specific spans** | No | Yes |
| **Token tracking** | No | Yes |
| **Tool observability** | No | Yes |
| **Cost analysis** | No | Yes |
| **Examples** | No | Yes |

## Key Takeaways

1. **Production AI agents need observability** — Can't operate blind
2. **Conventional logging falls short** — Doesn't capture agent-specific data
3. **Dev-Agent-Lens solves this gap** — Open-source proxy layer
4. **Five span types provide complete visibility** — From prompt to output
5. **Tool reliability is measurable** — See which tools fail and why
6. **Latency is decomposable** — Model time vs. tool time vs. overhead
7. **Token consumption is trackable** — Spot bloat and accumulation
8. **Costs are controllable** — Visibility enables cost management
9. **Failure patterns are identifiable** — Debug and prevent issues
10. **Standards-based approach** — OpenTelemetry + OpenInference
11. **Works with multiple backends** — Arize AX or Phoenix
12. **Evaluation framework included** — Trace and session level
13. **Production monitors built-in** — Alert on metrics
14. **Examples provided** — Security, incident, code review agents
15. **Three-second setup** — Docker Compose for quick start
16. **Transparent and extensible** — Full data ownership
17. **Cost controls recommended** — Trim, deduplicate, cap, limit, budget
18. **SLA monitoring possible** — Alert when latency exceeds thresholds
19. **Tool-specific insights** — See success rates, failures, latency
20. **Future-proof architecture** — Built on industry standards

## The Bottom Line

Arize's Dev-Agent-Lens addresses a critical infrastructure gap: the lack of comprehensive observability for production Claude Code deployments.

**The core problem:**
While Claude Code excels at reasoning and code generation, production workflows need visibility into what's actually happening: tool reliability, latency breakdown, token consumption, cost drivers, and failure patterns.

**The solution:**
A standards-based observability proxy (OpenTelemetry + OpenInference) that captures five distinct span types across the entire Claude Code execution, from initial prompt through final output.

**Key capabilities:**
- **Complete visibility:** Every step from prompt to output
- **Tool observability:** Which tools run, succeed, fail, and why
- **Latency decomposition:** Model time vs. tool time
- **Token tracking:** Per-prompt and per-completion consumption
- **Cost management:** Identify and control token bloat
- **Failure analysis:** Debug and prevent errors
- **Production monitoring:** SLA enforcement and alerting

**For practitioners:**
If you're running Claude Code in production, observability isn't optional. Dev-Agent-Lens provides a complete, standards-based solution in hours instead of weeks of custom instrumentation.

**Strategic value:**
As AI agents become critical infrastructure, observability becomes critical infrastructure. Dev-Agent-Lens positions teams to:
- Understand agent behavior in production
- Control costs and token consumption
- Monitor SLAs and reliability
- Debug issues quickly
- Optimize agent workflows

**The approach:**
Standards-based (OpenTelemetry/OpenInference), open-source core, flexible backends (cloud or self-hosted), production-ready with rate limiting, authentication, cost tracking, and alerting.

Dev-Agent-Lens makes it possible to run Claude Code with confidence in production: visible, measurable, controllable, debuggable.

