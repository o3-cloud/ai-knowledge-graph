---
summary: Mathias Biilmann introduces Agent Experience (AX) as critical design discipline—as AI agents become autonomous actors, platforms must optimize specifically for agent usability, following DX and UX precedent
event_type: article
sources:
    - https://biilmann.blog/articles/introducing-ax/
tags:
    - Agent-Experience
    - AX
    - AI-agents
    - product-design
    - platform-design
    - API-design
    - future-of-software
    - user-experience
---

# Introducing AX: Why Agent Experience Matters

**Author:** Mathias Biilmann
**Publication:** Biilmann Blog
**Publication Date:** January 28, 2025

## Overview

Biilmann argues that "Agent Experience" (AX) is becoming as critical as User Experience (UX) and Developer Experience (DX). As AI agents become autonomous actors in digital environments, platforms that optimize for agent interaction will dominate. The shift isn't about AI's generative capabilities—it's about bringing agency and autonomous action to computers.

## The Agency Shift

### From Generation to Action

**Previous focus:**
- AI's ability to generate text/images
- Impressive outputs
- Human evaluation of quality
- Asynchronous interaction

**Current shift:**
- AI's ability to perceive environments
- Take autonomous actions
- Make decisions with consequences
- Continuous interaction with systems

**Significance:** The real disruption isn't generation—it's agency.

## Historical Precedent: Experience Design Disciplines

### User Experience (UX)

**Era:** 1990s–2000s
- **Definition:** How systems work for humans
- **Competitive advantage:** Better UX won markets
- **Examples:** Apple vs. Windows, mobile revolution
- **Impact:** Companies built around UX principles dominated

### Developer Experience (DX)

**Era:** 2010s–2020s
- **Definition:** How systems work for software developers
- **Competitive advantage:** Easier APIs, better docs won adoption
- **Examples:** Stripe, GitHub, AWS APIs
- **Impact:** Platforms with great DX dominated in their categories

### Agent Experience (AX)

**Era:** 2020s–2030s
- **Definition:** How systems work for autonomous AI agents
- **Competitive advantage:** Platforms optimized for agents will dominate
- **Examples:** Emerging now
- **Impact:** AX will determine which platforms thrive

## Core Concept: Agent Experience Definition

### What Is AX?

**Agent Experience is:**
"The holistic experience AI agents will have as the user of a product or platform."

**Includes:**
- API design for agent access
- Decision clarity for autonomous systems
- Feedback loops for learning
- Error handling for failures
- Permission/authorization for agents
- Monitoring/observability for oversight

### Why It Matters

**Agents need different things than humans or developers:**

| Aspect | Human | Developer | Agent |
|--------|--------|-----------|-------|
| Interface | Visual, intuitive | Documented APIs | Structured APIs |
| Feedback | Immediate visual | Status codes/responses | Deterministic results |
| Decision making | Guided, explained | Explicit, documented | Clear, unambiguous |
| Error handling | Graceful degradation | Informative errors | Recoverable states |
| Interaction speed | Minutes to hours | Seconds | Milliseconds |

### API Design for Agents

**Traditional API design:**
- Assumes human engineers reading docs
- Some ambiguity acceptable
- Documentation explains behavior
- Edge cases documented informally

**AX-optimized API design:**
- Explicit state representations
- Clear, unambiguous semantics
- Structured error responses
- Deterministic behavior
- Machine-readable specifications

## Two Strategic Approaches

### Approach 1: Closed Proprietary Agents

**Strategy:**
- Build agents owned by platform
- Deep integration with service
- Proprietary intelligence
- User interacts with company's agents

**Examples:**
- ChatGPT plugin ecosystem (limited)
- Proprietary AI assistants

**Advantages:**
- Full control
- Consistent experience
- IP protection

**Disadvantages:**
- Limited adoption
- Slower iteration
- Missing diverse use cases

### Approach 2: Open External Agents

**Strategy:**
- Enable external agents to access platform
- Open APIs and integrations
- Third-party developers build agents
- Compete on platform quality

**Examples:**
- Netlify's ChatGPT integration (1,000+ daily deployments)
- Open source tools

