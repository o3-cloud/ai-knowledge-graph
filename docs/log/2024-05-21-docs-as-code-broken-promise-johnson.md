---
summary: Tom Johnson examines docs-as-code as a broken promise—acknowledging practical challenges like Git complexity for non-technical writers while defending the value of diffs and version control in documentation workflows
event_type: blog_post
sources:
    - https://idratherbewriting.com/blog/thoughts-on-docs-as-code-promise
tags:
    - docs-as-code
    - documentation
    - technical-writing
    - version-control
    - Git
    - diffs
    - workflow-challenges
    - tooling
---

# Thoughts on Docs as Code Being a Broken Promise

**Author:** Tom Johnson
**Publication Date:** May 21, 2024
**Blog:** I'd Rather Be Writing
**Type:** Practice Reflection and Analysis

## Overview

Tom Johnson responds to critiques that docs-as-code has failed to deliver on its promises, offering a nuanced perspective that acknowledges genuine challenges while defending core benefits. Rather than dismissing either position, Johnson presents a pragmatic assessment: docs-as-code provides real value (diffs, version control, scriptable builds) but creates real friction (Git complexity for non-technical writers, steep learning curves).

His conclusion: the promise was partially fulfilled, partly broken, and the fitness of docs-as-code depends on team composition and organizational priorities.

## The Promise of Docs-as-Code

### What Was Promised

**Original vision:**
Documentation treated like code would gain all benefits of software development:
- Version control and history
- Code review processes
- Continuous integration and deployment
- Programmable builds
- Developer workflow integration
- Automated testing
- Easy collaboration

**The appeal:**
Documentation could achieve the same rigor, trackability, and automation as codebases.

### How It Was Supposed to Work

**Workflow:**
```
Writer makes change
    ↓
Commits to version control (Git)
    ↓
Creates pull request
    ↓
Diffs shown to reviewer
    ↓
Reviewer examines changes
    ↓
Approval and merge
    ↓
Automated publishing
```

**Tool stack:**
- Markdown (instead of proprietary formats)
- Git (version control)
- GitHub/GitLab (collaboration)
- CI/CD pipelines (automated publishing)
- Text editors (VS Code, etc.)

**Promise:**
Documentation would be as professional and automated as software.

## The Reality: Benefits That Hold True

### Benefit 1: Markdown Over XML

**What changed:**
XML, DocBook, and other markup formats were complex and hard to read.

**What Markdown provided:**
- Human-readable source format
- Natural, unstyled appearance
- Easy to edit and understand
- Lightweight and portable
- Wide tool support

**Outcome:**
This promise delivered. Most docs-as-code implementations use Markdown, and it's genuinely better than proprietary formats.

### Benefit 2: Diffs for Review

**What this enables:**
Reviewers see exactly what changed, highlighted visually.

**Tom's assessment:**
"I can't imagine going back to a system that wouldn't have diffs."

**Why it matters:**
- Changes are visible and explicit
- Easy to spot errors
- Previous versions visible for comparison
- Review process becomes concrete
- Accidental changes caught immediately

**Example:**
```
Old system: "Is this change good?" (reviewer reads entire document)
New system: "Is this change good?" (reviewer sees exact diff of changes)
```

The diff makes review massively faster and more accurate.

### Benefit 3: Text Editor Compatibility

**What this enables:**
Writers can use familiar tools:
- VS Code
- Vim
- Sublime
- Any text editor

**Why it matters:**
- No need for specialized documentation software
- Developers already know these tools
- Customizable workflows
- Lightweight and fast

### Benefit 4: Scriptable Builds

**What this enables:**
Documentation generation can be automated:
- Build triggers on commit
- Publishing automated
- Testing integrated
- Static site generation
- Multi-format output

**Outcome:**
This promise delivered. Docs-as-code enables sophisticated automation that manual systems can't achieve.

### Benefit 5: Developer Integration

**What this enables:**
Documentation in same repository as code:
- Changes in same PR
- Documentation and code versioned together
- Easier to keep in sync
- Developer workflow integrated

**Outcome:**
Strong benefit for developer-focused documentation.

## The Reality: Challenges That Undermine the Promise

### Challenge 1: Git Complexity for Non-Technical Writers

