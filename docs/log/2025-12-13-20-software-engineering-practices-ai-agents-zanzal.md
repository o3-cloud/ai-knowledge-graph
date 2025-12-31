---
summary: Owen Zanzal presents 20 software engineering practices and tools AI agents should be taught—from semantic commits and ADRs to mutation testing and canary analysis—with focus on how each practice enables agents to reason, learn, and operate autonomously
event_type: blog_post
sources:
    - https://medium.com/devops-ai/20-software-engineering-practices-and-tools-we-should-teach-our-ai-agents-today-914ccab7332b
tags:
    - AI-agents
    - software-engineering
    - best-practices
    - DevOps
    - testing
    - architecture
    - operational-excellence
    - agent-training
---

# 20 Software Engineering Practices (and Tools) We Should Teach Our AI Agents Today

**Author:** Owen Zanzal
**Publication:** DevOps<>AI
**Publication Date:** December 13, 2025
**Read Time:** 4 minutes

## Overview

Owen Zanzal catalogs 20 concrete software engineering practices and associated tools that AI agents need to understand and apply effectively. Rather than treating AI agents as black boxes that magically produce code, this framework recognizes that agents operating in mature codebases need explicit instruction in how that codebase thinks, structures decisions, and validates quality.

The key insight: each practice isn't just good software engineering—it's a communication protocol between human developers and AI agents, allowing agents to understand intent, prevent regressions, and learn from patterns in the codebase.

## The Core Philosophy

### Why Teach Practices to Agents?

**Traditional AI agent approach:**
- Give agent codebase
- Ask it to do something
- Hope it figures out the patterns

**Better approach:**
- Explicitly teach practices
- Make patterns explicit
- Enable agents to reason about decisions
- Build systems that teach themselves

**The shift:**
From "hope the agent is smart enough" to "make success inevitable through structure."

## The 20 Practices and Tools

### 1. Semantic Commit Messages with Conventional Commits

**Practice:**
Write structured commits like:
- `feat(auth): add OAuth2 support`
- `fix(db): resolve connection pool exhaustion`
- `docs(api): update endpoint documentation`

**Tools:**
- commitlint (enforces format)
- commitizen (interactive commit builder)
- semantic-release (auto-generates changelogs)

**Why it matters for AI:**
- Agents can understand change intent
- Can generate accurate changelogs automatically
- Can predict impact radius from commit patterns
- Can reason about what changed and why

**Agent capability unlocked:**
Understanding not just code changes, but the intention and impact of those changes.

### 2. Property-Based Testing Beyond Unit Tests

**Practice:**
Define invariants and let framework generate test cases.

**Examples:**
- "Sorting never changes array length"
- "Hashing same input always produces same output"
- "Payment amounts must stay positive"

**Tools:**
- Hypothesis (Python)
- fast-check (JavaScript)
- QuickCheck (Haskell)

**Why it matters for AI:**
- Agents reason about properties rather than memorizing specific test cases
- Can generate new test cases exploring edge cases
- Understands fundamental constraints of system

**Agent capability unlocked:**
Moving from "pass these specific tests" to "maintain these invariants."

### 3. Architecture Decision Records (ADRs) as Code

**Practice:**
Document every non-trivial decision in markdown files with:
- Context (why decision was needed)
- Options considered
- Rationale for chosen option
- Consequences and tradeoffs

**Tools:**
- adr-tools (CLI for ADR management)
- Log4brains (visual ADR documentation)
- Backstage TechDocs (centralized documentation)

**Why it matters for AI:**
- Prevents agents from unknowingly reverting architectural decisions
- Stops agents from proposing already-rejected solutions
- Provides context for design choices
- Explains why certain approaches were intentionally not taken

**Agent capability unlocked:**
Understanding not just what was decided, but why alternatives were rejected.

### 4. Contract Testing at Boundaries

**Practice:**
Define explicit contracts between services/modules that can be verified independently.

**Pattern:**
Service A must call Service B with these inputs; Service B guarantees these outputs.

**Tools:**
- Pact (contract testing framework)
- Spring Cloud Contract
- OpenAPI validators

**Why it matters for AI:**
- Agents can modify implementations while guaranteeing interface compatibility
- Can refactor internals without breaking contracts
- Knows exactly what assumptions downstream services make

**Agent capability unlocked:**
Safe refactoring while maintaining system-wide consistency.

### 5. Observability-Driven Development (ODD)

**Practice:**
Add metrics, traces, and structured logs before writing business logic.

**Approach:**
Design observability first, then implement features.

**Tools:**
- OpenTelemetry (unified observability)
- Honeycomb (log analysis)
- Datadog (monitoring and alerting)

