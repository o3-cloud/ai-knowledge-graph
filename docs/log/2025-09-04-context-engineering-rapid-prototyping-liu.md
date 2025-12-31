---
summary: Jason Liu advocates validating agent concepts rapidly using Claude Code project mode with CLAUDE.md instructions, CLI tool wrappers, and concrete test scenarios—avoiding months of infrastructure building before proving feasibility
event_type: blog_post
sources:
    - https://jxnl.co/writing/2025/09/04/context-engineering-rapid-agent-prototyping/
tags:
    - context-engineering
    - agent-prototyping
    - Claude-Code
    - rapid-validation
    - test-driven-development
    - tool-design
    - prototype-methodology
    - MVP-agents
---

# Context Engineering: Rapid Agent Prototyping

**Author:** Jason Liu
**Source:** jxnl.co
**Publication Date:** September 4, 2025

## Overview

Jason Liu presents a methodology for validating agent concepts quickly using Claude Code as a testing harness before investing in production infrastructure. The core principle: use Claude Code's project mode to test whether an idea works with perfect tool access and no constraints. If it doesn't work there, it won't work in production. This approach reduces time from idea to evidence from weeks to hours.

## The Core Problem

### The Infrastructure Trap

**Common pattern:**
Teams spend months building agent frameworks before knowing if their idea actually works.

**Result:**
- Months of work
- Uncertain feasibility
- Wasted resources
- Unknown architectural requirements

**The trap:**
Assuming you need infrastructure before validating concept.

### The Question

**Better approach:**
Can this idea work? Prove it first, build infrastructure later.

**Validation method:**
Use Claude Code as harness; if it doesn't work with perfect tool access, production won't either.

## Rapid Prototyping Methodology

### Core Principle

**Philosophy:**
Validate feasibility before building infrastructure.

**Timeline:**
- Prototype and passing test: hours
- Production build: later, if needed

**Risk reduction:**
Discover whether idea is sound before major investment.

### Prototype Anatomy

**Standard structure:**

```
agent-prototype/
├── CLAUDE.md              # System instructions + tool inventory
├── tools/                 # CLI wrappers for APIs
│   ├── fetch_youtube.sh
│   ├── analyze_content.sh
│   └── save_notes.sh
└── tests/                 # Test scenarios with validation
    ├── scenario1/
    │   ├── request.txt    # Input specification
    │   └── check.py       # Success validation
    ├── scenario2/
    ├── scenario3/
```

**Each component serves specific purpose.**

### Execution Model

**How it works:**

```
Write CLAUDE.md with system instructions
    ↓
Create CLI tool wrappers for APIs
    ↓
Define test scenarios with inputs
    ↓
Write success validation (check.py)
    ↓
Run: claude -p
    ↓
Claude reads CLAUDE.md
    ↓
Claude executes tools via CLI
    ↓
Tests validate output
    ↓
Iterate until tests pass
```

**Speed:**
Hours from concept to evidence of feasibility.

## CLAUDE.md: The System Prompt

### Structure and Content

**Key sections:**

#### Mission Statement
Clear problem definition.

**Example:**
```markdown
# Mission
Given a YouTube URL, produce structured study notes
with organized sections, key takeaways, and further
reading recommendations.
```

**Purpose:**
Clarify what success looks like.

#### Execution Flow
Step-by-step workflow with tool sequencing.

**Example:**
```markdown
# Execution Flow
1. Fetch YouTube transcript with fetch_youtube
2. Analyze content structure with analyze_content
3. Generate notes with generate_notes
4. Validate against success criteria
5. Save to notes.md
```

**Purpose:**
Guide Claude through logical sequence.

#### Available Tools
Documented CLI commands with expected outputs.

**Example:**
```markdown
# Available Tools

## fetch_youtube
- Usage: ./tools/fetch_youtube.sh <url>
- Returns: transcript.txt
- On error: Provides helpful next step

## analyze_content
- Usage: ./tools/analyze_content.sh transcript.txt
- Returns: structure.json with sections
- Outputs: section_count, key_themes
```

**Purpose:**
Let Claude discover what's available.

#### Success Criteria
Concrete, measurable requirements.

**Example:**
```markdown
# Success Criteria
- Output file: notes.md exists
- Structure: One H1 title, three H2 sections
- Content density: 10+ bullet points per section
- Links: "Further Reading" section with 3+ sources
- Format: Valid markdown
```

**Purpose:**
Enable automated validation.

#### Error Recovery
Specific handling for predictable failures.

**Example:**
```markdown
# Error Handling
- If transcript unavailable: Try alternative video sources
- If content too long: Summarize each section independently
- If structure unclear: Create outline first
```

**Purpose:**
Guide recovery without human intervention.

### CLAUDE.md Best Practices

**Clarity is essential:**
- Explicit about what tools do
- Clear expected inputs/outputs
- Specific success criteria
- Binary pass/fail conditions

