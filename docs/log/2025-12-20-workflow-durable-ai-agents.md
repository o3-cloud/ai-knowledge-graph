---
summary: Documentation guide for Workflow DevKit on converting basic AI chat applications into production-ready durable agents with statefulness, observability, resumability, and human-in-the-loop capabilities
event_type: deep dive
sources:
    - https://useworkflow.dev/docs/ai
tags:
    - AI-agents
    - production-agents
    - workflow-orchestration
    - durable-execution
    - observability
    - state-management
    - agent-architecture
---

# Building Durable AI Agents with Workflow DevKit

**Platform:** Workflow DevKit (useworkflow.dev)
**Documentation Type:** Developer Guide
**Focus:** Production-ready AI agent implementation

## Core Problem

Standard LLM-based agents built on "the primitive of LLM and tool-call loops" lack essential production capabilities:
- No persistent state across sessions
- Limited visibility into execution
- Session data lost on service interruptions
- No structured approval workflows
- Difficult to scale and monitor

Converting basic AI chat into production-ready agents requires solving four critical challenges.

## Four Critical Challenges

### 1. Statefulness

**Problem:** Chat sessions aren't inherently durable. LLM operations and tool invocations must survive service restarts, network interruptions, and multi-turn conversations.

**Solution:**
- Convert LLM operations into asynchronous, queue-based jobs
- Maintain persistent state separate from ephemeral connections
- Enable agents to resume from exact point of interruption
- Session state survives client reconnections and service deployments

### 2. Observability

**Problem:** Standard message history insufficient for production visibility. Need to track:
- Which tools executed and why
- Execution failures and retries
- LLM reasoning steps
- Performance metrics and latency
- Debugging information for failures

**Solution:**
- Collect structured traces separate from message history
- Comprehensive dashboard showing execution flows
- Trace inspection for troubleshooting
- Performance monitoring and metrics
- Audit trails for compliance

### 3. Resumability

**Problem:** Stream data lost when connections break. Clients reconnecting must receive full history without re-executing agent logic.

**Solution:**
- Persistent streaming via `getWritable()` interface
- Clients reconnect and resume data stream from last known point
- No data loss across service boundaries
- Support for long-running operations without client connection requirement
- Stream checkpointing for recovery

### 4. Human-in-the-Loop

**Problem:** Approval workflows require coordination across clients, APIs, and orchestration. Agents can't autonomously approve critical operations.

**Solution:**
- Structured approval workflow integration
- Pause agent execution pending human decision
- Resume execution after human verification
- Support for conditional approval chains
- Audit trail of human decisions

## Implementation Architecture

### Core Components

**DurableAgent Class**
Replaces standard Agent implementation, ensuring all LLM calls execute as trackable steps with:
- Automatic persistence
- Retry handling (default 3 attempts)
- Structured logging
- Observable execution traces

**Workflow Function**
Marked with `"use workflow"` directive to enable:
- Workflow orchestration and management
- Automatic state persistence
- Integration with workflow infrastructure
- Durable execution semantics

**Step Functions**
Tool implementations marked with `"use step"` directive providing:
- Automatic retry on transient failures
- Structured execution monitoring
- Performance tracking
- Error handling and recovery

### Integration Pattern

Four-step process to convert standard agent to durable agent:

**Step 1: Install Packages**
```
npm install workflow @workflow/ai
```

Install Workflow DevKit packages providing durable execution and AI integration.

**Step 2: Extract Agent Logic**
Wrap agent logic in workflow function with `"use workflow"` directive:
- Central place for agent orchestration
- Persistence automatically handled
- State accessible across invocations

**Step 3: Replace API Route Logic**
Replace direct API calls with `start()` function:
- Initiates durable workflow execution
- Returns execution context/reference
- Enables client reconnection and monitoring

**Step 4: Annotate Tool Functions**
Mark tool implementations with `"use step"`:
- Each tool execution becomes observable step
- Automatic retries on failure
- Structured logging of tool invocations

## Key Features

