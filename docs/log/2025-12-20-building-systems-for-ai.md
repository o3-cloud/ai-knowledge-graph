---
summary: Adam Tankanow applies DevOps principles to AI governance—systems thinking for visibility, feedback loops for cost control, and safe experimentation culture to prevent costly mistakes in AI deployment
event_type: article
sources:
    - https://www.cloudzero.com/blog/building-systems-for-ai/
tags:
    - AI-governance
    - DevOps
    - systems-thinking
    - cost-management
    - risk-management
    - AI-operations
    - organizational-practice
    - infrastructure
---

# Building Systems for AI: Lessons from DevOps History

**Author:** Adam Tankanow
**Publication:** CloudZero Blog
**Publication Date:** December 20, 2025

## Overview

Tankanow draws critical parallels between the chaotic early cloud computing era and today's enthusiastic AI adoption. He argues that successful AI governance requires applying proven DevOps principles—systems thinking, feedback loops, and experimentation culture—to manage costs and risks. The core insight: "systems thinking" matters more than tool selection or raw capability.

## The Parallel: Cloud Chaos Then, AI Chaos Now

### Early Cloud Era
- Unlimited provisioning, no visibility
- Massive bills with no clear owner
- Innovation without guardrails
- Reactive crisis management

### Current AI Adoption
- Unlimited API calls, no cost visibility
- Massive bills appearing suddenly
- Innovation without governance
- Reactive crisis management

**The Pattern:** Enthusiasm without systems causes expensive chaos.

## The Three Ways Applied to AI

### The First Way: Systems Thinking

**The Problem:**
Most organizations approach AI adoption without understanding the system:
- How many prompts are running?
- Which models are being used?
- What are the token costs?
- Where are the bottlenecks?

**Without visibility, optimization is impossible.**

**Systems Thinking for AI Requires:**

| Component | Understanding Needed |
|-----------|----------------------|
| Prompts | What's being asked, how frequently |
| Models | Which models, costs per use case |
| Tokens | Input/output distribution, waste patterns |
| Costs | Per feature, per team, per user |
| Latency | Response times, user experience impact |
| Quality | Accuracy metrics, hallucination rates |

**The Insight:**
Teams must see the entire system—not just individual prompts or models, but how they interact, cascade, and accumulate costs.

**Implementation:**
- Instrument AI pipelines for observability
- Track metrics across the stack
- Connect costs to business outcomes
- Identify system bottlenecks
- Understand interdependencies

### The Second Way: Feedback Loops

**The Problem:**
Unmanaged AI is "a Ferrari without brakes." Sending prompts into production without validation creates:
- Cascading failures
- Unexpected costs
- Quality degradation
- Liability exposure

**The Solution: Structured Workflows with Human Checkpoints**

**Traditional model:** Prompt → AI → Production
**Managed model:** Prompt → AI → Validation → Checkpoint → Production

**Feedback Loop Architecture:**

```
Planning → Execution → Validation → Learning → Adjustment
   ↑                                              ↓
   └──────────────────────────────────────────────
```

**Key Checkpoints:**
1. **Pre-deployment** — Validate prompt quality, test outputs
2. **During execution** — Monitor token usage, cost, quality
3. **Post-execution** — Measure outcomes, identify issues
4. **Learning cycle** — Apply insights to improve prompts/models

**Result:** Problems caught before they cascade. Costs visible in real-time.

### The Third Way: Experimentation Culture

**The Problem:**
Innovation requires experimentation, but unconstrained experimentation is expensive. Most organizations either:
- Lock down AI (kills innovation)
- Enable unrestricted use (budget hemorrhage)

**The Solution: Safe Sandbox with Guardrails**

**"A sandbox filled with Monopoly money"**

Create environments where:
- Teams can experiment freely
- Costs are capped and visible
- Failures are acceptable
- Learning is systematic

**Safe Experimentation Design:**

| Element | Purpose |
|---------|---------|
| Budget limits | Prevents budget surprises |
| Monitoring | Visibility into what's happening |
| Automated gates | Prevent accidental production deployment |
| Historical data | Learn from past experiments |
| Shared learnings | Don't repeat mistakes |

**Impact:** Innovation thrives within guardrails. Failures become learning opportunities, not budget crises.

## Critical Insights

### Liability Doesn't Disappear—It Shifts

**The Myth:**
"AI does it, so we're not responsible."

**The Reality:**
AI doesn't eliminate code liability; it transfers it. Humans remain responsible for:
- What the AI decides
- How the AI is deployed
- Outcomes the AI produces
- Failures the AI causes

**Implication:**
Governance structures aren't optional—they're liability management infrastructure.

### Microservices Governance Applies to AI

