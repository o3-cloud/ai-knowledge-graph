---
summary: Owen Zanzal reframes AI coding agents through the lens of traditional craftsmanship—arguing that automation reveals weak craft rather than destroying strong craft, and that true skill migrates from execution to constraint-design and system setup
event_type: blog_post
sources:
    - https://medium.com/devops-ai/craftsmanship-under-power-from-power-tools-to-ai-coding-agents-a1d2602fccab
tags:
    - craftsmanship
    - AI-agents
    - software-architecture
    - constraint-design
    - code-quality
    - system-design
    - skill-migration
    - professional-development
    - DevOps
---

# Craftsmanship Under Power: From Power Tools to AI Coding Agents

**Author:** Owen Zanzal
**Publication:** DevOps<>AI
**Publication Date:** December 16, 2025 (5 days ago)
**Read Time:** 8 minutes

## Overview

Owen Zanzal demolishes the persistent anxiety that AI coding agents will erode professional craftsmanship, reframing the entire debate through the lens of traditional craft disciplines—carpentry, machining, structural engineering.

His core insight: automation doesn't destroy craftsmanship; it reveals whether craftsmanship was ever there. True craft isn't about manual dexterity or genius improvisation—it's about control achieved through the systematic design of constraints. AI agents don't threaten strong craft; they expose fragile systems that relied on luck, heroics, and sustained human attention to avoid failure.

## The Persistent Professional Anxiety

### The Story We Tell Ourselves

**The narrative:**
Every generation of workers believes new technology will wash away hard-won knowledge and replace skillful effort with button-pushing.

**The anxiety:**
- If the machine does the heavy lifting, does expertise vanish?
- If automation handles the work, does quality suffer?
- If the tool is powerful enough, is the discipline itself hollowed out?
- Real skill is disappearing.

**The pattern:**
This story repeats across carpentry → metalworking → manufacturing → software engineering → AI agents.

### The Fundamental Misunderstanding

**What's wrong with the narrative:**
It misidentifies what craftsmanship actually is.

**The myth:**
Craftsmanship = manual dexterity, raw talent, genius operating without guardrails, perfect execution.

**The reality:**
Craftsmanship = systematic design of constraints that make failure difficult.

## The Diagnostic Test: What Automation Reveals

**Core principle:**
Automation doesn't destroy craft—it reveals process weaknesses that were always hidden by low stakes and slow pace of manual work.

**The reframe:**
AI and advanced tools don't threaten true craftsmanship; they reveal whether it was ever there in the first place.

**Implication:**
If your system collapses under AI-powered speed, your system was always fragile. You just couldn't see it because manual work moved slowly enough that human attention and heroics papered over the cracks.

### Craftsmanship Is About Inevitability

**Not about:**
- Avoiding mistakes
- Perfect human execution
- Sustained attention
- Never slipping

**It's about:**
- Making mistakes non-catastrophic
- Anticipating error
- Building defensive systems
- Making failure expensive to reach

**The master craftsperson's defining characteristic:**
Not the person who never slips. The person whose system makes it almost impossible for a slip to ruin the whole project.

## The Visceral Lesson: Hand Tools to Power Tools

### The Handsaw vs. Table Saw Comparison

**Handsaw (4-6 inches per second):**
- Immediate tactile feedback
- Feel the grain of the wood
- Crooked stroke creates resistance—you feel it, adjust mid-cut
- Error space is small
- Speed lets you recover
- Forgiving of small mistakes

**Table Saw (4,000 RPM):**
- Powerful amplifier of capability
- Cuts vastly faster
- Equally amplifies mistakes
- Tiny wobble that handsaw forgives becomes ruined board
- Slight miscalculation becomes serious injury
- Zero forgiveness

### The Skill Migration

**What happens:**
Freehand technique that worked for decades suddenly collapses under industrial power.

**The skill doesn't disappear—it migrates.**

**Old skill (execution):**
Muscle memory of the cut. Steady hand. Feel for the grain.

