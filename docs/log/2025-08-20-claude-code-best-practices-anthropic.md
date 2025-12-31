---
summary: Anthropic's Claude Code best practices guide—covering CLAUDE.md customization, tool configuration, workflows (explore-plan-code-commit, TDD, visual iteration), safe YOLO mode, multi-Claude orchestration, and practical optimization techniques
event_type: article
sources:
    - https://www.anthropic.com/engineering/claude-code-best-practices
tags:
    - Claude-Code
    - best-practices
    - developer-workflow
    - tool-configuration
    - test-driven-development
    - automation
    - CLAUDE.md
    - MCP-servers
    - git-integration
---

# Claude Code Best Practices

**Source:** Anthropic Engineering Blog
**Publication Date:** August 2025 (estimated)

## Overview

Anthropic shares comprehensive best practices for using Claude Code effectively, based on how the organization uses the tool internally. The guide covers setup customization, workflow patterns, tool integration, safety considerations, and optimization techniques. Key insight: Claude Code effectiveness depends on deliberate setup and workflow discipline, not just the tool itself.

## 1. Customize Your Setup with CLAUDE.md

### What is CLAUDE.md?

**Definition:**
Special configuration document automatically pulled into context at session start.

**Purpose:**
Reduce token consumption and improve instruction adherence by documenting project-specific knowledge.

**Key benefit:**
Context once, use many times.

### CLAUDE.md Structure

**What to include:**

#### Bash Commands
```markdown
# Bash commands
- npm run build: Build the project
- npm run typecheck: Run type checking
- npm test: Run test suite
- npm run deploy: Deploy to production
```

**Purpose:**
Quick reference for common commands Claude should know.

#### Code Style Guidelines
```markdown
# Code style
- Use ES modules (import/export), not CommonJS
- Destructure imports when possible
- Max line length: 100 characters
- Use const/let, never var
- Async/await preferred over .then()
```

**Purpose:**
Guide code generation to match project style.

#### Testing Instructions
```markdown
# Testing
- Write tests for all public functions
- Use Jest for unit tests
- 80%+ code coverage required
- Tests in __tests__ subdirectories
```

**Purpose:**
Clarify testing expectations and patterns.

#### Project-Specific Knowledge
```markdown
# Architecture
- Frontend: React + TypeScript
- Backend: Node.js + Express
- Database: PostgreSQL
- Cache: Redis

# Key files
- src/api/index.ts: Main API setup
- src/db/schema.sql: Database schema
- .env.example: Environment variables
```

**Purpose:**
Help Claude understand system architecture.

#### Repository Etiquette
```markdown
# Git workflow
- Feature branches off main
- PR reviews required
- Commits must reference issues
- Squash commits before merge
```

**Purpose:**
Ensure Claude integrates with team practices.

### CLAUDE.md Placement

**Multiple levels available:**

**Project root (./.claude/CLAUDE.md):**
- Shared via git
- Applies to entire project
- Team-wide consistency

**Parent directories:**
- Useful for monorepos
- Applied to all subdirectories
- Hierarchy of specificity

**Child directories:**
- Project-specific overrides
- More specific than parent
- Fine-grained customization

**Home folder (~/.claude/CLAUDE.md):**
- Global across all projects
- Personal preferences
- Cross-project patterns

### Tuning CLAUDE.md

**Approach:**
Treat like prompt engineering—iterate and improve.

**Process:**
1. Write initial CLAUDE.md
2. Use Claude Code
3. Observe results
4. Update based on learnings
5. Repeat

**Key insight:**
CLAUDE.md effectiveness improves with use and refinement.

## 2. Give Claude More Tools

### Bash Commands and Utilities

**Configuration:**
Make useful bash commands available.

**Examples:**
- `npm` scripts
- Custom shell scripts
- System utilities
- Development tools

**Documentation:**
Document available commands in CLAUDE.md.

### MCP Server Integration

**What are MCP servers:**
Specialized tools for specific integrations.

**Common examples:**
- Puppeteer (browser automation, screenshots)
- Sentry (error tracking)
- Stripe (payment processing)
- Custom APIs

**Configuration methods:**