**Iterate CLAUDE.md:**
- Test failures reveal needed clarifications
- Update instructions based on failures
- Over-specification beats ambiguity

## Tool Implementation: CLI Wrappers

### Design Philosophy

**Principle:**
Minimize complexity; maximum clarity.

**Pattern:**
Wrap actual APIs with helpful interface for Claude.

### Wrapper Structure

**What each wrapper includes:**

```
1. Parameter validation
   - Check inputs provided
   - Validate formats
   - Helpful error messages

2. API call
   - Actual functionality
   - Error handling
   - Timeout management

3. Structured output
   - Status indicator
   - Primary output
   - Metadata and context

4. Next step guidance
   - Suggest next action
   - Highlight warnings
   - Provide debugging info
```

### Structured Response Format

**Output should include metadata:**

```
STATUS: SUCCESS
OUTPUT_FILE: notes.md
METRICS: tokens_used=15420, sections=3, bullets=47
WARNINGS: Used auto-generated subtitles (lower quality)
FACETS: language=auto-generated, quality=medium
NEXT_STEP: Review quality and add citations if needed
```

**Why metadata matters:**
- Gives Claude peripheral vision
- Enables intelligent follow-up
- Guides decision-making
- Informs context

### Error Messages That Help

**Bad error:**
```
ERROR: Failed to fetch
```

**Good error:**
```
ERROR: user_id parameter missing
REASON: YouTube authentication requires user ID
NEXT_STEP: Call lookup_user --email [email] first
EXAMPLE: ./tools/lookup_user.sh --email user@example.com
```

**Difference:**
Guides Claude toward solution, not just failure.

## Test Scenario Design

### Test Structure

**Each test represents real-world usage:**

```
test/scenario1/
├── request.txt    # Input specification
├── check.py       # Validation script
└── README.md      # What this test validates
```

### Request.txt

**What goes here:**
- Real input the agent receives
- Example YouTube URL
- Specific requirements
- Edge cases

**Example:**
```
Analyze this video for study notes:
https://www.youtube.com/watch?v=example

Requirements:
- Target audience: undergraduate students
- Focus: key concepts and applications
- Include: real-world examples
```

### Check.py Validation Script

**What it does:**
Verify output meets success criteria.

**Example:**

```python
#!/usr/bin/env python3
import os
import re

def check_notes():
    if not os.path.exists('notes.md'):
        return False, "notes.md not found"

    with open('notes.md') as f:
        content = f.read()

    # Check structure
    h1_count = len(re.findall(r'^# ', content, re.MULTILINE))
    h2_count = len(re.findall(r'^## ', content, re.MULTILINE))

    if h1_count != 1:
        return False, f"Expected 1 H1, found {h1_count}"

    if h2_count < 3:
        return False, f"Expected 3+ H2 sections, found {h2_count}"

    # Check content
    bullets = len(re.findall(r'^\- ', content, re.MULTILINE))
    if bullets < 30:  # 10+ per 3 sections
        return False, f"Expected 30+ bullets, found {bullets}"

    # Check further reading
    if "Further Reading" not in content:
        return False, "Missing 'Further Reading' section"

    return True, "All checks passed"

if __name__ == "__main__":
    success, message = check_notes()
    print(message)
    exit(0 if success else 1)
```

**Purpose:**
Binary pass/fail validation.

### Test Requirements

**Each check.py should have:**
- File existence checks
- Structural validation (counts, formats)
- Content density validation
- Specific, helpful failure messages

**Binary outcome:**
Pass or fail, not subjective assessment.

## Success Criteria: The Filter

### Characteristics of Good Criteria

**1. Binary Outcome**
- Pass or fail
- Not "kind of works"
- Not subjective

**2. Specification-Based**
- Tied to concrete output requirements
- Not "good enough"
- Measurable

**3. Observable**
- Can be validated automatically
- Can be tested repeatedly
- Doesn't require human judgment

### Examples

**Poor criteria:**
"Generate comprehensive notes"

**Good criteria:**
"Generate notes with one H1 title, three H2 sections, 10+ bullet points per section, and a Further Reading section with 3+ links in valid markdown format"

**Difference:**
Clarity enables automation.

## Architecture Exploration Through Prototyping

### What You Discover

**Slash commands vs. subagents:**
Prototyping reveals which manages context better.

**Example:**
- Long transcripts might benefit from subagents that return clean summaries
- Short content better as inline tool calls
- Prototyping shows which works better

**Context management patterns:**
- Some approaches create context pollution
- Others maintain cleanliness
- Prototyping reveals impact

**Tool design:**
- Are tools intuitively named?
- Are error messages helpful?
- Do tools provide right granularity?
- Prototyping gives immediate feedback

### Questions Answered by Prototyping

- Does the agent understand its task?
- Are tools designed well?
- Is CLAUDE.md clear enough?
- Do test scenarios cover edge cases?
- What context management works best?
- Are success criteria observable?

