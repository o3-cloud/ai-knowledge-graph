---
summary: Simon Willison provides practical design patterns for agentic loops—emphasizing safe execution environments, tool selection, credential scoping, and recognizing that loops work best for problems with clear success criteria and automated testing
event_type: blog_post
sources:
    - https://simonwillison.net/2025/Sep/30/designing-agentic-loops/
tags:
    - agentic-loops
    - agent-design
    - tool-design
    - safety
    - automation
    - execution-environment
    - credential-management
    - testing
---

# Designing Agentic Loops

**Author:** Simon Willison
**Publication Date:** September 30, 2025
**Blog:** Simon Willison's Weblog
**Type:** Practical Design Guidance

## Overview

Simon Willison provides practical guidance on designing effective agentic loops—the iterative processes where agents repeatedly call tools to achieve goals through trial-and-error problem-solving.

Rather than architectural abstractions, Willison focuses on concrete design decisions: what makes loops effective, which execution environments are safe, how to scope credentials, and which tool designs work best.

## What Is an Agentic Loop?

### The Definition

**Agentic loop:**
"Something that runs tools in a loop to achieve a goal."

**Mechanism:**

```
Agent has goal
    ↓
Agent reasons about problem
    ↓
Agent calls tool
    ↓
Agent observes result
    ↓
Agent decides next action
    ↓
Repeat until goal achieved or stopped
```

### The Core Idea

**Approach:**
Let agent iteratively try approaches, learn from results, and adjust.

**Not:**
- Single-step tool calls
- Linear execution
- No iteration or feedback

**It is:**
- Repeated tool calls
- Feedback-driven adjustments
- Trial-and-error problem-solving
- Loop continues until success or limit reached

## When Agentic Loops Work Best

### Ideal Problem Characteristics

**Clear success criteria:**
You can measure when goal is achieved.

**Trial-and-error suitable:**
Multiple approaches possible; agent can try variations.

**Feedback available:**
Results of each attempt provide information.

**Improvement possible:**
Agent can learn from failures and adjust.

### Ideal Problem Examples

1. **Debugging failing tests**
   - Goal: Tests pass
   - Tool: Run tests, examine output, modify code
   - Feedback: Test results
   - Suitability: Excellent

2. **Performance optimization**
   - Goal: Code runs faster
   - Tool: Benchmark, analyze, modify, re-benchmark
   - Feedback: Performance metrics
   - Suitability: Excellent

3. **Dependency upgrades**
   - Goal: Dependencies upgraded without breaking code
   - Tool: Update, test, fix conflicts, repeat
   - Feedback: Test results
   - Suitability: Good

4. **Container image optimization**
   - Goal: Image size reduced
   - Tool: Analyze, modify Dockerfile, rebuild, measure
   - Feedback: Image size metrics
   - Suitability: Good

### Not Suitable Cases

- Tasks without clear success criteria
- One-shot operations
- Tasks where feedback is delayed or unclear
- High-risk operations (financial transactions, data deletion)

## The Safety Challenge: YOLO Mode

### YOLO: "You Only Loop Once"

**Concept:**
Running agentic loop with unattended execution on your machine.

**The appeal:**
Let the agent work autonomously while you do other things.

**The risk:**
Agent can cause real damage if something goes wrong.

### The Three Major Risks

#### Risk 1: Shell Commands Causing Data Loss

**Scenario:**
Agent executes shell command that deletes or corrupts data.

**Examples:**
- `rm -rf` in wrong directory
- Database commands that modify or delete
- Configuration changes that break systems
- Unintended side effects

**Impact:**
Data loss, system breakage, recovery required.

**Prevention:**
- Don't let agents run on production systems
- Don't give agents access to critical data
- Don't allow destructive commands without verification

#### Risk 2: Exfiltration Attacks

**Scenario:**
Agent or its tools are compromised or backdoored.

**What happens:**
Agent/tool steals code, credentials, secrets, private data.

**Examples:**
- Malicious tool exfiltrates API keys
- Backdoored utility sends code to attacker
- Credential theft through tool

**Impact:**
Credential compromise, code theft, security breach.

**Prevention:**
- Verify tool sources carefully
- Use only trusted tools
- Scope credentials to test accounts
- Don't store real credentials in agent environment

#### Risk 3: Using Your Machine as Attack Proxy

**Scenario:**
Compromised agent or tool uses your machine to attack others.

**What happens:**
Your machine becomes part of botnet; used to attack other systems.

**Impact:**
Your machine implicated in cyberattacks; potential legal/liability issues.

**Prevention:**
- Isolate agent environment
- Monitor network traffic
- Use containers/sandboxing
- Don't allow unrestricted network access

## Safe Execution Environments

### Option 1: Isolated Containers

**Setup:**
Run agent in Docker container isolated from host system.

**Benefits:**
- Agent can't access host files
- Network can be restricted
- Easy to destroy and recreate
- Clear boundary between agent and system

**Considerations:**
- Container still needs to run somewhere (your machine, server)
- Network access can still escape

