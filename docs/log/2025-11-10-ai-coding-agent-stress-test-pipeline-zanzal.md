---
summary: Owen Zanzal reframes AI coding agents from liability to asset—showing how they reveal pipeline weaknesses, expose gaps in automation, and provide continuous stress testing of development infrastructure before production failures occur
event_type: blog_post
sources:
    - https://medium.com/devops-ai/your-ai-coding-agent-is-running-a-free-stress-test-on-your-pipeline-510a8b952178
    - https://danielmiessler.com/blog/ai-influence-level-ail
tags:
    - AI-coding-agents
    - DevOps
    - pipeline-resilience
    - process-improvement
    - code-quality
    - testing-strategy
    - continuous-integration
    - chaos-engineering
    - automation-gaps
    - system-design
---

# Your AI Coding Agent Is Running a Free Stress Test on Your Pipeline

**Author:** Owen Zanzal
**Platform:** Medium (DevOps+AI)
**Publication Date:** November 10, 2025
**Type:** Practice/Strategy
**Key Concept:** AI-generated code as continuous pipeline validation

## Overview

Owen Zanzal reframes the problem of AI-generated code failures from a threat to be mitigated into an asset to be leveraged. AI coding agents writing problematic code isn't evidence they're unreliable—it's evidence that development pipelines have undetected gaps.

Rather than trying to make AI agents write perfect code, the smarter strategy is to use AI's prolific code generation as a continuous, comprehensive, cost-free stress test of development infrastructure. Every failure an AI agent creates is an opportunity to harden the pipeline, making it more resilient to all contributors—human or artificial.

## The Story: A Production Incident That Didn't Happen

### The Incident That Exposed Everything

**What happened:**
Last week, an AI coding assistant committed code that:
- Was syntactically perfect
- Passed all tests
- Used valid SQL
- Followed the instructions exactly

**What it did:**
Scanned 14 billion rows without an index—a query designed to take down production.

**What it revealed:**
Multiple pipeline gaps that would have caught this if they existed, or would have prevented production impact if they had been implemented.

### The Comfortable Narrative

**What teams say:**
"AI agents write bad code, therefore AI agents are risky. We need human review and oversight."

**Why this is incomplete:**
This narrative treats AI as the problem rather than as the messenger. It misses the fundamental insight: if AI code is getting through your pipeline, what else is?

## The DevOps Wake-Up Call

### The Dirty Secret

**What every DevOps engineer knows:**
We've always wanted stronger processes. We've always known our pipelines had gaps. We just never had time to fix them.

**The excuses we told ourselves:**
- "We'll add that security scanner next sprint."
- "Performance testing is on the roadmap."
- "We trust senior developers to catch these things in review."
- "We'll implement that architecture check when we have bandwidth."

### How AI Changed the Equation

**Before AI:**
- Humans commit code occasionally
- Review process gates some issues
- Some problems slip through to production
- Post-mortems happen
- "We'll prevent this next time" (rarely happens)

**With AI:**
- AI commits code constantly (10× human rate)
- Same gaps in pipeline → Every weakness exposed
- Problems become patterns, patterns become undeniable
- You can't blame individual developers anymore

**The result:**
Improvements we'd been postponing for years became urgent in weeks.

## What AI Coding Agents Actually Expose

### Category 1: Missing Guardrails (The Easy Ones)

**Things policy-as-code can catch:**
- API keys in code → Secret scanning
- Undersized resources → Kubernetes limits
- Unindexed database queries → Schema validation
- SQL injection vectors → Static analysis
- Missing error handling → Linter rules

**The pattern:**
These are automatable. Any decent policy tool catches them. AI agents finding these means your pipeline lacks the policy tools you should have implemented months ago.

### Category 2: The Subtle Failures (The Interesting Ones)

**Code that's correct but problematic:**
- N+1 queries that work but destroy performance
- Architectural pattern violations that function but create brittle systems
- Solutions that pass tests but miss business context
- Implementations that work in isolation but break integration
- Patterns that "everyone just knows" not to use
- Maintainability issues that don't affect current functionality

