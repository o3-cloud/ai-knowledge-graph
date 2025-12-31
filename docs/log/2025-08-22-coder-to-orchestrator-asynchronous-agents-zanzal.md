---
summary: Owen Zanzal shares early lessons on shifting from solo coder to orchestrator of asynchronous AI agents—managing artifacts, aligning cadence, controlling WIP, and leading a tiny invisible team through structured feedback and clear specifications
event_type: blog_post
sources:
    - https://medium.com/devops-ai/from-coder-to-orchestrator-my-early-lessons-with-asynchronous-ai-agents-edfc20c9f1ac
tags:
    - asynchronous-agents
    - agent-orchestration
    - AI-team-management
    - artifact-specification
    - work-in-progress
    - cadence
    - delegation
    - AI-workflows
    - productivity
    - mindset-shift
---

# From Coder to Orchestrator: My Early Lessons with Asynchronous AI Agents

**Author:** Owen Zanzal
**Platform:** Medium (DevOps+AI)
**Publication Date:** August 22, 2025
**Type:** Personal Narrative and Framework
**Duration:** 3 min read
**Key Insight:** Role transformation from individual contributor to manager of invisible team

## Overview

Owen Zanzal shares personal lessons from experimenting with asynchronous AI agents in his workflows, revealing that the biggest shift isn't productivity—it's a fundamental change in role and thinking. Instead of using AI as extra coding hands, he discovered that managing asynchronous agents requires thinking like a manager: defining artifacts upfront, establishing cadences, managing work-in-progress, and treating agents as junior teammates requiring clear specifications and structured feedback.

The core insight: agents aren't tools that do your work; they're extensions of your capacity that need orchestration.

## The Unexpected Shift: From Coder to Manager

### What I Expected vs. What Happened

**Initial expectation:**
AI agents like Copilot—extra hands to crank out code faster.

**What actually happened:**
Agents behave like junior teammates, not extension of your existing coding ability.

**The difference:**
```
Coding tool (Copilot):
- You direct, it assists
- Incremental productivity boost
- You stay in the execution mindset

Junior teammate (Agent):
- Needs clear instructions
- Requires feedback loops
- Demands defined standards of "done"
- Changes your role fundamentally
```

### The Role Transformation

**Before agents:**
- Solo IC (Individual Contributor)
- Direct execution
- Code → Ship
- All work is your responsibility

**After agents:**
- Managerial IC
- Planning and oversight
- Direction → Review → Feedback → Iteration
- Work is mediated through agents

**What the new role looks like:**

```
Up front (Planning)
├── Define what artifacts you want
├── Specify success criteria
└── Plan cadence and timing

Midstream (Monitoring)
├── Check in on agents' work
├── Unblock when needed
├── Adjust context/specifications
└── Review intermediate outputs

At the end (Feedback)
├── Review final outputs
├── Give structured feedback
├── Tighten specs for next time
└── Close the feedback loop
```

**The discovery:**
This loop—plan, review, retro—feels way more like managing than coding.

## Eyes First, Hands Second: The Trust-Building Approach

### The Observation Pattern

**Most valuable agents right now aren't "doers," they're "observers."**

**What these agents do:**
- Surface observations
- Identify patterns
- Suggest improvements
- Flag issues
- Propose next steps

**Only after review and approval do they act.**

### Examples of "Eyes First" Agents

**1. PR Review Agent**

**What it does:**
- Reviews pull requests
- Flags risky diffs
- Identifies coverage gaps
- Suggests refactoring
- Checks for known antipatterns

**Why "eyes first":**
Humans make final call on merge. Agent provides informed perspective.

**2. Alert Triage Agent**

**What it does:**
- Reviews incoming alerts
- Determines severity
- Suggests immediate actions
- Identifies patterns
- Recommends escalation

**Why "eyes first":**
Humans make incident response decision. Agent provides context and options.

**3. Research Agent**

**What it does:**
- Researches topics
- Gathers information
- Identifies key sources
- Drafts initial summary
- Flags uncertainties

**Why "eyes first":**
Humans validate findings. Agent does legwork and initial synthesis.

**4. Documentation Agent**

**What it does:**
- Analyzes codebase
- Identifies missing documentation
- Flags outdated documentation
- Suggests improvements
- Drafts missing docs

**Why "eyes first":**
Humans review and approve content. Agent identifies gaps.

### Why This Approach Works

**Trust is key:**
```
Agent makes observation
    ↓
You review observation
    ↓
You approve or adjust
    ↓
Agent acts (or reports back)
    ↓
You verify result
    ↓
Repeat with more trust
```