**Implementation:**
```dockerfile
FROM python:3.11
# Minimal dependencies only
# No access to host files
# Restricted network
# Limited resources
```

### Option 2: Browser-Based Development

**Examples:**
- GitHub Codespaces
- VS Code Remote
- Cloud-based IDEs

**Benefits:**
- All execution in cloud
- Your machine not involved
- Clear isolation
- Easy to reset

**Considerations:**
- Credentials in cloud environment
- Must trust cloud provider
- Slightly slower feedback loop

**Best for:**
When you want agent work without local system risk.

### Option 3: Ephemeral VMs

**Setup:**
Start fresh VM; agent works there; VM destroyed after.

**Benefits:**
- Complete isolation
- No persistent state to compromise
- Can't affect other systems
- Destroyed after each run

**Considerations:**
- Slower startup time
- More resource intensive
- Complex setup

**Best for:**
High-risk operations requiring maximum isolation.

### Option 4: Limited-Access Machine

**Setup:**
Dedicated machine for agent work; limited access; restricted permissions.

**Benefits:**
- Real machine for realistic testing
- Isolation from important systems
- Can test real interactions

**Considerations:**
- Still a real machine that could be compromised
- Requires ongoing security maintenance

**Best for:**
When you need realistic environment but can afford to lose the machine.

## Tool Design for Agentic Loops

### Simple Tool Approach

**Recommendation:**
Provide shell command access plus simple documentation.

**Why:**
- Agents understand shell commands well
- Flexible for unexpected situations
- No need to pre-define all tools
- Simple for agent to reason about

**Implementation:**

```bash
# agent-tools.sh
# Available commands for agent:
# - python: Run Python code
# - node: Run Node code
# - docker: Docker operations
# - git: Git operations
# - curl: HTTP requests
# - jq: JSON processing
```

### Tool Documentation

**What agent needs:**
Simple reference of available tools.

**Format:**
Plain text file (AGENTS.md) listing available commands.

**Example:**

```markdown
# Available Tools

## Code Execution
- python: Run Python code
- node: Run Node code
- bash: Run bash commands

## Version Control
- git: Git operations (clone, commit, push, etc.)
- gh: GitHub CLI

## Building/Testing
- npm: Node package manager
- pip: Python package manager
- pytest: Python testing
- npm test: Run tests

## Utilities
- curl: HTTP requests
- jq: JSON processing
- find: File search
```

### Anti-Pattern: Complex Tool Frameworks

**Common mistake:**
Build elaborate tool frameworks with type signatures, validation, etc.

**Problem:**
- Agent must learn your custom API
- Inflexible for unexpected needs
- Harder to debug
- More failure points

**Better approach:**
Simple shell access with documentation.

### Tool Selection Principle

**Philosophy:**
Give agent access to standard tools; document what's available.

**Don't:**
- Pre-define every possible operation
- Force agent into narrow tool set
- Build custom tool frameworks for agents

**Do:**
- Expose shell, Python, Node
- Document available commands
- Let agent compose solutions
- Keep it simple

## Credential Scoping: Critical for Safety

### Principle: Minimize Blast Radius

**Key insight:**
If agent credentials are compromised, what's the damage?

**Goal:**
Limit damage to testing/staging, not production.

### Credential Scope Strategies

#### Strategy 1: Test/Staging Only

**Rule:**
Agent credentials only access test and staging environments.

**Advantage:**
- Real problem-solving possible
- No production risk
- Safe to let agent work autonomously

**Implementation:**
- Create test database account
- Use staging API keys
- Test credentials for external services

#### Strategy 2: Budget Limits

**Rule:**
Credentials with spending caps.

**Examples:**
- API key limited to $10/day
- Cloud account limited to $100/month
- Rate-limited API keys

**Advantage:**
Runaway costs limited to max budget.

#### Strategy 3: Isolated Accounts

**Rule:**
Separate accounts for agent work; never production credentials.

**Structure:**
```
Production:
- Real database
- Real API keys
- Real production system

Agent Testing:
- Test database
- Test API keys
- Staging systems
- Budget-limited accounts
```

**Advantage:**
Clear separation; credentials compromise can't affect production.

#### Strategy 4: Short-Lived Credentials

**Rule:**
Credentials expire quickly; must be refreshed.

**Example:**
- API tokens valid for 1 hour
- Temporary credentials for cloud access
- Session-based authentication

**Advantage:**
Even if compromised, window of exposure is small.

### What NOT to Do

❌ **Don't use production credentials**
Agent mistakes become production incidents.

❌ **Don't use unlimited budgets**
Runaway costs can be devastating.

❌ **Don't store real credentials in agent environment**
Increases exfiltration risk.

❌ **Don't trust credentials are never logged**
Assume they'll appear in logs/output.

## Designing Effective Loops

### The Basic Loop Structure

**Template:**

```
Initialize(goal, tools, test_suite)
    ↓
iteration = 0
while iteration < MAX_ITERATIONS:
    ↓
    Agent reasons about goal
    ↓
    Agent calls tool
    ↓
    Observe result
    ↓
    If goal achieved: break
    ↓
    If no progress: break
    ↓
    iteration += 1
    ↓
Return (success/failure, result)
```

