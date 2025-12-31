---
summary: Addy Osmani outlines a disciplined LLM coding workflow emphasizing planning first, iterative chunking, rich context management, model selection flexibility, human accountability, version control discipline, and robust quality infrastructure—treating humans as directors of AI-amplified development
event_type: blog_post
sources:
    - https://addyo.substack.com/p/my-llm-coding-workflow-going-into
tags:
    - LLM-coding
    - AI-assisted-development
    - workflow-discipline
    - code-quality
    - human-oversight
    - planning
    - version-control
    - testing
    - Addy-Osmani
---

# My LLM Coding Workflow Going into 2026

**Author:** Addy Osmani
**Publication:** Elevate (Substack)
**Publication Date:** December 18, 2025
**Type:** Practical Workflow and Process Guide
**Duration:** Complete methodology for AI-assisted development
**Key Concept:** Disciplined approach to LLM-based coding with human oversight as centerpiece

## Overview

Addy Osmani outlines a disciplined, structured approach to AI-assisted software development, emphasizing that effective LLM coding requires deliberate process design and human oversight rather than naive automation. Rather than asking AI to write code and hoping for the best, Osmani advocates a methodology built around planning first, working iteratively in small chunks, providing rich context, selecting appropriate models, maintaining human accountability, using version control as safety infrastructure, and building quality systems that help AI self-correct. The philosophy is clear: humans remain the directors; AI amplifies expertise.

## The Core Philosophy: Human Direction, AI Amplification

### The Central Principle

**AI will happily produce plausible-looking code.**

But humans remain responsible for:
- Correctness
- Quality
- Safety
- Understanding every line before deployment

### The Role Clarification

**Humans:** Directors of the show
**AI:** Amplifier of expertise

Not:
- AI as autonomous developer
- AI as replacement for judgment
- AI as source of truth

But:
- AI as tool magnifying human capability
- AI as assistant following human direction
- AI as executor of human-designed plans

## Principle 1: Planning First — Detailed Specifications Before Code

### Why Planning Matters

**Problem it solves:**
- Vague requirements → messy code
- Unclear expectations → wasted iterations
- Misaligned goals → rework required
- Confusion → poor quality

**Planning prevents:**
- Circular refinement cycles
- Scope creep mid-implementation
- Fundamental misunderstandings
- Wasted AI generations

### The Planning Process

**Step 1: Define Requirements**
- What problem are we solving?
- Who is this for?
- What are the constraints?
- What's out of scope?

**Step 2: Identify Edge Cases**
- What could go wrong?
- What are the boundary conditions?
- What are the error scenarios?
- What's the failure mode?

**Step 3: Sketch Architecture**
- How should this be organized?
- What are the main components?
- How do they interact?
- What are the dependencies?

**Step 4: Create Specification**
- Document all findings
- Make it comprehensive
- Be specific, not vague
- Include examples and scenarios

### Collaborating with AI on Specifications

**The process:**
1. Share initial thoughts with AI
2. AI asks clarifying questions
3. Refine requirements based on feedback
4. AI helps identify edge cases
5. AI suggests architectural patterns
6. Human validates and finalizes
7. Compile into specification document

**Why this works:**
- AI helps think through problems
- AI suggests patterns and edge cases
- Humans maintain control and judgment
- Specification becomes shared understanding
- Alignment achieved before coding

### The Specification Document

**Should include:**
- Problem statement
- Requirements (functional and non-functional)
- Edge cases and error handling
- Architecture overview
- Data models
- API contracts
- Examples of expected behavior
- Constraints and limitations
- Testing strategy
- Deployment considerations

**Benefits:**
- Clear expectations for AI
- Reference point for implementation
- Testable requirements
- Reduces iterations
- Enables progress tracking

## Principle 2: Iterative Chunking — Small, Manageable Tasks

### Why Chunking Matters

**Large code generation problems:**
- Models get confused
- Output becomes inconsistent
- Context degradation
- Hard to debug failures
- Difficult to iterate

**Small chunked tasks:**
- Clear focus
- Consistent output
- Easy to verify
- Simple to iterate
- Traceable logic

### The Chunking Strategy

**Break projects into logical pieces:**

| Task | Size | Scope |
|------|------|-------|
| Write API endpoint | Small | Single responsibility |
| Implement data model | Small | Schema + CRUD |
| Add validation layer | Small | Input validation |
| Write tests | Chunked | One feature at a time |
| Integrate components | Small | Two-component glue |