**Benefits:**
- Reduces catastrophic failures
- Builds confidence in agent
- Enables feedback-driven improvement
- Keeps human in the loop
- Maintains control and oversight

## Cadence Matters: Timing Agent Execution

### The Insight

**Not every agent should run constantly.**

**Reality:**
Some work better at different rhythms depending on:
- Urgency level
- Information freshness
- User context
- Team workflow

### Agent Rhythm Framework

**Three cadence types:**

**Immediate (Real-Time)**
- High-priority incidents
- Critical alerts
- PR reviews (pre-merge)
- Security issues

**Why real-time:**
- Time-sensitive
- Can't wait for batch processing
- Impacts production

**Daily**
- PR summaries
- Slack digests
- Bug reports
- Status updates

**Why daily:**
- Relevant for daily standup
- Not urgent, but timely
- Matches work cadence
- Prevents information staleness

**Weekly/Monthly**
- Documentation suggestions
- Dependency upgrade reviews
- Tech debt reports
- Code quality assessments

**Why periodic:**
- Less time-sensitive
- Useful for planning blocks
- Prevents noise
- Organized review windows

### Aligning Cadence with Your Workflow

**The key principle:**
Align agent cadence with your natural work rhythm.

**Example:**
```
You have a monthly cleanup block (2 hours, last Friday)
    ↓
Tech debt agent runs Thursday evening
    ↓
Reports ready when you start cleanup
    ↓
You have curated list of improvements
    ↓
Not flooded daily with noise
    ↓
Value delivered at right moment
```

**Benefit:**
Right information, right time, right quantity.

## Artifacts as the Anchor: Specifications Drive Consistency

### The Strategy

**Define outputs upfront using Artifact Specs.**

**What this provides:**
- Clear definition of "done"
- Machine-readable specification
- Validation mechanism
- Feedback foundation

### Using Specs to Improve Agent Output

**Process:**

```
Agent produces output
    ↓
Output misses mark
    ↓
You could:
    - Adjust context
    - Rewrite instructions
    - Change prompt wording
    OR
    - Tighten the specification
```

**Better approach:**
Tighten the specification (JSON Schema).

**Example:**
```
Initial spec: "Action item as string"

Agent output: "Vague, unclear action items"

Improved spec:
{
  "action_item": {
    "type": "object",
    "properties": {
      "description": "string, max 50 chars",
      "owner": "string, one person",
      "due": "ISO 8601 date",
      "priority": "enum: [critical, high, medium, low]"
    },
    "required": ["description", "owner", "due"]
  }
}

Result: Agent produces precise, actionable items
```

### Specs as Job Descriptions

**Analogy:**
```
Refining a spec is like refining a job description for a teammate.

The more precise the description:
- Clearer expectations
- Better outcomes
- Easier feedback
- Consistent quality
```

**What to tighten:**
- Field lengths
- Enum values
- Regex patterns
- Required vs. optional
- Nesting and structure

## The WIP (Work-In-Progress) Trap

### The Problem

**Easy to feel productive when agents are generating outputs.**

**What actually happens:**
Work-in-progress piles up fast.

**Reality:**
```
Agent generates output
    ↓
Feels like progress
    ↓
But output isn't done
    ↓
Agent rarely takes tasks to completion
    ↓
You have to review, approve, close loop
    ↓
WIP backlog grows faster than completion rate
```

### Why This Happens

**Agents are good at:**
- Generating options
- Producing drafts
- Surface-level analysis

**Agents are not good at:**
- Closing tickets
- Completing full workflows
- Making final decisions
- Taking work over the line

**Result:**
Illusion of progress, growing backlog.

### Managing WIP Actively

**What to do:**

**1. Track WIP explicitly**
```
Don't lose track of agent-generated work
Maintain a visible backlog
Know what's pending review/action
```

**2. Set WIP limits**
```
If you have 20 pending agent outputs
That's too much WIP

Set limit (e.g., max 5 pending)
Agents wait until you process current backlog
Creates natural pacing
```

**3. Close loops regularly**
```
Don't let work sit in review forever
Set review schedule
Approve, reject, or iterate
Get to completion
```

**4. Distinguish states**
```
Generated (needs review)
Reviewed (needs action)
Approved (ready for use)
In-progress (being worked on)
Completed (done)

Don't let items get stuck in intermediate states
```

## The Surprise Advantage: Accessibility and Delegation

### Asynchronous as Superpower

**The realization:**
With agents, you can delegate from anywhere.

**Example:**
```
Coffee shop, having an idea
    ↓
Open phone
    ↓
Write brief agent instruction
    ↓
Kick off research/analysis task
    ↓
Go sit down with coffee
    ↓
By time you're ready, draft is waiting
```

