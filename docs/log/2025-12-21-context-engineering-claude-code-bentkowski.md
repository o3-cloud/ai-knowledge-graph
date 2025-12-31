---
summary: Thomas Bentkowski introduces the Claude Stack—a five-layer framework (Agents, Skills, Slash Commands, Hooks, MCP Servers) for structuring context and workflows in Claude Code, emphasizing that AI agent performance directly correlates with context quality and recommending iterative building starting with simple documentation
event_type: blog_post
sources:
    - https://tbtki.com/2025/12/21/context-engineering-with-claude-code/
tags:
    - Claude-Code
    - context-engineering
    - Claude-Stack
    - agents
    - skills
    - slash-commands
    - hooks
    - MCP-servers
    - workflow-architecture
    - Thomas-Bentkowski
---

# Context Engineering with Claude Code: Building Smarter AI Workflows

**Author:** Thomas Bentkowski
**Publication:** TBTKI.com
**Publication Date:** December 21, 2025
**Modified:** December 21, 2025
**Type:** Framework and Implementation Guide
**Key Concept:** Five-layer architecture for structuring AI agent context and workflows

## Overview

Thomas Bentkowski presents the Claude Stack—a five-layer framework for organizing how Claude Code understands projects, workflows, and agent capabilities. The core thesis is deceptively simple: "AI agents are only as good as the context you give them." Context quality directly determines agent performance. Rather than treating Claude Code as a single tool, the framework organizes it as a composable stack with distinct layers that build on each other, from basic documentation through specialized agents. Bentkowski uses a Formula 1 pit crew analogy to illustrate how these layers work together, and emphasizes an iterative approach: start simple, add layers as friction emerges.

## The Central Insight: Context Is the Bottleneck

### The Core Principle

**The assertion:**
"AI agents are only as good as the context you give them."

**The implication:**
- Better context → Better agent performance
- Poor context → Poor outputs regardless of model quality
- Context quality is often the limiting factor
- Investment in context engineering pays dividends

### Why Context Matters

**What context enables:**
- Agents understand project norms and standards
- Agents make decisions aligned with values
- Agents know what "good" looks like locally
- Agents avoid mistakes from misunderstanding
- Agents coordinate with other agents

**What poor context causes:**
- Generic responses without local knowledge
- Decisions misaligned with values
- Work redone because standards weren't clear
- Agents stepping on each other
- Repeated guidance on same topics

### The Mental Model

**Quality context ≠ quantity of context**

It's about:
- Relevant information at right time
- Clear standards and values
- Accessible reference material
- Actionable guidance
- Structured for agent access

## The Claude Stack: Five Layers

### Layer Architecture

```
Layer 5: MCP Servers
        ↓ (Integrations)
Layer 4: Hooks
        ↓ (Automation)
Layer 3: Slash Commands
        ↓ (Manual triggers)
Layer 2: Skills
        ↓ (Reusable knowledge)
Layer 1: Agents
        ↓ (Specialized personas)
Foundation: Context Documentation
```

Each layer builds on foundation, adds capabilities, increases automation.

### Layer 1: Agents — Specialized Personas with Domain Expertise

**What agents are:**
Specialized personas representing domain expertise that Claude invokes autonomously when relevant.

**Characteristics:**
- Domain-specific (security reviewers, performance analysts, etc.)
- Invoked automatically when relevant
- Bring specialized perspective
- Can be stacked (multiple agents in single task)
- Context-aware (reference your standards)

**Examples of agent types:**

| Agent Type | Domain | When Invoked |
|-----------|--------|--------------|
| **Security Reviewer** | Security analysis | Code review, vulnerability assessment |
| **Performance Analyst** | Performance optimization | Latency bottleneck detection, scaling |
| **Documentation Scout** | Documentation quality | Code changes, API updates |
| **Accessibility Reviewer** | Accessibility standards | UI implementation, user interaction |
| **Cost Analyzer** | Infrastructure costs | Architecture decisions, resource allocation |

**How they work:**
- You define agent personas (instructions, standards, domain knowledge)
- Claude recognizes when a task needs that perspective
- Agent operates autonomously within defined scope
- Agents coordinate with each other

**Implementation approach:**
Start with one or two high-value agents (security, performance). Add more as you identify friction points.

### Layer 2: Skills — Reusable Knowledge Packages

**What skills are:**
Collections of procedures, best practices, supporting code, and reference material that multiple contexts can reference.

