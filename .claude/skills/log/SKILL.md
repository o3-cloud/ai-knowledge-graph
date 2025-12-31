---
name: log
description: Create log entries with timestamps. Use this when documenting discoveries, research findings, meetings, code reviews, articles, videos, or significant events during development.
---

# Log Findings Skill

This skill provides instructions for documenting analysis findings, deep dives, research, and code reviews to the `docs/log` directory in a consistent, discoverable format.

## Purpose

The `docs/log` directory serves as a searchable knowledge base of all graph analysis, infrastructure findings, and architectural decisions. Each log entry is a standalone markdown document that can be referenced, tagged, and discovered over time.

## Quick Start

### 1. Choose Your Filename

Use the pattern: `YYYY-MM-DD-descriptive-title.md`

Examples:
- `2025-12-23-scheduled-tasks-analysis.md`
- `2025-12-23-ecs-env-vars-research.md`
- `2025-12-23-kafka-ui-service-analysis.md`

**Naming conventions:**
- Use ISO date (YYYY-MM-DD) for chronological sorting
- Use kebab-case for the title portion
- Be specific and descriptive (avoid generic titles like "findings" or "notes")

### 2. Add Frontmatter

Every log entry must start with YAML frontmatter. Use the `TEMPLATE.md` file as reference:

```yaml
---
summary: A brief (1-2 sentence) summary of what this log entry covers
event_type: deep dive | meeting | research | code | code review
sources:
    - https://example.com/resource-url
    - https://github.com/user/repo/path
    - /path/to/local/file.md
tags:
    - tag1
    - tag2
    - tag3
---
```

#### Frontmatter Fields Explained

**`summary`** (required)
- 1-2 sentences describing the log's content
- Used in directory listings and search
- Example: "Deep analysis of scheduled task infrastructure - 6 ECS tasks + 1 state machine orchestrating trap/device monitoring"

**`event_type`** (required)
- One of: `deep dive`, `meeting`, `research`, `code`, `code review`
- Classifies the type of work documented
- **deep dive**: Technical analysis of a system/component
- **meeting**: Outcomes from meetings or discussions
- **research**: Investigation into a problem or exploration
- **code**: Code implementation or changes
- **code review**: Review of code changes and feedback

**`sources`** (required - list)
- URIs pointing to actual resources (websites, APIs, files, repositories)
- Each entry must be a valid URI: URLs, file paths, repository links, etc.
- Do not include descriptive text or method descriptions—those belong in the content
- Examples:
  - `https://github.com/markburgess/SSTorytime/tree/main`
  - `https://aicoding.leaflet.pub/3malrv6poy22a`
  - `/path/to/local/file.md` (for local files)
  - `https://www.youtube.com/watch?v=VIDEO_ID` (for video)
  - `https://example.com/api/endpoint` (for APIs)

**Important:** Speaker names, article titles, and metadata go in the content section (after frontmatter), not in sources. Sources are only URIs.

```yaml
# ✓ Correct
sources:
    - https://www.youtube.com/watch?v=ShuJ_CN6zr4

# ✗ Incorrect
sources:
    - https://www.youtube.com/watch?v=ShuJ_CN6zr4
    - Speaker: Eno Reyes, CTO at Factory AI
```

Then in the content:
```markdown
**Speaker:** Eno Reyes, CTO at Factory AI
**Duration:** 15 minutes
**Source:** AI Engineer Conference
```

**`tags`** (required - list)
- Technology stack, components, and topics
- Use lowercase, kebab-case, plural where appropriate
- Examples:
  - `neo4j`, `cloudwatch`, `ecs`, `state-machines`
  - `scheduled-tasks`, `automation`, `monitoring`
  - `infrastructure`, `security`, `performance`

### 3. Write the Content

After the frontmatter, write the main content using markdown.

#### Recommended Structure