**The problem:**
Git is powerful but complex, with many concepts:
- Branches and merging
- Commits and history
- Pull requests and reviews
- Diffs and conflicts
- Rebasing and force pushes

**Tom's experience:**
At Amazon, using Git for documentation created significant barriers for non-technical writers.

**Manifestations:**
- Anxiety about making simple changes
- Fear of breaking something
- Difficulty understanding feedback in diffs
- Frustration with conflict resolution
- Steep learning curve
- Time wasted on git mechanics instead of writing

**Practical consequence:**
Non-technical writers working slower and less confidently than in simpler systems.

### Challenge 2: Branching Workflow Complexity

**The scenario:**
Multiple writers working on different documentation simultaneously.

**What can go wrong:**
- Complex merge conflicts
- Difficulty understanding others' branches
- Uncertainty about when to merge
- Coordination overhead
- Potential for lost work

**In complex organizations:**
Branching strategies become sophisticated (git-flow, trunk-based, etc.), adding more cognitive load.

### Challenge 3: Accidental Content Merges and Conflicts

**The problem:**
When two writers edit nearby content, conflicts emerge that require manual resolution.

**Challenge:**
Non-technical writers often don't understand how to resolve merge conflicts.

**Outcome:**
Conflicts become blockers instead of solvable problems.

### Challenge 4: Theme and Build Maintenance Burden

**The assumption:**
Docs-as-code allows writers to focus on content while developers handle infrastructure.

**The reality:**
Theme maintenance, style updates, and build process changes fall on whoever is available.

**Problem:**
Writers often become responsible for these tasks, diverting attention from writing.

**Consequence:**
Docs-as-code systems require ongoing technical maintenance that non-technical teams may struggle with.

### Challenge 5: Learning Curve and Adoption

**Timeline for competency:**
- Weeks to months for non-technical writers to become comfortable
- Git concepts require time to internalize
- Workflow patterns need practice
- Recovery from mistakes requires help

**Organizational cost:**
- Training time required
- Reduced productivity while learning
- Potential errors from misunderstanding
- Frustration and resistance

## Where Docs-as-Code Works Well

### Ideal Scenario 1: Developer-Focused Teams

**Prerequisites:**
- Team members already know Git
- Working in same repository as code
- Small, technical team
- Frequent documentation changes

**Why it works:**
- No learning curve
- Integrates with existing workflow
- Benefits (diffs, CI/CD) heavily utilized
- Pain points (Git complexity) are non-issues

### Ideal Scenario 2: Open-Source Projects

**Prerequisites:**
- Contributor community already technical
- Distributed contributors
- GitHub/GitLab already primary interface
- Community can help with conflicts

**Why it works:**
- Contributors expect Git workflow
- Open-source tools align with philosophy
- Community can support each other
- Benefits outweigh challenges

### Ideal Scenario 3: Large Documentation Teams with Developer Support

**Prerequisites:**
- Large enough to justify dedicated developers
- Git expertise available internally
- Complex builds justified
- Long-term commitment to tooling

**Why it works:**
- Technical support available for challenges
- Benefits (automation, integration) heavily utilized
- Scale justifies complexity
- Workflow can be optimized

## Where Docs-as-Code Struggles

### Scenario 1: Mixed Technical/Non-Technical Teams

**Challenge:**
Some team members comfortable with Git, others not.

**Problem:**
System optimal for one group is painful for another.

**Result:**
Bottlenecks emerge; some team members contribute less.

### Scenario 2: Primarily Non-Technical Documentation Teams

**Challenge:**
Few or no team members with Git expertise.

**Problem:**
Learning curve is steep; support is limited; frustration high.

**Result:**
Productivity drops; quality suffers; adoption resisted.

### Scenario 3: Business Documentation (Process Docs, Policies, etc.)

**Challenge:**
Business users, HR, compliance need to update documentation.

**Problem:**
Expecting them to use Git is unrealistic.

**Result:**
Either bottleneck to developers or adoption fails.

## The Recommendation: Layer Abstraction

### Tom's Advice

**For smaller teams:**
Purchase commercial docs-as-code solutions rather than building custom systems.

**Why:**
- Commercial solutions abstract Git complexity
- User interfaces hide version control
- Developers can focus on tech; writers on content
- Less support burden internally

