---
summary: Anthropic engineering guide on maintaining agent progress across multiple context windows using initializer agents, feature lists, progress tracking files, and structured workflows that prevent premature completion and context exhaustion
event_type: article
sources:
    - https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
tags:
    - long-running-agents
    - context-management
    - agent-architecture
    - Anthropic
    - progress-tracking
    - multi-session
    - harness-design
---

# Effective Harnesses for Long-Running Agents

**Author:** Justin Young
**Publication:** Anthropic Engineering
**Publication Date:** November 26, 2025

## Overview

This research addresses a critical challenge in AI agent development: **maintaining consistent progress across multiple context windows**. Agents work in discrete sessions with no memory of previous work, requiring structured approaches to bridge gaps between coding sessions.

## The Core Problem

Even advanced models like Claude Opus 4.5 struggle with extended tasks. Agents typically fail in two ways:

### Failure Mode 1: Context Exhaustion
Attempting to complete entire applications in one session, exhausting context mid-implementation.

### Failure Mode 2: Premature Completion
Declaring projects complete after partial progress, losing track of remaining work.

Both failures stem from lack of persistent state and progress visibility across sessions.

## Two-Part Solution Architecture

### 1. Initializer Agent

The first session uses a specialized prompt to establish foundational infrastructure:

**Creates:**
- `init.sh` script for development server startup
- `claude-progress.txt` for tracking work history
- Initial git repository with baseline commits

**Purpose:**
- Standardize environment setup
- Establish progress tracking mechanisms
- Create reproducible starting point for subsequent sessions

### 2. Coding Agent

Subsequent sessions follow a structured workflow:
- Focus on incremental progress
- Maintain clean, production-ready code
- Single-feature implementation per session
- Comprehensive testing before completion

## Key Components

### Feature Lists

The initializer creates comprehensive JSON files containing **200+ features** as discrete, testable units.

**Structure:**
```json
{
  "feature_id": "user-auth-001",
  "description": "User login with email",
  "passes": false,
  "priority": 1
}
```

**Critical constraint:** Agents modify only the `passes` field, preventing:
- Accidental feature deletions
- Scope creep
- Loss of project visibility

### Progress Tracking Files

`claude-progress.txt` maintains:
- Completed work history
- Current session focus
- Known issues and blockers
- Next priorities

This bridges the memory gap between sessions.

### Incremental Approach

**Rule:** Restrict agents to single-feature work per session.

**Benefits:**
- Prevents context exhaustion
- Improves efficiency
- Eliminates guesswork about previous sessions
- Creates clear commit history

### Testing Strategy

**Key insight:** Browser automation tools and end-to-end verification dramatically improved bug detection compared to unit testing alone.

**Explicit prompts direct agents toward:**
- Browser automation (Playwright, Puppeteer)
- End-to-end verification
- Human-like interaction testing
- Visual confirmation of functionality

## Implementation Workflow

Each session follows a structured startup sequence:

```
1. Verify working directory with `pwd`
2. Review git logs and progress documentation
3. Select highest-priority incomplete feature
4. Execute baseline functionality tests
5. Implement single feature
6. Test thoroughly
7. Commit with descriptive messages
8. Update progress tracking
```

## Failure Modes and Mitigations

| Problem | Solution |
|---------|----------|
| Premature project completion | Feature list maintains scope visibility |
| Undocumented progress | Git commits and progress files create continuity |
| Poor feature verification | Browser automation enables human-like testing |
| Configuration confusion | Init scripts standardize setup |
| Context exhaustion | Single-feature focus per session |
| Lost work | Git commits preserve all progress |

## Environment Management

### init.sh Script

Standardizes development environment:
- Starts development servers
- Sets up dependencies
- Configures environment variables
- Ensures reproducible state

### Git Integration

Every session:
- Reviews recent commit history
- Creates atomic commits per feature
- Uses descriptive commit messages
- Maintains clean history for debugging

## Architectural Patterns

### Session Handoff Pattern

```
Session N                    Session N+1
    │                            │
    ├── Implement feature        ├── Read progress.txt
    ├── Test thoroughly          ├── Review git log
    ├── Update progress.txt      ├── Select next feature
    ├── Git commit               ├── Continue work
    └── End session              └── ...
```

### Feature State Machine

```
Feature States:
  - pending (default)
  - in_progress (current session)
  - passes: true (completed)
  - blocked (needs external input)
```

## Design Principles

### 1. Explicit Over Implicit

Don't assume agent remembers anything. Every session starts fresh with explicit context loading.

### 2. Atomic Progress Units

Features small enough to complete in single session. Progress measurable and verifiable.

### 3. Structured Handoffs

Clear documentation of state enables seamless session transitions.

### 4. Defensive Testing

Assume implementation bugs. Test as end-user would, not just code paths.

### 5. Immutable Feature Scope

Feature list defines scope. Agents implement, don't redesign.

## Future Directions

### Multi-Agent Architectures

Single general-purpose agents may underperform compared to specialized agents:
- **Testing Agent:** Dedicated to verification
- **QA Agent:** Code review and quality checks
- **Cleanup Agent:** Refactoring and optimization
- **Implementation Agent:** Feature development

### Domain Expansion

Currently optimized for web development, but approach generalizes to:
- Scientific research
- Financial modeling
- Data pipelines
- Infrastructure automation

## Key Takeaways

1. **Context windows are the constraint** — design around discrete sessions
2. **Progress tracking is essential** — files and git bridge memory gaps
3. **Feature lists maintain scope** — prevent drift and premature completion
4. **Single-feature focus** — prevents context exhaustion
5. **Browser testing beats unit tests** — for catching real bugs
6. **Structured startup sequences** — ensure consistent session beginnings
7. **Defensive design** — assume agent forgets everything between sessions

## Implications for Agent Development

This harness pattern suggests that **agent reliability comes from scaffolding, not just model capability**:

- Environment management matters as much as prompting
- Persistence mechanisms bridge context limitations
- Structured workflows prevent common failure modes
- Testing strategies must match deployment reality

## The Bottom Line

Long-running agents require explicit infrastructure for progress tracking, scope management, and session handoffs. The techniques work with current models—the challenge is disciplined implementation of harness components rather than waiting for model improvements.