**Characteristics:**
- Reusable across projects/agents
- Contain procedures and scripts
- Include best practices
- Versioned and maintained
- Referenced by agents and commands

**Examples of skill domains:**

| Skill | Contents | Who Uses It |
|-------|----------|------------|
| **Git Workflow** | Commit conventions, branch strategy, PRs | All agents, developers |
| **Testing Standards** | Test structure, coverage requirements, patterns | Security agent, agents reviewing code |
| **Deployment Safety** | Canary deployments, rollback procedures | Deploy command, release agents |
| **Database Migrations** | Migration patterns, safety checks, rollback | All agents touching schema |
| **Incident Response** | Response procedures, escalation paths, documentation | Alert agents, incident responders |

**What goes in skills:**
- Procedures (step-by-step guidance)
- Best practices (what works in your context)
- Code templates (common patterns)
- Supporting scripts (automation helpers)
- Reference material (why these approaches)

**How agents use skills:**
When agent needs guidance, it references relevant skills rather than re-generating best practices.

**Implementation approach:**
Start by documenting one critical skill (e.g., deployment). Add more as patterns emerge.

### Layer 3: Slash Commands — Manual Workflow Triggers

**What slash commands are:**
User-triggered workflows stored as Markdown files activated by commands like `/deploy` or `/commit`.

**Characteristics:**
- User-initiated (not autonomous)
- Stored as Markdown files
- Reference agents and skills
- Standard trigger syntax
- Consistent behavior

**Examples of slash commands:**

```
/deploy — Trigger deployment workflow
  - Safety checks
  - Staging verification
  - Production promotion
  - Notification

/commit — Generate structured commit
  - Analysis of changes
  - Category detection
  - Message generation
  - Sign-off

/review — Request code review
  - Security review
  - Performance analysis
  - Test coverage check
  - Accessibility audit

/estimate — Size estimation task
  - Complexity analysis
  - Risk assessment
  - Time estimation
  - Dependencies flagged

/incident — Incident response workflow
  - Immediate triage
  - Communication template
  - Investigation structure
  - Resolution tracking
```

**How they work:**
1. User types `/command`
2. Claude looks up command definition (Markdown file)
3. Command specifies which agents/skills to use
4. Claude executes workflow using referenced context
5. Results returned to user

**Implementation approach:**
Start with 2-3 most-used workflows (e.g., `/deploy`, `/review`, `/commit`). Add more as adoption increases.

### Layer 4: Hooks — Event-Driven Automation

**What hooks are:**
Event-driven automation responding to lifecycle moments (before tool usage, session starts, before commits, etc.).

**Characteristics:**
- Triggered automatically by events
- Run before/after key moments
- Enforce standards automatically
- Operate in background
- Can block or warn

**Examples of hook triggers:**

| Hook Trigger | When | What Happens |
|------------|------|--------------|
| **session:start** | New Claude Code session | Load project context, display standards |
| **before:tool_use** | Before using tool | Validate parameters, check safety |
| **before:commit** | Before git commit | Verify message format, run tests |
| **before:deploy** | Before deployment | Safety checklist, approval workflow |
| **after:code_generation** | After code written | Auto-format, run linter, suggest tests |
| **on:pull_request** | PR created | Auto-review, label, assign reviewers |

**Benefits of hooks:**
- Standards enforced automatically
- No manual reminders needed
- Catches mistakes early
- Maintains consistency
- Reduces friction

**Implementation challenges:**
- Debugging can be difficult
- Error handling needs clarity
- Context availability varies by hook
- May slow down common operations if too many

**Implementation approach:**
Start with one high-value hook (`before:commit` for message validation). Add others carefully, monitoring for friction.

### Layer 5: MCP Servers — External Integrations

**What MCP Servers are:**
External integrations bridging Claude to APIs, databases, and tools via the Model Context Protocol (MCP) standard.

**Characteristics:**
- Follow MCP standard
- Connect to external systems
- Provide tools and resources
- Bidirectional communication
- Enable agent action outside Claude

**Examples of MCP integrations:**

| Integration | System | Capability |
|------------|--------|-----------|
| **GitHub** | Version control | PR operations, issue management, branch creation |
| **Datadog** | Monitoring | Alert querying, dashboard access, metric analysis |
| **AWS** | Cloud infrastructure | Resource querying, configuration, deployment |
| **PostgreSQL** | Database | Schema inspection, query execution, migration |
| **Slack** | Communication | Message posting, thread creation, user lookup |
| **Linear** | Issue tracking | Issue creation, status updates, linking |