**Why it matters for AI:**
- Agents get immediate feedback on system behavior
- Don't have to wait for human interpretation
- Can see patterns across logs and metrics
- Understands impact of changes in real time

**Agent capability unlocked:**
Autonomous verification of behavior without human intermediaries.

### 6. Explicit Error Handling Strategies

**Practice:**
Document and implement consistent patterns:
- Retry logic (exponential backoff)
- Circuit breakers (prevent cascade failures)
- Fallback strategies (graceful degradation)

**Tools:**
- Resilience4j (Java)
- Polly (.NET)
- Hystrix patterns

**Why it matters for AI:**
- Agents know exactly how to handle failures
- Not guessing at recovery strategies
- Understands which failures are recoverable
- Can implement consistent error handling across codebase

**Agent capability unlocked:**
Robust failure handling without human intervention.

### 7. Feature Flags as Experimental Infrastructure

**Practice:**
Ship code dark and gradually roll out with kill switches.

**Pattern:**
Deploy code, gradually enable for users, measure impact, roll back if needed.

**Tools:**
- LaunchDarkly (commercial feature management)
- Unleash (open-source)
- Flipper (Rails-native)
- OpenFeature (vendor-neutral)

**Why it matters for AI:**
- Agents can safely deploy risky changes
- Measure impact incrementally
- Roll back instantly if issues detected
- Can A/B test different approaches

**Agent capability unlocked:**
Safe experimental deployment and validation.

### 8. Dependency Injection with Explicit Wiring

**Practice:**
Make all dependencies explicit and injectable, avoiding magic or implicit construction.

**Pattern:**
Instead of component finding its own dependencies, they're explicitly provided.

**Tools:**
- Wire (Go)
- Dagger (Java/Android)
- inversify (TypeScript)

**Why it matters for AI:**
- Agents can trace data flow clearly
- Can modify components without breaking hidden dependencies
- Understands exactly what each component needs
- Can safely swap implementations

**Agent capability unlocked:**
Understanding component relationships and safe modification.

### 9. Database Migration as Code

**Practice:**
Version control schema changes with up/down migrations and data transformation scripts.

**Pattern:**
Every schema change is a migration; can be applied or rolled back.

**Tools:**
- Flyway (Java)
- Liquibase (multi-platform)
- Alembic (Python)
- golang-migrate (Go)

**Why it matters for AI:**
- Agents can evolve schemas safely
- Automatic rollback capabilities exist
- Understands data transformation requirements
- Can preview impact of schema changes

**Agent capability unlocked:**
Safe database evolution with rollback guarantees.

### 10. Design by Contract with Runtime Assertions

**Practice:**
Define preconditions, postconditions, and invariants checked at runtime.

**Pattern:**
Functions explicitly state what they require and guarantee.

**Tools:**
- Python's contracts library
- Java's Bean Validation
- Eiffel patterns

**Why it matters for AI:**
- Agents get immediate feedback when violating assumptions
- Understands what inputs functions accept
- Knows what outputs to expect
- Catches violations before they cascade

**Agent capability unlocked:**
Immediate validation of assumption violations.

### 11. Structured Logging with Correlation IDs

**Practice:**
Use JSON logs with consistent fields; trace requests across services.

**Pattern:**
Every log entry structured; correlation IDs link related entries.

**Tools:**
- structlog (Python)
- logrus (Go)
- winston with correlation middleware (Node.js)

**Why it matters for AI:**
- Agents trace issues across distributed systems
- Don't need human interpretation to understand flows
- Can correlate events happening in different services
- Understands system behavior from log patterns

**Agent capability unlocked:**
Autonomous distributed system debugging.

### 12. API Versioning with Sunset Headers

**Practice:**
Version APIs explicitly; communicate deprecation timelines programmatically.

**Pattern:**
APIs are versioned; HTTP Sunset headers communicate when old versions end.

**Tools:**
- API versioning middleware
- Sunset HTTP headers
- OpenAPI versioning

**Why it matters for AI:**
- Agents understand compatibility requirements
- Know migration timelines for API changes
- Can propose compatible changes
- Understands breaking change implications

**Agent capability unlocked:**
Safe evolution of public interfaces.

### 13. Mutation Testing for Test Quality

**Practice:**
Verify test effectiveness by introducing bugs and ensuring tests catch them.

**Pattern:**
Framework introduces intentional bugs; if tests don't catch them, tests are inadequate.

**Tools:**
- Pitest (Java)
- mutmut (Python)
- Stryker (JavaScript)

**Why it matters for AI:**
- Agents assess whether their tests actually prevent regressions
- Understands which tests are effective
- Knows whether coverage is meaningful
- Can improve test quality based on mutation scores

**Agent capability unlocked:**
Quality assurance for the quality assurance system.

### 14. Performance Budgets in CI/CD