**Advantages:**
- Rapid adoption
- Diverse use cases
- Network effects
- Faster innovation

**Disadvantages:**
- Less control
- Competing implementations
- Quality variance

**Author's view:** Open approach wins long-term.

## Real-World Example: Netlify and ChatGPT

### The Integration

**What Netlify did:**
- Optimized APIs for agent access
- Clear deployment semantics
- Structured responses
- Permission/scoping system
- Monitoring and safety features

**Result:**
- 1,000+ sites deploy daily directly from ChatGPT
- ChatGPT users can deploy to Netlify without authentication friction
- Agent-initiated deployments just work
- Reliability is high enough for autonomous operation

### Why This Works

**Netlify optimized for AX:**
1. APIs are deterministic (agents need predictability)
2. Error cases are clear (agents need to handle failures)
3. Permissions are scoped (agents need authorization)
4. Feedback is structured (agents need signals)
5. Side effects are safe (agents need reversibility)

**Result:** ChatGPT agents feel as natural deploying to Netlify as users do.

## Practical Implications

### For Platform Builders

**Audit your product for AX:**
1. Can agents access your APIs?
2. Are APIs deterministic?
3. Are error cases clear?
4. Can agents be authorized safely?
5. Can agents undo changes?
6. Is behavior monitorable?

**Design for agents:**
- Explicit state representations
- Clear semantics
- Structured responses
- Safe failure modes
- Observable behavior

### For API Design

**AX-conscious API principles:**

| Principle | Application |
|-----------|------------|
| Determinism | Same input → Same output always |
| Clarity | Unambiguous success/failure |
| Reversibility | Changes can be undone |
| Safety | Authorization enforced |
| Observability | Actions are logged/monitored |
| Idempotency | Safe to retry operations |

### For Product Teams

**Shift in thinking:**
- UX optimization (for humans) still important
- DX optimization (for developers) still important
- **New:** AX optimization (for agents) now critical

**Competitive advantage:**
- Companies that optimize AX early will own agent-enabled markets
- APIs optimized for agents enable new use cases
- Open approaches will scale faster

## Market Implications

### The Competitive Shift

**Today:**
- Companies compete on UX (customer experience)
- Companies compete on DX (developer adoption)
- AX is optional/secondary

**Tomorrow:**
- Companies compete on all three
- **AX becomes primary differentiator**
- Platforms with poor AX struggle to support agents
- Agent adoption determines market dominance

### Why Open Wins

**In agent economy:**
- Proprietary agents limited by single vendor
- Open APIs enable any agent to access
- Network effects favor platforms, not agents
- Competition drives agent quality
- Open platforms scale faster

## Key Takeaways

1. **Agency is the shift** — Not AI generation, but autonomous action
2. **AX is emerging discipline** — Following UX (1990s) and DX (2010s) precedent
3. **It will determine winners** — Platforms optimized for agents will dominate
4. **Open beats closed** — External agents scale faster than proprietary ones
5. **Netlify proves it works** — 1,000+ ChatGPT deployments daily show real demand
6. **API design matters** — Agents need determinism, clarity, safety
7. **Time to optimize now** — Early movers gain competitive advantage
8. **Development changes** — As dev becomes AI-assisted, AX becomes critical

## The Bottom Line

Agent Experience (AX) is emerging as a critical design discipline as AI agents become autonomous actors in digital systems. Following the precedent of User Experience (UX) revolutionizing software in the 1990s and Developer Experience (DX) in the 2010s, AX will determine which platforms thrive in the agent-enabled future. Biilmann argues that companies optimizing for agent access—with clear APIs, deterministic behavior, safe failure modes, and open permissions—will dominate their categories. The Netlify example demonstrates this works in practice: over 1,000 sites deploy daily directly from ChatGPT because the platform optimized for agent usability. As software development increasingly becomes AI-assisted, AX will shift from nice-to-have to critical competitive advantage. The winning strategy is open: platforms that enable external agents to access their services will scale faster than those attempting proprietary agent integrations. The time to optimize AX is now, during the early transition to agent-enabled systems.
