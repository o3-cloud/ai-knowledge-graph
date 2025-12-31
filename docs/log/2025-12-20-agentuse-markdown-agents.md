---
summary: AgentUse framework enables building and deploying AI agents using markdown files with YAML frontmatter instead of traditional code, supporting multi-provider models and MCP integration with sub-second startup
event_type: code
sources:
    - https://github.com/agentuse/agentuse
tags:
    - AI-agents
    - markdown
    - agent-framework
    - MCP
    - infrastructure-as-code
    - low-code
    - agent-deployment
---

# AgentUse: Write and Run AI Agents with Markdown

**Repository:** agentuse/agentuse
**Primary Contributors:** Leon Ho, Claude
**License:** Apache License 2.0

## Overview

AgentUse is a framework for building and deploying AI agents using **markdown files instead of traditional code**. The core philosophy treats agents as infrastructure-as-code artifacts—text files that can be versioned, reviewed, and deployed like any other codebase.

## Core Concept

**"Write and Run AI Agents with Markdown. Run automated AI agents with ease."**

Rather than writing Python or JavaScript to define agent behavior, AgentUse uses plain markdown files with YAML frontmatter for configuration. This enables:
- Non-programmers to create functional agents
- Standard development workflows (git, code review)
- Easy sharing and distribution
- Rapid iteration on agent design

## Key Features

### Markdown-First Design
Agents are plain markdown files with YAML frontmatter for configuration. The markdown content becomes the agent's system prompt.

### Zero Boilerplate
Minimal setup required to create functional agents. No complex framework initialization or configuration files.

### Sub-Second Startup
Optimized for performance with minimal dependencies. Agents launch quickly for interactive use cases.

### Multi-Provider Support
Compatible with multiple LLM providers:
- Anthropic (Claude)
- OpenAI
- OpenRouter models

### MCP Integration
Built-in support for Model Context Protocol servers, enabling agents to use external tools and data sources.

### URL-Shareable
Agents can be distributed and run directly from web URLs. Share agent definitions as easily as sharing links.

### Version Control Friendly
Git-compatible format enables standard development workflows:
- Pull requests for agent changes
- Code review for agent modifications
- Version history and rollback
- Branch-based development

## Agent Structure

Agents consist of:

### YAML Frontmatter
```yaml
---
model: claude-sonnet-4-20250514
mcp_servers:
  - filesystem
  - web-search
sub_agents:
  - researcher
  - writer
---
```

Specifies:
- Model to use
- MCP servers for tools
- Sub-agents for delegation

### Markdown Instructions
The markdown content forms the agent's system prompt:

```markdown
# Daily Metrics Reporter

You are a metrics reporting agent. Your job is to:
1. Gather metrics from the database
2. Generate summary statistics
3. Create a formatted report
...
```

### Optional Tool Integrations
Via MCP servers for external capabilities.

## Usage Examples

### Running Agents

**Via CLI:**
```bash
agentuse run my-agent.md
```

**From URL:**
```bash
agentuse run https://example.com/agents/reporter.md
```

**With Arguments:**
```bash
agentuse run my-agent.md --input "analyze sales data"
```

### Scheduling Agents

Run agents on schedule with cron:
```bash
0 9 * * * agentuse run daily-report.md
```

### CI/CD Integration

Include agents in pipelines:
```yaml
- name: Run Analysis Agent
  run: agentuse run analysis.md
```

## Real-World Applications

The project demonstrates applications including:
- **Daily metrics reporters:** Automated data gathering and reporting
- **SEO analyzers:** Website analysis and recommendations
- **Social media automation:** Content scheduling and posting
- **Research assistants:** Information gathering and synthesis

## Architecture Benefits

### Declarative Agent Definition
Agents defined by what they do, not how they're implemented. The framework handles execution details.

### Separation of Concerns
- Agent logic in markdown
- Tool capabilities via MCP
- Execution handled by framework

### Composability
Sub-agents enable building complex workflows from simple components.

### Portability
Markdown files run anywhere AgentUse is installed. No environment-specific configuration.

## Comparison to Traditional Approaches

| Aspect | Traditional Agent Code | AgentUse Markdown |
|--------|------------------------|-------------------|
| Syntax | Python/JavaScript | Markdown + YAML |
| Learning curve | Programming required | Minimal |
| Version control | Standard but verbose | Natural fit |
| Sharing | Package/deploy | Share URL |
| Startup time | Framework initialization | Sub-second |
| Customization | Unlimited | Template-based |

## MCP Server Integration

AgentUse supports MCP servers for tool capabilities:

```yaml
---
mcp_servers:
  - filesystem    # File operations
  - web-search    # Search capabilities
  - database      # Data access
  - api-client    # External APIs
---
```

Agents automatically gain access to tools provided by configured MCP servers.

## Sub-Agent Delegation

Complex tasks can be delegated to specialized sub-agents:

```yaml
---
sub_agents:
  - researcher    # Information gathering
  - writer        # Content creation
  - reviewer      # Quality checking
---
```

The main agent orchestrates sub-agents for multi-step workflows.

## Key Takeaways

1. **Markdown as agent definition** lowers barrier to agent creation
2. **YAML frontmatter** provides structured configuration
3. **MCP integration** enables tool use without custom code
4. **Sub-second startup** supports interactive use cases
5. **URL sharing** enables easy agent distribution
6. **Git-friendly format** supports standard development workflows

## Implications

AgentUse represents a trend toward **democratizing agent creation**:
- Non-programmers can define agents
- Agents become shareable artifacts
- Standard tools (git, editors) work naturally
- Focus shifts from implementation to design

## Getting Started

1. Install AgentUse
2. Create markdown file with YAML frontmatter
3. Write agent instructions in markdown
4. Run with `agentuse run agent.md`
5. Iterate on agent definition

The framework demonstrates that sophisticated AI agents don't require sophisticated code—clear instructions in plain text can be surprisingly effective.