**For Deep Dives:**
```markdown
# [Title]

## Overview
- Brief context and scope

## Inventory/Summary
- List of resources/findings

## Detailed Analysis
- Breakdowns, diagrams, dependencies

## Key Observations
- What's important to know

## Recommendations
- Next steps, improvements

## Data Quality Notes
- Gaps, limitations in what was analyzed

## Related Analysis
- Links to other log entries
```

**For Research:**
```markdown
# [Title]

## Question/Goal
- What were we investigating?

## Findings
- Key discoveries

## Implications
- How this affects the system

## Open Questions
- What else needs investigation?

## References
- Sources consulted
```

### 4. Include Useful Content

Good log entries include:

- **Tables**: Resource inventories, comparisons, metrics
- **Code blocks**: Cypher queries, configuration examples, command snippets
- **Diagrams**: ASCII art dependency flows, architecture diagrams
- **Lists**: Categorized findings, ordered recommendations
- **Data**: Metrics, counts, statistics with before/after comparisons

Example tables:
```markdown
| Module | Purpose | Event Rule | Event Target |
|--------|---------|------------|--------------|
| scheduled-task-amount-lost | Track amounts | event_rule | ecs_scheduled_task |
```

Example Cypher queries:
```cypher
MATCH (n:aws_lambda_function)
RETURN n.address, n.arn, n.runtime
ORDER BY n.address
```

### 5. Extracting Information from Media Sources

When documenting video content and other media, use tools to extract structured metadata:

#### YouTube Videos with yt-dlp

Use `yt-dlp` to extract video metadata without needing to watch the entire video:

```bash
# Extract key metadata from a YouTube video
yt-dlp --dump-json "https://www.youtube.com/watch?v=VIDEO_ID" 2>/dev/null | jq '{title, description, uploader, duration}'
```

**Example output:**
```json
{
  "title": "Making Codebases Agent Ready – Eno Reyes, Factory AI",
  "description": "Agents are eating software engineering...",
  "uploader": "AI Engineer",
  "duration": 933
}
```

**Use yt-dlp when:**
- Logging conference talks, tutorials, or educational content
- Extracting speaker information and affiliations
- Capturing video descriptions with key points or links
- Duration helps gauge content scope

**Template for video log entries:**
```yaml
---
summary: [Brief summary of video content]
event_type: research
sources:
    - https://www.youtube.com/watch?v=VIDEO_ID
    - "Video Title" - Speaker Name
tags:
    - video-content
    - [relevant topics]
---

# [Video Title]

**Speaker:** [Name, Title, Affiliation]
**Duration:** [MM:SS or total minutes]
**Source:** [Conference/Channel Name]

## Key Points
- [Main takeaway 1]
- [Main takeaway 2]
...
```

### 6. Reference Other Logs

Link to related analysis:

```markdown
## Related Analysis

See also:
- `2025-12-23-comprehensive-graph-analysis-and-next-steps.md` - Overall graph state
- `2025-12-23-ecs-env-vars-research.md` - ECS environment variables
```

## Complete Examples

### Example 1: Infrastructure Deep Dive

Here's the structure of a well-formatted log entry:

```yaml
---
summary: Analysis of RabbitMQ infrastructure - queue topology, consumer patterns, and failover configuration
event_type: deep dive
sources:
    - https://github.com/example/terraform/blob/main/modules/rabbitmq.tf
    - https://github.com/example/infrastructure/blob/main/queries/rabbitmq-analysis.cypher
    - /docs/architecture/rabbitmq-design.md
tags:
    - rabbitmq
    - message-queues
    - infrastructure
    - high-availability
---

# RabbitMQ Infrastructure Deep Dive

## Overview
Analysis of the RabbitMQ message broker infrastructure...

## Queue Inventory

| Queue Name | Type | Consumers | Durability |
|-----------|------|-----------|-----------|
| events.live | standard | 3 | durable |
```

### Example 2: Video Content Research

Example of logging conference talk or educational video:

