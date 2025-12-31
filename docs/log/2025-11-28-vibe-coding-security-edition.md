---
summary: Jon Zeolla shares how Policy as Code creates automated guardrails ensuring only high-quality, compliant AI-generated code reaches production—enforced on every commit across every repository without slowing teams down
event_type: video
sources:
    - https://www.youtube.com/watch?v=InXEWRBsgXI
tags:
    - security
    - vibe-coding
    - policy-as-code
    - AI-code-quality
    - guardrails
    - compliance
    - DevSecOps
---

# How I Learned to Stop Worrying and Love Vibe Coding: Security Edition

**Speaker:** Jon Zeolla
**Event:** DevOpsDays DC
**Upload Date:** November 28, 2025
**Duration:** ~30 minutes

## Overview

As a security professional, Jon Zeolla reconciles two opposing views: AI-generated code feels like a nightmare (fast but often wrong), yet AI tools are incredibly useful for development. The solution: **Policy as Code (PaC)** to create automated guardrails ensuring only high-quality, compliant code reaches production.

## The Security Professional's Dilemma

### The Nightmare View

AI-generated code problems:
- **Incredibly fast to write** — speed masks quality issues
- **Looks convincing** — polished surface hides problems
- **Rarely meets standards first time** — security and quality gaps
- **Erodes trust in tests** — AI writes both code AND tests
- **Creates and validates its own bugs** — self-reinforcing errors

### The Love View

AI tools benefits:
- **Instant boilerplate** — frames out projects almost instantly
- **Continuous suggestions** — improvements throughout development
- **Quick troubleshooting** — helps debug issues rapidly
- **Productivity gains** — significant time savings

### The Reconciliation

**Enter Policy as Code.**

## Policy as Code Solution

### Core Concept

Codify organizational requirements as **machine-enforceable policies**:
- Automated guardrails
- Enforced on every commit
- Across every repository
- Without manual review bottlenecks

### Benefits

- **Scale security expectations** without slowing teams
- **Consistent enforcement** across all repositories
- **Automatic compliance** checking
- **Early detection** of quality and security issues

## Real-World Implementation

Zeolla shares 18 months of experience rolling out Policy as Code across multiple engineering organizations.

### What Gets Enforced

- Security standards
- Quality requirements
- Compliance rules
- Organizational policies

### Where Enforcement Happens

- Every commit
- Every pull request
- Every repository
- Automatically

## The Trust Problem

### AI Writes Both Code and Tests

Traditional testing relies on separation:
- Developer writes code
- Tests verify code works correctly
- Independent validation

With AI:
- AI generates code
- AI generates tests for that code
- AI may create bugs and then validate them
- Self-reinforcing errors possible

### Policy as Code Addresses This

External, human-defined policies:
- Independent of AI generation
- Consistent standards
- Not self-validating
- Enforced uniformly

## Current Industry State

### Companies Have Jumped In

Many organizations have adopted AI for:
- Developer efficiency
- Product features
- Code generation
- Documentation

### Now: Responsible Management Era

The focus shifts to:
- Managing AI wins responsibly
- Ensuring compliance at scale
- Protecting against attackers
- Maintaining quality standards

## Practical Approaches

Zeolla shares field-tested techniques for:

### Getting Arms Around AI-Generated Code

- Policy definitions that work
- Enforcement mechanisms that scale
- Integration with existing workflows
- Minimal developer friction

### Without Slowing Teams Down

- Automated enforcement (no manual gates)
- Clear, fast feedback
- Actionable error messages
- Self-service remediation

## Key Lessons Learned

### Mistakes Made

Zeolla explicitly shares failures and lessons, not just successes—providing realistic expectations for implementation.

### What Works

- Start with critical policies
- Iterate based on feedback
- Balance strictness with practicality
- Communicate clearly with teams

## The Vibe Coding Reality

### Accept the Productivity

AI tools are here and useful. Fighting adoption is futile and counterproductive.

### Add the Guardrails

Policy as Code ensures benefits without unacceptable risks:
- Speed of AI generation
- Quality of enforced standards
- Security of automated checks
- Compliance of codified policies

## Implementation Strategy

### Phase 1: Define Policies

Codify existing organizational requirements:
- Security standards
- Quality thresholds
- Compliance requirements
- Best practices

### Phase 2: Automate Enforcement

Integrate with development workflow:
- CI/CD pipelines
- Pre-commit hooks
- Pull request checks
- Repository-wide rules

### Phase 3: Scale and Iterate

Roll out across organization:
- Start with pilot teams
- Gather feedback
- Refine policies
- Expand coverage

## Key Takeaways

1. **AI code quality is real concern** — looks good but often wrong
2. **AI tools are valuable** — productivity benefits are significant
3. **Policy as Code bridges the gap** — automated guardrails at scale
4. **Enforce on every commit** — consistent, automatic checking
5. **Don't slow teams down** — automation beats manual review
6. **Era of responsible management** — must control AI wins
7. **Field-tested approaches exist** — practical techniques available now

## Implications for Teams

### For Security Teams

- Define policies as code
- Automate enforcement
- Scale without bottlenecks
- Maintain visibility

### For Development Teams

- Keep AI productivity benefits
- Meet quality/security standards automatically
- Clear feedback on violations
- Self-service remediation

### For Organizations

- Standardize expectations
- Ensure compliance
- Protect against vulnerabilities
- Enable responsible AI adoption

## The Bottom Line

You don't have to choose between AI productivity and security/quality. Policy as Code enables both—automated guardrails that enforce standards without slowing development. The approach is practical, field-tested, and ready for implementation today.
