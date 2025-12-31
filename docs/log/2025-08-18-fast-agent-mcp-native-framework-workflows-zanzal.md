---
summary: Owen Zanzal introduces Fast Agent—an MCP-native Python framework for rapid, interoperable agent orchestration that leverages Model Context Protocol as universal interface, enabling portable workflows and rapid prototyping without vendor lock-in
event_type: blog_post
sources:
    - https://medium.com/devops-ai/fast-agent-the-mcp-native-framework-for-smarter-ai-workflows-5d7224278a7d
    - https://fast-agent.ai
tags:
    - Fast-Agent
    - MCP
    - agent-orchestration
    - Python-framework
    - workflow-patterns
    - multi-agent-systems
    - interoperability
    - rapid-prototyping
    - agent-composition
    - MCP-servers
---

# Fast Agent: The MCP-Native Framework for Smarter AI Workflows

**Author:** Owen Zanzal
**Platform:** Medium (DevOps+AI)
**Publication Date:** August 18, 2025
**Type:** Framework Guide and Tutorial
**Website:** https://fast-agent.ai
**Key Concept:** MCP-first agent orchestration framework

## Overview

Owen Zanzal introduces Fast Agent, an open-source Python framework built from the ground up for MCP (Model Context Protocol) compliance. Rather than building proprietary tool integrations and adapters, Fast Agent leverages MCP as the universal interface, making workflows portable, interoperable, and future-proof.

The framework enables rapid prototyping through a decorator-based API, includes prebuilt workflow patterns (chain, parallel, router, evaluator-optimizer), and uniquely allows agents themselves to be exposed as MCP servers, enabling composition of agents-of-agents without glue code.

## The Convergence of Two Trends

### The Current Landscape

**Trend 1: Better Tool Integration**
- Frameworks improving at chaining models, APIs, and data
- Orchestration becoming more sophisticated
- Workflows becoming more capable

**Trend 2: Emerging Standards**
- Model Context Protocol (MCP) gaining adoption
- Tools standardizing on MCP interfaces
- Interoperability becoming expected

### Why This Matters

**Intersection:**
Fast Agent sits where these trends meet.

**What this enables:**
Instead of writing adapters for each tool, Fast Agent speaks the universal language (MCP).

**Result:**
Portable, composable, standards-aligned workflows.

## Why Fast Agent Is Different

### The MCP-First Superpower

**Standard approach:**
Each framework reinvents tool integration.

```
Framework A ↔ Tool integration A
Framework B ↔ Tool integration B
Framework C ↔ Tool integration C

Each framework has its own adapters
Duplicate code across frameworks
Tools work in some frameworks, not others
Vendor lock-in
```

**Fast Agent approach:**
One standard interface (MCP).

```
Fast Agent ↔ MCP
LangChain ↔ MCP
AutoGen ↔ MCP
CrewAI ↔ MCP

Any tool speaking MCP works anywhere
No adapters needed
Truly interoperable
Future-proof
```

### Complete MCP Compliance

**Key principle:**
If a tool speaks MCP, Fast Agent can use it without writing a single line of adapter code.

**Implications:**

```
Swap tools instantly
    ↓
No code changes, just configuration

Mix local and cloud MCP services
    ↓
Seamless hybrid workflows

Run agents as MCP servers
    ↓
Agents become reusable components
```

## Core Features

### 1. Interoperability First

**What it means:**
Works with any MCP-compliant tool or model provider.