```yaml
---
summary: Framework for measuring and improving codebase readiness for autonomous AI agents. Covers 8 categories of environment readiness.
event_type: research
sources:
    - https://www.youtube.com/watch?v=ShuJ_CN6zr4
tags:
    - ai-agents
    - video-content
    - codebase-readiness
---

# Making Codebases Agent Ready

**Speaker:** Eno Reyes, CTO at Factory AI
**Duration:** 15.5 minutes
**Source:** AI Engineer Conference

## Core Problem

Autonomous AI agents fail unreliably in production despite strong demo performance. The gap isn't model quality—it's **environment readiness**.

## Agent Readiness Framework

Eight categories determine agent success: style validation, build systems, dev environments, observability, testing, dependencies, documentation, and error handling.

(Continue with findings, implications, and recommendations)
```

## File Organization

All log entries live in: `docs/log/`

```
docs/log/
├── TEMPLATE.md                                          # Template for new entries
├── 2025-12-23-scheduled-tasks-analysis.md
├── 2025-12-23-ecs-env-vars-research.md
├── 2025-12-23-comprehensive-graph-analysis-and-next-steps.md
└── ... (more log entries)
```

## Tips for Effective Logging

### 1. Be Specific
- Document the exact version, date, and tool versions used
- Include sample queries and results
- Provide concrete metrics and counts

### 2. Think About Discovery
- Future developers will search by tag, date, or keyword
- Use consistent terminology across logs
- Reference related analyses

### 3. Include Data Quality Notes
- What's missing from the graph?
- What properties are NULL?
- What would improve the analysis?

### 4. Actionable Recommendations
- Prioritize (High/Medium/Low)
- Explain why each recommendation matters
- Link to implementation if completed

### 5. Keep It Discoverable
- Avoid overly long summaries
- Use clear section headers
- Include a "Related Analysis" section
- Tag consistently with previous logs

## Common Tags to Use

**Technologies:**
- neo4j, terraform, aws, kubernetes, docker, postgresql, redis, rabbitmq, elasticsearch

**AWS Services:**
- ecs, lambda, cloudwatch, rds, s3, kms, iam, vpc, sqs, sns, eventbridge

**Domains:**
- scheduled-tasks, monitoring, security, networking, databases, queues, caching, infrastructure

**Analysis Types:**
- architecture, dependencies, permissions, performance, reliability, data-quality

## Related Tools and Skills

- `query-graph`: Execute Cypher queries against the Neo4j database
- `yt-dlp`: Extract metadata from YouTube videos (title, description, uploader, duration, etc.)
  - **Install:** `pip install yt-dlp`
  - **Usage:** `yt-dlp --dump-json "https://www.youtube.com/watch?v=VIDEO_ID" | jq '{title, description, uploader, duration}'`
- See also: Query patterns in `SKILL.md` for query-graph skill

## Troubleshooting

**Problem:** "My log entry is too long"
- **Solution:** Split into multiple focused entries (one per component/domain)
- Link them together in "Related Analysis"

**Problem:** "I'm not sure what tags to use"
- **Solution:** Check existing log entries in `docs/log/` for tag patterns
- Be consistent with previous entries

**Problem:** "I have findings from a query but don't know how to structure them"
- **Solution:** Use the TEMPLATE.md as a starting point
- Choose the most relevant frontmatter fields
- Write in the "deep dive" or "research" style depending on your content

**Problem:** "yt-dlp fails to fetch YouTube video metadata"
- **Solution:** Update yt-dlp: `pip install --upgrade yt-dlp`
- Check network connection
- Some videos may be region-restricted; try the `--no-warnings` flag to see raw error
- If video is private/deleted, log what information you have and note unavailability in the entry

**Problem:** "I want to log a video but can't watch the full content"
- **Solution:** Use yt-dlp to extract title, description, and uploader
- Read the video description (often contains speaker bios, slides links, key timestamps)
- Include a "Video Summary" section based on extracted metadata
- Add a note: "Logged from video metadata; full content not reviewed"
