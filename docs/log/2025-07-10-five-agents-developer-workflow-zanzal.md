---
summary: Owen Zanzal explores the paradigm shift when developers work with multiple coordinated AI agents instead of a single tool—showing how the role transforms from operator to orchestrator, introducing management challenges (task ownership, escalation, duplication) and requiring invisible team coordination while maintaining human oversight
event_type: blog_post
sources:
    - https://medium.com/devops-ai/what-changes-when-developers-work-with-five-agents-not-one-37f78b531b0d
tags:
    - multi-agent-systems
    - developer-workflow
    - orchestration
    - async-agents
    - task-management
    - team-coordination
    - AI-integration
    - DevOps
    - Owen-Zanzal
---

# What Changes When Developers Work with Five+ Agents, Not One?

**Author:** Owen Zanzal
**Platform:** Medium (DevOps+AI)
**Publication Date:** July 10, 2025
**Type:** Workflow Evolution and Management Patterns
**Duration:** 4 min read
**Key Concept:** Transition from single-tool usage to multi-agent orchestration and invisible team management

## Overview

Owen Zanzal explores the fundamental shift in developer experience when moving from single AI tools (like Copilot) to managing teams of coordinated AI agents. The insight is that while one agent feels like a productivity tool, five agents feel like managing a junior team—asynchronous, invisible, tireless, but requiring real management: task ownership, feedback loops, escalation paths, and invisible coordination. The role transforms from operator (doing work) to orchestrator (managing work being done on your behalf).

## The Quiet Shift Happening

### From One Tool to Many

**What most people know:**
- Copilot for quick refactors
- ChatGPT for tricky regex
- One-off AI assistance

**What's changing:**
- Not asking AI to help with one task
- Asking AI to handle ongoing responsibilities
- Not just in terminal or one tool
- Across entire workflow
- Multiple agents working in parallel
- Invisible background coordination

### The Boundary

**Single agent feels like:**
- Tool
- Sidekick
- Chatbot you query
- Quick wins

**Multiple agents feel like:**
- Team
- Invisible coworkers
- Background processes
- Coordination challenge

## The Progression

### Stage 1: Single Agent (Easy)

**Experience:**
- Spin up one agent
- Assign one task (triage inbox, summarize PR, suggest tests)
- Runs in background
- You check Slack or grab coffee
- One task delegated
- Feels like productivity win

**Complexity level:** Low

**Management overhead:** Minimal

### Stage 2: Adding Agents (Compound)

Then you add another.

And another.

**What changes:**
- No longer just writing code
- Managing small team
- Team is asynchronous
- Team is invisible
- Team is tireless
- Team needs context
- Team needs feedback on failures
- Team doesn't know when they're wrong unless told

**Complexity level:** Compounds non-linearly

**Management overhead:** Significant

## The Core Insight: This Is a Management Problem

### Not a Tooling Problem

**Wrong framing:**
"How do we make agents better?"

**Right framing:**
"How do we manage multiple async agents well?"

### Why This Matters

**At one agent:**
- Tooling makes a big difference
- Better model = better results
- Easy to debug

**At five agents:**
- Tooling is table stakes
- Management is the limiting factor
- Coordination is the bottleneck
- Visibility is critical

## The Role Transformation: Operator to Orchestrator

### What Changes

**From Operator:**
- You do the work
- Direct execution
- Clear cause-and-effect
- Single point of failure = you

**To Orchestrator:**
- You manage work being done
- Indirect execution (through agents)
- Complex dependencies and interactions
- Multiple points of failure
- Responsible for outcomes you don't directly produce

### Familiar Management Challenges

Working with multiple agents introduces challenges that sound like managing junior team members:

**1. Task Ownership**
- Who is responsible for what?
- Clear assignments essential
- No ambiguity

**2. Escalation Paths**
- When does an agent need to escalate?
- What constitutes "ask me first"?
- What can be decided independently?

**3. Duplication**
- Are two agents doing the same thing?
- Overlapping responsibilities
- Wasted effort

**4. Degraded Performance**
- Agent A finishes, waits on Agent B
- Blocking dependencies
- Async coordination challenges

**5. Unclear Feedback Loops**
- How does agent know it did poorly?
- How does it learn from mistakes?
- No visibility unless you build it

### Why It's Familiar

"Sound familiar? That's because this isn't a tooling problem — it's a management one."

These are classic team management challenges. Except now:
- No standups
- No calendar invites
- No visibility unless you build it
- Completely asynchronous
- Invisible unless explicitly surfaced

## The Hypothetical Day: Multi-Agent Workflow

### 9:00 AM — Start with Your Team (Not Email)

**PR Diff Auditor agent:**
- Reviewed five pull requests overnight
- Flagged risky database changes in one
- Noted reduced test coverage in another
- Suggested merging two clean, well-documented PRs

