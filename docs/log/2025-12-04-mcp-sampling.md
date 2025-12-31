---
summary: Explores MCP Sampling, a feature that inverts typical AI-tool relationships by allowing MCP servers to delegate intelligent tasks to the user's connected AI through bidirectional channels, eliminating embedded LLM infrastructure
event_type: article
sources:
    - https://block.github.io/goose/blog/2025/12/04/mcp-sampling/
tags:
    - MCP
    - sampling
    - tool-design
    - AI-architecture
    - Goose
    - agent-tools
    - bidirectional-communication
---

# MCP Sampling: When Your Tools Need to Think

**Author:** Angie Jones (Head of Developer Relations)
**Publication:** Block/Goose Blog
**Publication Date:** December 4, 2025

## Overview

MCP Sampling inverts the typical AI-tool relationship: instead of AI calling tools, **tools can call the AI**. This feature enables MCP servers to delegate intelligent tasks to the user's connected AI through bidirectional communication channels.

## The Core Insight

Traditional approach:
```
AI → Tool → Hardcoded Logic → Result
```

With sampling:
```
AI → Tool → AI (via sampling) → Result
```

Rather than hardcoding logic or embedding separate LLM calls within MCP servers, sampling enables servers to leverage the existing AI connection for intelligent processing.

## Why This Matters

### The Problem with Embedded LLMs

Without sampling, MCP servers needing AI capabilities must:
- Make their own calls to OpenAI, Anthropic, or other providers
- Manage API keys within the server
- Handle model selection and configuration
- Duplicate AI infrastructure already available

### The Sampling Solution

With sampling:
- **No API key management** within the server
- **Model flexibility** — users choose their LLM provider
- **Simplified architecture** — focus on orchestration, not AI implementation
- **Consistent AI behavior** — same model handles all reasoning

## Technical Implementation

### Bidirectional Channels

When MCP clients connect to servers, bidirectional communication channels are established. This allows:
- Clients to call server tools (standard)
- Servers to request AI processing from clients (sampling)

### Using ctx.sample()

Developers use `ctx.sample()` calls to:
1. Send prompts to the connected AI
2. Configure parameters (temperature, token limits)
3. Receive AI responses

```python
# Conceptual example
response = await ctx.sample(
    prompt="Analyze this sentiment: {text}",
    temperature=0.7,
    max_tokens=500
)
```

### Configurable Parameters

- **Temperature:** Control response creativity
- **Token limits:** Manage response length
- **System prompts:** Provide context for the AI

## Real-World Example: Council of Mine

**Council of Mine** demonstrates sampling in practice by simulating nine AI personas with distinct perspectives debating topics.

### The Nine Personas
- Pragmatist
- Visionary
- Devil's Advocate
- (and six others with unique viewpoints)

### Orchestration Flow

The server orchestrates **19 sampling calls per debate**:

| Phase | Sampling Calls | Purpose |
|-------|----------------|---------|
| Initial opinions | 9 | Each persona shares perspective |
| Voting | 9 | Personas vote on positions |
| Synthesis | 1 | Final summary of debate |

### Key Achievement

All this orchestration happens **without embedded LLM infrastructure**. The server focuses purely on:
- Managing personas
- Structuring the debate flow
- Aggregating responses

The connected AI handles all the actual reasoning.

## Benefits of Sampling Architecture

### For Server Developers

1. **Simpler code:** No LLM SDK integration needed
2. **No secrets:** API keys stay with the user
3. **Reduced dependencies:** Fewer external services to manage
4. **Easier testing:** Mock sampling responses for tests

### For Users

1. **Model choice:** Use preferred LLM provider
2. **Cost control:** All AI calls through existing subscription
3. **Consistent behavior:** Same model across all tools
4. **Privacy:** Data stays within existing AI relationship

### For the Ecosystem

1. **Interoperability:** Servers work with any MCP-compatible client
2. **Standardization:** Common pattern for AI delegation
3. **Innovation focus:** Developers build unique orchestration, not AI plumbing

## Recommended Use Cases

### Good Fit for Sampling

- **Summarization:** Compress long content
- **Translation:** Convert between languages
- **Sentiment analysis:** Evaluate tone and emotion
- **Creative tasks:** Generate variations or ideas
- **Complex reasoning:** Multi-step analysis

### Poor Fit for Sampling

- **Deterministic operations:** When exact same output needed every time
- **Latency-sensitive workflows:** Sampling adds round-trip time
- **Simple logic:** If/else better than AI for basic decisions
- **High-volume processing:** Each sample is an AI call

## Architectural Pattern

### Traditional MCP Server
```
Request → Process → Return Result
```

### Sampling-Enabled Server
```
Request → Orchestrate → Sample AI → Process Response → Return Result
           ↓
    (May loop multiple times)
```

### Multi-Sample Orchestration (Council of Mine Pattern)
```
Request
   ↓
┌──────────────────────────────┐
│  Sample 1 (Persona A)        │
│  Sample 2 (Persona B)        │
│  ...                         │
│  Sample N (Persona N)        │
└──────────────────────────────┘
   ↓
Aggregate/Process
   ↓
Optional: Additional Sample (Synthesis)
   ↓
Return Result
```

## Implementation Considerations

### When to Sample

Ask: "Does this task require intelligence/creativity?"
- Yes → Consider sampling
- No → Use deterministic logic

### Sample Count

More samples = More AI calls = Higher latency and cost
- Balance thoroughness with performance
- Consider caching where appropriate

### Error Handling

Sampling can fail (rate limits, timeouts). Plan for:
- Retries with backoff
- Fallback behavior
- Graceful degradation

## Key Takeaways

1. **Sampling inverts the tool-AI relationship** — tools can request AI thinking
2. **Eliminates embedded LLM infrastructure** in MCP servers
3. **Users keep model choice and API key control**
4. **Enables sophisticated orchestration** like multi-persona debates
5. **Best for creative/analytical tasks**, not deterministic operations
6. **Bidirectional channels** are the enabling mechanism

## Implications for MCP Server Design

Sampling changes how developers think about MCP servers:

**Before:** "My server needs to be smart"
**After:** "My server needs to orchestrate smartly"

The intelligence lives in the user's AI. The server's job is to:
- Structure the problem
- Manage the workflow
- Aggregate results
- Return useful output

This separation of concerns enables more powerful, flexible, and maintainable MCP servers.
