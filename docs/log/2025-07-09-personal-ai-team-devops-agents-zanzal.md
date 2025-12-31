---
summary: Owen Zanzal introduces pAI (personal AI)—a framework where DevOps engineers build personal AI agents encoded with individual standards, preferences, and decision-making, using GitHub Actions as the runtime to create lightweight agents that amplify judgment rather than replace it
event_type: blog_post
sources:
    - https://medium.com/devops-ai/you-your-tools-and-your-team-of-ai-agents-5bb4122e656d
tags:
    - personal-AI
    - pAI
    - AI-agents
    - DevOps
    - GitHub-Actions
    - automation
    - workflow-engineering
    - context-encoding
    - individual-agency
    - Owen-Zanzal
---

# You, Your Tools, and Your Team of AI Agents

**Author:** Owen Zanzal
**Platform:** Medium (DevOps+AI)
**Publication Date:** July 9, 2025
**Type:** Methodology and Architecture Guide
**Duration:** 5 min read
**Key Concept:** Personal AI (pAI) as context-aware agent framework for individual engineers

## Overview

Owen Zanzal presents a paradigm shift in how individual engineers think about AI tooling: not as generic replacements for human work, but as personalized AI agents (pAI) that encode your standards, preferences, and decision-making into the loop. Rather than treating off-the-shelf AI tools as the solution, the framework is about building your own AI team—lightweight agents that understand your context, amplify your judgment, and integrate seamlessly into existing workflows using GitHub Actions as the runtime.

The insight is that generic AI tooling misses because it lacks context. Personal AI solves this by encoding how you think, what you care about, and what constitutes good work in your domain.

## The Problem: Generic AI Tooling Misses Context

### Why Off-the-Shelf Tools Fall Short

**What tools like GitHub Copilot or AI PR reviewers lack:**
- Your personal engineering standards
- Your organization's communication norms
- The coding practices you care about
- The specific tradeoffs you weigh in your domain
- Your judgment patterns and decision-making logic

### The Core Insight

**Generic AI tooling is generic because:**
It treats all users the same, all organizations the same, all workflows the same.

**Result:**
Helpful but not contextual. Useful but not personal. Amplifying but not aligned with how you actually work.

### The DevOps Perspective

As a DevOps engineer, Zanzal noticed:
- AI tooling for infrastructure is abundant
- Most tools miss infrastructure-specific context
- None understand org-specific standards
- Few integrate naturally into existing pipelines

**What's needed:**
AI that knows how *you* think about infrastructure, not how some generic model thinks about infrastructure.

## What Is pAI (Personal AI)?

### Definition

**pAI (Personal AI):**
AI agents that are personalized to your individual standards, preferences, and decision-making, operating within your existing workflows, amplifying your judgment rather than replacing it.

### The Core Principle

```
Generic AI + Your Context = Personal AI
```