### Persistent Streaming
Clients maintain connection to durable agent:
- Stream data flows to client in real-time
- Disconnection doesn't lose data
- Reconnection resumes from last checkpoint
- No re-execution of completed work

### Automatic Retry Handling
Tool execution failures automatically retried:
- Default: up to 3 attempts
- Configurable per tool or globally
- Transient failures don't break workflow
- Permanent failures captured and traced

### Observability Dashboard
Access execution visibility through `npx workflow web`:
- Visual representation of execution flow
- Step-by-step trace inspection
- Performance metrics and latency
- Error details and retry history
- Search and filter capabilities

### Worker Process Architecture
In production:
- Tool execution in separate worker processes
- Automatic scaling with workload
- Resource isolation
- Failure containment
- Performance optimization

## Architectural Benefits

### Reliability
- Persistent state survives failures
- Automatic retries for transient errors
- No state loss on service interruption
- Graceful degradation on partial failures

### Scalability
- Tool execution decoupled from agent logic
- Worker processes scale independently
- Load distribution across infrastructure
- Resource pooling and optimization

### Observability
- Comprehensive execution traces
- Real-time monitoring and alerting
- Historical audit trails
- Performance analytics and insights

### Maintainability
- Explicit workflow definitions
- Clear step boundaries
- Structured error handling
- Standard logging and tracing

### Developer Experience
- Simple integration with existing agents
- Minimal code changes required
- Familiar async/await patterns
- Integrated development tools

## Production Considerations

### State Management
- Persistence layer handles durability
- State survives service deployments
- Consistent state across retries
- Proper cleanup of completed workflows

### Failure Handling
- Transient failures auto-retried
- Permanent failures surface to workflow
- Human intervention capabilities
- Circuit breakers and fallbacks

### Scaling
- Horizontal scaling of worker processes
- Load balancing across instances
- Resource constraints respected
- Backpressure handling

### Monitoring
- Structured tracing and logging
- Real-time alerts on failures
- Historical performance analysis
- SLA tracking and reporting

## Common Use Cases

### Approval Workflows
Agent performs analysis, pauses for human approval, resumes execution:
- Financial decisions requiring sign-off
- Content moderation workflows
- Access control decisions
- Compliance checkpoints

### Long-Running Tasks
Multi-hour or multi-day operations:
- Data processing pipelines
- Research and analysis agents
- Report generation
- Batch processing workflows

### Streaming Operations
Real-time data processing with client visibility:
- Live analysis and updates
- Progressive result display
- User-visible progress tracking
- Cancellation and pausing

### Multi-Step Reasoning
Complex workflows with multiple decision points:
- Planning and decomposition
- Tool orchestration
- Error recovery
- Fallback strategies

## Comparison to Naive Agent Implementation

### Naive Approach
```
LLM + Tools + Chat Session Loop
```

Problems:
- State lost on restart
- No visibility into execution
- Tool failures break entire flow
- No human approval mechanism
- Difficult to debug and monitor

### Durable Agent Approach
```
Workflow(LLM + DurableAgent + Tools)
```

Advantages:
- Persistent state across failures
- Full execution visibility and tracing
- Automatic retry and error recovery
- Built-in human-in-the-loop
- Production monitoring and debugging

## Key Takeaways

1. **State matters:** Durable execution requires explicit state management
2. **Observability essential:** Production agents must be fully observable
3. **Resilience required:** Automatic retry and recovery mechanisms critical
4. **Human oversight:** Approval workflows needed for high-stakes operations
5. **Architecture matters:** Proper separation enables scaling and reliability

## Integration Philosophy

Rather than requiring complete rewrite:
- Minimal changes to existing agent code
- Incremental adoption possible
- Works with existing LLM libraries
- Compatible with standard frameworks
- Backward compatible patterns

## Getting Started

1. Install Workflow DevKit packages
2. Wrap agent logic in workflow function
3. Annotate tool functions with `"use step"`
4. Deploy and access dashboard via `npx workflow web`
5. Monitor executions and refine as needed

The progression from prototype to production agent becomes systematic and repeatable, enabling reliable AI systems suitable for customer-facing applications.
