---
summary: Adam Conway argues that AI agents need infrastructure for reversible decisions, proposing transaction support in MCP to enable agents to handle consequential decisions safely
event_type: article
sources:
    - https://theoryvc.com/blog-posts/its-not-too-late-to-roll-back-mcp
tags:
    - MCP
    - AI-agents
    - transaction-systems
    - reversibility
    - agent-safety
---

# It's Not Too Late to Roll Back MCP

## The Problem

Despite 2025 being branded the "Year of AI Agents," current systems cannot handle consequential decisions like purchasing vehicles. Decisions exist on two axes:

- **Consequence level** — How much impact does the decision have?
- **Reversibility** — How easily can the decision be undone?

## Why Software Development Works

Agents successfully operate in software development because existing infrastructure makes decisions more reversible and less consequential:

- **Version control** — Easy rollback of code changes
- **Code review** — Catches mistakes before deployment
- **Observability tools** — Clear visibility into decision outcomes

Outside software, no such safety mechanisms exist, leaving agents exposed to irreversible mistakes.

## The Two-Part Solution

### 1. Make Decisions Less Consequential
Better outcome prediction helps agents understand the impact before committing. This involves improving models and adding better feedback loops.

### 2. Make Decisions More Reversible
Implement transaction systems that allow agents to:
- Reverse mistakes automatically
- Understand decision outcomes before committing
- Rollback to previous states

## Proposed Infrastructure

Extend the Model Context Protocol (MCP) with native transaction support. This mirrors database transactions used in distributed systems:
- Begin transaction
- Execute decision
- Preview/validate outcome
- Commit or rollback

## Key Insight

**Improved AI models alone won't solve this challenge.** Engineers must build infrastructure that permits agents to reverse mistakes and understand decision outcomes before committing to actions, similar to existing software development practices.