**How MCP servers work:**
1. Claude recognizes need for external action
2. Invokes relevant MCP server tool
3. Server executes action in external system
4. Results returned to Claude
5. Agent processes results and continues

**Implementation approach:**
Start with read-only integrations (GitHub info, Datadog queries). Add write operations (deployments, issue creation) only after patterns stabilize.

## The Formula 1 Pit Crew Analogy

### Why This Analogy Works

**What a Formula 1 pit crew does:**
- Each member has specialized role
- Perfect coordination required
- Multiple roles work in parallel
- Clear standards and procedures
- Quick feedback and adjustment
- Team executes in seconds

**What the Claude Stack does:**
- Each layer has specialized purpose
- Coordination between layers
- Parallel execution possible
- Clear standards documented
- Quick feedback from hooks
- Efficient workflow

### Mapping the Analogy

| Pit Crew | Claude Stack | Role |
|----------|------------|------|
| **Tire change specialist** | Security Agent | Specialized expertise |
| **Fuel system technician** | Performance Analyst | Domain knowledge |
| **Team radio** | Slash Commands | Communication and coordination |
| **Pit signals** | Hooks | Real-time feedback and correction |
| **Vehicle systems** | MCP Servers | Integration with external systems |
| **Team leader** | You | Overall coordination and decisions |

### Why It Matters

Both require:
- Clear roles and responsibilities
- Perfect understanding of procedures
- Immediate feedback loops
- Consistent practice
- Continuous improvement

## Implementation Strategy: Progressive Building

### The Philosophy: Iteration Over Perfection

**Don't start by:**
- Building all five layers at once
- Creating comprehensive documentation
- Implementing all agents
- Setting up all MCP servers

**Do start by:**
- Basic context documentation
- One or two high-value agents
- Simple slash commands
- Feedback loops to identify friction

### The Three-Phase Approach

#### Phase 1: Foundation (Week 1-2)

**What to build:**
- Basic project context documentation
- README for agents
- One critical skill (e.g., deployment process)
- Document current pain points

**How to start:**
```
1. Write down your project standards
2. Document how you currently work
3. Identify most repeated workflows
4. Create basic agent personas
```

**Expected outcome:**
- Clear picture of what agents should know
- One skill documented
- Baseline for improvement

**Effort:** Low (4-8 hours)

#### Phase 2: Automation (Week 3-4)

**What to build:**
- 2-3 slash commands for critical workflows
- One simple agent (security or performance)
- Basic hooks for validation
- Skills for those workflows

**How to expand:**
```
1. Implement /deploy or /commit command
2. Define one specialized agent
3. Add one before-commit hook
4. Document skill for that workflow
```

**Expected outcome:**
- Manual workflows automated
- Specialized perspective available
- Feedback loop operational
- Team sees value

**Effort:** Medium (8-16 hours)

#### Phase 3: Integration (Week 5+)

**What to build:**
- Additional agents as friction emerges
- MCP servers for external systems
- More sophisticated hooks
- Growing skill library

**How to scale:**
```
1. Monitor usage patterns
2. Add agents where decisions are repeated
3. Integrate with critical systems
4. Build comprehensive skill library
```

**Expected outcome:**
- Comprehensive AI augmentation
- Deep integration with workflow
- Measurable efficiency gains
- Team comfortable delegating to Claude

**Effort:** Ongoing (continuous improvement)

## Real-World Implementation Challenges

### Challenge 1: Agent Refinement Requires Multiple Cycles

**The reality:**
First agent definition rarely gets it right.

**What happens:**
- Agent makes mistakes
- You refine instructions
- Agent's behavior shifts
- More refinement cycles
- Eventually reaches steady state

**Time to proficiency:** 3-5 iterations per agent

**Best practice:**
- Start with narrow scope
- Tighten incrementally
- Monitor edge cases
- Document learnings

### Challenge 2: Hooks Are Powerful but Hard to Debug

**The challenge:**
Hooks run automatically, making problems hard to spot.

**Common issues:**
- Hook runs at wrong time
- Context unavailable at hook stage
- Performance degradation
- Silent failures

**Debugging difficulty:** High (logs may not be available)

