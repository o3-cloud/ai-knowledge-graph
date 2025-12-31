---
summary: MCP Agent Mail - A coordination layer for multiple coding agents using messaging, file reservations, and git-backed audit trails to prevent conflicts and enable collaborative AI development
event_type: research
sources:
  - https://github.com/Dicklesworthstone/mcp_agent_mail
  - https://github.com/Dicklesworthstone/mcp_agent_mail/blob/main/README.md
tags:
  - mcp
  - agent-coordination
  - multi-agent-systems
  - agent-communication
  - file-locking
  - conflict-prevention
  - git-audit-trail
  - ai-coding-agents
  - collaboration
  - beads-integration
---

# MCP Agent Mail: Multi-Agent Coordination Framework

**Project:** MCP Agent Mail
**Author:** Dicklesworthstone
**Repository:** https://github.com/Dicklesworthstone/mcp_agent_mail
**License:** MIT

## Problem Statement

When multiple AI coding agents work simultaneously on the same codebase:
- Agents overwrite each other's edits
- Parallel workstreams lack visibility into each other's changes
- Conflicts require manual human intervention
- Context about what other agents are doing is inaccessible

## Solution: Agent Email System

MCP Agent Mail implements a **coordination layer** inspired by email systems, enabling agents to:
- Maintain persistent, memorable identities (e.g., "GreenCastle")
- Send and receive messages with full context
- Declare file intentions via "leases" to prevent conflicts
- Create auditable, human-readable artifact trails

## Core Components

### 1. Messaging & Identity
- Agents register memorable identities (adjective + noun combinations)
- GitHub-Flavored Markdown messages with image support
- Searchable conversation history and threading
- Message summarization capabilities

### 2. File Reservation System
- Advisory file leases signal which files an agent is modifying
- Optional exclusive locks for critical sections
- TTL-based automatic expiration
- Prevents agents from unknowingly conflicting over the same files

### 3. Git-Backed Infrastructure
- All coordination data stored in Git repositories
- Human-auditable artifacts (not opaque databases)
- Full historical tracking of all agent interactions
- Enables review and recovery of agent decisions

### 4. Search & Indexing
- SQLite database with FTS5 (Full-Text Search)
- Fast searching across agent messages and metadata
- Efficient querying of agent states and file reservations

## Architecture

- **HTTP-only FastMCP server** (no STDIO or SSE required)
- **Git repository backend** for human auditability
- **SQLite with FTS5** for performant searches
- **Integration with Beads CLI** for dependency-aware task planning
- **Beads Viewer (bv)** for graph analytics and agent status

## Key Features

1. **Agent Identity Management**: Memorable, persistent agent identities
2. **Message Threading**: Organized conversations with search capabilities
3. **File Lease System**: Prevent write conflicts across agents
4. **Audit Trail**: Complete git-backed history of all operations
5. **Web UI**: Human review of messages, agents, and file reservations
6. **Beads Integration**: Works with Beads for intelligent task coordination

## Installation & Usage

**One-line install:**
```bash
curl -fsSL "https://raw.githubusercontent.com/Dicklesworthstone/mcp_agent_mail/main/scripts/install.sh?$(date +%s)" | bash -s -- --yes
```

**Start the server:**
```bash
am
```

## Relevance to Our Project

This framework directly addresses critical challenges for our AI Shoplogix system:

1. **Multi-Agent Safety**: Prevents agents from conflicting when working on the same features
2. **Traceability**: Every agent action is auditable and human-reviewable via Git
3. **Coordination Pattern**: Provides a proven architectural pattern for agent collaboration
4. **Task Planning**: Integrates with Beads for intelligent, dependency-aware work allocation
5. **Scalability**: Enables coordinated work of many agents on complex projects

## Architectural Insights

- **Communication Protocol**: Agent-to-agent via messaging rather than direct file manipulation
- **Conflict Prevention**: Proactive declaration of intent vs. reactive conflict resolution
- **Human Oversight**: Git-backed, human-readable artifacts enable review and intervention
- **MCP Integration**: Fits within the Model Context Protocol ecosystem for standardized agent APIs

## Related Concepts

- Agent coordination patterns
- Multi-agent conflict resolution
- Audit trails and compliance
- File locking and resource management
- Message-based architecture
- Git as a coordination medium