**Project-specific:**
```json
./.claude/mcp.json
```

**Global:**
```json
~/.claude/mcp.json
```

**Team-wide:**
```json
.mcp.json (checked into git)
```

**Benefit of checked-in configs:**
Team shares common tools; no setup needed per developer.

### Custom Slash Commands

**Purpose:**
Create project-specific shortcuts and workflows.

**Storage:**
Store templates in `.claude/commands/` folder.

**Features:**
- Support `$ARGUMENTS` for parameterization
- Enable complex workflows
- Create shortcuts for common tasks

**Example:**
```
/project:fix-github-issue 1234
(Runs custom prompt templated for issue fix)
```

### Permission Management

**Control tool access:**
Use `/permissions` command to customize allowed tools.

**Options:**
- "Always allow" for specific tools
- Manual `.claude/settings.json` edits
- CLI flags for one-time settings

**GitHub integration:**
Install `gh` CLI to enable GitHub capabilities.

## 3. Common Workflows

### Workflow 1: Explore, Plan, Code, Commit

**This is the foundational pattern.**

**Steps:**

#### Step 1: Explore
**Action:**
Request file/image/URL review without immediate coding.

**Example:**
"Review this codebase structure" or "Analyze this design mockup"

**Purpose:**
Let Claude understand context before planning.

**Why it matters:**
Without this step, Claude tends to jump straight to coding.

#### Step 2: Extended Thinking (Plan)
**Action:**
Use "think" mode for extended reasoning.

**Variants:**
- `think` (standard extended reasoning)
- `think hard` (more intensive)
- `think harder` (even more)
- `ultrathink` (maximum reasoning)

**Purpose:**
Complex problems benefit from deeper reasoning.

**Claude's output:**
Visible thinking process, then solution.

#### Step 3: Plan Checkpoint
**Action:**
Have Claude create written plan before implementation.

**Example:**
```markdown
# Plan for Feature X

## Step 1: Modify database schema
- Add new columns to users table
- Create migration file

## Step 2: Update API endpoints
- Add GET /users/:id/profile
- Update PUT /users/:id

## Step 3: Add frontend components
- Create ProfileCard component
- Add to user dashboard

## Step 4: Test
- Write unit tests
- Write integration tests
```

**Purpose:**
Verify understanding before coding.

**Human role:**
Review plan; approve, question, or suggest changes.

#### Step 4: Implement
**Action:**
Claude implements per plan, iteratively verifying.

**Process:**
- Implement step 1
- Test
- Move to step 2
- Repeat

**Flexibility:**
Adapt if implementation reveals issues.

#### Step 5: Commit
**Action:**
Commit changes with meaningful messages.

**Claude role:**
Write good commit messages.

#### Step 6: Update Documentation
**Action:**
Update relevant documentation.

**Examples:**
- README changes
- API documentation
- Architecture decisions

**Claude helps:**
Keeping docs up-to-date with code.

### Workflow 2: Test-Driven Development

**Approach:**
Write tests first, then implementation.

**Process:**

#### Step 1: Write Tests
**Action:**
Claude writes test suite based on specifications.

**Focus:**
Input/output specifications, expected behavior.

**Example:**
```typescript
describe('calculateTotal', () => {
  it('sums all items', () => {
    const items = [{price: 10}, {price: 20}];
    expect(calculateTotal(items)).toBe(30);
  });

  it('applies discount', () => {
    const items = [{price: 100}];
    expect(calculateTotal(items, 0.1)).toBe(90);
  });
});
```

#### Step 2: Confirm Failure
**Action:**
Run tests; verify they fail (no implementation yet).

**Purpose:**
Confirm tests are actually testing something.

#### Step 3: Commit Tests
**Action:**
Commit test suite before implementation.

**Purpose:**
Lock in requirements.

#### Step 4: Implement
**Action:**
Claude writes code to pass tests.

**Constraint:**
Only write what's needed to pass tests.

**Verification:**
All tests pass before done.

#### Step 5: Verify Validity
**Action:**
Use independent subagents to verify implementation.

**Process:**
One agent writes code, another reviews for quality, edge cases, security.

**Benefit:**
Higher quality through independent review.

