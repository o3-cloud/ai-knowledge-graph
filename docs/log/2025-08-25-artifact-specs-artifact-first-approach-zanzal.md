---
summary: Owen Zanzal introduces Artifact Specs—JSON Schema blueprints that define AI output structure, enabling model-agnostic workflows, standardized validation, and LLM-as-a-Judge evaluation while grounding the artifact-first approach in concrete, reusable specifications
event_type: blog_post
sources:
    - https://medium.com/devops-ai/how-artifact-specs-bring-the-artifact-first-approach-to-life-4f47a66a74af
    - https://github.com/o3-cloud/artifact-specs
tags:
    - artifact-first
    - JSON-schema
    - structured-outputs
    - AI-workflows
    - specification-driven
    - model-agnostic
    - output-validation
    - LLM-evaluation
    - artifact-specs
    - workflow-design
---

# How Artifact Specs Bring the Artifact-First Approach to Life

**Author:** Owen Zanzal
**Platform:** Medium (DevOps+AI)
**Publication Date:** August 25, 2025
**Type:** Technical Framework and Guide
**Repository:** https://github.com/o3-cloud/artifact-specs
**Key Concept:** Artifact specifications as blueprints for AI output

## Overview

Owen Zanzal provides the practical mechanism for implementing the artifact-first approach: Artifact Specs—JSON Schema specifications that define exactly what an AI output should look like, structure by structure, field by field.

Rather than designing agents first and hoping outputs match requirements, artifact specs force clarity upfront: define the artifact before building the workflow. This enables model-agnostic workflows (use any LLM), automatic validation, reusability across teams, and even enables "poor man's evaluations" where the same schema structure used for generation can be used for quality assessment.

## The Problem: Agent-First Thinking

### The Default Instinct

**When teams start with AI agents:**
- "We need a meeting note-taker"
- "Let's build a research assistant"
- "We should have an alert triage bot"

**What's wrong with this:**
Agent design is the wrong starting point. Agents are just delivery mechanisms.

### Why Artifact-First Matters

**The insight:**
The real work is the output—the artifact. The agent is merely the mechanism.

**Implication:**
Start by defining the artifact clearly. Then design the workflow to produce it.

**Benefit:**
Better workflows, consistent quality, adaptability across tools.

## What is an Artifact Spec?

### Definition

**Artifact Spec:**
A JSON Schema that defines exactly what a given output should look like.

**Contains:**
- Structure of the output
- Field definitions
- Data types
- Field descriptions
- Required vs. optional fields
- Format constraints

**Serves as:**
- Blueprint for AI's deliverable
- Contract between workflow and output
- Validation ruleset
- Reusable specification

### Why It Matters

**Clarifies "done":**
What exactly is the deliverable? What does success look like?

**Reduces ambiguity:**
LLM knows precisely what structure is expected.

**Enables machine-readability:**
Outputs can be validated automatically, parsed, integrated.

**Enables human-readability:**
Same spec can generate human-friendly formatted versions.

**Enables reuse:**
One spec works across models, tools, teams.

## Real Example: Meeting Summary Artifact Spec

### The Specification

**Meeting Summary Schema:**

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "MeetingSummary",
  "type": "object",
  "properties": {
    "title": {
      "type": "string",
      "description": "Calendar event title."
    },
    "date": {
      "type": "string",
      "format": "date-time",
      "description": "Date and time of the meeting (ISO 8601 format)."
    },
    "participants": {
      "type": "array",
      "items": { "type": "string" },
      "description": "List of meeting participants."
    },
    "summary": {
      "type": "array",
      "items": { "type": "string" },
      "description": "Key bullet points summarizing the meeting."
    },
    "decisions": {
      "type": "array",
      "items": { "type": "string" },
      "description": "List of decisions made."
    },
    "actions": {
      "type": "array",
      "description": "List of action items.",
      "items": {
        "type": "object",
        "properties": {
          "action": {
            "type": "string",
            "description": "Description of the action."
          },
          "assignee": {
            "type": "string",
            "description": "Person responsible."
          },
          "due": {
            "type": "string",
            "format": "date-time",
            "description": "Due date/time (ISO 8601 format)."
          }
        },
        "required": ["action"]
      }
    }
  },
  "required": ["title", "date", "participants", "summary"]
}
```

**What this defines:**
- Title (string)
- Date (ISO 8601 datetime)
- Participants (array of strings)
- Summary (array of bullet points)
- Decisions (array of decisions)
- Actions (array of tasks with assignee and due date)

## The Three-Step Process

### Step 1: Unstructured Data Input

**Source:** Raw meeting transcript

**Example transcript:**

```
# Product Team Sync Meeting

