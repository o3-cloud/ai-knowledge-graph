---
summary: Guide to writing effective CLAUDE.md files emphasizing that LLMs are stateless—covering the WHAT/WHY/HOW framework, 150-200 instruction limits, progressive disclosure patterns, and anti-patterns to avoid
event_type: article
sources:
    - https://www.humanlayer.dev/blog/writing-a-good-claude-md
tags:
    - CLAUDE.md
    - Claude-Code
    - context-engineering
    - configuration
    - best-practices
    - agent-setup
    - documentation
---

# Writing a Good CLAUDE.md

**Author:** Kyle
**Publication:** HumanLayer Blog
**Publication Date:** November 25, 2025

## Overview

`CLAUDE.md` (or `AGENTS.md` for open-source agents) represents the **single highest-leverage configuration point** for Claude Code interactions. Since LLMs are stateless and retain no memory between sessions, this file becomes the exclusive mechanism for persistent context delivery.

## Foundational Principle: Statelessness

**"LLMs are stateless functions. Their weights are frozen by the time they're used for inference, so they don't learn over time."**

Implications:
- Agents possess **zero prior knowledge** about codebases at session start
- Every session begins fresh
- CLAUDE.md is the only way to provide persistent context
- What's not in the file doesn't exist to the agent

## Three Essential Components

### WHAT: Technical Stack and Structure

Describe the project's technical foundation:
- Programming languages used
- Frameworks and libraries
- Project structure and organization
- Key directories and their purposes
- Important configuration files

### WHY: Purpose and Function

Explain the project's intent:
- What the project does
- Why components exist
- How pieces relate to each other
- Business context when relevant

### HOW: Operational Procedures

Document workflows and verification:
- How to run tests
- Compilation and build steps
- Verification methods
- Common development tasks
- Deployment procedures

## Critical Constraints

### Instruction Limitations

**Research indicates:** Frontier LLMs reliably follow approximately **150-200 instructions**.

**Budget breakdown:**
- Claude Code system prompt: ~50 instructions
- Remaining for user: ~100-150 instructions

This means every instruction must earn its place.

### Relevance Filtering

Claude implements a system reminder: instructions may be **ignored if deemed irrelevant** to current tasks.

**Implication:** Include only universally applicable content. Task-specific instructions belong elsewhere.

## Best Practices

### Progressive Disclosure

Rather than embedding all documentation in CLAUDE.md:

```
CLAUDE.md (brief, universal)
    │
    ├── docs/testing.md (testing details)
    ├── docs/deployment.md (deployment procedures)
    ├── docs/architecture.md (system design)
    └── docs/api.md (API documentation)
```

Main file provides:
- Pointers to detailed docs
- Brief descriptions
- When to reference each

Claude reads detailed docs when relevant to current task.

### Keep It Short

**HumanLayer maintains less than 60 lines** in their CLAUDE.md.

Target: Under 300 lines maximum.

### Universal vs. Task-Specific

**In CLAUDE.md (universal):**
- Project structure overview
- Core technical stack
- Standard verification commands
- Critical constraints

**In separate docs (task-specific):**
- Detailed procedures
- Component-specific instructions
- Feature documentation
- API references

### Leverage In-Context Learning

Rather than explicit instructions, provide:
- Examples of good patterns
- References to well-written code
- Pointers to documentation

Claude learns from examples better than rules.

## Anti-Patterns to Avoid

### 1. Overstuffing with Style Guidelines

**Don't:** Fill CLAUDE.md with formatting rules.

**Do:** Use linters and formatters instead:
- ESLint, Prettier for JavaScript
- Black, Ruff for Python
- Automated enforcement beats instructions

### 2. Auto-Generating via /init

**Don't:** Run `/init` and accept the generated file.

**Do:** Manually craft based on actual project needs.

Auto-generated files tend to be:
- Generic and unfocused
- Missing project-specific context
- Wasteful of instruction budget

### 3. Task-Specific in Universal Context

**Don't:** Include instructions for specific tasks in main file.

**Do:** Create task-specific markdown files:
- `docs/refactoring-guide.md`
- `docs/new-feature-checklist.md`
- `docs/debugging-procedures.md`

### 4. Exceeding Length Limits

**Don't:** Create comprehensive documentation in CLAUDE.md.

**Do:** Keep it focused and reference external docs.

Long files:
- Dilute important instructions
- Risk relevance filtering
- Waste context window

## Effective Structure Template

```markdown
# Project Name

Brief description of what this project does and why.

## Stack
- Language: [language]
- Framework: [framework]
- Key dependencies: [list]

## Project Structure
- `src/` - Main source code
- `tests/` - Test files
- `docs/` - Documentation (Claude should read when relevant)

## Development

### Testing
```bash
[test command]
```

### Building
```bash
[build command]
```

## Critical Constraints
- [Constraint 1]
- [Constraint 2]

## Additional Documentation
- See `docs/architecture.md` for system design
- See `docs/api.md` for API details
```

## Tools for Separation of Concerns

### Hooks

Handle operational concerns separately:
- Pre-commit formatting
- Post-build verification
- Automated checks

### Slash Commands

Create task-specific workflows:
- `/test` for testing procedures
- `/deploy` for deployment
- `/review` for code review

These keep CLAUDE.md focused on universal context.

## Key Takeaways

1. **CLAUDE.md is highest-leverage config** — single source of persistent context
2. **LLMs are stateless** — what's not in the file doesn't exist
3. **150-200 instruction limit** — every line must earn its place
4. **WHAT/WHY/HOW framework** — cover all three dimensions
5. **Progressive disclosure** — point to detailed docs, don't embed
6. **Keep it short** — under 60 lines ideal, 300 max
7. **Universal only** — task-specific goes elsewhere
8. **Use tooling** — linters, hooks, commands for specific concerns
9. **Don't auto-generate** — manually craft for your project
10. **Examples beat rules** — leverage in-context learning

## The Bottom Line

A good CLAUDE.md is **brief, universal, and high-signal**. It provides essential context without wasting the limited instruction budget on task-specific details or formatting rules that tools handle better. Progressive disclosure through separate documentation files lets Claude access detail when needed while keeping the main file focused.