#### Step 6: Commit Implementation
**Action:**
Commit final code.

**Benefits of TDD:**
- Clear requirements
- Verifiable implementation
- Confidence in correctness
- Catches edge cases

### Workflow 3: Visual Iteration

**Purpose:**
For UI development, iterate based on visual targets.

**Process:**

#### Step 1: Provide Visual Reference
**Method:**
- Paste screenshot (or use system shortcut)
- Drag-drop image file
- Reference image file path
- Use Puppeteer MCP for automated screenshots
- Use iOS simulator MCP for app UI

**Example:**
"Here's the design mockup (screenshot). Make the UI match this."

#### Step 2: Implement
**Action:**
Claude implements UI to match reference.

#### Step 3: Verify
**Action:**
Take screenshot of implementation.

**Comparison:**
Compare to original reference.

#### Step 4: Iterate
**Action:**
Provide feedback: "The button color should be darker" or "Spacing is too tight."

**Repeat:**
2-3 iterations typically yields significantly improved results.

**Key insight:**
Visual reference eliminates ambiguity about UI requirements.

### Workflow 4: Safe YOLO Mode

**Purpose:**
Skip permission prompts in safe environments.

**Flag:**
`--dangerously-skip-permissions`

**Usage:**
```bash
claude --dangerously-skip-permissions
```

**Safety requirement:**
Use in container without internet access to mitigate risks.

**Docker implementation:**
Reference implementation available in Claude Code repository.

**Benefit:**
Uninterrupted workflow for automated tasks.

**Risk:**
Only use in secure sandboxed environment.

## 4. Optimize Your Workflow

### Be Specific in Instructions

**Vague:**
"Add tests for foo.py"

**Specific:**
"Write test cases covering the logged-out user edge case; avoid using mocks; focus on behavior verification"

**Impact:**
Detailed instructions significantly improve results.

### Provide Images and File References

**Effective:**
- Screenshots for UI work
- Design mocks for visual iteration
- File paths for code context
- URLs for external references

**Benefit:**
More context = better results.

### Course-Correct Early with Plans

**Key timing:**
Before coding, review and adjust plans.

**Process:**
1. Ask Claude to plan
2. Review plan
3. Suggest corrections
4. Then implement

**Benefit:**
Catch issues early; avoid wrong implementations.

### Use `/clear` Between Tasks

**Command:**
`/clear`

**Purpose:**
Reset context between unrelated tasks.

**Benefit:**
Prevents context bleed; clean start for new task.

### Active Collaboration Tools

**Escape key:**
Interrupt and preserve context for redirection.

**Double-tap Escape:**
Jump back in history and explore alternatives.

**Markdown checklists:**
Track progress on complex multi-step tasks.

**Example:**
```markdown
- [ ] Write tests
- [ ] Implement feature
- [ ] Add documentation
- [ ] Code review
```

## 5. Headless Mode for Automation

**Purpose:**
Run Claude Code without interactive terminal.

**Applications:**

### Issue Triage
Automatically categorize and triage GitHub issues.

**Implementation:**
GitHub Actions workflow triggered on new issues.

**Process:**
- Receive issue text
- Claude analyzes
- Claude categorizes
- Claude adds labels

### Code Review Automation
Detect common issues in pull requests.

**Examples:**
- Typos and grammar
- Stale comments
- Misleading variable names
- Pattern violations

**Process:**
- Receive PR changes
- Claude analyzes
- Claude suggests fixes
- Claude creates PR with fixes

### Task Distribution
Fan out large tasks across multiple Claude instances.

**Example:**
Large codebase migration split into 10 tasks, each handled by Claude.

### CI/CD Integration
Integrate Claude into deployment pipelines.

**Examples:**
- Generate deployment notes
- Verify configuration changes
- Analyze failed builds
- Suggest fixes

### Usage
```bash
claude -p "<prompt>" --output-format stream-json
```

## 6. Multi-Claude Orchestration

### Separate Verification Pattern

**Setup:**
Two Claude instances:
1. Writer: implements code
2. Reviewer: independently reviews

**Process:**
- Writer implements feature
- Reviewer analyzes code quality
- Reviewer verifies correctness
- Reviewer reports issues