**New skill (setup):**
Design and construction of jigs, fixtures, fences, and reference surfaces that make the intended cut physically impossible to screw up.

**The shift:**
From execution → setup
From muscle memory → rigid structures
From improvisation → pre-engineered precision

**The craftsperson's work now:**
Spend 20 minutes to an hour building a dedicated jig that makes the correct cut the only possible outcome. The tool just executes what you pre-programmed into that system.

### The Universal Law

**The principle that applies across all disciplines:**
Speed and power demand structure.

The requirement for constraint increases proportionally with tool power.

## Frozen Experience: The Universal Principle

### What Is Frozen Experience?

**Definition:**
The crystallization of accumulated knowledge, judgment, and hard lessons from past failures into rigid structures.

**Why it matters:**
You don't have to constantly reaccess that knowledge. You freeze the judgment right into the process itself. The system embodies the wisdom.

### Examples Across Disciplines

**Structural engineering:**
Building codes literally encode decades of structural failures and catastrophes.

**What the codes say:**
"We tried this. It failed. People died. Do not do it again."

The code removes the choice. No calculation needed. No judgment call. The constraint is absolute.

**Machining:**
Tolerances of a ten-thousandth of an inch.

The choice has been removed. You can't accidentally use a tolerance of a ninth of an inch; the tool and process don't allow it.

**Software development:**
Strong type systems are frozen experience.

Type systems make entire categories of errors (mixing data types, wrong function signatures) physically impossible to compile or run. The fence that keeps the tool from cutting where it shouldn't.

### The Craft Definition

**Craftsmanship is the systematic reduction of your degrees of freedom.**

What is not constrained will eventually fail.

Complex systems have too many variables for humans to track reliably. True craft means reducing choices until the only path left is the correct one.

## AI Agents: High RPM on Exceptionally Fragile Material

### The Context

If the table saw was 4,000 RPM on wood, then AI coding agents are operating at extreme RPM on exceptionally fragile material.

### Why Code Is Fragile

**Physical materials (wood, metal, concrete):**
- Tactile feedback exists
- Resistance provides information
- Errors are often immediately visible
- Link between action and consequence is immediate

**Code:**
- Zero physical resistance
- No tactile feedback at all
- Errors can be silent and invisible
- AI agent can inject a subtle bug across 10 files in seconds
- Won't know until weeks later when it hits production
- Complete severance between action and consequence

### The Real Danger

**What people usually judge:**
Agent intelligence. Is it smart enough to avoid mistakes?

**What actually matters:**
Constraint design. An intelligent agent with unconstrained freedom is just high-speed improvisation.

**The analogy:**
It's like giving a brilliant apprentice keys to all industrial machinery but saying, "Hey, you're smart. You don't need safety guards or fixtures."

**The truth:**
Relying on brilliance (human or artificial) to avoid errors is the definition of a fragile system.

**Current assumption:**
The tool assumes perfection. Perfection can't be relied on.

**True craft:**
Design for the inevitable slip.

## Building Jigs and Fixtures for Code

### What Does This Actually Look Like?

### Strategy 1: Limit Degrees of Freedom

**Current approach:**
Let agents generate whole files from scratch.

**Problem:**
Errors hide inside new code; you can't compare against old state.

**Better approach:**
Require diffs and patches instead of full file replacement.

**Why it works:**
Your fence. Limits the agent to proposing specific, measurable changes.

**Implementation:**
- Instead of freeform prose, demand absolute structure
- JSON schemas for output
- Specific code blocks
- Force intelligence to operate within predefined geometry

**Benefit:**
Changes are visible and bounded.

### Strategy 2: Control Speed Through Iteration

**The principle:**
Speed is the most dangerous part of power. Intentionally slow the cut down.

**Implementation:**
- Small, composable changes instead of huge sweeping refactors
- Minimize error surface
- One concern per invocation

