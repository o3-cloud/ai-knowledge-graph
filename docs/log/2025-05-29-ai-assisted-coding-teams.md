---
summary: Nilenso's guide for teams that "can't get away with vibes"—AI multiplies strong engineers, thrives in well-tested codebases, and enables reconsidering old wisdom like over-engineering when regenerating code is cheap
event_type: article
sources:
    - https://blog.nilenso.com/blog/2025/05/29/ai-assisted-coding/
tags:
    - AI-assisted-coding
    - engineering-teams
    - best-practices
    - testing
    - code-quality
    - agentic-tools
    - production-systems
---

# AI-Assisted Coding for Teams That Can't Get Away with Vibes

**Author:** Atharva Raykar
**Publication:** Nilenso Blog
**Publication Date:** May 29, 2025 (Updated June 5, 2025)
**Status:** Living document based on production experience

## Overview

A practical guide for serious engineering teams adopting AI tools while maintaining code quality. The core argument: AI should be adopted, but skillful usage is essential to avoid generating technical debt. Velocity gains matter because they enable tighter feedback loops with users.

## The Core Principle

### AI as a Multiplier

**"AI is a multiplier"**

Strong engineers extract more value because they:
- Communicate technical ideas clearly
- Possess good instincts for system design
- Maintain strong fundamentals
- Have refined taste in code quality

**Implication:** AI amplifies existing skill, it doesn't replace it.

## Environmental Requirements

### Codebases Where AI Thrives

| Marker | Why It Matters |
|--------|----------------|
| Good test coverage | AI changes verified automatically |
| Meaningful assertions | Tests catch real issues |
| Automated linting/formatting | Consistent output quality |
| Testing gates | Quality floor enforced |
| Well-documented changes | Context available for AI |
| Consistent style | Predictable patterns |
| Simple, organized structure | Easier navigation |
| Small, defined tasks | Manageable scope |

### The Tale of Two Services

**Anecdote from the article:**
- Well-structured service thrived with AI assistance
- Messier codebase proved equally challenging for humans AND AI

**Lesson:** AI doesn't fix bad codebases—it amplifies the existing state.

## Practical Techniques

### Editor-Based Tactics

**Tool Selection:**
- Use frontier AI models, not cheaper alternatives
- Employ agentic coding tools (Claude Code, Windsurf, Cursor, Cline)
- Tools should read files, run commands, execute plans

**Workflow Patterns:**

1. **Create RULES.md files**
   - Encode standards and practices
   - AI references automatically
   - Consistent output

2. **Break problems down**
   - Specific, manageable components
   - Clear scope per task
   - Reduces hallucination

3. **Provide specifications**
   - Technical documentation
   - API contracts
   - Expected behaviors

4. **Separate planning and execution**
   - Plan the approach first
   - Then execute implementation
   - Review at each phase

5. **Request justification**
   - Ask AI to explain choices
   - Request alternatives
   - Understand trade-offs

### Outside-the-Editor Applications

**Skill Development:**
- Use AI for learning
- Explore unfamiliar domains
- Get explanations of complex code

**Documentation:**
- Generate docs from codebases
- Create runbooks and deployment guides
- Produce API documentation

**Cross-Team Coordination:**
- Create mock servers
- Generate integration stubs
- Document interfaces

**Code Review:**
- Generate initial review summaries
- Identify potential issues
- Suggest improvements

**Performance:**
- Database optimization analysis
- Performance profiling suggestions
- Query optimization

**Observability:**
- Write monitoring queries
- Create alerting rules
- Generate dashboards

## Evolving Best Practices

### Reconsidering Old Wisdom

**Over-engineering abstractions:**
- *Old:* Build abstractions for future flexibility
- *New:* Regenerating code is cheap—abstract when needed

**Code organization:**
- *Old:* Micro-level sophistication matters
- *New:* Organization at scale matters more

**Prototyping:**
- *Old:* Risk of throwaway code
- *New:* Prototype-driven development viable before formal implementation

**Testing:**
- *Old:* Tests are nice to have
- *New:* Tests are non-negotiable given generation speed

### The Generator-Verifier Gap

**Key insight:** Verification often requires less effort than creation.

**Implication:**
- Review AI-generated code carefully
- Verification is your primary contribution
- Don't skip this step because code came fast

## Agentic Coding Tools

### Recommended Tools

- **Claude Code** — Anthropic's CLI tool
- **Windsurf** — Codeium's agentic IDE
- **Cursor** — AI-native editor
- **Cline** — VS Code extension

### What Makes Them "Agentic"

- Read files across codebase
- Run commands (tests, linters)
- Execute multi-step plans
- Iterate on failures
- Maintain context

## Future Topics (Article Roadmap)

- Deploying autonomous agents effectively
- AI for data analysis and query writing
- Proprietary code security and self-hosted options
- Team culture around prompt sharing
- Organizational adoption strategies

## Key Takeaways

1. **AI multiplies skill** — Strong engineers benefit most
2. **Environment matters** — Tests, linting, organization enable AI
3. **Use frontier models** — Don't cheap out on model quality
4. **Agentic tools** — Choose tools that can act, not just suggest
5. **RULES.md** — Encode standards for consistent output
6. **Plan then execute** — Separate thinking from implementation
7. **Request justification** — Understand AI's reasoning
8. **Tests non-negotiable** — Generation speed demands verification
9. **Generator-verifier gap** — Your job is verification

## The Bottom Line

Teams that "can't get away with vibes" need structured approaches to AI adoption. The key is recognizing AI as a multiplier—it amplifies existing engineering skill and codebase quality. Well-tested, well-organized codebases thrive with AI assistance; messy ones struggle equally with humans or AI. The practical techniques center on providing context (RULES.md, specifications), breaking work into manageable pieces, and maintaining quality gates (tests, linting). Old engineering wisdom needs updating: when regenerating code is cheap, abstraction timing changes, and testing becomes absolutely non-negotiable.
