---
summary: Simon Willison argues Claude Skills may surpass MCP in impact—simple, shareable folders with instructions and resources prove more token-efficient and practical than complex tool integration protocols
event_type: blog_post
sources:
    - https://simonwillison.net/2025/Oct/16/claude-skills/
tags:
    - Claude-skills
    - model-capabilities
    - MCP-comparison
    - tool-integration
    - prompt-engineering
    - practical-tools
    - AI-extensions
---

# Claude Skills Are Awesome, Maybe a Bigger Deal Than MCP

**Author:** Simon Willison
**Publication Date:** October 16, 2025
**Blog:** Simon Willison's Weblog
**Type:** Technology Analysis and Prediction

## Overview

Simon Willison makes a bold claim: Claude Skills might prove more impactful than Model Context Protocol (MCP) as a mechanism for extending AI model capabilities.

His reasoning: Skills are radically simple—just folders containing Markdown instructions, YAML metadata, scripts, and resources—yet remarkably effective. They're token-efficient, shareable, model-agnostic, and practical. While MCP offers sophisticated tool orchestration, Skills offer simplicity and directness that may prove more valuable for most use cases.

## What Are Claude Skills?

### The Definition

**Official description from Anthropic:**
"Skills are folders that include instructions, scripts, and resources that Claude can load when needed."

**In practice:**
A skill is a directory containing:
- Markdown documentation with YAML frontmatter
- Optional executable scripts
- Optional resource files
- Optional supporting code and utilities

### Structure Example

```
my-skill/
├── README.md (with YAML metadata)
├── script.sh or script.py
├── utils/
│   └── helper_functions.py
└── resources/
    └── config.json
```

**The YAML frontmatter includes:**
- Skill name
- Description (brief)
- What it does
- How to use it
- Any requirements

### Token Efficiency: The Key Advantage

**How skills load:**

```
Session start:
Claude scans available skills
Reads brief descriptions from metadata (dozens of tokens)
Full details remain unloaded

User task:
Claude recognizes relevant skill needed
Loads full skill documentation only then
Uses skill for task
Other skills remain unloaded
```

**Why this matters:**
- Only active skills consume tokens
- Lazy loading keeps context clean
- Multiple skills available without bloating prompt
- Perfect for skill libraries with dozens of skills

## How Skills Work

### Skill Discovery and Loading

**Phase 1: Initialization**
```
Skill folder exists in filesystem accessible to Claude
Session starts
Claude scans skill manifests (brief YAML metadata)
Descriptions loaded (~dozens of tokens per skill)
```

**Phase 2: Recognition**
```
User gives task: "Create a Slack animation"
Claude matches task to slack-gif-creator skill
Realizes full skill details needed
```

**Phase 3: Activation**
```
Full skill documentation loaded
Scripts become available
Resource files accessible
Claude uses skill to complete task
```

### Execution Model

**Skills require:**
- Filesystem access (can read skill files)
- Execution environment (can run scripts)
- Appropriate permissions

**Skills are:**
- Self-contained (work independently)
- Reusable (used across multiple tasks)
- Discoverable (Claude finds them)
- Documented (self-documenting via Markdown)

## Practical Example: The Slack GIF Creator Skill

### What It Does

Creates animated GIFs suitable for sharing on Slack.

### How Willison Used It

**Task:**
Generate an animated GIF for use in Slack.

**What happened:**
1. Described what he wanted
2. Claude recognized slack-gif-creator skill was relevant
3. Loaded skill documentation
4. Used built-in validation functions
5. Generated GIF that met Slack's constraints (2MB file size limit)
6. Successfully created working animation

### Why This Worked Well

**Validation built-in:**
Skill included functions to validate output against Slack's requirements.

**Utility classes:**
Pre-written helper code Claude could leverage.

**Self-documenting:**
Markdown docs clearly explained what skill did.

**No integration overhead:**
Skill was directly usable without orchestration setup.

### The Efficiency Contrast