**Benefit:**
Independent verification improves quality.

### Multiple Checkouts Pattern

**Setup:**
Maintain 3-4 git branches in separate folders.

**Process:**
- Each folder has different Claude instance
- Work on different features in parallel
- Merge when complete

**Tool:**
Git worktrees (lightweight alternative to separate clones).

**Benefit:**
Parallel development on multiple features.

### Custom Harness Pattern

**Concept:**
Custom orchestration logic for complex workflows.

**Example:**
Large migration split across multiple Claude instances, custom harness coordinates.

**Benefit:**
Enables scaling beyond single machine capability.

## Real-World Applications

### Codebase Q&A

**Use case:**
Onboarding new developers.

**Example questions:**
- "How does logging work?"
- "What edge cases does CustomerOnboardingFlowImpl handle?"
- "Where are API error responses formatted?"

**Claude's approach:**
Explores codebase agentically to answer.

**Benefit:**
Faster onboarding; reduce load on other engineers.

### Git Integration

**Capabilities:**
- Search git history
- Write commits intelligently
- Handle complex operations (rebases, conflicts)
- Format commit messages contextually

**Integration:**
Claude works naturally with `git` commands.

### Jupyter Notebook Enhancement

**Use cases:**
- Interpret outputs (including images)
- Improve aesthetic presentation
- Explain results
- Generate summaries

**Benefit:**
Better research documentation and sharing.

## Key Metrics and Impact

### At Anthropic

**Claude Code usage:**
- Core onboarding workflow
- Significantly improves ramp-up time
- Reduces load on other engineers

**Developer adoption:**
- Engineers use Claude for "90%+ of git interactions"
- Includes: commits, history searching, complex operations

**Impact:**
- Faster development
- Better code quality
- Reduced context switching

## Key Takeaways

1. **CLAUDE.md is foundational** — Project-specific configuration reduces friction
2. **Multiple CLAUDE.md levels** — Hierarchy of specificity from global to local
3. **Tools extend capability** — MCP servers, bash commands, custom commands
4. **Explore before coding** — Review first; understand before implementing
5. **Extended thinking helps** — Use think mode for complex problems
6. **Plan as checkpoint** — Written plan enables verification before coding
7. **Test-driven development works** — Tests first ensures verified requirements
8. **Visual iteration powerful** — Screenshots/mocks eliminate UI ambiguity
9. **Safe YOLO mode exists** — Skip permissions in sandboxed environments
10. **Specificity matters** — Detailed instructions improve results significantly
11. **Multi-Claude orchestration scales** — Multiple instances handle larger tasks
12. **Headless mode automates** — Integration into CI/CD and workflows
13. **Git integration natural** — Claude works seamlessly with git
14. **Verification helps** — Independent review improves code quality
15. **Iteration improves visuals** — 2-3 rounds of visual iteration yield good results
16. **90%+ for git operations** — High adoption for commits and history
17. **Context tools available** — /clear, escape, double-escape for workflow
18. **Nothing is set in stone** — Adapt these practices to your needs

## The Bottom Line

Anthropic's Claude Code best practices emphasize that effectiveness comes from deliberate setup and workflow discipline, not just the tool. The CLAUDE.md file provides foundation—project-specific knowledge that accumulates over time. Tool integration extends capability. Workflow patterns provide structure. And multi-instance orchestration enables scaling.

Key insight: Invest upfront in configuration (CLAUDE.md, tool setup, workflow definition) and it compounds. The explore-plan-code-commit workflow with extended thinking and plan verification catches errors early and prevents wasted implementation effort. Test-driven development with independent verification produces higher quality code.

For developers adopting Claude Code, the recommendation is clear: customize your setup from day one (CLAUDE.md), establish consistent workflows (explore-plan-code-commit for complex work), and iterate on what works. At Anthropic, this approach has made Claude Code the core onboarding workflow and reduced ramp-up time significantly.

The tool is powerful; the setup and workflow discipline determine how well you leverage that power. Start with solid foundation (CLAUDE.md), use proven patterns (explore-plan-code-commit, TDD), and refine continuously as you learn what works for your projects and team.
