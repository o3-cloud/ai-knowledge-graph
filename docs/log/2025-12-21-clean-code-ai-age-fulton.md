---
summary: Jonathan Fulton revisits his "clean code" advice in the era of AI agents, arguing that four original principles still hold but require strategic reframing—tests become about agent autonomy, dependency structure matters more than local cleanliness, data models are foundational and human responsibility, and the goal shifts from perfect elegance everywhere to cheap change at edges
event_type: blog_post
sources:
    - https://medium.com/jonathans-musings/clean-code-in-the-age-of-ai-fc00d204d3e4
tags:
    - clean-code
    - AI-agents
    - testing
    - code-quality
    - data-modeling
    - software-architecture
    - dependency-structure
    - code-maintainability
    - Jonathan-Fulton
---

# Clean Code in the Age of AI: How to Think About Clean Code When AI Agents Write Most Code

**Author:** Jonathan Fulton
**Platform:** Jonathan's Musings (Medium)
**Publication Date:** 2 days ago (December 2025)
**Type:** Principles and Best Practices Update
**Duration:** 6 min read
**Key Concept:** Strategic recalibration of clean code principles for AI-assisted development

## Overview

Jonathan Fulton revisits his widely-read post on clean code tips, originally written years ago, and asks: what has changed now that AI agents write most code? His answer: most advice still holds, but the reasoning and framing needs fundamental recalibration. Tests matter more than ever—but now for agent autonomy, not just human confidence. Dependency structure matters more than local cleanliness. Data models become human responsibility, not AI capability. The goal shifts from "perfect elegance everywhere" to "fast feedback, stable foundations, cheap change at edges." Clean code didn't go away in the AI age; it got more strategic and higher leverage.

## The Original Four Clean Code Principles

### What Jonathan Originally Recommended

**1. "If it isn't tested, it's broken"**
- Write lots of tests, especially unit tests
- Or you'll regret it

**2. Choose meaningful names**
- Short, precise names for variables, classes, functions
- Names communicate intent

**3. Functions and classes should be small**
- Functions: no more than four lines
- Classes: no more than 100 lines
- Single Responsibility Principle
- Do one thing, and only one thing

**4. Functions should have no side effects**
- Avoid mutating input arguments
- Side effects are evil
- Specify this explicitly in contracts
- Prefer immutable inputs and objects without setters

### What Still Holds

**The short answer:**
Most of the advice still holds.

**The longer answer:**
The why matters more than ever, and the framing needs to change.

### What's Relaxed

**The one exception:**
The rigid guidance around four-line functions and 100-line classes.

**Honest reflection:**
That rule was always a forcing function, not a law of nature.

AI makes that clearer.

## What Has Changed: Four Strategic Shifts

### Shift 1: Tests Are More Important Than Ever—But For Different Reasons

#### The Old Framing: Tests = Confidence

**Before (human-written code):**
- Tests give you confidence the code works
- Safety net for human developers
- Catch bugs before production
- Insurance policy against mistakes

#### The New Framing: Tests = Agent Autonomy

**Now (AI-written code):**
Tests are what allow agents to:
- Operate independently without constant supervision
- Detect their own mistakes automatically
- Iterate without human intervention
- Self-correct and improve

**The transformation:**
Fancy autocomplete → Self-correcting system

Strong test suite is the key difference.

#### Why This Matters Practically

**For agents to work well:**
They need immediate feedback on whether they're right or wrong.

**In compiled languages:**
Compilation provides this feedback for free (go build, tsc).

**In dynamic languages (Python, JavaScript):**
Tests ARE your build step.

No tests in dynamic languages = agents flying blind.

#### The Language Implication

**Compiled languages are more agent-friendly.**

Why?
- Fast, binary signal that something is wrong
- Immediate feedback loop
- Agents can iterate rapidly

**Dynamic languages need aggressive testing:**
Agents must rely on test feedback to know they're on track.

#### The Volume Shift

**The cost curve has flipped:**
- Tests are cheap to write (agents excel at this)
- Bugs are expensive to fix
- No reason to skimp on test coverage

**What this means:**

| Test Type | Historical | AI Era |
|-----------|-----------|--------|
| **Happy path** | 1 test | 1 test |
| **Edge cases** | 0-1 tests | 3-4 tests |
| **Invalid inputs** | 0-1 tests | 2-3 tests |
| **Parameter combinations** | 0 tests | Multiple pairwise tests |
| **Regression tests** | Occasional | Many (cheap to generate) |

**The directive:**
Let agents generate 3-4× more test coverage than you'd write manually.

The cost is trivial; the benefit is huge.

### Shift 2: Dependency Structure Matters More Than Local Cleanliness

#### The Mental Model: Vibe Coding in Prod

**From Anthropic's concept:**
Not all code needs to be equally clean.

What matters is where code sits in your dependency graph.

#### The DAG Perspective

**Think of codebase as directed acyclic graph (DAG):**

```
        Root (core abstractions)
           ↑
      Mid-level dependencies
           ↑
     Leaf nodes (implementation)
```

