---
summary: cass-memory system implements procedural memory for AI coding agents, creating persistent cross-agent knowledge base where all agents learn from each other's debugging strategies and code patterns
event_type: research
sources:
  - https://github.com/Dicklesworthstone/cass_memory_system
tags:
  - agent-memory
  - procedural-memory
  - multi-agent-learning
  - coding-agents
  - knowledge-management
  - episodic-memory
  - working-memory
  - playbook
  - ai-coordination
  - agent-context
---

# cass-memory System: Procedural Memory for AI Agents

**Project**: Dicklesworthstone/cass_memory_system
**License**: MIT
**Status**: Alpha
**Platform**: Linux, macOS, Windows (Bun runtime)

## Core Problem Solved

When using multiple AI coding tools (Claude Code, Cursor, Codex, etc.), each session's knowledge is lost. Developers repeat debugging steps, rediscover patterns, and fail to leverage insights from previous agent interactions.

**cass-memory creates a unified memory system** where every AI agent learns from every other agent's experience.

## Three-Layer Cognitive Architecture

### 1. Episodic Memory
- Raw session logs from all agents
- Ground truth accessible via cass search engine
- Complete history of what agents did and discovered

### 2. Working Memory
- Structured summaries called "diary entries"
- Contextually relevant subset of episodic memory
- Filtered, organized information for agent reasoning

### 3. Procedural Memory
- Distilled, actionable rules in a "playbook"
- Confidence-tracked patterns (lose credibility after 90 days without revalidation)
- Generalizable strategies across projects and agents

## Key Features

### Cross-Agent Learning
- Rules discovered by Cursor automatically help Claude Code
- Anti-patterns found by one agent warn all others
- Debugging strategies compound across team usage

### Scientific Validation
- New rules must evidence-gate against historical sessions
- Prevents false patterns from spreading
- Maintains playbook credibility through validation

### Confidence Decay
- Rules lose credibility over 90 days without revalidation
- Prevents stale heuristics from misleading agents
- Encourages continuous validation and learning

### Anti-Pattern Tracking
- Instead of deleting failed approaches, track them as warnings
- Preserve institutional memory of "what not to do"
- Agents avoid repeating failed patterns

### Graceful Degradation
- System works without cass search engine
- Functions without complete playbook
- Supports offline operation
- Fails safely when components unavailable

## Agent Integration

**Primary command for agents:**
```
cm context "<task>" --json
```

Returns:
- Relevant procedural rules
- Applicable anti-patterns
- Historical context from similar sessions
- All output JSON-structured for agent parsing
- Diagnostics go to stderr only

## Relevance to Agent Architecture

This system addresses a critical gap in multi-agent deployments:
- **Memory fragmentation**: Agents working in isolation lose collective learning
- **Redundant work**: Multiple agents repeat same debugging/discovery cycles
- **Pattern dilution**: Successful approaches aren't systematized
- **Context loss**: Each session starts without team knowledge

## Design Insights

The three-layer structure mirrors cognitive science:
- **Episodic**: What happened (history)
- **Working**: What's relevant now (context)
- **Procedural**: How to do things (patterns)

This separation allows agents to:
- Access full history when needed (episodic)
- Get focused context for immediate task (working)
- Apply learned heuristics automatically (procedural)

## Related Concepts
- Agent memory systems
- Multi-agent coordination
- Knowledge graph patterns
- Feedback loops for AI improvement
- Institutional knowledge capture
- Confidence-tracked learning