**Not:**
- "Build the whole system"
- "Write the complete auth flow"
- "Implement all database operations"

**But:**
- "Implement login endpoint validation"
- "Add password hashing function"
- "Write user creation tests"

### Sequential Execution

**Process:**
1. Execute task 1
2. Verify and integrate
3. Execute task 2
4. Verify and integrate
5. Continue...

**Benefits:**
- Each piece can be reviewed
- Mistakes caught early
- Easier to rollback
- Progress is visible
- Complexity manageable

### Example Workflow

**Feature: User Authentication**

Chunk 1: User model definition
- Database schema
- ORM model
- Validation rules

Chunk 2: Password hashing
- Hash function
- Salt strategy
- Verification function

Chunk 3: Login endpoint
- Request validation
- Hash comparison
- Response handling

Chunk 4: Token generation
- JWT structure
- Signing
- Expiration

Chunk 5: Middleware
- Token verification
- Request enrichment
- Error handling

Chunk 6: Tests
- Happy path
- Edge cases
- Security scenarios

## Principle 3: Context Management — Rich Information for Better Output

### The Context Problem

**Poor context:**
- AI guesses about your codebase
- Makes incorrect assumptions
- Produces incompatible code
- Needs many iterations

**Rich context:**
- AI understands your patterns
- Produces consistent code
- Respects your conventions
- Fewer iterations needed

### What Context to Provide

**Essential context:**

| Context Type | Examples | Value |
|-------------|----------|-------|
| **Existing code** | Similar implementations, patterns | Shows expected style and structure |
| **Technical constraints** | Framework versions, libraries | Prevents incompatibility |
| **API documentation** | Endpoint specs, data contracts | Ensures correct usage |
| **Architecture docs** | System design, dependencies | Maintains consistency |
| **Code standards** | Naming conventions, style guides | Produces consistent code |

### How to Provide Context

**Option 1: Direct inclusion**
Copy relevant snippets directly into prompt.

**Option 2: Bundled files**
Use tools like gitingest to bundle project files.

**Option 3: Documentation**
Include architecture docs, API references.

**Option 4: Specification**
Reference the planning spec created earlier.

### Context Best Practices

**1. Include working examples**
"Here's how we do validation in this project..."
Shows expected patterns.

**2. Share relevant snippets**
Don't need whole files, just the relevant parts.

**3. Document your patterns**
"We use X pattern for Y problem."

**4. Explain constraints**
"We target Node 18+, TypeScript, avoid regex."

**5. Show anti-patterns**
"We avoid using this pattern because..."

**6. Include test examples**
Shows expected behavior and testing style.

## Principle 4: Model Selection — Choose the Right Tool for the Task

### The Reality: No One-Size-Fits-All

**Different models have different strengths:**
- Some excel at reasoning
- Some at code generation
- Some at analysis
- Some at documentation

**The implication:**
Use different models for different tasks.

### Model Strengths Vary

| Task | Strong Models | Why |
|------|---------------|-----|
| **Code generation** | Claude, Grok | Training on code, reasoning |
| **Reasoning/Analysis** | Claude, o1 | Deep reasoning capability |
| **Structured output** | Claude | Format compliance |
| **Long context** | Gemini 2.0 | Very large context windows |
| **Speed** | Grok, Llama | Fast inference |
| **Specialization** | Domain-specific | Trained on specific domains |

### The Selection Process

**For each task:**
1. Understand the task requirements
2. Consider relevant model strengths
3. Test multiple models if critical
4. Use model that performs best
5. Document why that model was chosen

**Example:**
- Authentication logic → Claude (reasoning)
- Database queries → Claude (code + reasoning)
- Performance optimization → o1 (deep reasoning)
- Documentation generation → Any capable model
- Quick refactoring → Fast model (Grok)

### Avoiding Tool Lock-In

**Don't:**
- Pick one LLM and only use it
- Assume it's best for all tasks
- Ignore model-specific strengths

**Do:**
- Test models on your specific tasks
- Use different models where appropriate
- Keep integrations flexible
- Switch as new models emerge

## Principle 5: Human Accountability — Verification Before Deployment

### The Core Responsibility

**Humans are accountable for:**
- Code correctness
- Security
- Performance
- Maintainability
- Deployment safety

**AI is a tool**, not a source of authority.

### What This Means Practically

