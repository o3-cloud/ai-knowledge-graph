---
summary: Owen Zanzal argues for personal AI (pAI)—encoding individual engineering judgment into agents that handle routine decisions while humans retain control, with GitHub Actions as ideal infrastructure and four example agents (PR review, AWS deprecation, Terraform diff, observability triage)
event_type: article
sources:
    - https://www.linkedin.com/pulse/you-your-tools-team-ai-agents-owen-zanzal-87wpe/
tags:
    - pAI
    - personal-AI
    - AI-agents
    - GitHub-Actions
    - automation
    - DevOps
    - engineering-judgment
---

# You, Your Tools, and Your Team of AI Agents

**Author:** Owen Zanzal
**Publication:** LinkedIn
**Publication Date:** June 30, 2025

## Overview

An argument for personal AI (pAI)—the idea that individuals should develop personalized AI agents tailored to their work context rather than relying on generic tools. This represents a fundamental shift in how professionals approach automation.

## The Problem with Generic AI

### Missing Context

Current AI tooling lacks:
- Personal standards
- Organizational norms
- Domain-specific decision-making
- Individual judgment patterns

### The Gap

Generic AI knows general patterns but not:
- What "good" looks like to you
- Your team's conventions
- Your organization's risk tolerance
- Your domain's edge cases

## The pAI Solution

### Encoded Workflows

**Core concept:** Encode your engineering judgment into agents.

**What gets encoded:**
- Personal heuristics
- Quality standards
- Decision patterns
- Risk assessment

### The Goal

Build "what good work looks like, from my perspective" into automation systems.

### Human-in-the-Loop

pAI handles routine decisions while:
- Humans retain control
- Judgment calls escalate
- Accountability stays clear
- Learning happens both ways

## Four Example Agents

### 1. PR Review Agent

**Function:** Analyze pull requests using personal heuristics

**What it knows:**
- Your code quality standards
- Patterns you watch for
- Common mistakes in your codebase
- When to flag for human review

### 2. AWS Deprecation Agent

**Function:** Monitor and assess service changes

**What it knows:**
- Services your team uses
- Impact assessment criteria
- Migration urgency factors
- Who to notify

### 3. Terraform Diff Whisperer

**Function:** Flag risky infrastructure changes

**What it knows:**
- Your infrastructure patterns
- High-risk change types
- Environment-specific concerns
- Rollback complexity signals

### 4. Observability Triage Agent

**Function:** Consolidate alerts and suggest improvements

**What it knows:**
- Your alert fatigue patterns
- Signal vs noise in your system
- Correlation between alerts
- Improvement opportunities

## GitHub Actions as Platform

### Why GitHub Actions for pAI

| Characteristic | Benefit for pAI |
|----------------|-----------------|
| Event-driven | Triggers on relevant activity |
| Contextually embedded | Lives in the codebase |
| Auditable | Actions visible in history |
| Familiar | DevOps engineers know it |
| Pipeline abstractions | Natural fit for workflows |

### The Mental Model

DevOps engineers already think in:
- Event triggers
- Workflow steps
- Conditional logic
- Environment contexts

pAI fits naturally into this paradigm.

## Broader Implications

### Hiring Evolution

**Future evaluation criteria:**
- Personal automation ecosystems
- AI delegation capabilities
- Judgment encoding ability
- Tool-building patterns

**Not just:**
- Raw technical skills
- Years of experience
- Credential accumulation

### The New Differentiator

**Old:** What can you do?
**New:** What can you automate?

Engineers who build effective pAI multiply their impact.

## Building pAI

### The Process

1. **Identify routine decisions**
   - What do you do repeatedly?
   - What patterns do you apply?
   - What could be automated?

2. **Encode your judgment**
   - What makes something "good"?
   - What signals risk?
   - What triggers escalation?

3. **Choose platform**
   - GitHub Actions for code-centric
   - Other triggers for other contexts
   - Event-driven architecture

4. **Iterate and refine**
   - Watch for edge cases
   - Improve heuristics
   - Expand scope gradually

### What to Automate First

**Good candidates:**
- High-frequency, low-variance tasks
- Pattern-matching decisions
- Information consolidation
- Notification and triage

**Bad candidates:**
- Novel situations
- High-stakes judgment calls
- Context-dependent decisions
- Relationship-heavy work

## Key Takeaways

1. **Generic AI lacks context** — Doesn't know your standards
2. **pAI encodes judgment** — Your perspective in automation
3. **Human-in-the-loop** — Control retained, routine delegated
4. **Four agent examples** — PR review, AWS, Terraform, observability
5. **GitHub Actions platform** — Event-driven, embedded, auditable
6. **Hiring implications** — Automation ecosystems become criteria
7. **Multiply impact** — Engineers who automate scale themselves

## The Bottom Line

Personal AI (pAI) addresses the fundamental limitation of generic AI tools: they don't know what "good" means to you. By encoding your engineering judgment into agents, you can delegate routine decisions while maintaining control over what matters. GitHub Actions provides natural infrastructure for this—event-driven, embedded in code, and familiar to engineers already thinking in pipeline abstractions. The implications extend beyond productivity: hiring will increasingly evaluate candidates on their ability to build and delegate to personal automation ecosystems. The engineers who build effective pAI multiply their impact; those who don't may find their generic-tool approach increasingly commoditized.