Time: 10:00 AM – 10:30 AM
Date: Tuesday, August 12, 2025
Attendees: Alice (PM), Ben (Engineer), Carla (Designer), David (Ops)

Alice (PM): "Okay, let's get started. Thanks everyone. Quick agenda
today — updates on the new dashboard rollout, bug fixes from last week,
and then any blockers."

Ben (Engineer): "Yeah, so, on the dashboard… we got the API changes
merged yesterday. They're in staging now, but I noticed a couple of
requests timing out when you hit the filter by date."

Carla (Designer): "Yeah I saw that too. The loading spinner just…
it spins forever."

David (Ops): "Could be the query hitting the old index. I haven't
updated the cache yet — I was waiting for confirmation before flipping
it over."

Alice (PM): "Okay, so timeline-wise, do we think this is still going
live by Thursday?"

Ben (Engineer): "If we fix the indexing issue today, then yeah. But if
it's something deeper, might slip to next week."

Carla (Designer): "I'd rather delay than ship something broken. We
already had complaints about the old dashboard."

Alice (PM): "Got it. So let's put a soft hold on comms for Thursday,
pending a test run tomorrow. David, can you—"

David (Ops): "Yeah, I'll reindex right after this call. Should take
about 30 minutes."

Ben (Engineer): "Cool, then I'll rerun the tests."

Alice (PM): "Perfect. Okay, next — bug fixes. Anyone got updates on
the login issue?"

Carla (Designer): "Oh yeah, that one was mostly visual. The error
message was hidden under the header. I fixed the CSS."

Ben (Engineer): "Right, but there's still a backend piece. If you
enter the wrong password three times, it doesn't lock out the user."

David (Ops): "That's a feature not a bug!"

Alice (PM): "Ha, okay, but let's not ship that to production. Ben,
can you put in a PR today?"

Ben (Engineer): "Yeah, I'll do it this afternoon."

Alice (PM): "Great. Last thing — blockers. Anyone stuck?"