**Components:**
- Off-the-shelf LLM capability
- Your domain standards (codified)
- Your decision-making patterns (encoded)
- Your workflow integration (embedded)
- Your control and oversight (maintained)
```

### Not Autonomous Agents

**Important distinction:**
pAI is not about autonomous agents doing work independently.

**Instead:**
- You remain in the loop
- Agents amplify your decisions
- Context flows through every action
- You retain control

### The Value Proposition

pAI solves:
- Context gap (agents understand your standards)
- Scale problem (amplify across multiple tasks)
- Communication gap (agents speak your language)
- Decision support (encoded heuristics assist judgment)

## What Good pAI Looks Like: Four Example Agents

### 1. PR Review Agent

**Trigger:** PR notification

**What it does:**
1. Reviews changes using your personal heuristics
2. Sends Slack message with breakdown of what changed
3. Explains why changes might matter
4. Asks clarifying questions
5. (Optional) Checks out branch locally for quick access

**What you do:**
- Review summary and context
- Approve through bot or dig in deeper
- Maintain final decision authority

**Encodes:**
- Your code review standards
- Your communication preferences
- What details matter to you

### 2. AWS Deprecation Agent

**Trigger:** AWS deprecation email notification

**What it does:**
1. Receives deprecation notice in inbox
2. Researches the change
3. Scans your AWS accounts for impact
4. Drafts proposal with:
   - What needs to change
   - Potential impacts
   - Recommended next steps
5. Posts to org channel

**What you do:**
- Review proposal
- Answer clarifying questions
- Make edits
- Approve for distribution

**Encodes:**
- Your risk assessment standards
- Communication norms
- Escalation criteria

### 3. Terraform Diff Whisperer

**Trigger:** Terraform plan generation

**What it does:**
1. Reviews Terraform diff using your IaC principles
2. Checks against internal standards
3. Flags risky changes:
   - Data loss risks
   - Critical infrastructure replacements
4. Suggests safer alternatives:
   - create_before_destroy patterns
   - Module refactoring approaches
5. Sends Slack summary with options

**What you do:**
- Review flagged risks
- Decide: deploy as-is or adjust
- Optionally approve human-readable changelog for stakeholders

**Encodes:**
- Your infrastructure safety standards
- Preferred IaC patterns
- Risk tolerance thresholds

### 4. Observability Triage Agent

**Trigger:** Schedule or alert volume threshold

**What it does:**
1. Pulls Datadog alerts, logs, dashboards
2. Summarizes recent incidents
3. Identifies top alerts (by frequency/severity)
4. Distinguishes signal from noise
5. Suggests alert tuning or threshold changes
6. Identifies observability gaps:
   - Services without SLOs
   - Dashboards with zero views
7. Posts weekly Slack digest or opens Jira tickets

**What you do:**
- Review digest
- Prioritize cleanup work
- Delegate or act on suggestions

**Encodes:**
- What constitutes signal vs. noise
- SLO philosophy
- Observability standards

## Key Insight: These Aren't Toys

The four examples above aren't experiments or proof-of-concepts.

**They're functional agents because:**
- They embody how you work
- They encode your standards
- They reflect your communication style
- They implement your priorities
- You stay in control

**Result:**
You don't have to do everything manually anymore, but you also don't give up judgment or oversight.

## Why GitHub Actions Is the Perfect Runtime

### Natural Fit for DevOps

As a DevOps engineer, you already think in terms of:
- Pipelines
- Triggers
- YAML configuration
- Event-driven workflows
- Permissions and secrets

GitHub Actions is native to this mindset.

### Key Advantages

**1. Event-Driven**
- Trigger workflows when:
  - PR opens or changes
  - File changes
  - Scheduled times
  - External events (Slack, webhooks)

**2. Native Context**
- Embedded in codebase
- Agent has natural access to:
  - Code changes
  - Repository context
  - History and patterns
  - Team standards (in repo)

**3. Security and Auditability**
- Built-in permissions model
- Secrets management
- Complete audit logs
- Clear responsibility trails

**4. Tool Integration**
- CLI tools work naturally
- API integrations straightforward
- Slack bots easy to implement
- LLM calls simple to orchestrate

**5. Familiarity**
- Uses YAML (infrastructure-as-code mindset)
- Familiar pipeline concepts
- Standard workflow patterns
- Works with existing tools

### GitHub Actions as Runtime

**The model:**
```
GitHub Actions = Runtime for AI team
Each workflow = Lightweight agent
Each agent = Multiplier of your judgment
```

**Benefits:**
- Stays close to code
- Works naturally with DevOps tools
- Integrates with existing infrastructure
- Respects existing security models
- Requires no new platforms

## The Mindset Shift: Personal Automation Ownership

### The Old Model

**Automation was:**
- Organizational responsibility
- Central platform/tools
- Shared infrastructure
- Top-down implementation

### The New Model

**Automation becomes:**
- Individual responsibility
- Personal agent frameworks
- Integrated into personal workflow
- Bottom-up implementation

### What This Means

Each individual will:
- Build personal agents for their scope
- Define what "good automation" looks like
- Continuously evolve workflow with AI in loop
- Own their AI-enabled capabilities

**It's not:**
- Giving up shared infrastructure
- Abandoning org-wide tools
- Chaos and fragmentation

**It's:**
- Adding a personal layer on top
- Taking ownership of AI integration
- Making AI part of your role

### The Broader Implication

**From:**
"Our organization adopted this AI tool"

**To:**
"I've built this AI team that works for me"

## Implications for Hiring and Team Building

### What Hiring Looks Like Today

**Standard questions:**
- Can you write clean Terraform?
- Can you debug incidents quickly?
- Do you know Kubernetes?

### What Hiring Looks Like With pAI

**New dimensions:**
- What have you automated in your own role?
- How do you delegate to AI effectively?
- What's in your personal pAI toolkit?
- How has it improved your work?
- What systems have you built to amplify your capabilities?

### What Teams Look Like

**Before:**
Individual engineers + organizational tools

**After:**
Individual engineers + their AI teams + organizational tools

### Competitive Advantage

Hiring someone increasingly means:
- Bringing in a person with skills
- Plus their personal AI system
- Plus their workflow optimizations
- Plus their judgment-amplifying agents

**This creates:**
- Individual competitive edge
- Team capability multiplier
- Organizational advantage

## Building Your Personal AI Team

### Getting Started

**Step 1: Identify Your Workflows**
- What does a typical week look like?
- Where do you spend the most time?
- What decisions do you make repeatedly?
- Where would context help most?

**Step 2: Codify Your Standards**
- How do you think about good infrastructure?
- What communication norms matter?
- What are your decision criteria?
- Where do you want to stay in the loop?

**Step 3: Start Small**
- Pick one workflow (e.g., PR review)
- Build one agent in GitHub Actions
- Encode your standards
- Iterate and improve

**Step 4: Expand Systematically**
- Add next workflow
- Build next agent
- Connect agents
- Create team of agents

### Example Workflow: PR Review Agent

**In GitHub Actions:**

```yaml
name: Personal PR Review
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Analyze changes
        run: |
          # Use your personal standards
          # Check against your heuristics
          # Generate personalized review

      - name: Send to Slack
        run: |
          # Post summary with your context
          # Ask clarifying questions
          # Wait for your decision