### Abstraction Layer Approach

**Concept:**
Build interface between writers and Git system.

**Examples:**
- Visual diff interfaces that don't require Git knowledge
- Simplified branching/merging workflows
- Automated conflict resolution for common cases
- User-friendly publishing process
- Templates and guided workflows

**Benefit:**
Writers get docs-as-code benefits (version control, diffs, CI/CD) without Git complexity.

**Cost:**
Requires building or purchasing abstraction layer.

## The Assessment: Promise vs. Reality

### What Was Promised and Delivered

✅ **Diffs and version control** — Genuinely valuable; revolutionary for review processes
✅ **Markdown format** — Better than proprietary alternatives; still holds true
✅ **Scriptable builds** — Automation benefits real and substantial
✅ **Developer integration** — Works well when developers are the users
✅ **Tool diversity** — Text editor ecosystem is rich and powerful

### What Was Promised but Unrealized

❌ **Universal adoption** — Non-technical writers still struggle
❌ **Simplified workflow** — Git is complex; no getting around that
❌ **Reduced learning curve** — Takes weeks to months for non-experts
❌ **Theme/build abstraction** — Maintenance still falls on someone
❌ **Conflict-free collaboration** — Merge conflicts still problematic

### The Honest Assessment

**Docs-as-code is:**
- Excellent for developer-focused documentation
- Excellent for technical teams
- Challenging for non-technical teams
- Requires support infrastructure
- Best with abstraction layers for mixed teams

**The promise was:**
- Partially delivered (benefits exist and are real)
- Partially broken (complexity remains for non-technical users)
- Context-dependent (works great for some, poorly for others)

## Key Takeaways

1. **Diffs revolutionized review** — Visual comparison genuinely valuable; hard to give up
2. **Markdown is genuine improvement** — Over XML and proprietary formats; holds true
3. **Git complexity is real** — No amount of tooling completely eliminates it
4. **Non-technical writers struggle** — Learning curve significant; adoption requires support
5. **Automation benefits substantial** — CI/CD, scripting, publishing gains are real
6. **Developer integration works** — When developers are users, benefits are clear
7. **Mixed teams are challenging** — Workflow optimal for one group may pain another
8. **Conflict resolution is hard** — Merge conflicts remain problematic for non-technical users
9. **Theme maintenance is burden** — Doesn't automatically abstract away
10. **Learning curve is steep** — Weeks to months for non-technical competency
11. **Abstraction layers help** — Can provide benefits while reducing complexity
12. **Commercial solutions worth considering** — Might save internal support burden
13. **Context determines suitability** — Not one-size-fits-all solution
14. **Promise was overstated** — Set expectations higher than delivery
15. **Benefits are real but conditional** — Not automatic for all teams
16. **Team composition matters most** — Technical team → docs-as-code works; non-technical → struggles
17. **Support infrastructure essential** — Need developers available for problems
18. **Workflow training required** — Can't just adopt; needs education
19. **Adoption resistance predictable** — Non-technical users resisting expected; provide tools to reduce friction
20. **Pragmatism beats purity** — Use what works for your team, not what's theoretically pure

## The Bottom Line

Tom Johnson's assessment is refreshingly honest: docs-as-code has delivered genuine benefits (diffs, version control, scriptable builds, developer integration) but has also created real challenges (Git complexity, learning curve, mixed-team workflows).

**The key insight:**
The promise was partially delivered, partially broken, and the fitness depends entirely on team composition and organizational context.

**What works:**
- Developer-focused documentation
- Technical teams comfortable with Git
- Open-source projects
- Teams with dedicated developer support

**What struggles:**
- Non-technical teams
- Mixed technical/non-technical teams
- Business documentation
- Teams without internal Git expertise

**The practical recommendation:**
For organizations with non-technical writers, invest in abstraction layers (either built or commercial) that provide docs-as-code benefits while reducing Git complexity.

**The realistic conclusion:**
Docs-as-code isn't a broken promise—it's a promise that works when conditions are right and creates friction when they're not. The dishonesty wasn't in docs-as-code itself, but in treating it as universally applicable when it's actually context-dependent.

The best outcomes come from matching tooling to team composition, providing adequate support and training, and being honest about the tradeoffs.