**You must:**
1. Read the generated code
2. Understand every line
3. Test it thoroughly
4. Review for security issues
5. Check for performance problems
6. Verify it matches requirements
7. Ensure it follows standards
8. Only then deploy it

### Code Review

**Review types:**

| Review Type | Checker | Purpose |
|------------|---------|---------|
| **Correctness** | Human | Does it work? |
| **Security** | Human + AI | Are there vulnerabilities? |
| **Performance** | Human | Could it be faster? |
| **Style** | AI (linter) | Does it match standards? |
| **Consistency** | Human | Matches codebase patterns? |
| **Clarity** | Human | Is it understandable? |

**AI can help with style and format.**
**Humans must verify correctness and safety.**

### Testing Responsibility

**You must ensure:**
- Tests cover happy path
- Tests cover edge cases
- Tests cover error cases
- Tests verify security
- Tests check performance
- Tests run and pass
- Tests are maintainable

**AI can help generate tests, but you verify they're correct.**

### The Verification Checklist

Before deploying code generated by AI:
- [ ] Read all code thoroughly
- [ ] Understand every line
- [ ] Run all tests (they pass)
- [ ] Code review completed
- [ ] Security check done
- [ ] Performance verified
- [ ] Deployment tested
- [ ] Rollback plan ready

## Principle 6: Version Control Discipline — Granular Checkpoints

### Why Version Control Matters

**Version control serves as:**
- Safety net (easy rollback)
- Progress tracking
- Change documentation
- Collaboration tool
- Audit trail

### Granular Commits

**Make frequent, small commits:**

| Commit | Message | Size |
|--------|---------|------|
| First | Add user model schema | 50 lines |
| Second | Implement password hashing | 30 lines |
| Third | Add login validation | 60 lines |
| Fourth | Write user tests | 80 lines |

**Not:**
- One giant commit: "Implement authentication" (300 lines)

**But:**
- Many small commits, each logically complete

### Benefits of Granular Commits

**1. Easy to understand**
Each commit is focused and clear.

**2. Easy to review**
Reviewers can understand changes.

**3. Easy to rollback**
If one commit is problematic, revert it specifically.

**4. Easy to debug**
Use git bisect to find problematic commits.

**5. Easy to cherry-pick**
Move specific commits between branches.

**6. Safe checkpoints**
Each commit is a known-good state.

### Commit Message Discipline

**Write clear messages:**

```
Good:
"Add password validation to login endpoint"
"Implement bcrypt hashing for user passwords"
"Write tests for user creation"

Bad:
"Fix stuff"
"Updates"
"WIP"
```

**Message should explain:**
- What changed
- Why it changed
- Any important context

## Principle 7: Quality Infrastructure — Feedback Loops for Improvement

### The Purpose

Quality infrastructure helps:
- AI identify mistakes early
- Humans catch issues before deployment
- Automated testing prevent regressions
- Standards stay consistent

### Components of Quality Infrastructure

#### 1. Automated Testing

**Purpose:** Catch bugs automatically

**What to test:**
- Unit tests (individual functions)
- Integration tests (component interactions)
- End-to-end tests (full workflows)
- Security tests (vulnerability checks)
- Performance tests (speed/resource use)

**Who benefits:**
- AI learns from test failures
- Humans get confidence
- Teams get regression detection

#### 2. Linting and Formatting

**Purpose:** Enforce code standards

**What it does:**
- Style consistency
- Common mistake detection
- Security rule checking
- Performance anti-pattern detection

**Why it helps:**
- AI gets immediate feedback
- Standards automatically enforced
- Frees humans from style review

#### 3. Type Checking

**Purpose:** Catch type errors

**Tools:**
- TypeScript
- mypy (Python)
- Go's built-in typing
- Flow (JavaScript)

**Why it helps:**
- Catches errors before runtime
- AI learns what's valid
- Type safety enforced

#### 4. CI/CD Pipeline

**Purpose:** Automated verification

**What it does:**
1. Run all tests
2. Run linters
3. Check types
4. Build the application
5. Run security checks
6. Report results

**Why it helps:**
- Feedback within minutes
- AI can learn from failures
- Broken code never reaches production
- Safe to take risks

#### 5. Code Review

**Purpose:** Human verification

**What to review:**
- Correctness of logic
- Security implications
- Performance concerns
- Alignment with architecture
- Code clarity

