---
summary: Anthropic engineers present Skills—a minimal, portable form factor for packaging procedural knowledge that agents can dynamically load to acquire domain expertise and specialized capabilities
event_type: video
sources:
    - https://www.youtube.com/watch?v=CEvIs9y1uog
tags:
    - AI-skills
    - agent-architecture
    - domain-expertise
    - capability-abstraction
    - procedural-knowledge
    - Anthropic
    - reusable-expertise
---

# Don't Build Agents, Build Skills Instead

**Speakers:** Barry Zhang & Mahesh Murag (Anthropic)
**Platform:** AI Engineer
**Upload Date:** December 8, 2025

## Core Thesis

Rather than building monolithic agents with hard-coded capabilities, build **Skills**—minimal, portable form factors for packaging procedural knowledge that agents can dynamically load and compose. This enables agents to acquire domain expertise and specialized capabilities for real-world work.

## The Agent Gap

Despite rapid advancement in model intelligence and convergence on agent scaffolding, a critical gap remains: **agents lack domain expertise and specialized knowledge needed for real-world work**.

Problems with traditional agent design:
- Hard-coded capabilities don't transfer across domains
- No mechanism for agents to acquire new expertise dynamically
- Monolithic implementations couple intelligence with domain knowledge
- Limited composability—agents can't leverage capabilities from other domains

## Skills as Solution

**Skills** represent a new approach: minimal packaging of procedural knowledge.

### Key Characteristics

**Portable:** Skills can be applied across different domains and use cases. A skill for API interaction is reusable whether calling payment APIs, analytics APIs, or data transformation services.

**Composable:** Agents dynamically load and combine multiple skills. Single skill focuses on narrow domain expertise; agents orchestrate skills to solve complex problems.

**Minimal Form Factor:** Skills are lightweight—not full agent frameworks, not extensive documentation. Procedural knowledge sufficient to execute specialized task.

**Dynamically Loadable:** Agents discover and load appropriate skills at runtime based on task requirements. No static predefinition of agent capabilities.

**Reusable Expertise:** Skills encode hard-won domain knowledge—patterns, edge cases, best practices—making them valuable across many agent deployments.

## How Anthropic Built Skills

Implementation approach:
1. **Identify Core Procedures:** Extract procedural knowledge—step-by-step approaches to common domain tasks
2. **Package as Skills:** Encode procedures as minimal, well-defined components
3. **Create Discovery Mechanism:** Enable agents to find and load appropriate skills for given task
4. **Define Composition Interface:** Standardize how agents invoke and combine skills
5. **Support Feedback Loops:** Enable agents to refine and improve skills from experience

## Network Effects

Skills enable powerful network effects:

**Skill Marketplace:** As more domain experts create skills, agents gain access to wider expertise without reimplementation.

**Cross-Domain Transfer:** Skills developed for one domain become foundations for adjacent domains.

**Community Contribution:** External developers create skills, multiplying available expertise without central team building everything.

**Cumulative Knowledge:** Skills improve over time as agents use them, discover edge cases, and provide feedback.

## Emergent Capability: Agents Writing Skills

Anthropic's vision extends to **agents autonomously writing their own skills from experience**:

- Agents recognize patterns in repeated task execution
- Extract generalizable procedures from experience
- Package as reusable skill
- Share with agent ecosystem
- Other agents benefit immediately

This represents move from static capability distribution to dynamic, self-improving agent ecosystem.

## Advantages Over Traditional Agent Design

### Modularity
Single-purpose skills are easier to reason about, test, and improve than monolithic agents.

### Scalability
Adding domain expertise doesn't require retraining agents or modifying core architecture—new skills simply mounted.

### Transferability
Skills developed for one agent context apply to other agents, domains, and organizations.

### Interpretability
Focused procedural skills more interpretable than general agent reasoning across all domains.

### Maintainability
When skill fails, update skill logic, not agent architecture. Changes isolated to specific domain.

### Testability
Skills with clear inputs, outputs, and procedures easier to test than integrated agent systems.

## Real-World Applications

Skills enable agents to handle:
- **Technical Integration:** API interaction, data transformation, system integration
- **Domain Expertise:** Financial analysis, medical knowledge, legal reasoning
- **Workflow Execution:** Multi-step procedures, edge case handling, error recovery
- **Specialized Tools:** Complex software operation, specialized hardware control
- **Knowledge Application:** Drawing from accumulated expertise in narrow domain

## The Shift

Skills represent shift from:
- ❌ "Build agents with hard-coded capabilities"
- ✅ "Equip agents with dynamically loadable domain expertise"

From:
- ❌ "One agent, many capabilities"
- ✅ "Many reusable skills, flexibly composed by agents"

## Key Insight

**Domain expertise is distinct from agent intelligence.** Models excel at reasoning and coordination; domain expertise (procedures, edge cases, best practices) should be packaged separately, enabling reuse and specialization.

Agents should be orchestrators of skills, not repositories of all knowledge.

## Future Vision

Anthropic's thesis points toward:
1. **Rich skill ecosystems** capturing organizational and domain knowledge
2. **Skill marketplaces** enabling knowledge exchange between teams and organizations
3. **Self-improving agents** that discover patterns and write new skills autonomously
4. **Composable intelligence** where capabilities combine flexibly for novel problems
5. **Decentralized expertise** where knowledge distribution doesn't require central control

## Speakers

**Barry Zhang** - https://twitter.com/barry_zyj
**Mahesh Murag** - https://twitter.com/MaheshMurag

Both from Anthropic's team exploring next-generation agent architectures.

## Implications

For organizations building agent systems:
- Don't hard-code all capabilities into agent logic
- Extract and package reusable domain procedures as skills
- Design skill discovery and composition interfaces
- Plan for skills to improve over time
- Consider how to enable agent autonomy in skill development