**Anti-pattern:**
Don't ask agent to fix bug AND add feature AND refactor tests all at once. That's inviting chaos.

**Key insight:**
Iteration has to be designed into the process.

### Strategy 3: Externalize Judgment

**The principle:**
The agent shouldn't be deciding what's correct.

**Implementation:**
Treat tests as the fundamental reference surface—the geometry.

**What this means:**
- Tests define required shape of solution
- Agent output either fits that geometry or doesn't
- Tests are non-negotiable
- They're the enforcement mechanism

**The stop block:**
Continuous integration is the stop block on the table saw. If change doesn't fit the jig (test fails), system stops cold before error propagates.

**Benefit:**
Failures caught before they become systemic.

### Strategy 4: Prevent Cumulative Drift

**The problem:**
Errors in constraint and standards accumulate invisibly.

**In physical craft:**
Always measure from known flat reference surface, not from last piece you just cut.

**In code, this means two things:**

**1. Coding standards as reference faces**
- Prevent slow, invisible drift
- If every function structured consistently, deviations jump out
- If everything's different, you can't tell mistake from style variation

**2. Canonical implementations as anchors**
- Give agent golden path to copy
- Established example prevents agent from inventing potentially-wrong approach
- When good solution already exists, use it

### Strategy 5: Encode Wisdom

**Implementation:**
Use specs and ADRs (Architecture Decision Records) as blueprints.

**What this does:**
- Records critical past judgments
- Anchors intent
- Agent knows what's a load-bearing wall in your software
- That judgment is now frozen and external
- Guidance is structural, not optional

**Benefit:**
Past hard-won knowledge prevents repeating mistakes.

### Strategy 6: Manage Context

**The problem:**
Giving agent entire codebase is like trying to cut on vibrating workpiece—just noise.

**Principle:**
Over-context degrades precision immediately.

**What happens:**
Agent can't distinguish signal from noise. Answer drifts toward generic or wrong.

**Solution:**
Rigorous separation of planning and execution.

**Implementation:**
- Planning phase might need broad context
- Execution phase needs narrow, surgical, laser-focused context
- Reset state between distinct operations
- Long meandering conversations accumulate subtle drift

**Better approach:**
Start from known good, minimal state for each task.

## The Migration of Skill: What Changes for Craftspeople

### The Job Shifts Entirely Upstream

If the machine handles execution, the human role moves completely upstream—from writing code to designing the system that makes bad code harder than good code.

### The Uniquely Human Tasks

**1. Boundary decisions**
- What is a single function vs. module vs. whole external service?
- Agents can't make these architectural value judgments
- Requires understanding business tradeoffs and long-term consequences

**2. Exception handling**
- When to incur technical debt on purpose
- When unique problem needs nonstandard solution
- AI doesn't have that context

**3. Knowing when not to automate**
- Some work must stay manual
- Constraint system isn't mature yet
- Doing work itself provides vital knowledge human needs to internalize
- Sometimes the friction is the feature

### The Value Migration

**From:**
- Execution
- Writing tons of code
- Visible labor
- Muscle memory
- Speed of individual output

**To:**
- Setup
- Designing systems that make bad code harder than good code
- Invisible rigor
- Architecture and constraint design
- Quality and reliability of system behavior

## Why We're Anxious: The Visibility Problem

### The True Source of Professional Anxiety

**Manual skill:**
- Visible and tangible
- You can see it
- Easy to respect
- Obvious that expertise mattered

**Setup work:**
- Designing the jig
- Writing the ADR
- Defining type system
- Creating reference surfaces
- This is true craft
- Invisible rigor
- Often undervalued

**The anxiety:**
It's really just anxiety over the visibility of valuable labor.

**The truth:**
The value hasn't gone anywhere. It's just moved to structural layer where stakes are infinitely higher, but very few people can see the discipline involved.

### The Paradox

The more mature the craft, the more invisible it becomes. A perfectly designed constraint system looks like it didn't require skill—it just works.