**Your work:**
- Review agent's analysis
- Approve what's ready
- Leave feedback where it missed
- Loop in teammates for second opinions where needed

**Management pattern:**
Quick validation and delegation decisions.

### Late Morning — Cross-Functional Planning Meeting

**Meeting Transcriber Agent:**
- Listens to cross-functional planning meeting (Payments team)
- Captures full discussion
- Distills timestamped summary
- Delivers before meeting ends

**Plan Builder Agent:**
- Receives transcript from Meeting Transcriber
- Extracts key objectives
- Identifies constraints
- Surfaces risks
- Flags open questions
- Drafts execution plan within an hour
- Links to relevant repos
- References previous migrations
- Flags dependencies you hadn't surfaced

**Your work:**
- Conduct actual meeting (human-focused)
- Review Plan Builder output
- Validate or adjust
- Approve for team sharing

**Management pattern:**
Coordinated pipeline: Meeting Transcriber → Plan Builder. Your oversight at each step.

### Mid-Day — Alert Management

**Ping from Alert Triage Agent:**
- High-priority incident detected
- Summarized Datadog alert
- Correlated logs
- Scoped affected services
- Proposed three mitigation paths

**Your work:**
- Review three options
- Tweak one
- Approve mitigation plan
- Click to execute

**Management pattern:**
Structured decision point. Agent does analysis, you decide.

### Lunch — Progress Visibility

**Progress Tracker agent:**
- Reports on all running agents
- Infra Refactor Assistant: Stuck, no progress

**Your work:**
- Identify blocker
- Pull branch locally
- Pair with IDE-based agent
- Push across finish line
- Push back up
- Notify PR reviewer

**Management pattern:**
Monitoring and intervention when blocked.

### Late Afternoon — Continuous Improvement

**Feedback Synthesizer agent:**
- Reviews today's agent logs
- Analyzes comments
- Reads ME.md (personal standards document)
- Surfaces three suggestions:
  1. Tighten acceptance criteria for Planning Scout
  2. Update Alert Triage escalation policy
  3. Set check-in timer for Infra Refactor when progress stalls

**Your work:**
- Review suggestions
- Implement improvements
- Refine agent instructions
- Adjust policies

**Management pattern:**
Retrospective and continuous improvement cycle.

### End of Day — Cross-Team Opportunity

**Cross-Team PR Sentinel agent:**
- Found PR in another repo
- Changes match your expertise
- Drafted review summary
- Highlighted concerns
- Asks: "Want to take a look before it ships?"

**Your work:**
- Look at PR
- Leave two comments
- Log off

**Management pattern:**
Agent surfaces opportunities for your contribution outside immediate scope.

### The Summary

**What actually happened today:**
- You didn't do everything
- But your team did
- You orchestrated, validated, decided, improved
- Invisible team worked in parallel
- You stayed in loop where it mattered

## Key Operational Patterns

### Pattern 1: Agent Specialization

**Each agent owns:**
- Specific task or responsibility
- Clear scope
- Defined triggers
- Expected outputs

**Examples:**
- PR Diff Auditor → Code review
- Alert Triage Agent → Incident response
- Meeting Transcriber → Meeting notes
- Plan Builder → Planning documentation

### Pattern 2: Agent Pipelines

**Agents work in sequence:**

```
Meeting Transcriber
    ↓ (output)
Plan Builder
    ↓ (output)
Your review and approval
    ↓ (feedback)
Distribution
```

**Benefit:**
Structured information flow.

### Pattern 3: Async Coordination

**Agents run in parallel:**
- No waiting for human
- Work happens while you're in meetings
- Results ready when you return
- Asynchronous by design

### Pattern 4: Human Validation Points

**You stay in loop at:**
- Decision points
- Risk assessments
- Escalation situations
- Quality assurance
- Policy updates

### Pattern 5: Feedback Integration

**Agents improve through:**
- Your comments and feedback
- ME.md updates (personal standards)
- Policy adjustments
- Escalation rules refinement

## Management Requirements

### What You Need to Build

**1. Visibility Systems**
- Progress tracker
- Agent status dashboard
- Failure notifications
- Output logs

**2. Feedback Mechanisms**
- How agents receive feedback
- How they adjust behavior
- How standards are communicated
- How policies are updated

**3. Escalation Paths**
- What requires human decision
- What agents can decide independently
- When to escalate
- How to escalate

**4. Context Repository**
- ME.md or equivalent
- Your standards documented
- Your preferences encoded
- Your decision-making logic

**5. Coordination Mechanisms**
- How agents sequence work
- How to handle dependencies
- How to avoid duplication
- How to share context

### The Overhead

**This overhead is real:**
- Visibility systems to build
- Feedback loops to establish
- Policies to define
- Coordination to manage