**Why these matter:**
These are exactly the failures human developers create. AI just makes them:
- Faster (10× throughput)
- More consistent (reproducible patterns)
- Harder to rationalize (can't blame individual judgment)

**The question:**
If your processes depend on every code contributor understanding architecture and business context, they're broken. AI is just making that obvious.

## The Real Problem: Process Dependency on Perfect Developers

### The Failed Assumption

**What most teams assume:**
"If we hire good enough developers and have code review, we'll catch problems."

**The reality:**
- Good developers make mistakes
- Code review catches some issues, not all
- Contractors don't know your architecture
- Junior developers miss context
- Everyone's tired sometimes
- Six months later, nobody remembers why decisions were made

**AI exposes this:**
By writing code at 10× volume without context, AI makes it obvious that process can't depend on developer perfection.

### The Wrong Question

**Teams ask:**
"How do we make AI write better code?"

**This is like asking:**
"How do we ensure contractors understand our architecture?"
"How do we make junior developers never make mistakes?"
"How do we ensure tired developers make good decisions?"

**The right question:**
"Why did this get through our pipeline in the first place?"

## How AI Failures Become Process Improvements

### The Reframe

**From:** "AI wrote bad code"
**To:** "Our pipeline couldn't catch bad code"

**From:** "AI is a liability"
**To:** "AI is a free stress test"

**From:** "How do we restrict AI?"
**To:** "How do we strengthen our process to handle imperfection?"

### The Feedback Loop

**Current pipeline gap:**
AI agent commits N+1 query that degrades performance.

**Immediate response:**
"Wow, we're lucky we caught this."

**Smart response:**
Add automated query analyzer that flags N+1 patterns.

**Better response:**
Turn this into a permanent test case.

**Best response:**
Build learning directly into pipeline so *every* caught issue becomes a new check.

## The Practical Four-Phase Path

### Phase 1: Accept Reality

**What to realize:**
- AI agents will expose pipeline weaknesses
- This is valuable, not dangerous
- Better exposed at commit-time than in production
- Better exposed at zero cost than with customer impact

**Organizational shift:**
"AI found a problem" = "We now see what was always weak"
Not: "AI broke something we need to prevent"

### Phase 2: Harden the Basics

**What to implement:**
- All security scanners (secret detection, dependency scanning, SAST)
- Performance checks (N+1 detection, resource limits, timeout analysis)
- Architectural guardrails (service boundary enforcement, pattern detection)
- Consistency checks (linting, formatting, style)

**The shortcut:**
Use AI itself to write the boring infrastructure code while you design the policies.

**The principle:**
Let AI handle the tedious automation of guardrails while humans focus on policy design.

### Phase 3: Capture Context

**What to do:**
Make implicit knowledge explicit and machine-readable.

**Documentation:**
- Architectural decisions (in code-readable format)
- Performance requirements (queryable)
- Team conventions (checkable)
- Service boundaries (enforceable)
- Business logic constraints (testable)

**The goal:**
Both humans and AI can understand what you're trying to achieve.

**Format:**
Decision records, architecture documentation, policy-as-code, constraint files, test cases.

### Phase 4: Close the Loop

**What happens:**
Every AI failure → Learning in system

**Implementation:**
- New test case added
- New lint rule created
- New architectural constraint enforced
- New performance check automated
- Documentation updated

**Result:**
Pipeline gradually hardens. Future AI agents (and humans) hit the guardrails earlier and earlier in the process.

## The Stress Test Perspective

### AI as Chaos Engineering Tool

**What chaos engineering tests:**
"What breaks when things fail?"

**What AI coding agents test:**
"What breaks when code is written without context?"

**The value:**
Free, continuous, comprehensive stress test of your entire pipeline.

**Advantage over chaos engineering:**
- Always running (every commit)
- Zero cost (AI is doing it anyway)
- Reproducible (same prompts often get same results)
- Immediate (no separate testing phase)

### The Hidden Value

**What you're really testing:**
Not just code quality, but:
- Test coverage comprehensiveness
- Documentation accuracy
- Architectural robustness
- Service isolation strength
- Error handling completeness
- Performance assumptions

## What Happens When You Fix the Pipeline

### The Virtuous Cycle

**Starting state:**
- AI writes code without context
- Some gets through; catches problems
- You add check for that pattern
- Pipeline strengthens

**Progression:**
- Next AI failures happen at different points
- You add checks for those
- Pipeline continues strengthening
- Coverage expands

**Final state:**
Pipeline that can handle code written by anyone without context:
- Tired developers
- New hires
- Contractors
- Your future self who forgot the context
- AI agents

**The benefit:**
Much stronger system overall.

## The Time Argument

### The Excuse That Doesn't Work Anymore

**What teams said:**
"We don't have time to implement all these guardrails."

**The reality now:**
If you have time to integrate AI coding agents, you have time to harden your pipeline. The freed-up development labor can be redirected to building the robust delivery system you always wanted.

**The reframe:**
You don't have time *not* to build these guardrails. AI will keep finding gaps until you do.

## The Two Choices

### Choice 1: Fix the Problems

**What to do:**
- Implement pipeline improvements
- Add guardrails AI revealed
- Capture implicit context
- Build continuous learning

**What you get:**
- Stronger systems
- More resilient processes
- Better able to handle any code source
- Competitive advantage through reliability

**Timeline:**
Months to years, but sustainable improvement.

### Choice 2: Shoot the Messenger

**What to do:**
- Ban or restrict AI agents
- Pretend human developers don't make same mistakes
- Hope process works without guardrails
- Ignore warnings

**What you get:**
- Same failures, slower discovery
- Failures happen in production
- Process still doesn't catch them
- Competitive disadvantage in speed

**The illusion:**
That human code is inherently safer. (It's not. It's just slower and less obvious.)

## The Uncomfortable Honesty

### What AI Reveals About Your Process

**If your process depends on:**
- Developers understanding all context
- Senior review catching all issues
- Conventions being "generally known"
- Architects preventing all bad patterns
- Everyone making good decisions all the time

**Then your process was always fragile.**

AI just makes it obvious.

**The good news:**
You can fix this. And it's actually not that hard. It just requires:
- Investment in automation
- Willingness to be explicit about constraints
- Commitment to hardening infrastructure
- Acceptance that code comes from imperfect sources

### The Question About Organizational Maturity

**Immature organizations:**
"AI is dangerous. We need more process."

**Mature organizations:**
"AI is revealing what was always dangerous. We need better process."

## Key Takeaways

1. **AI agents expose pipeline gaps** — Not breaking systems, revealing weaknesses
2. **Stress testing happens continuously** — Every commit is a test
3. **Cost is zero** — Free information about your infrastructure
4. **Subtle failures are the learning** — N+1 queries, architectural violations
5. **Process can't depend on perfection** — Human or AI perfection unlikely
6. **Wrong question is about AI** — Right question is about pipeline
7. **Secret scanning is necessary** — Automated secret detection essential
8. **Performance checks catch patterns** — N+1 detection, resource limits
9. **Architectural constraints enforceable** — Service boundaries, pattern detection
10. **Context must be explicit** — Can't rely on implicit knowledge
11. **Feedback loops drive improvement** — Caught problems → New checks
12. **Hardening happens iteratively** — Each failure → Pipeline strengthens
13. **Documentation matters for automation** — Must be machine-readable
14. **Policy-as-code is foundational** — Constraints enforceable automatically
15. **Guardrails need design** — Humans decide policy, automation enforces
16. **Test coverage becomes visible** — Gaps exposed by AI failures
17. **Assumptions become testable** — Business logic constraints explicit
18. **Future selves benefit most** — Documented decisions prevent forgotten context
19. **Human developers win too** — Stronger pipeline helps all contributors
20. **Maturity shown by response** — Great orgs use this as learning opportunity

## The Bottom Line

Owen Zanzal presents a strategic reframe: AI coding agents generating problematic code isn't evidence of AI unreliability—it's evidence of pipeline immaturity, revealed through continuous stress testing.

**The core insight:**
If your process depends on every code contributor being perfect, it was never sound. AI is just making that obvious by writing code at 10× volume without organizational context. Rather than restricting AI, the smart strategy is to use AI failures as signals for pipeline improvement.

**The practical opportunity:**
Every AI agent failure is actionable information about where your pipeline is weak. Instead of fighting AI, teams that harness this information will systematically harden their delivery infrastructure, making it more resilient to all sources of code—human or artificial.

**The four-phase approach:**
1. Accept that AI reveals weaknesses
2. Harden basic guardrails (security, performance, architecture)
3. Capture context explicitly (decisions, requirements, conventions)
4. Close the learning loop (failures → new checks)

**The competitive advantage:**
Organizations that embrace this shift will have:
- More reliable delivery pipelines
- Faster integration of AI-powered development
- Better ability to handle any team composition
- Continuous improvement built into infrastructure
- More resilient systems overall

**The honest truth:**
Your AI coding agent isn't breaking your process. It's giving you a free, comprehensive stress test showing exactly where to invest in infrastructure. The question is whether you'll use that information to build something stronger.

The future belongs to development teams whose pipelines can handle imperfect code from any source. AI is just forcing us to build them sooner. And that's actually a gift.