**Benefits:**
- No vendor lock-in
- Future-proof (new tools don't require framework updates)
- Standardized integrations
- Seamless composition

### 2. Decorator-Based API

**What it looks like:**

```python
@fast.agent(name="calendar",
            instruction="What events are on today's calendar?",
            servers=["calendar"])
```

**Benefits:**
- Concise definition
- Most agents take handful of lines
- Clean, readable code
- Fast prototyping

### 3. Prebuilt Workflow Patterns

**Chain:**
Run steps in sequence.

```
Step 1 → Step 2 → Step 3 → Done
```

**Parallel:**
Fan-out tasks and optionally merge results.

```
Input → [Task A, Task B, Task C] → Fan-in → Merge → Output
```

**Router:**
Send input to the most relevant sub-agent.

```
Input → Classify type → Route to Agent A/B/C → Output
```

**Evaluator-Optimizer:**
Auto-critique and refine outputs.

```
Generate → Evaluate quality → Refine → Validate → Output
```

### 4. Multi-Modal Support

**Handles:**
- Images
- PDFs
- Text
- All in same workflow

### 5. Full Model Support

**Compatible with:**
- Anthropic Claude
- OpenAI GPT
- Google Gemini
- Azure
- Ollama
- TensorZero
- And more

**Benefit:**
Not locked to single LLM provider.

### 6. Testing Modes

**Passthrough mode:**
Test workflow structure and logic.

**Playback mode:**
Offline debugging using recorded API responses.

**Benefit:**
No API costs during development and debugging.

### 7. Observability

**Built-in OpenTelemetry integration:**
- Tracing
- Metrics collection
- Performance monitoring
- Debugging visibility

## Real-World Example: Morning Brief Agent

### The Scenario

**Goal:**
An AI agent that every morning:
- Checks your calendar
- Pulls latest GitHub activity
- Lists open issues
- Aggregates into human-readable report

### The Implementation

**Structure:**

```
Source Agents (parallel):
├── Calendar Agent
│   └── Gets today's events
├── GitHub Changes Agent
│   └── Gets recent commits
└── GitHub Issues Agent
    └── Gets open issues

Fan-in Agent:
└── Merges into standard JSON schema

Reporting Agent:
└── Converts JSON to Markdown report
```

### The Code

**Decorator-based definition:**

```python
request_params = RequestParams(
    use_history=False,
    maxTokens=200000,
    response_format=get_spec("morning_brief", "artifacts"))

fast = FastAgent("Morning Brief Agent")

@fast.agent(name="calendar",
            instruction="What events are on today's primary calendar?",
            servers=["calendar"],
            tools={
                "calendar": ["list-calendars", "get-freebusy", "list-events"],
            },
            request_params=request_params)

@fast.agent(name="github_changes",
            instruction="What has changed in GitHub repo past 24 hours?",
            servers=["github", "time"],
            tools={
                "time": ["get_current_time"],
                "github": ["get_commit", "list_commits", "list_issues"]
            },
            request_params=request_params)

@fast.agent(name="github_issues",
            instruction="What issues are open in the GitHub repo?",
            servers=["github", "time"],
            tools={
                "time": ["get_current_time"],
                "github": ["get_issue", "list_issues"]
            },
            request_params=request_params)

@fast.agent(name="reporting",
            model="openrouter.gpt-5",
            instruction="""Generate human-readable report from
                          gathered information in markdown format.
                          Save to ./reports/<date>.md""",
            servers=["filesystem"],
            request_params=RequestParams(use_history=False,
                                       maxTokens=200000))

@fast.agent(name="fan_in",
            instruction="Aggregate results from various sources.",
            request_params=request_params)

@fast.parallel(name="parallel",
               fan_out=["github_changes", "calendar", "github_issues"],
               fan_in="fan_in")

@fast.chain(name="default",
            sequence=["parallel", "reporting"])

async def main():
    async with fast.run() as agent:
        await agent.interactive()
```

**What you get:**
- Fully functional multi-agent workflow
- MCP-compliant throughout
- ~50 lines of clean code
- Ready for interactive testing

## How It Compares to Other Frameworks

### LangChain

**Strengths:**
- Huge integration ecosystem
- Mature framework
- Widely adopted

**Limitations:**
- No MCP-native support
- Requires adapters for tool compatibility
- Vendor specific integrations

**Fast Agent advantage:**
- MCP-native from ground up
- No adapters needed
- Standards-aligned

### AutoGen

**Strengths:**
- Multi-agent conversation loops
- Research-backed patterns
- Flexible architectures

**Limitations:**
- Less structured workflow orchestration
- Not MCP-focused
- Conversation-centric (not task-centric)

**Fast Agent advantage:**
- Explicit workflow patterns
- MCP-native
- Task-oriented orchestration

### CrewAI

**Strengths:**
- Role-based multi-agent "crews"
- Team-style collaboration metaphor
- User-friendly API

**Limitations:**
- Less programmatic
- Not MCP-oriented
- Requires custom integrations

**Fast Agent advantage:**
- More programmatic and precise
- MCP-oriented
- Standards-aligned

### Verdict

**If you prioritize:**
- Standardized interoperability → Fast Agent
- Avoiding vendor lock-in → Fast Agent
- MCP adoption trajectory → Fast Agent
- Fast prototyping → Fast Agent
- Reproducible, debuggable workflows → Fast Agent

## Interactive Development

### The REPL-Like Experience

**Launch interactive session:**

```bash
uv run agent.py
```

**Result:**
CLI where you can interact with agents in real time.

### Interactive Capabilities

**Chat with individual agents:**
```
calendar: What's on my schedule today?
```

**Switch between workflows:**
```
@default
Generate today's morning brief
```

**Debug behavior in real time:**
- Watch tool calls flow through system
- See responses step by step
- Experiment with prompts
- Validate tool outputs

### Agent Switching

**Switch context:**
```
@extract_labels
```

**Now all messages go to that agent:**
```
Extract labels from this issue
```

**Run workflows:**
```
@default Generate morning brief
```

### Slash Commands

**Available commands:**

```
/tools — List and call available MCP tools
/prompt — List/select MCP prompts
/agents — Show all available agents
/usage — Display current usage statistics
/markdown — Re-render last message without formatting
/help — Show available commands
/clear — Clear screen
```

### Why This Matters

**Benefits:**
- Sandboxed REPL for agents
- Safe space to tune instructions
- Debug workflows interactively
- Explore integrations
- Test before committing to production

**Workflow:**
```
Prototype locally (interactive)
    ↓
Tune instructions and prompts
    ↓
Debug workflows
    ↓
Validate tool outputs
    ↓
Switch to headless operation
    ↓
Expose as MCP server
```

## Agents as MCP Servers

### The Superpower

**What if your agent becomes a reusable tool?**

```
Your Fast Agent
    ↓
Becomes MCP Server
    ↓
Other apps can call it
    ↓
Other agents can use it
    ↓
Compose agents-of-agents
```

### Running as Server

**One-liner:**

```bash
uv run agent.py --server --transport http --port 9090
```

**Flags:**
- `--server` — Start service mode
- `--transport http` — MCP over HTTP
- `--host 0.0.0.0` — Listen on all interfaces
- `--port 9090` — Choose port

**Result:**
Agent exposed as MCP tools at `http://localhost:9090`

### Consuming from Another Agent

**Configuration (fastagent.config.yaml):**

```yaml
mcp:
  hosts:
    my_service:
      transport: http
      url: http://localhost:9090
```

**Usage in agent:**

```python
@fast.agent(
  name="orchestrator",
  instruction="Call downstream tools exposed by my_service.",
  servers=["my_service"]
)
```

**Result:**
Remote agent appears as tools. Use it like any other MCP server.

### Agent Composition

**What this enables:**

```
Micro-Agent 1 → MCP Server
Micro-Agent 2 → MCP Server
Micro-Agent 3 → MCP Server
        ↓
Orchestrator Agent consumes all three
        ↓
Complex workflow from simple pieces
        ↓
No glue code, just MCP
```

## Getting Started

### Installation

```bash
uv pip install fast-agent-mcp
```

### Setup

```bash
fast-agent setup
```

### Run

```bash
uv run agent.py
```

### Next Steps

1. Add your MCP servers
2. Write your instructions
3. Watch agents come to life

## Key Takeaways

1. **MCP-first architecture** — Built from ground up for Model Context Protocol
2. **No adapter code** — If it speaks MCP, Fast Agent uses it
3. **Tool swapping trivial** — Change configuration, not code
4. **Interoperable** — Works with local and cloud MCP services
5. **Future-proof** — Standards-aligned, not vendor-locked
6. **Decorator-based API** — Clean, concise agent definitions
7. **Rapid prototyping** — Most agents in handful of lines
8. **Prebuilt patterns** — Chain, Parallel, Router, Evaluator-Optimizer
9. **Multi-modal support** — Images, PDFs, text in same workflow
10. **Full model support** — Claude, GPT, Gemini, Azure, Ollama, etc.
11. **Testing modes** — Passthrough and Playback for offline debugging
12. **Observable** — Built-in OpenTelemetry integration
13. **Interactive development** — REPL-like CLI for testing and tuning
14. **Agents as servers** — Run agents as MCP endpoints
15. **Agent composition** — Agents-of-agents without glue code
16. **No vendor lock-in** — Standards-aligned from day one
17. **Workflow patterns included** — Best practices built-in
18. **Less boilerplate** — Focus on logic, not framework mechanics
19. **Debugging friendly** — Step-by-step visibility into execution
20. **Production ready** — From prototype to server in one command

## Comparison Context

### Why It Matters Now

**Historical progression:**
```
2023: Frameworks compete on tool ecosystems
2024: MCP emerges as standard interface
2025: Fast Agent demonstrates what MCP-native looks like
```

**Strategic implication:**
As MCP adoption increases, frameworks designed around MCP standards will become increasingly valuable.

## Integration with Best Practices

### Grounded in Anthropic's Guidance

**Fast Agent patterns align with:**
- Anthropic's "Building Effective Agents" principles
- Best practices for reliable agent design
- Proven strategies for agent orchestration
- Patterns for multi-agent systems

**Benefit:**
Implementing best practices from day one, not retrofitting.

## The Bottom Line

Owen Zanzal introduces Fast Agent as a standards-aligned, rapid-prototyping framework that solves a critical problem in agent development: interoperability without vendor lock-in.

**The core value:**

**Instead of:**
- Building proprietary tool integrations
- Writing adapters for each framework
- Being locked to specific models/tools
- Complex boilerplate for agent definition

**Do this:**
- Leverage MCP as universal interface
- Write zero adapter code
- Switch tools and models at will
- Define agents in 10 lines of code

**The three-layer strategy:**

1. **Development layer** — Interactive REPL for prototyping and debugging
2. **Execution layer** — Orchestrate workflows with prebuilt patterns
3. **Distribution layer** — Expose agents as MCP servers for composition

**Key innovations:**
- Decorator-based API for conciseness
- MCP-native throughout (no adapters)
- Agents as first-class MCP servers
- Testing modes for offline debugging
- Interactive development experience

**For practitioners:**
If you're building multi-agent workflows and care about portability and standards, Fast Agent provides a solid, future-proof foundation.

**For the ecosystem:**
As MCP becomes the lingua franca of AI tools, frameworks like Fast Agent that embrace standards from the ground up will likely become essential infrastructure.

**The philosophy:**
Standards-aligned from day one. Portable by design. Composable without glue code. Rapid prototyping with best practices built in.

Fast Agent makes it faster (pun intended) to go from "I need an AI that does X" to "It's running, integrated, and future-proof."