**Can involve:**
- Manual review (traditional)
- AI-assisted review (faster)
- Pair programming (collaborative)

#### 6. Monitoring and Alerting

**Purpose:** Catch issues in production

**What to monitor:**
- Errors and exceptions
- Performance metrics
- Resource usage
- User-facing issues

**Why it helps:**
- Problems detected immediately
- Quick response possible
- Data for improvement

### Creating the Feedback Loop

```
AI generates code
    ↓
Automated tests run
    ↓
Linting/formatting check
    ↓
Type checker runs
    ↓
CI/CD pipeline executes
    ↓
Results reported
    ↓
Human reviews
    ↓
Feedback to AI (if iterating)
    ↓
Or deployment (if all good)
```

**Speed matters:**
Feedback within minutes, not hours.

## Practical Workflow Example

### Building a Feature: User Preferences API

#### Phase 1: Planning
- Define requirements
- Identify edge cases
- Sketch architecture
- Create specification

#### Phase 2: Chunk 1 — Data Model
Request to AI:
"Create a user preferences data model based on this specification..."
- AI generates schema
- Review and verify
- Commit to version control

#### Phase 3: Chunk 2 — API Endpoint
Request to AI:
"Create the GET /api/preferences endpoint based on..."
- AI generates endpoint code
- Test locally
- Run tests
- Code review
- Commit

#### Phase 4: Chunk 3 — Validation
Request to AI:
"Add input validation to the preferences endpoint..."
- AI adds validation
- New tests run
- Old tests still pass
- Commit

#### Phase 5: Chunk 4 — Tests
Request to AI:
"Write comprehensive tests for preferences endpoint..."
- AI generates tests
- Review for coverage
- Run all tests
- Commit

#### Phase 6: Integration
- All commits together form feature
- Full system test
- Staging deployment
- Production deployment

#### Phase 7: Monitoring
- Watch for errors
- Monitor performance
- Gather user feedback
- Plan improvements

## Key Takeaways

1. **Human as director** — Humans guide, AI amplifies
2. **Planning first** — Detailed specs before code
3. **Collaborative specs** — Work with AI to define requirements
4. **Chunking strategy** — Small, sequential, manageable tasks
5. **Context rich** — Provide extensive relevant information
6. **Model selection** — Use different models for different tasks
7. **No tool lock-in** — Test models, choose best fit
8. **Human accountability** — Humans verify correctness
9. **Read all code** — Understand every line before deployment
10. **Thorough testing** — Your responsibility to verify
11. **Code review** — Human verification of logic and security
12. **Version control** — Frequent, granular, safe commits
13. **Small commits** — Easy to understand and rollback
14. **Automated testing** — Catch bugs early
15. **Linting/formatting** — Enforce standards automatically
16. **Type checking** — Catch errors before runtime
17. **CI/CD pipeline** — Automated verification in minutes
18. **Fast feedback** — Results within minutes, not hours
19. **Monitoring** — Catch production issues
20. **Iterate safely** — Frequent commits make risk safe

## The Bottom Line

Addy Osmani presents a disciplined, structured approach to LLM-assisted coding that prioritizes human oversight, planning, and systematic verification over naive automation.

**The core philosophy:**
Humans remain directors; AI amplifies expertise. AI will happily produce plausible-looking code, but humans are responsible for correctness, quality, and safety.

**The seven principles:**

1. **Plan first** — Create detailed specifications before coding
2. **Chunk iteratively** — Break projects into small, manageable tasks
3. **Manage context** — Provide rich, relevant information to AI
4. **Select models** — Choose appropriate models for specific tasks
5. **Maintain accountability** — Humans verify every line before deployment
6. **Use version control** — Frequent, granular, safe commits
7. **Build quality infrastructure** — Testing, linting, CI/CD, monitoring

**The workflow:**
Plan → Specify → Chunk → Generate → Verify → Test → Review → Commit → Integrate → Deploy → Monitor

**For success:**
- Don't treat AI as autonomous developer
- Don't skip planning or verification
- Don't deploy without human review
- Don't ignore testing
- Do maintain high standards
- Do stay accountable
- Do verify everything

This approach transforms AI from a risky autocomplete into a capable assistant that can significantly amplify human expertise while maintaining quality, safety, and human control.

The future of LLM-assisted coding isn't about letting AI code alone—it's about humans and AI working together systematically, with humans maintaining direction and accountability at every step.