```

**What it encodes:**
- Your code review standards
- Patterns you care about
- Questions you typically ask
- Communication style

## The Reality: Early Exploration

### Current State

Zanzal notes he's in early stages:
- Mapping out workflows
- Writing scaffolding
- Testing integration
- Building foundation

### Not a Side Project

The conviction is clear: this isn't experimental or optional.

**This is:**
- A new layer in how work happens
- Fundamental shift in capability
- Core to individual and team effectiveness
- Becoming essential skill

## The Open Questions

### To the Community

Zanzal invites exploration:

**What's your AI team look like?**
- What agents have you built?
- Which ones provide most value?
- Which are still experimental?

**How are you stitching it into day-to-day?**
- Integration challenges?
- Workflow friction points?
- Success patterns?

**Where does your context matter most?**
- Which decisions benefit from encoding?
- Which workflows resist automation?
- Where are the biggest gains?

## Key Principles

### 1. Context Is King

Generic AI without context = limited value
Your context + AI = amplified judgment

### 2. You Stay in the Loop

Agents amplify, not replace
Your decision authority remains
Oversight is built-in

### 3. Start With Your Standards

Not off-the-shelf AI workflows
Your standards, your communication, your judgment
Encoded into agents

### 4. GitHub Actions Is the Platform

Native to DevOps thinking
Event-driven and flexible
Secure and auditable
Integrates naturally

### 5. Ownership Matters

Not organizational automation
Your personal AI team
Your competitive edge
Your responsibility

## Key Takeaways

1. **pAI framework** — Personal AI agents encode your standards and judgment
2. **Generic tools miss context** — Off-the-shelf AI lacks your domain knowledge
3. **Four example agents** — PR Review, AWS Deprecation, Terraform Diff Whisperer, Observability Triage
4. **These aren't toys** — Functional agents that embody how you work
5. **GitHub Actions as runtime** — Natural fit for DevOps thinking
6. **Event-driven workflows** — Trigger agents on PRs, changes, schedules
7. **Native context access** — Agents embedded in codebase
8. **Security built-in** — Permissions, secrets, audit logs
9. **Mindset shift** — Automation becomes individual responsibility
10. **Not replacing shared tools** — Adding personal layer on top
11. **New hiring dimension** — What's your personal AI team?
12. **Individual competitive edge** — Brings AI team to role
13. **You amplify, don't replace** — Judgment and oversight maintained
14. **Communication encoded** — Agents speak your language
15. **Standards codified** — What good looks like in your domain
16. **Workflow integration** — Fits naturally into existing processes
17. **Start small** — One workflow, one agent, expand systematically
18. **Continuous evolution** — AI-enabled work improves over time
19. **Early exploration stage** — Not a side project, foundation for future
20. **Community collaboration** — Invite others exploring same patterns

## The Bottom Line

Owen Zanzal presents pAI (Personal AI) as a fundamental shift in how engineers think about AI tooling. Rather than adopting generic AI tools, the framework is about building your own AI team—lightweight agents that encode your standards, preferences, and decision-making, operating within existing workflows like GitHub Actions.

**The core insight:**
Generic AI misses because it lacks context. Personal AI solves this by encoding how *you* think, what *you* care about, and what constitutes good work *in your domain*.

**The four example agents:**
1. PR Review Agent — Understands your code review standards
2. AWS Deprecation Agent — Speaks your risk language
3. Terraform Diff Whisperer — Follows your IaC principles
4. Observability Triage Agent — Knows your signal vs. noise

**The platform:**
GitHub Actions is the natural runtime—event-driven, natively embedded in codebase, secure, auditable, and requires no new tools.

**The mindset shift:**
Automation ownership moves from organizational to individual. You build your AI team, define good automation for your scope, and continuously evolve how you work.

**For hiring:**
Bringing in engineers increasingly means bringing in their personal AI systems. What's in your pAI toolkit becomes as important as traditional skills.

**For work:**
You amplify your judgment rather than replace it. You stay in the loop. You maintain control while getting the benefits of AI-enhanced workflow.

**The philosophy:**
Not flashy demos. Better work. Thoughtful, efficient, human-guided work—amplified by personal AI. Your AI team becomes an extension of your capabilities, not a replacement for your judgment.

This isn't a side project or an experiment. It's the beginning of a new layer in how engineering work happens.