**But the tradeoff:**
- You multiply your output
- Agents handle routine work
- You focus on decisions and strategy
- Work happens asynchronously

## The Role of ME.md

### What Is ME.md?

Personal standards document that agents reference:
- Your decision-making principles
- Your code standards
- Your communication preferences
- Your risk tolerance
- Your escalation criteria

### Why It Matters

**Without ME.md:**
- Agents must infer your preferences
- Inconsistent behavior
- Frequent misses
- Lots of correction cycles

**With ME.md:**
- Agents have explicit guidance
- Consistent behavior
- Fewer misses
- Self-correcting over time

### Examples of ME.md Content

```
## Code Standards
- Test coverage minimum: 80%
- PR size: max 400 lines
- Commit messages: conventional format

## Communication Style
- Tone: Direct but collaborative
- Escalations: Flag and ask before acting
- Explanations: Short summaries preferred

## Risk Tolerance
- Database changes: Always ask first
- Breaking changes: Require approval
- Infrastructure: Run by me
- Tests: Can auto-merge if green

## Decision-Making
- When in doubt: Ask
- Precedent: Reference previous decisions
- Trade-offs: Show all options
```

## Emerging Developer Skills

### New Competencies Needed

**1. Agent Management**
- How to task agents
- How to give feedback
- How to coordinate them
- How to measure their work

**2. Context Engineering**
- Documenting standards (ME.md)
- Making implicit explicit
- Keeping context current
- Communicating through artifacts

**3. Async Coordination**
- Working with async feedback
- Non-blocking workflows
- Parallel execution
- Result validation

**4. Visibility Ownership**
- Building dashboards
- Monitoring agents
- Surfacing blockers
- Continuous improvement

## Key Takeaways

1. **Shift from operator to orchestrator** — Managing agents, not just doing work
2. **Single agent feels easy** — One task delegated, minimal management
3. **Multiple agents compound complexity** — Non-linear increase in coordination needs
4. **Management, not tooling** — The limiting factor at scale
5. **Familiar team challenges** — Task ownership, escalation, duplication, dependencies
6. **Invisible team** — Asynchronous, no standups, no visibility unless built
7. **Hypothetical day structure** — Progress tracking, decision points, feedback loops
8. **Agent specialization** — Each owns specific task or responsibility
9. **Agent pipelines** — Sequential workflows with human validation points
10. **Async coordination** — Parallel execution while you're in meetings
11. **Human validation required** — Stay in loop at decisions, risks, escalations
12. **Visibility systems needed** — Progress tracking, status, failures
13. **Feedback mechanisms essential** — How agents learn and improve
14. **ME.md as context repository** — Your standards made explicit
15. **Escalation paths clear** — When agents ask vs. decide independently
16. **Coordination overhead real** — But offset by multiplied output
17. **Progress tracker pattern** — Monitor all agents, intervene when blocked
18. **Feedback synthesizer pattern** — Continuous improvement from agent logs
19. **Emerging developer skills** — Agent management, context engineering, async coordination
20. **Workflow transformation** — From direct execution to orchestrated delegation

## The Bottom Line

Owen Zanzal reveals the hidden complexity of multi-agent workflows: the shift from operator (doing work) to orchestrator (managing work being done on your behalf).

**The core insight:**
While one agent feels like a productivity tool, five agents feel like managing a junior team. The challenges are familiar (task ownership, escalation, duplication, dependencies) but harder because the team is:
- Asynchronous
- Invisible
- Tireless
- Without natural human communication

**The hypothetical day shows:**
- 9am: PR Diff Auditor validates overnight work
- Late morning: Meeting Transcriber → Plan Builder pipeline
- Mid-day: Alert Triage decision point
- Lunch: Progress Tracker surfaces blocker; you intervene
- Afternoon: Feedback Synthesizer enables continuous improvement
- EOD: Cross-Team PR Sentinel surfaces opportunities

**What this requires:**
- Visibility systems (progress tracking, monitoring)
- Feedback mechanisms (how agents learn)
- Escalation paths (what requires human decision)
- Context repository (ME.md for standards)
- Coordination systems (avoiding duplication, handling dependencies)

**The management overhead:**
Real and significant. But the tradeoff is that you multiply your output while staying in control.

**For developers:**
The developer experience is changing. You're not just writing code anymore—you're orchestrating invisible teams. The skills that matter are shifting: from individual execution to team coordination, from direct work to management.

**The final insight:**
"When you're not working alone anymore, your workflow can't stay the same."

The role transforms from operator to orchestrator. The challenges transform from individual productivity to team management. The opportunity transforms from getting more done yourself to multiplying your impact through coordinated agents.

This is the future of development: invisible teams, asynchronous coordination, human oversight, orchestrated execution.