## Common Implementation Pitfalls

### Misconception: Complexity Won't Work

**Belief:**
"Complex authentication, multi-session state, real-time interaction won't work in Claude Code"

**Reality:**
Often works well through CLI wrappers.

**Why:**
- CLI provides abstraction
- Claude handles orchestration
- Complexity hidden behind clean interface

### Misconception: Can Only Test Simple Ideas

**Belief:**
"Only trivial prototypes feasible"

**Reality:**
Surprisingly complex systems prototypeable.

**Why:**
- CLAUDE.md provides structure
- Tools handle complexity
- Tests validate behavior

### Actual Limitations

**High-volume concurrent loads:**
- Claude Code suited for prototyping
- Not ideal for production scale

**Direct hardware integration:**
- Can't directly drive hardware
- Can call hardware APIs

**Real-time requirements:**
- Latency might not meet requirements
- Reveals that testing is needed

## Practical Checklist: Before Going to Production

**Before writing orchestration code, verify:**

- [ ] Define specific success criteria with measurable outputs
- [ ] Identify 3-6 core tools enabling the task
- [ ] Create 5-10 test scenarios using real-world inputs
- [ ] Write comprehensive CLAUDE.md with clear execution flow
- [ ] Build simple CLI wrappers for APIs
- [ ] Execute test scenarios and iterate
- [ ] Update instructions based on failures
- [ ] Achieve at least one passing test
- [ ] Test slash commands vs. subagents approach
- [ ] Validate context management strategy
- [ ] Verify error handling and recovery
- [ ] Document lessons learned
- [ ] Archive successful tests for production suite

**Outcome:**
Evidence of feasibility and optimal architecture.

## Economic and Risk Benefits

### Time Savings

**Traditional path:**
Weeks to months building architecture, then discovering if concept works.

**Rapid prototyping:**
Hours to days proving feasibility, then informed decisions on production architecture.

### Risk Mitigation

**Key principle:**
"If Claude Code can't achieve the task with perfect tool access and no UI constraints, your production version probably won't either."

**Implication:**
Prototyping is lower-risk way to discover showstoppers.

### Architecture Intelligence

**What you learn:**
- Which architectural patterns needed
- Tool design implications
- Context management strategy
- Success criteria in practice

**Benefit:**
Informed production decisions, not guesses.

### Production Migration

**Test folders become production tests:**
- Already have test scenarios
- Already have validation scripts
- Already understand success criteria
- Ready for production test suite

## Key Takeaways

1. **Validate before building** — Prototype first, infrastructure later
2. **Use Claude Code as harness** — Project mode ideal for testing
3. **CLAUDE.md is system prompt** — Clear instructions drive success
4. **CLI wrappers abstract complexity** — Tools provide clean interface
5. **Structured responses help** — Metadata guides Claude decisions
6. **Test scenarios are essential** — Real inputs reveal readiness
7. **Success criteria must be binary** — Measurable pass/fail
8. **Check scripts automate validation** — Don't judge subjectively
9. **Error messages guide recovery** — Help Claude self-correct
10. **Prototype reveals architecture** — Learn what works before building
11. **Hours not weeks** — Rapid feedback cycle
12. **Perfect tool access** — If it doesn't work here, won't work in production
13. **Tests become production suite** — Reuse prototyping tests
14. **Iteration matters** — CLAUDE.md improves with failures
15. **Tool design visible** — See what works, what confuses
16. **Context management tested** — Discover best patterns
17. **Misconceptions challenged** — Many things work that you'd assume don't
18. **Economic advantage clear** — Risk reduction through validation
19. **No infrastructure needed** — Concept testing before building
20. **Evidence before commitment** — Make informed decisions

## The Bottom Line

Jason Liu's rapid prototyping methodology inverts conventional wisdom: don't build infrastructure before proving the concept works. Instead, use Claude Code with a clear CLAUDE.md, CLI tool wrappers, and concrete test scenarios to validate feasibility in hours, not months.

The genius is in simplicity: system instructions, simple tool wrappers, passing tests. No complex frameworks. No uncertain assumptions. Just evidence of whether the idea works.

Key insight: "If Claude Code can't make it work with perfect tool access and no constraints, your production version probably won't either." This reframes prototyping from optional to essential—the fastest way to prove or disprove viability.

For teams considering building AI agents, the recommendation is clear: start with rapid prototyping using Claude Code. Write CLAUDE.md describing the task, wrap APIs in simple CLI tools, create tests with real inputs, and iterate until tests pass. This takes hours. Once you have passing tests, you know:
1. The idea works
2. What architecture is needed
3. What tools are optimal
4. What success looks like

Then build production infrastructure informed by evidence, not assumption. This dramatically reduces risk and wasted effort while accelerating time to actual value.

The methodology also naturally supports context engineering principles: clear tool response structure provides context, CLAUDE.md organizes information, test scenarios validate behavior. Rapid prototyping becomes context engineering in action.