**Proven patterns from DevOps:**

| DevOps Practice | AI Equivalent |
|-----------------|---------------|
| Version control | Model versioning, prompt versioning |
| Service validation | Prompt testing, output validation |
| Deployment gates | Quality checks before production |
| Observability | Cost, latency, quality monitoring |
| Rollback capability | Revert to previous prompts/models |
| SLO/SLA tracking | Response time, quality guarantees |

**Key insight:** AI governance isn't new—it's applying proven infrastructure patterns to a new domain.

### Prevention > Crisis Management

**Reactive approach (expensive):**
- Wait for cost overrun → Panic
- Wait for quality failure → Crisis
- Wait for security issue → Breach

**Proactive approach (effective):**
- Build governance before scale
- Establish visibility immediately
- Create feedback loops from day one
- Test safe experimentation early

**Cost difference:** Significant. Organizations with proactive governance spend 30-50% less on AI operations.

## The Three Principles in Practice

### Systems Thinking Example: Cost Attribution

**Without systems thinking:**
```
AI bill: $50,000/month
Questions: Where did it come from?
Answer: Unknown
```

**With systems thinking:**
```
AI costs breakdown:
- Feature A (customer support): $30,000 (60% of budget)
- Feature B (content generation): $15,000 (30% of budget)
- Feature C (analytics): $5,000 (10% of budget)
```

**Result:** Can optimize highest-impact areas first.

### Feedback Loops Example: Prompt Evolution

**Without feedback loops:**
- Deploy prompt → Hope it works → Deal with issues

**With feedback loops:**
1. Draft prompt
2. Test on 100 samples → Measure quality
3. Check cost per request → Measure efficiency
4. Deploy to 10% of users → Monitor real-world performance
5. Adjust based on feedback
6. Roll out to 100% with confidence

**Result:** Higher quality, predictable costs, reduced risk.

### Experimentation Culture Example: Model Selection

**Without safe sandbox:**
- Engineering wants to try GPT-4
- Finance says "too expensive"
- Nothing happens

**With safe sandbox:**
- Engineering allocates $1,000 test budget
- Compares GPT-4 vs GPT-3.5 vs Claude
- Measures quality difference
- Decides based on data
- Applies learnings organization-wide

**Result:** Evidence-based decisions, controlled innovation.

## Organizational Implications

### What Leadership Should Do

1. **Establish AI governance before scale**
   - Don't wait for budget overruns
   - Build infrastructure early
   - Invest in observability

2. **Create accountability structures**
   - Cost ownership by team
   - Quality metrics visibility
   - Feedback loops to teams

3. **Enable safe experimentation**
   - Budget for learning
   - Fail fast, learn faster
   - Share results across organization

### What Engineering Should Do

1. **Instrument everything**
   - Track prompts, models, tokens
   - Monitor costs in real-time
   - Log quality metrics

2. **Build validation gates**
   - Pre-deployment testing
   - Production monitoring
   - Rollback capability

3. **Document and share learning**
   - What prompts work
   - Which models fit which tasks
   - Cost optimization insights

### What Product Should Do

1. **Include AI governance in roadmap**
   - Observability features
   - Cost tracking
   - Quality monitoring

2. **Design with costs in mind**
   - Efficient prompts
   - Model stratification
   - Caching where possible

3. **Measure AI impact systematically**
   - User satisfaction
   - Operational cost
   - Reliability metrics

## Key Takeaways

1. **Systems thinking first** — Visibility into prompts, models, tokens, and costs is mandatory before optimization
2. **Feedback loops prevent cascades** — Structured workflows with human checkpoints catch problems early
3. **Safe sandbox culture** — Enable innovation with guardrails, not prohibition
4. **Liability remains** — AI doesn't eliminate responsibility; it transfers it
5. **Microservices patterns apply** — DevOps governance directly translates to AI operations
6. **Prevention over crisis** — Build governance structures before they're desperately needed
7. **Cost attribution matters** — Understand where money actually goes before trying to optimize
8. **Shared learning accelerates** — Document and distribute insights across organization

## The Bottom Line

Building systems for AI requires applying proven DevOps principles—systems thinking for visibility, feedback loops for cost control, and safe experimentation culture for innovation. The parallel to early cloud computing is instructive: organizations that embrace governance structures early thrive, while those that allow unconstrained innovation pay dearly. The core insight is that "systems thinking" matters more than tool selection, model capability, or raw innovation velocity. Success requires deliberate, systematic approaches that prevent expensive mistakes while enabling rapid learning. By treating AI governance as infrastructure work—not as bureaucracy—organizations can scale AI responsibly and sustainably, capturing innovation benefits while maintaining cost control and quality standards.