**Best practice:**
- Start with logging hooks
- Test extensively in development
- Monitor in production
- Have kill switch for problematic hooks

### Challenge 3: Context Complexity Grows Over Time

**The problem:**
As you add layers, context becomes complex.

**What happens:**
- Skill library grows
- Agent definitions become detailed
- Command complexity increases
- Hook interactions compound
- Hard to modify safely

**Management strategy:**
- Regular documentation review
- Deprecate unused elements
- Refactor duplicate skills
- Keep each component focused

## Best Practices for Claude Stack Implementation

### 1. Start Simple, Add Complexity Gradually

Don't try to build everything at once.
Each layer has value independently.
Add next layer only when previous is stable.

### 2. Document Everything

- Why decisions were made
- What agent personas do
- How skills relate to standards
- When hooks trigger and why
- MCP server capabilities

Without documentation, stack becomes opaque and hard to maintain.

### 3. Measure Impact

Track:
- Time saved by automations
- Errors caught by agents
- Standards enforced by hooks
- Integrations used most

Use data to decide where to expand.

### 4. Keep Agents Focused

Don't create agents that do everything.

Better to have:
- Security agent (focused on security)
- Performance agent (focused on performance)

Than:
- Super agent (does everything, masters nothing)

### 5. Version Your Context

Like code, context evolves.

Track:
- Agent definition versions
- Skill changes
- Hook modifications
- MCP server updates

Enables rollback if something breaks.

### 6. Test Your Workflows

Before deploying workflows broadly:
- Test slash commands manually
- Verify agent outputs
- Check hook behavior
- Validate MCP integrations

Production-ready context prevents problems.

## Key Takeaways

1. **Context is bottleneck** — Quality context determines agent performance
2. **Claude Stack framework** — Five-layer architecture for context organization
3. **Layer 1: Agents** — Specialized personas with domain expertise
4. **Layer 2: Skills** — Reusable knowledge and procedures
5. **Layer 3: Slash Commands** — Manual workflow triggers
6. **Layer 4: Hooks** — Event-driven automation
7. **Layer 5: MCP Servers** — External system integrations
8. **Progressive building** — Start simple, add layers as friction emerges
9. **Phase approach** — Foundation, automation, integration
10. **Agent refinement** — Multiple iterations to proficiency
11. **Hook debugging** — Challenging; start with logging
12. **Context complexity** — Grows over time; requires management
13. **Documentation critical** — Without it, stack becomes opaque
14. **Measurement matters** — Track impact to guide expansion
15. **Focused agents better** — Specialized agents outperform generalists
16. **Version your context** — Track changes for rollback capability
17. **Test workflows** — Verify before broad deployment
18. **Formula 1 analogy** — Specialized roles, coordination, procedures
19. **Iteration over perfection** — Get something working, refine continuously
20. **Value compounds** — Each layer enables better performance of others

## The Bottom Line

Thomas Bentkowski presents the Claude Stack as a systematic framework for structuring how Claude Code understands and operates within your projects. The core insight—"AI agents are only as good as the context you give them"—positions context engineering as the primary lever for improving agent performance.

**The five-layer architecture:**
1. **Agents** — Specialized personas representing domain expertise
2. **Skills** — Reusable knowledge and procedures
3. **Slash Commands** — Manual workflow triggers
4. **Hooks** — Event-driven automation
5. **MCP Servers** — External system integrations

**The implementation philosophy:**
Start with basic documentation and one or two high-value agents. Add layers progressively as you identify friction points. Don't try to build everything at once.

**The challenges:**
- Agents require multiple refinement cycles
- Hooks are powerful but hard to debug
- Context complexity grows over time

**For practitioners:**
The Claude Stack provides a composable, layered approach to AI integration. Rather than treating Claude Code as a single tool, organize it as a coordinated system where each layer builds on previous ones. Start with Phase 1 (foundation), move to Phase 2 (automation), then Phase 3 (integration).

**The Formula 1 analogy:**
Just as pit crews coordinate specialized roles for peak performance, the Claude Stack coordinates specialized agents, skills, triggers, and integrations for optimal workflow enhancement.

**The final principle:**
Context quality determines outcomes. Invest in clear, accessible, well-structured context, and agents will perform at their best. Neglect context, and even powerful agents will miss the mark.

The Claude Stack is not a tool—it's a way of thinking about how to make Claude Code a fundamental part of your development workflow through structured, layered context engineering.