**Practice:**
Define and enforce performance thresholds:
- Response time limits
- Bundle size constraints
- Memory usage bounds

**Tools:**
- Lighthouse CI (web performance)
- k6 (load testing)
- WebPageTest API
- pytest-benchmark (Python)

**Why it matters for AI:**
- Agents get automatic feedback when changes degrade performance
- Understands performance constraints
- Can't accidentally introduce slow code
- Measures impact of changes on system performance

**Agent capability unlocked:**
Automatic performance regression prevention.

### 15. Documentation as Tests

**Practice:**
Write executable documentation that fails if code examples become outdated.

**Pattern:**
Documentation code examples are actually run as tests.

**Tools:**
- doctest (Python)
- Spring REST Docs (Java)
- MDX (React components in markdown)
- Cucumber (behavior-driven)

**Why it matters for AI:**
- Agents maintain accurate documentation automatically
- Documentation and code stay synchronized
- Understands what examples demonstrate
- Can't accidentally break documentation

**Agent capability unlocked:**
Self-maintaining documentation.

### 16. Deterministic Builds and Environments

**Practice:**
Pin all dependencies; use lock files; ensure reproducible builds.

**Pattern:**
Same source code + same inputs = identical build always.

**Tools:**
- Nix (reproducible environments)
- Bazel (hermetic builds)
- Docker with specific tags
- poetry/npm lock files

**Why it matters for AI:**
- Agents can confidently modify dependencies knowing exact outcomes
- Understands dependency state exactly
- Can reproduce issues reliably
- Knows side effects of dependency changes

**Agent capability unlocked:**
Predictable, reproducible modifications.

### 17. Canary Analysis with Statistical Rigor

**Practice:**
Deploy to small traffic percentage; automatically analyze metrics for regressions.

**Pattern:**
Deploy to 5% of users, measure metrics, automatically roll back if bad.

**Tools:**
- Flagger (automated canary analysis)
- Spinnaker (deployment platform)
- Argo Rollouts with Prometheus

**Why it matters for AI:**
- Agents can deploy and validate changes without human oversight
- Gets statistical feedback on impact
- Can automatically roll back if issues detected
- Understands deployment safety

**Agent capability unlocked:**
Autonomous deployment with validation.

### 18. Code Ownership via CODEOWNERS

**Practice:**
Explicitly define who owns what code; require their review.

**Pattern:**
Each file has defined owner; changes require their approval.

**Tools:**
- GitHub CODEOWNERS
- GitLab Code Owners
- Bitbucket CODEOWNERS

**Why it matters for AI:**
- Agents know exactly who to consult for different parts
- Understands decision authority for each area
- Can respect domain ownership
- Prevents agents from making decisions in unfamiliar domains

**Agent capability unlocked:**
Respecting organizational structure and expertise.

### 19. Snapshot Testing for Complex Outputs

**Practice:**
Capture expected output and detect any changes, intentional or not.

**Pattern:**
Store reference output; fail if actual output differs (unless updated).

**Tools:**
- Jest snapshots (JavaScript)
- pytest-snapshot (Python)
- cupaloy (Go)

**Why it matters for AI:**
- Agents refactor safely while ensuring output remains consistent
- Can't accidentally change behavior
- Catches subtle output differences
- Enables confident refactoring

**Agent capability unlocked:**
Safe refactoring with regression detection.

### 20. Runbooks as Executable Playbooks

**Practice:**
Write operational procedures as scripts that can be run, not just read.

**Pattern:**
Runbooks are executable code, not prose documentation.

**Tools:**
- Ansible (infrastructure automation)
- Rundeck (job execution)
- StackStorm (workflow automation)
- Jupyter notebooks (for ops)

**Why it matters for AI:**
- Agents execute recovery procedures without interpreting prose
- Understands operational procedures exactly
- Can run them without human intermediaries
- Handles incident response autonomously

**Agent capability unlocked:**
Autonomous operational procedures and incident response.

## The Meta-Practice: Teaching Agents to Learn

### The Most Important Practice Isn't on the List

**Key insight:**
Teach your AI agents to recognize when they need to learn a new practice.

**What agents should do when encountering unfamiliar patterns:**

1. **Search for existing examples** in the codebase
2. **Look for documentation** in the repo
3. **Check for configuration files** that might explain the pattern
4. **Ask for clarification** rather than guess

**Why this matters:**
- Codebases evolve and introduce new patterns
- New testing frameworks appear
- Unfamiliar architectural patterns emerge
- Domain-specific conventions develop

### Building Systems That Teach Themselves

**The real goal:**
Not to teach agents everything upfront, but to build codebases that teach themselves.