## The Core Conclusion: Three Insights

### Insight 1: Automation Reveals, Not Replaces

**AI agents expose weak craft—they don't replace strong craft.**

If process depends on improvisation and last-minute heroics from experienced reviewers, it was never robust. It was always fragile, always relying on luck.

### Insight 2: Precision Comes From Constraint

**Precision doesn't come from intelligence. It comes from constraint.**

Brilliance without constraint is just fast chaos.

### Insight 3: Craft Survives Automation

**This definition of craftsmanship survives any wave of automation.**

It's the refusal to rely on luck—not luck that your hand is steady, not luck that the agent understood your ambiguous prompt.

**Craftsmanship is building a system where:**
- Luck isn't a factor
- Constraints are so tight
- Success is the engineered default outcome

## The Challenge to You

**Provocative question:**
If success is the default outcome engineered by constraints, what specific fixture, test, standard, or architectural record are you personally responsible for building right now?

**What will you build today that will make failure impossible for the AI agents you'll use tomorrow?**

**Who designs the systems that survive the next wave of power?**

Start designing that jig today.

## Key Takeaways

1. **Automation reveals weak craft; doesn't replace strong craft** — If system collapses under AI speed, it was always fragile
2. **Craftsmanship is control through constraints** — Not genius or perfection, but systematic reduction of failure modes
3. **Manual skill doesn't disappear—it migrates** — From execution to setup, from writing code to designing systems
4. **Speed demands structure** — Power tool requires more constraint, not less
5. **Frozen experience prevents error** — Codify knowledge into rigid structures (codes, types, standards)
6. **Degrees of freedom must be reduced** — What's unconstrained will fail
7. **AI agents operate on fragile material** — Code has no tactile feedback; errors are silent
8. **Tool power amplifies mistakes equally** — High-speed improvisation is fast chaos
9. **Tests are reference surfaces** — Define geometry of correct solution; agent executes within constraints
10. **Diffs over full files** — Limit degrees of freedom; make changes visible and bounded
11. **One concern per invocation** — Iteration must be designed into process
12. **Jigs are pre-engineered precision** — Spend time setting up constraints, tool just executes
13. **Context must be managed** — Over-context degrades precision; narrow execution context
14. **Coding standards prevent drift** — Consistent structure makes deviations visible
15. **Canonical implementations anchor decisions** — Golden path prevents invention of potentially-wrong approaches
16. **ADRs freeze judgment** — Architecture decision records externalize critical wisdom
17. **Boundary decisions remain human** — Architectural tradeoffs require human judgment
18. **Visibility anxiety is understandable** — But value migrated to invisible rigor, not disappeared
19. **Mature craft is invisible** — Perfect systems don't look like they required skill
20. **Professional survival depends on constraint design** — Next generation builds jigs that make failure impossible

## The Bottom Line

Owen Zanzal reframes the entire AI anxiety debate through traditional craftsmanship, revealing something profound: we're not losing skill to automation; we're upgrading to a different kind of skill.

**The old skill (execution):**
- Writing code fast
- Debugging by inspection
- Relying on experience and intuition
- Heroic code review and intervention

**The new skill (constraint design):**
- Building systems where bad code is harder than good code
- Designing tests that define correct behavior
- Creating structures that make errors non-catastrophic
- Encoding wisdom into types, standards, and references

**The crucial insight:**
An intelligent agent with unconstrained freedom is just high-speed chaos. But an intelligent agent operating within well-designed constraints becomes amplified capability.

**The professional challenge:**
Are you building the jigs and fixtures that will make success inevitable? Or are you hoping the AI stays smart enough to avoid mistakes?

**The answer determines whether AI becomes a tool for acceleration or a mirror revealing fragile craft.**

True craftsmanship—the systematic reduction of degrees of freedom until success is the engineered default—survives every technological wave. It's not threatened by AI agents. It's demanded by them.

The question is: which craftspeople will design the constraints?

Start building that jig today.