[Everyone says they're good except Ben waiting on index update]

Alice: "Okay, cool. Thanks everyone. Let's reconvene tomorrow if needed."
```

**What we have:**
Raw, unstructured conversation with important information scattered throughout.

### Step 2: Structured Extraction

**Process:**
Feed schema and transcript to LLM, ask it to produce JSON conforming to schema.

**Prompt to LLM:**

```
Extract meeting information from the provided transcript and
produce JSON that conforms to this schema:

[Schema definition provided]

Meeting transcript:
[Transcript provided]

Respond only with valid JSON conforming to the schema.
Do not add fields not in the schema.
Extract only information explicitly stated in the transcript.
```

**LLM Output (JSON):**

```json
{
  "title": "Product Team Sync",
  "date": "2025-08-12T10:00:00Z",
  "participants": [
    "Alice (PM)",
    "Ben (Engineer)",
    "Carla (Designer)",
    "David (Ops)"
  ],
  "summary": [
    "Dashboard API changes merged and in staging; date filter causing
    timeouts likely due to old index.",
    "Ops to reindex; tentative Thursday rollout but communications on
    hold pending test run.",
    "Login issue: CSS fixed for hidden error message; backend still
    needs password lockout after 3 failed attempts.",
    "No major blockers besides waiting on reindex completion."
  ],
  "decisions": [
    "Soft hold on Thursday communications until successful test run.",
    "Prioritize stability over timeline; delay rollout if issues persist."
  ],
  "actions": [
    {
      "action": "Reindex database/cache for dashboard queries",
      "assignee": "David (Ops)",
      "due": "2025-08-12T10:30:00Z"
    },
    {
      "action": "Rerun tests after reindexing completes",
      "assignee": "Ben (Engineer)",
      "due": "2025-08-12T11:00:00Z"
    },
    {
      "action": "Submit backend PR to implement login lockout",
      "assignee": "Ben (Engineer)",
      "due": "2025-08-12T17:00:00Z"
    }
  ]
}
```

**What we have:**
Structured, machine-readable, validated against schema.

### Step 3: Human-Readable Rendering

**Process:**
Take JSON and convert to formatted markdown/text for human consumption.

**Prompt to LLM:**

```
Convert this JSON to a clear, readable markdown summary:

[JSON from Step 2]

Format should be:
- Clear sections with emojis
- Bullet points for readability
- Easy to scan
- Professional appearance
```

**Human-Readable Output:**

```
📝 Meeting Summary — Product Team Sync

Date: August 12, 2025 — 10:00 AM – 10:30 AM
Participants: Alice (PM), Ben (Engineer), Carla (Designer), David (Ops)

🔑 Key Points
- Dashboard API changes merged and in staging; date filter requests timing out due to old indexing
- Ops will reindex to resolve; Thursday rollout tentative but comms on hold until tests pass
- Login issue: frontend CSS fixed, but backend needs password lockout after 3 failed attempts
- No major blockers besides waiting on reindex completion

✅ Decisions
- Put soft hold on Thursday communications until tomorrow's test run succeeds
- Prioritize stability over timeline; delay rollout rather than ship broken code

📌 Action Items
1. David (Ops): Reindex database/cache for dashboard queries — Due by 10:30 AM, Aug 12
2. Ben (Engineer): Rerun tests after reindexing completes — Due by 11:00 AM, Aug 12
3. Ben (Engineer): Submit backend PR to implement login lockout — Due by 5:00 PM, Aug 12
```

**What we have:**
Clean, scannable, useful for humans without losing the structured information.

## Why This Works with Any LLM or Agent

### Model Agnostic

**Because the spec is separate from implementation:**

```
Artifact Spec (stable, reusable)
    ↓
Can use with OpenAI
Can use with Anthropic Claude
Can use with Mistral
Can use with open-source models
Can use with any agent framework
```

**Implications:**
- Not locked into one vendor
- Can switch models as capabilities improve
- Can test different models with same spec
- Spec is the stable contract

### Validation is Automatic

**Process:**
```
LLM generates output
    ↓
Validate against schema
    ↓
If valid: use it
If invalid: reject and retry with error details
```

**Benefits:**
- No manual checking
- Guaranteed structure
- Can integrate downstream systems

### Switching Agents is Trivial

**Scenario:**
You have a workflow that:
1. Generates meeting summary (using Claude)
2. Validates against schema
3. Sends to stakeholders

**If you want to switch to GPT:**
Change the LLM call. The schema, validation, everything else stays the same.

**Result:**
Tools are interchangeable parts. The artifact is the stable contract.

## Using a Schema as a Prompt

### Plain-Text Alternative

**Not all workflows use JSON directly.**

**Alternative:**
Translate schema into plain-text instructions.

**Schema:**
```json
{
  "properties": {
    "title": "string (meeting name)",
    "date": "ISO 8601 datetime",
    "participants": "array of names",
    "summary": "bullet points",
    "decisions": "array of decisions made",
    "actions": "array with action, assignee, due date"
  }
}
```

**Becomes prompt:**
```
You are to produce a meeting summary. Structure it as follows:

1. Title of the meeting
2. ISO 8601 date/time
3. List of participants (names only)
4. Summary of discussion (bullet points)
5. Decisions made (bullet points)
6. Action items with assignee and due date

Do not add extra sections. Use only information from the transcript.
```

**Benefit:**
Works with any LLM, even those without JSON schema support.

## Beyond Artifact-First: Other Applications

### 1. Research Pipelines

**Use case:**
Standardize how research findings are extracted and structured.

**Benefit:**
Consistent format across many papers/sources.

### 2. Multi-Agent Systems

**Use case:**
Define contracts between agents.

**Benefit:**
Each agent produces standardized output that next agent can process.

### 3. Reporting Workflows

**Use case:**
Automated report generation from structured data.

**Benefit:**
Same spec generates different report formats.

### 4. System Integration

**Use case:**
Machine-readable outputs for APIs and integrations.

**Benefit:**
No parsing required; structure is guaranteed.

## Poor Man's Evaluations: The Hidden Superpower

### The Insight

**Standard approach (expensive):**
Build expensive evaluation framework
Use human judges
Slow, costly, limited scale

**Better approach (cheap):**
Use the same schema for evaluation
One model generates, another evaluates
Same structure, consistent metrics

### The Evaluation Schema

**Structure:**

```json
{
  "input": "original task/prompt",
  "output": "model's output being judged",
  "reference": "gold/reference answer or spec",
  "task_type": "qa, summarization, extraction, etc.",
  "evaluation": {
    "score": 0-1,
    "verdict": "pass, fail, borderline",
    "reason": "explanation",
    "criteria": [
      {
        "name": "accuracy",
        "score": 0-1,
        "notes": "details"
      }
    ],
    "confidence": 0-1
  },
  "checks": {
    "instruction_following": boolean,
    "factuality": boolean,
    "safety_ok": boolean
  }
}
```

### Evaluation Process

**Process:**

```
Input: The task the model received
Output: What the model produced
Reference: The spec/expectation
    ↓
Judge LLM evaluates output against reference
    ↓
Produces structured evaluation
    ↓
Can score across multiple criteria
    ↓
Can compare models/agents side-by-side
```

**Example evaluation:**

```json
{
  "input": "Meeting transcript provided",
  "output": "Meeting summary produced in step 2",
  "reference": "Schema definition + requirements",
  "evaluation": {
    "score": 0.95,
    "verdict": "pass",
    "reason": "Summary is accurate, complete, well-structured.
              All key points captured. Minor details omitted
              but acceptable.",
    "criteria": [
      {
        "name": "accuracy",
        "score": 0.95,
        "notes": "All main facts correct"
      },
      {
        "name": "completeness",
        "score": 0.9,
        "notes": "All agenda items included; minor asides omitted"
      },
      {
        "name": "clarity",
        "score": 1.0,
        "notes": "Well formatted, easy to scan"
      },
      {
        "name": "instruction_following",
        "score": 1.0,
        "notes": "Matches schema structure exactly"
      }
    ],
    "confidence": 0.95
  }
}
```

### Why This Works

**Advantages:**
- Same structure for input and evaluation
- Consistent metrics across runs
- Compare models objectively
- Close the feedback loop
- One model generates, another grades
- All anchored to the same artifact spec

**Result:**
Standardized generation AND standardized evaluation.

## From Spec to Evaluation: The Complete Picture

### The Full Workflow

```
1. Define Artifact Spec
   (JSON Schema of desired output)
    ↓
2. Create plain-text prompt from schema
   (Instructions for LLM)
    ↓
3. LLM generates structured output
   (Validated against schema)
    ↓
4. Validate output against schema
   (Automatic validation)
    ↓
5. Render for humans
   (Convert JSON to readable format)
    ↓
6. Use evaluation spec to assess quality
   (LLM-as-a-Judge using same structure)
    ↓
7. Compare scores across models/runs
   (Objective, consistent metrics)
```

**Every step grounded in the schema.**

## Repository and Reusable Specs

### o3-cloud/artifact-specs

**Contains:**
- Meeting summary schema
- Research paper summary schema
- Action item extraction schema
- And many more...

**How to use:**
1. Find schema matching your need
2. Use as-is or adapt
3. Feed to LLM
4. Validate output
5. Render for humans
6. Evaluate quality

## Key Takeaways

1. **Artifact Specs are JSON Schemas** — Blueprints for outputs
2. **Define before building** — Artifact first, agent second
3. **Clarifies "done"** — Removes ambiguity about requirements
4. **Enables automation** — Validation is automatic
5. **Model agnostic** — Works with any LLM
6. **Reusable across teams** — One spec, many workflows
7. **Machine-readable** — Outputs can be validated and integrated
8. **Human-readable** — Same structure renders to clean formats
9. **Translation to prompts** — Schema becomes plain-text instructions
10. **Validation prevents garbage** — Bad outputs are rejected immediately
11. **Switching models is trivial** — Spec stays constant, LLM changes
12. **Beyond generation** — Specs define extraction, aggregation, everything
13. **Three-step process works** — Unstructured → Structured → Human-Readable
14. **Evaluation schemas enable assessment** — Same structure for judging quality
15. **LLM-as-a-Judge becomes practical** — Use one model to generate, another to score
16. **Consistent metrics across runs** — Compare models objectively
17. **Criteria-based scoring** — Break down evaluation across dimensions
18. **Feedback loops close** — Evaluation insights improve next generation
19. **Schema repository available** — Ready-to-use specs for common tasks
20. **No fancy infrastructure needed** — "Poor man's evaluation" without complexity

## The Bottom Line

Owen Zanzal's Artifact Specs framework provides the practical mechanism for implementing artifact-first thinking: concrete JSON Schema specifications that serve as blueprints for AI output, enabling standardized, validated, model-agnostic workflows.

**The core value:**

**Instead of:**
- Building agents and hoping outputs work
- Manually validating every output
- Being locked to one LLM vendor
- Treating evaluation as expensive

**Do this:**
- Define artifact spec upfront
- Use spec to validate outputs automatically
- Switch LLMs without changing workflow
- Use structured evaluation with same schema

**The three-step pattern:**
1. **Unstructured input** — Raw meeting transcript
2. **Structured extraction** — JSON conforming to schema
3. **Human rendering** — Readable format from structured data

**The evaluation superpower:**
Same schema structure that generates outputs can evaluate outputs. Use one model to generate, another to grade. Consistent metrics. Comparable results.

**For practitioners:**
Start with a spec. Make it explicit. Use it to guide generation and validate outputs. Don't build the agent until you know what artifact you're producing.

**For teams:**
Specs become organizational assets. One meeting summary spec used across all projects. Shared understanding. Consistent quality.

**For workflows:**
Schema becomes the stable contract. Everything else—agent, LLM, framework—is interchangeable.

**The philosophy:**
Artifacts first. Agents second. Specs concrete. Everything flows from clarity about what you're actually trying to build.

That's how artifact specs bring the artifact-first approach to life.