**How this works:**
- Agents encounter unfamiliar pattern
- Follow systematic process to learn it
- Apply pattern correctly
- Next agent encounters same pattern more easily

**Result:**
Codebases become increasingly self-documenting and self-teaching.

## Why These Practices Matter for Agents

### Principle 1: Practices Are Communication Protocols

Each practice is a way of saying:
- "This is what we care about"
- "This is how we ensure quality"
- "This is what makes decisions"
- "This is where to look for truth"

**For agents:**
These protocols are how humans and agents communicate about code quality and system behavior.

### Principle 2: Practices Enable Autonomous Operation

Without explicit practices:
- Agents must guess at intent
- Must infer quality standards
- Must reverse-engineer decision logic
- Must hope they understand culture

**With explicit practices:**
- Intent is clear
- Quality is measurable
- Decisions are documented
- Culture is codified

### Principle 3: Practices Create Feedback Loops

Every practice listed provides automatic feedback:
- Tests fail → immediate feedback
- Contracts break → immediate feedback
- Performance budgets exceeded → immediate feedback
- Assertions fail → immediate feedback

**For agents:**
This feedback enables learning and iteration.

## Implementation Strategy

### How to Teach These Practices to Your Agents

**Step 1: Identify Current Practices**
What practices is your codebase already using?

**Step 2: Document in Codebase**
Write guides/examples for each practice.

**Step 3: Make Tooling Explicit**
List tools and how to use them.

**Step 4: Include in Agent Context**
When briefing agents, reference relevant practices.

**Step 5: Enforce with CI/CD**
Tools should automatically enforce practices.

**Step 6: Evolve Over Time**
Add new practices as codebase matures.

## The Progression: From Chaos to Structure

### Level 1: No Explicit Practices
- Agents must guess
- Quality is inconsistent
- Decisions are ad hoc
- Codebases are fragile

### Level 2: Some Practices
- Common practices visible
- Quality improving
- Some guidance exists
- Codebases more stable

### Level 3: All 20 Practices
- Comprehensive structure
- Quality is measurable
- Decisions are documented
- Codebases are resilient

### Level 4: Self-Teaching Codebase
- Agents learn new practices automatically
- Codebase evolves gracefully
- New team members learn quickly
- System improves over time

## Key Takeaways

1. **Semantic commits enable understanding** — Agents understand change intent and impact
2. **Property-based testing teaches invariants** — Agents reason about constraints, not just cases
3. **ADRs prevent repeating mistakes** — Agents know why options were rejected
4. **Contract testing enables safe refactoring** — Agents can modify internals confidently
5. **Observability-driven development** — Agents get immediate feedback without humans
6. **Explicit error handling** — Agents know recovery strategies, don't guess
7. **Feature flags enable safe deployment** — Agents can deploy risky changes safely
8. **Dependency injection clarifies relationships** — Agents understand dependencies explicitly
9. **Database migrations as code** — Agents can evolve schemas safely
10. **Design by contract** — Agents get immediate feedback on violations
11. **Structured logging** — Agents trace systems autonomously
12. **API versioning** — Agents understand compatibility requirements
13. **Mutation testing** — Agents verify test quality
14. **Performance budgets** — Agents prevent performance regressions
15. **Documentation as tests** — Agents maintain accurate documentation
16. **Deterministic builds** — Agents know dependency impacts exactly
17. **Canary analysis** — Agents deploy and validate autonomously
18. **Code ownership** — Agents respect domain expertise
19. **Snapshot testing** — Agents refactor confidently
20. **Executable runbooks** — Agents handle incidents autonomously
21. **Meta-practice: teaching agents to learn** — Codebases become self-teaching

## The Bottom Line

Owen Zanzal's list of 20 practices isn't about following the latest trends. It's about making your codebase legible to AI agents.

**Each practice answers a specific question for agents:**

- Semantic commits: "What was this change trying to achieve?"
- ADRs: "Why was this approach chosen?"
- Contract testing: "What can I safely change?"
- Observability: "Did my change break anything?"
- Error handling: "How should I recover from failure?"
- Feature flags: "How can I deploy safely?"
- CODEOWNERS: "Who should approve this?"
- Tests: "What should succeed?"

**The radical insight:**
The more explicit and structured your practices are, the more autonomous your agents can be.

This doesn't mean removing human judgment. It means encoding human judgment into tools, tests, and structures so agents can operate confidently within those constraints.

**The goal:**
Build codebases that teach themselves, where agents learn patterns through systematic observation and explicit documentation, where practices accumulate into increasingly self-organizing systems.

Start with the practices that matter most in your codebase. Document them. Make them explicit. Let your agents learn. Then add more as your maturity increases.

The future isn't agents replacing engineers. It's engineers building practices that allow agents to accelerate engineering while maintaining quality and safety.