**Different levels have different requirements.**

#### Leaf Nodes: Can Be Messier

**Leaf nodes** = code nothing else depends on

Characteristics allowed:
- Some duplication
- Awkward loops
- Longer-than-ideal functions
- Workarounds and hacks

**Why it's OK:**
- Cheap to change
- Limited blast radius if wrong
- Isolated impact
- AI makes it even cheaper to refactor

#### Root Nodes: Must Be Clean

**Root nodes** = core abstractions many things depend on

Requirements:
- Stable (doesn't change randomly)
- Well-named (intent is clear)
- Carefully structured (clear design)
- Explicit contracts (invariants documented)
- Clear about guarantees

**Why it's critical:**
- One mistake cascades everywhere
- Huge blast radius for changes
- Affects entire system
- Refactoring is expensive

#### Real Example: Datadog Experimentation Pipeline

**Structure:**
- DAG of warehouse tasks
- Each node = task executing SQL queries
- Produces intermediate table

**Leaf level:**
Individual task implementations (can be messy)
- Generate SQL blocks
- Task orchestration code
- Specific logic

**Root level:**
Shared abstractions (must be clean)
- WarehouseQuerier
- WarehouseQuerierFactory
- Table builders
- Schema definitions

**The impact:**
Individual task can be ugly; shared abstractions must be clean.

#### The Key Insight

"Clean code, in the age of AI, is less about aesthetics and more about minimizing expensive change."

**Translate to:**
- Clean where change is expensive (root nodes)
- Accept mess where change is cheap (leaf nodes)
- Use dependency structure to guide cleanliness investment

### Shift 3: Data Models Are Foundational—And AI Is Still Bad at Them

#### Why Data Models Matter

**Data models are foundation:**
- SQL tables
- Schemas
- Event formats
- NoSQL documents

**Everything depends on them:**
- APIs
- Business logic
- Analytics
- Backfills
- Migrations
- Data processing pipelines

**If data models are wrong:**
Cost shows up everywhere
- Expensive migrations
- Buggy business logic
- Broken analytics
- Difficult backfills

#### Why AI Struggles Here

**The uncomfortable truth:**
AI is not great at designing data models.

**Not because of:**
- Lack of intelligence
- Bad reasoning
- Poor pattern recognition

**But because good data modeling requires:**
- Long-term thinking (this will change over time, how?)
- Cross-cutting context (how does this affect all systems?)
- Deep understanding (how will this be queried and evolved?)

**The context problem:**
Cross-cutting knowledge usually lives in:
- Documentation (often outdated)
- Tribal knowledge (in people's heads)
- Dashboards (show what, not why)
- Historical decisions (scattered across commits)

**Agents struggle holding all this context.**

#### The Human Responsibility

**Humans must do upfront thinking:**

- What are the core entities?
- What are the invariants?
- What must be immutable?
- What changes frequently vs. rarely?
- How will this evolve in 1, 5, 10 years?

**Then:**
AI is fantastic at implementing the model once it exists.

**The cost of being sloppy:**
"You'll spend months asking agents to clean up the mess later — and it will always be harder than doing it right once."

#### The Principle

**Data models = human responsibility**
**Implementation = AI capability**

Don't defer critical thinking to agents.

### Shift 4: Use an ORM with Explicit Schema

#### Why This Matters

**What agents need:**
Clear, explicit schema definitions.

**What agents struggle with:**
Reverse-engineering schema from:
- Migration files (hard to parse)
- Raw SQL (implicit and fragmented)
- Tribal knowledge (not explicit)
- Scattered documentation (incomplete)

#### The ORM Advantage

**An ORM with explicit models provides:**

| Benefit | Impact |
|---------|--------|
| **Single source of truth** | No confusion about what fields exist |
| **Clear contracts** | Code-to-data relationship explicit |
| **Type information** | Agents can reason about data |
| **Consistency** | Harder to diverge from definition |

#### Concrete Improvements

With explicit ORM models, agents get:
- Fewer subtle bugs
- Better query generation
- Safer refactors
- Faster iteration

#### The Framing

**You're not using ORM instead of understanding data.**

**You're using ORM to encode understanding** in a way both humans and agents can reliably consume.

**The principle:**
Make implicit knowledge explicit through structure.

## The Language Choice Implication

### Compiled vs. Dynamic Languages

**For AI agent coding:**

**Compiled languages win because:**
- Fast feedback (compilation fails immediately)
- Binary signal of correctness
- Agents iterate rapidly
- Testing is cheaper

**Dynamic languages require:**
- Much more aggressive testing
- Agents must get feedback from tests only
- No compilation safety net
- Higher risk of silent failures

**The conclusion:**
If you're choosing a language today, consider how AI-agent-friendly it is.

Compiled languages are significantly more agent-friendly.

## Strategic Recalibration: The New Mental Model

### The Goal Shift

**Old goal:**
Perfect elegance everywhere.

**New goal:**
- Fast feedback (tests)
- Stable foundations (data models, core abstractions)
- Cheap change at the edges (leaf nodes, implementation details)

### The Cleanliness Investment Strategy

**Invest heavily in:**
- Root-level abstractions (shared, depended-on)
- Data models (foundation of everything)
- Tests (agent feedback loops)
- Clear contracts (for AI to understand)

**Accept reasonable messiness in:**
- Leaf-level implementations (isolated, changeable)
- Temporary solutions (can be refactored easily)
- One-off code (limited impact)

### The Principles

1. **Cheap change at edges**
   - Keep implementation details simple to modify
   - Minimize blast radius

2. **Stable foundations**
   - Core abstractions highly polished
   - Data models carefully designed
   - Contracts explicitly clear

3. **Fast feedback**
   - Tests provide immediate signal
   - Compiled languages get this for free
   - Dynamic languages must earn it through tests

4. **Clear contracts**
   - Data models explicit (ORM)
   - Function signatures clear
   - Side effects documented

5. **Human expertise where it matters**
   - Data model design (human upfront thinking)
   - Architecture decisions (human judgment)
   - Contract definition (human clarity)

## Practical Recommendations

### For Codebases Using AI Agents

**1. Test aggressively**
- Especially in dynamic languages
- Let agents generate tests (cheap)
- 3-4× historical test volume
- Coverage everything: happy path, edges, invalids, combinations

**2. Invest in dependency structure**
- Map your DAG
- Identify root nodes (core abstractions)
- Keep root clean, accept leaf messiness
- Use this to guide cleanup efforts

**3. Design data models carefully**
- Don't delegate to AI
- Upfront human thinking required
- Long-term perspective essential
- Document invariants and evolution strategy

**4. Use explicit ORM**
- Every column, type, relationship clear
- Single source of truth
- Agents understand schema
- Cleaner implementation

**5. Consider language choice**
- Compiled languages are more agent-friendly
- Fast feedback is critical
- Dynamic languages need heavier testing burden

### For Code Reviews

**Ask different questions:**

**Don't ask:**
- Is this function short enough?
- Are there duplicated lines?
- Is this class too big?

**Do ask:**
- Is this in the dependency graph root?
- Will changes here cascade elsewhere?
- Are tests covering agent mistakes?
- Is the schema clear and documented?
- Does this violate the data model invariants?

## Key Takeaways

1. **Most clean code advice still holds** — But reasoning changed
2. **Tests now about autonomy** — Agent independence and self-correction
3. **Compiled languages advantage** — Fast feedback for agents
4. **Dynamic languages need more tests** — Agents rely on test feedback
5. **Cost curve flipped** — Tests cheap, bugs expensive
6. **3-4× test volume justified** — Let agents generate coverage
7. **Dependency structure critical** — Cleanliness investment depends on location
8. **Root nodes must be clean** — Shared dependencies carefully designed
9. **Leaf nodes can be messy** — Isolated code can be pragmatic
10. **DAG mental model** — Organize code by dependency level
11. **Data models human responsibility** — AI bad at design, good at implementation
12. **Upfront thinking required** — Long-term evolution planning essential
13. **ORM with explicit schema** — Encode understanding for agent consumption
14. **Agents as implementation** — Not architects or designers
15. **Cheap change at edges** — Minimize blast radius of modifications
16. **Stable foundations** — Core abstractions highly polished
17. **Fast feedback loops** — Tests are agent's build step in dynamic languages
18. **Clear contracts** — Explicit about guarantees and invariants
19. **Strategic cleanliness** — Not about aesthetics, about minimizing expensive change
20. **Language choice matters** — Consider agent-friendliness when picking tech

## The Bottom Line

Jonathan Fulton recalibrates clean code principles for the AI agent era by arguing that the principles remain valid but require strategic reframing and selective application.

**The four original rules:**
1. Test everything (still true, now for agent autonomy)
2. Meaningful names (still true)
3. Small functions/classes (relaxed; was forcing function)
4. No side effects (still true)

**The strategic shifts:**
- **Tests** = autonomy and feedback (not just confidence)
- **Dependency structure** matters more than local cleanliness
- **Data models** are human responsibility; implementation is AI's
- **Goal** shifts from elegance everywhere to cheap change at edges

**The mental model:**
Think in terms of dependency structure (DAG):
- Root nodes (shared, depended-on) = must be very clean
- Leaf nodes (isolated, implementation) = can be pragmatic
- Cleanliness investment follows the structure

**For language choice:**
Compiled languages are significantly more agent-friendly (fast feedback). Dynamic languages require much more aggressive testing (tests are the build step).

**For data models:**
Humans must do upfront thinking about what's immutable, what changes, how it evolves. Then AI excellently implements the design. Don't delegate data model design to agents.

**The final insight:**
"If you get that right, agents will make you faster than you ever thought possible. If you get it wrong, they'll help you dig a very deep hole — very quickly."

Clean code in the AI age is less about perfectionism and more about strategic minimization of expensive change, stability at the foundation, and empowering agents with clear feedback loops and explicit structures.