### The Test Suite Amplifier

**Key insight:**
Agentic loops dramatically amplified by automated tests.

**Why:**
- Clear success criteria (tests pass)
- Immediate feedback
- Objective measurement
- Reproducible

**Example:**

```
# Without good tests:
Agent: "Did I fix the bug?"
You: "Hmm, I think so?"
(unclear feedback)

# With good tests:
Agent: "Tests pass - goal achieved"
You: "Tests are the truth"
(clear, objective feedback)
```

### Best Practices for Loop Design

**1. Clear Success Criteria**
Define exactly what "success" means.

**2. Automated Measurement**
Tests, benchmarks, metrics—objective measurement.

**3. Iteration Limit**
Set max iterations; prevent infinite loops.

**4. Progress Detection**
Break if not making progress.

**5. Logging**
Record what agent tried; enables debugging.

**6. Safe Defaults**
If uncertain, fail safe; don't proceed.

## Use Case: Debugging Failing Tests

### The Scenario

**Goal:**
Fix failing tests.

**Setup:**
- Agent has test suite
- Agent can modify code
- Tests provide feedback

**Loop:**

```
1. Agent sees failing test
2. Agent analyzes test and code
3. Agent modifies code
4. Agent runs tests
5. If pass: done
6. If fail: analyze error, iterate
7. Repeat (max 10 iterations)
```

**Why it works:**
- Clear goal (tests pass)
- Immediate feedback (test results)
- Automated measurement (pass/fail)
- Improvement possible (agent can fix bugs)

### The Agent's Reasoning

```
Test output:
AssertionError: expected 5, got 3

Analysis: Something subtracts 2 instead of adding 2

Hypothesis: Line 42 has -= instead of +=

Fix: Change -= to +=

Test again: PASS

Goal achieved!
```

## Designing for Practicality

### The Real-World Reality

**What actually happens:**
- Agent gets stuck
- Progress stalls
- Different approaches needed
- Human intervention required

### Handling Stuck States

**Signs:**
- Same error repeating
- Different tool calls making no progress
- Agent cycling between approaches

**Response:**
- Break loop
- Get human to diagnose
- Provide additional context
- Try again with new approach

### The Interruption Principle

**Philosophy:**
Design loops to be easily interrupted and resumed.

**Implementation:**
- State easily saved
- Can pause mid-loop
- Human can diagnose
- Can resume with changes

## Key Takeaways

1. **Agentic loops are iterative tool calling** — Repeat tools until goal achieved
2. **Best for clear-success-criteria problems** — Debugging, optimization, testing
3. **YOLO mode has serious risks** — Unattended execution can cause damage
4. **Safe execution environments essential** — Containers, cloud IDEs, VMs
5. **Shell commands work well** — More flexible than custom tool frameworks
6. **Documentation matters** — Simple reference of available tools
7. **Credentials need scoping** — Test/staging only; never production
8. **Budget limits prevent runaway costs** — Cap spending on credentials
9. **Short-lived credentials safer** — Minimize exposure window
10. **Test suites amplify loops** — Clear feedback drives agent success
11. **Debugging failing tests ideal case** — Clear goal, immediate feedback
12. **Performance optimization works** — Measurable metrics guide iteration
13. **Dependency upgrades suitable** — Testable; feedback available
14. **Container isolation recommended** — Prevents host system risk
15. **Codespaces good alternative** — Cloud-based removes local risk
16. **Monitor what agent tries** — Logging enables debugging
17. **Iteration limits prevent infinite loops** — Set reasonable max iterations
18. **Progress detection important** — Break if not making headway
19. **Simplicity beats sophistication** — Shell commands > complex tool APIs
20. **Interrupted loops should be resumable** — Design for human intervention

## The Bottom Line

Simon Willison's guide to designing agentic loops cuts through the complexity to practical reality: agentic loops work well for problems with clear success criteria and automated testing, but safety demands careful thought about execution environments and credential scoping.

**Key design principles:**

1. **Choose the right problem type** — Clear success criteria, trial-and-error suitable
2. **Safe execution environment** — Don't run on your production machine
3. **Scope credentials carefully** — Test/staging, budgeted, short-lived
4. **Simple tool design** — Shell commands documented; no complex frameworks
5. **Automated tests drive success** — Feedback must be objective and immediate

**For practitioners:**

If you're considering agentic loops:
- **Don't:** Run unattended on your machine with real credentials
- **Do:** Use test environment with scoped credentials
- **Don't:** Build elaborate tool frameworks
- **Do:** Document available shell commands
- **Don't:** Trust implicit success criteria
- **Do:** Rely on automated tests

**The opportunity:**

Well-designed agentic loops can solve specific problems dramatically faster than manual approaches:
- Debugging: hours instead of days
- Optimization: exploring variants in minutes instead of weeks
- Testing: finding and fixing issues autonomously

But only if you design them safely and use them for appropriate problems.

The loops that win are those with clear success criteria, automated testing, safe execution environments, and scoped credentials. Everything else is details.

