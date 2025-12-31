---
summary: CLI tool and framework for scaffolding production-ready AI agents with built-in best practices including the Agent Testing Pyramid, scenario-based testing, versioned prompt management, and MCP integration for coding assistants
event_type: code
sources:
    - https://github.com/langwatch/better-agents
tags:
    - agent-framework
    - testing
    - best-practices
    - prompt-management
    - MCP
    - scaffolding
    - production-agents
    - evaluation
---

# Better Agents: Standards for Building Agents, Better

**Repository:** langwatch/better-agents
**License:** MIT
**Stars:** 1.4k+ | **Forks:** 146+
**Language:** TypeScript (99.6%)

## Overview

Better Agents is a CLI tool and framework for constructing AI agents with **industry best practices built-in**. It scaffolds agent projects following production-ready patterns and "supercharges your coding assistant" by providing expert guidance for frameworks like Agno and Mastra.

## Core Value Proposition

**Problem:** Building production-ready agents requires patterns that aren't obvious—testing strategies, prompt versioning, evaluation pipelines, observability.

**Solution:** Scaffold projects with these patterns already in place, guided by framework-specific expertise delivered through MCP.

## Key Features

### 1. Structured Project Template

Standardized directory organization:

```
project/
├── app/              # Agent application code (framework-agnostic)
├── tests/            # Scenario-based behavioral tests
├── notebooks/        # Jupyter evaluation notebooks
├── prompts/          # Versioned prompt management (YAML)
├── mcp/              # MCP server configuration
└── AGENTS.md         # Auto-generated best practices docs
```

### 2. Agent Testing Pyramid

Implements multi-level testing strategy:

| Level | Type | Purpose |
|-------|------|---------|
| Unit | Component tests | Individual function behavior |
| Integration | Pipeline tests | RAG, classification, tool use |
| E2E | Scenario tests | Full conversation simulations |
| Evaluation | Notebook-based | Performance measurement |

**Scenario-based testing:** Simulates agent conversations to validate behavioral expectations—not just code correctness.

### 3. Prompt Management

Collaborative tooling for prompt workflows:

- **Versioning:** Track prompt changes over time
- **Registry:** Centralized `prompts.json` manifest
- **YAML format:** Human-readable, diffable prompts
- **Playground integration:** Test prompts interactively
- **Team workflows:** Collaborate on prompt development

### 4. Evaluation Notebooks

Jupyter notebooks for measuring agent performance:

- RAG quality assessment
- Classification accuracy
- Tool use correctness
- Response quality metrics
- A/B comparison support

### 5. Developer Guidance

Auto-generated `AGENTS.md` documentation:

- Framework-specific best practices
- Project structure explanation
- Testing conventions
- Prompt management guidelines

## Coding Assistant Integration

Better Agents works with:

- **Claude Code** — MCP-based guidance
- **Cursor** — AI-assisted development
- **Antigravity** — Agent development
- **Kilocode** — Code generation

### MCP Integration

Configuration-driven framework expertise:

```yaml
# MCP servers provide contextual guidance
mcp:
  servers:
    - framework: agno
      expertise: agent-patterns
    - framework: mastra
      expertise: workflow-design
```

The MCP server delivers relevant best practices as you develop.

## Architecture Patterns

### Separation of Concerns

```
app/           → Business logic (framework-agnostic)
tests/         → Behavioral validation
prompts/       → Content management
notebooks/     → Performance measurement
mcp/           → Tool configuration
```

Each concern isolated for independent evolution.

### Configuration-Driven

- MCP integration via config files
- Prompt registry for centralized management
- Environment-based API key handling
- Framework selection at scaffold time

### Framework Agnostic Core

Application code remains portable:

- Core agent logic independent of framework
- Adapters for specific frameworks (Agno, Mastra)
- Testing works across frameworks
- Prompts reusable regardless of runtime

## The Agent Testing Pyramid

### Why a Pyramid?

Traditional testing pyramids (unit → integration → E2E) apply to agents:

**Base (many):** Unit tests for individual components
- Fast, cheap, focused
- Test tool implementations
- Validate helper functions

**Middle (some):** Integration tests for pipelines
- RAG retrieval quality
- Classification accuracy
- Multi-step workflows

**Top (few):** E2E scenario tests
- Full conversation flows
- Behavioral validation
- User journey simulation

### Scenario-Based Testing

```typescript
// Example scenario test structure
describe('Customer Support Agent', () => {
  scenario('refund request', async () => {
    // Simulate conversation
    const response = await agent.chat('I want a refund');

    // Validate behavior, not just output
    expect(response).toIncludeIntent('refund_process');
    expect(response).toMentionPolicy('30_day_return');
  });
});
```

## Prompt Versioning

### YAML Format

```yaml
# prompts/customer-support.yaml
name: customer-support-v2
version: 2.0.0
description: Customer support agent system prompt

template: |
  You are a helpful customer support agent for {{company}}.

  Guidelines:
  - Be empathetic and professional
  - Follow the {{policy_doc}} for refund requests
  ...

variables:
  - company
  - policy_doc
```

### Registry Management

```json
// prompts.json
{
  "prompts": {
    "customer-support": {
      "current": "2.0.0",
      "versions": ["1.0.0", "1.1.0", "2.0.0"]
    }
  }
}
```

## Technical Requirements

- **Node.js:** 22+
- **Package manager:** npm or pnpm
- **API keys:** LangWatch, LLM provider (OpenAI, Anthropic, etc.)
- **Compatible IDE:** Claude Code, Cursor, Antigravity, or Kilocode

## Getting Started

```bash
# Install CLI
npm install -g better-agents

# Scaffold new project
better-agents init my-agent --framework agno

# Run tests
npm test

# Launch evaluation notebook
jupyter notebook notebooks/evaluation.ipynb
```

## Key Takeaways

1. **Best practices built-in** — don't reinvent production patterns
2. **Testing pyramid for agents** — unit, integration, E2E, evaluation
3. **Scenario-based testing** — validate behavior, not just output
4. **Prompt versioning** — treat prompts as versioned artifacts
5. **Evaluation notebooks** — measure performance systematically
6. **MCP-powered guidance** — framework expertise in your IDE
7. **Framework agnostic core** — portable agent logic

## Relevance to Production Agents

Better Agents aligns with research findings on production agents:

- **Structured evaluation** — systematic quality measurement
- **Human oversight** — scenario tests encode expectations
- **Reliability through testing** — catch issues before production
- **Prompt management** — collaborative, versioned, reviewable

The framework codifies patterns that production teams discover through experience, making them accessible from project start.