**Benefit:**
Work happens without you sitting at desk.

### Productivity Comes from Thoughtfulness, Not Presence

**Key insight:**
Productivity is about thinking clearly and instructing well, not about hours spent coding.

**What changes:**
```
Before: Productivity = time at desk coding

After: Productivity = quality of specifications +
                     clarity of instructions +
                     timeliness of feedback
```

**Implications:**
- Better from coffee shop with clear spec than at desk without one
- Quality instructions beat long hours
- Async execution multiplies your time
- Strategic thinking > tactical execution

## Putting It Together: Managing Your Invisible Team

### The Framework

**Think of agents as junior team members, not coding tools.**

**What this requires:**

**1. Clear artifact definitions**
- Specify what done looks like
- Use JSON schemas or templates
- Tighten based on feedback
- Iterate toward consistency

**2. Aligned cadences**
- Match agent rhythm to your rhythm
- Immediate for urgent work
- Daily for operational tasks
- Weekly/monthly for planning work

**3. Eyes before hands**
- Observations before actions
- Review before agent acts
- Build trust gradually
- Maintain oversight

**4. WIP management**
- Actively track pending work
- Close loops regularly
- Set limits to prevent drowning
- Distinguish work states

**5. Structured feedback**
- Use specifications as feedback mechanism
- Adjust context when needed
- Refine specs for consistency
- Document what works

### The Mental Model

```
You are orchestrating a tiny team
    ├── Members never sleep
    ├── Members never get tired
    ├── Members need crystal-clear specs
    ├── Members execute with precision
    ├── Members don't close tickets
    └── You manage them like a leader

Your job is:
    ├── Clear direction (artifacts)
    ├── Right timing (cadence)
    ├── Trust building (eyes first)
    ├── Feedback loops (specs)
    └── WIP control
```

## Key Takeaways

1. **Shift from coder to manager** — Role changes fundamentally with agents
2. **Agents are teammates, not tools** — Require management, not just usage
3. **Plan, review, retro cycle** — Managerial workflow replaces execution workflow
4. **Eyes first, hands second** — Observations build trust before actions
5. **Cadence matters** — Different work needs different timing
6. **Immediate for urgent** — High-priority incidents run real-time
7. **Daily for operations** — PR summaries, digests, status
8. **Weekly/monthly for planning** — Tech debt, dependencies, docs
9. **Align with your rhythm** — Right information at right time
10. **Artifacts as anchor** — Define output before starting
11. **Specs drive consistency** — Tighten specification instead of rewording
12. **Specs as job descriptions** — More precise = better outcomes
13. **WIP accumulates fast** — Easier to generate than to complete
14. **Agents don't close tickets** — You have to shepherd work over line
15. **Track WIP explicitly** — Don't lose visibility
16. **Set WIP limits** — Prevent drowning in pending work
17. **Close loops regularly** — Process backlog continuously
18. **Accessibility bonus** — Delegate from anywhere, anytime
19. **Quality over presence** — Clear spec beats long hours
20. **Async multiplies time** — Work happens while you think

## The Bottom Line

Owen Zanzal's early lessons reveal that asynchronous AI agents represent not just a productivity tool but a fundamental mindset shift: from solo individual contributor to orchestrator of an invisible team.

**The core realization:**
Agents aren't faster coding—they're a different way of working entirely. They require management disciplines (planning, feedback, cadence, WIP control) rather than just technical skill.

**The framework for success:**

1. **Define artifacts upfront** — JSON schemas for clear specifications
2. **Establish appropriate cadences** — Immediate, daily, or periodic based on need
3. **Trust-building approach** — Eyes first (observe), hands second (act)
4. **Active WIP management** — Track, limit, and close loops deliberately
5. **Structured feedback** — Refine specifications rather than rewrite instructions

**The surprising benefits:**
- Accessibility: delegate from anywhere
- Productivity: quality of spec matters more than hours worked
- Scalability: one person orchestrates small invisible team

**The key insight:**
This isn't about coding faster. It's about thinking differently about your role, your workflow, and how you extend your capacity through others—even when those "others" are AI agents.

**The transformation:**
From "How do I code faster?" to "How do I orchestrate work effectively?" From execution mindset to management mindset. From doing everything yourself to leading a tiny, tireless team.

**For practitioners:**
If you're experimenting with agents, stop thinking of them as tools and start thinking of them as team members. Give them clear job descriptions (specs), align their work with your rhythms (cadence), trust them incrementally (eyes first), and manage their output actively (WIP control).

The shift from coder to orchestrator isn't accidental—it's the natural evolution of working with capable agents asynchronously. Embrace that shift, and the real productivity gains emerge.