**With MCP:**
- Define tool interface
- Register with protocol
- Claude calls tool through protocol layer
- Overhead for each interaction

**With Skills:**
- Folder with docs and scripts
- Claude reads and uses directly
- Minimal overhead
- Straightforward execution

## Skills vs. MCP: The Comparison

### What MCP Is

**Model Context Protocol:**
- Standardized protocol for tool integration
- Sophisticated orchestration capabilities
- Defines interfaces and contracts
- Designed for complex tool ecosystems

**Strengths:**
- Powerful for complex integrations
- Well-specified interfaces
- Composable tool ecosystems
- Enterprise-grade reliability

**Complexity:**
- Requires protocol compliance
- Tool authors must implement MCP
- Integration overhead
- Steep learning curve

### What Skills Are

**Simple capability packages:**
- Folders with instructions and scripts
- Self-documenting via Markdown
- Minimal specification required
- Direct execution

**Strengths:**
- Extremely simple to create
- Token-efficient
- Easy to understand
- Low barrier to entry

**Limitations:**
- Less formal than MCP
- No standardized interface contracts
- Less sophisticated orchestration
- Tool authors must choose to provide skills

### Willison's Prediction: Skills Win

**Why Skills might prove more impactful:**

1. **Simplicity barrier is lower**
   - Anyone can create a skill
   - MCP requires technical sophistication
   - Skills proliferate faster

2. **Token efficiency is critical**
   - Context window is expensive
   - Skills use tokens only when needed
   - MCP adds protocol overhead

3. **Speed of adoption**
   - Skills can be shared immediately
   - MCP requires ecosystem coordination
   - Skills easier for individual creators

4. **Practical effectiveness**
   - For most use cases, skills are sufficient
   - 80/20 rule: skills handle majority of cases
   - MCP addresses remaining 20%

5. **Model-agnostic potential**
   - Skills work with any model (not Claude-specific)
   - Can be adopted across different tools
   - Broader ecosystem potential

## Why Willison Thinks Skills Are "a Bigger Deal"

### The Ecosystem Argument

**MCP ecosystem:**
- Slower to build (requires specification compliance)
- Higher barrier to entry
- Powerful but complex
- Smaller total number of tools likely

**Skills ecosystem:**
- Rapid proliferation (easy to create)
- Low barrier to entry
- Practical and direct
- Potentially vast number of skills

**The outcome:**
Skills might create a richer, broader ecosystem despite being less sophisticated.

### The Practical Value Argument

**For end users:**
- Skills are simpler to discover and use
- Don't require understanding protocol details
- Feel more direct and efficient
- Work with minimal friction

**For creators:**
- Dramatically easier to create
- Share as GitHub folder
- No specification to learn
- Immediate utility

### The Efficiency Argument

**Token cost matters because:**
- Every token has financial cost
- Context window is limited
- Prompt quality depends on space available
- Skills use tokens more efficiently

## Creating Skills: The Barrier to Entry

### What's Required

**Minimal requirements:**
1. Create folder
2. Write Markdown documentation
3. Add YAML frontmatter
4. (Optional) Add scripts and utilities

**Example skill creation:**

```markdown
# my-data-processor

description: "Processes CSV files and generates reports"

## What it does
This skill processes CSV data and creates formatted reports.

## How to use
1. Provide CSV file
2. Specify report type
3. Skill generates report

## Resources
- data_processor.py (processes data)
- templates/ (report templates)
```

### Sharing Skills

**Distribution:**
- Share as GitHub repository folder
- Include in project structure
- Publish to skill registry (if exists)
- Share directly with others

**Discovery:**
- Register in skill directories
- Document in README
- Share in communities
- Recommendation networks

## Skills for Organizations

### Domain-Specific Skill Libraries

**Concept:**
Organizations build libraries of domain-specific skills.

**Examples:**

**Data journalism organization:**
```
- news-article-generator (writes news using data)
- source-verifier (checks information accuracy)
- layout-optimizer (optimizes article layout)
- chart-creator (creates visualizations)
```

**Publishing company:**
```
- manuscript-analyzer (analyzes manuscripts)
- copyeditor (editing suggestions)
- cover-designer (generates cover concepts)
- metadata-optimizer (optimizes book metadata)
```

**Financial services:**
```
- report-generator (generates financial reports)
- compliance-checker (checks regulatory compliance)
- risk-analyzer (analyzes risk exposures)
- portfolio-optimizer (optimizes allocations)
```

### Organizational Benefits

**Knowledge capture:**
Skills codify organizational knowledge.

**Reusability:**
Once created, skills used across projects.

**Consistency:**
Skills ensure consistent processes.

**Training:**
New team members learn through skill documentation.

**Automation:**
Routine tasks automated through skills.

## Predictions and Future Impact

### What Willison Predicts

**Short term (months):**
- Rapid skill creation
- Growing skill ecosystems
- Developer adoption
- Organizational skill libraries emerge

**Medium term (1-2 years):**
- Skills become standard practice
- Skill registries mature
- Cross-organization skill sharing
- Multiple skill formats/types

**Long term (2+ years):**
- Skills potentially surpass MCP in breadth
- Vast ecosystem of skills available
- Skills integrated into workflows everywhere
- Skills as primary extension mechanism

### The Broader Implication

**Simplicity wins:**
When two approaches exist—one simple, one sophisticated—the simple one often dominates because of adoption velocity and barrier to entry.

**Skills represent:**
- Accessibility over sophistication
- Pragmatism over specification
- Speed over standardization
- Direct utility over complex protocols

## Key Takeaways

1. **Skills are simple** — Just folders with Markdown, scripts, and resources
2. **They're token-efficient** — Load only when needed; keep context clean
3. **Creation barrier is low** — Anyone can create a skill
4. **They work with any model** — Not Claude-specific; portable
5. **They're discoverable** — Metadata enables easy skill discovery
6. **Validation is built-in** — Scripts can validate outputs
7. **They're self-documenting** — Markdown explains everything
8. **Sharing is trivial** — Just share folder/repository
9. **They scale to libraries** — Hundreds of skills can be available
10. **They're more practical than MCP** — For most use cases
11. **Barrier to entry vs. MCP is dramatic** — Skills much easier to create
12. **Ecosystem growth will be rapid** — Low barrier means proliferation
13. **Organizations will build libraries** — Domain-specific skill collections
14. **Skills enable specialization** — Create organizational knowledge libraries
15. **Token efficiency is competitive advantage** — Matters in constrained environment
16. **Simplicity beats sophistication** — When adoption is goal
17. **Skills will transform workflows** — Become extension mechanism of choice
18. **Multiple skills in context possible** — Efficient management of capability
19. **Skills cross organizational boundaries** — Shareable and reusable
20. **This is potentially bigger than MCP** — Despite MCP's sophistication

## The Bottom Line

Simon Willison makes a compelling argument that Claude Skills—despite their simplicity—may become more impactful than Model Context Protocol, a more sophisticated tool integration standard.

**The core insight:**
Sometimes the simpler approach wins not because it's better, but because it's accessible. The low barrier to creating and sharing skills means the ecosystem will grow far faster than MCP, despite MCP's greater sophistication for complex use cases.

**Why this matters:**
- **For users:** Skills make capabilities more discoverable and usable
- **For creators:** Skills make extending capabilities dramatically easier
- **For organizations:** Skills enable knowledge capture and reuse
- **For the field:** Skills might become the primary way capabilities are extended

**The key advantage:**
Token efficiency. In an environment where every token counts, loading only the skills you need rather than supporting a sophisticated protocol infrastructure is significant.

**The prediction:**
We'll see rapid skill proliferation. Within a year, there will be thousands of publicly available skills. Organizations will build internal skill libraries. Skills will become the standard way developers extend and customize AI capabilities.

**The broader lesson:**
Accessibility and simplicity often beat sophistication in determining what becomes standard practice. MCP is more powerful, but Skills are more usable. And for ecosystem growth, usability wins.

