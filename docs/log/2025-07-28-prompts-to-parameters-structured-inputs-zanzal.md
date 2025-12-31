---
summary: Owen Zanzal argues for structured inputs over freeform prompts in production LLM systems—showing how JSON-based, schema-validated inputs improve reliability, reduce ambiguity, enable chaining, and treat models as programmable functions rather than unpredictable oracles
event_type: blog_post
sources:
    - https://medium.com/devops-ai/from-prompts-to-parameters-the-case-for-structured-inputs-0fda3b69609f
tags:
    - structured-inputs
    - JSON-schema
    - prompt-engineering
    - LLM-reliability
    - system-design
    - input-validation
    - agent-design
    - production-systems
    - API-design
    - tool-use
---

# From Prompts to Parameters: The Case for Structured Inputs

**Author:** Owen Zanzal
**Platform:** Medium (DevOps+AI)
**Publication Date:** July 28, 2025
**Type:** Technical Practice Guide
**Duration:** 3 min read
**Key Concept:** Structured inputs as foundation for reliable LLM systems

## Overview

Owen Zanzal challenges the common assumption that prompting LLMs means typing natural-language requests. He argues that as LLMs move from consumer tools to production systems, structured inputs (typically JSON) become essential for reliability, safety, and composability.

Rather than treating LLMs as unpredictable conversational oracles, structured inputs enable treating them as programmable functions: testable, composable, predictable, with clear contracts and validation boundaries.

## The Common Misconception

### How People Think of Prompting

**Mental model:**
```
You → "Summarize this article"
    ↓
LLM → Understands and summarizes
    ↓
You → Get result
```

**In consumer context:**
This works reasonably well.

**In production context:**
This approach breaks down.

### Why Freeform Prompts Fail at Scale

**Problem 1: Ambiguity**
"Schedule a meeting with Sam next Tuesday"
- Which Sam? (3 people in contact list)
- Which timezone?
- What time?
- Which calendar?
- Virtual or in-person?

**Problem 2: Brittleness**
Slight wording differences cause different interpretations.

```
"Schedule meeting with Sam"
vs.
"Set up a meeting with Sam"
vs.
"Arrange a call with Sam"
```

All mean similar thing, but LLM might interpret differently.

**Problem 3: Scaling**
Building 100 features on freeform prompts means:
- 100 different prompt styles
- 100 times the potential for breakage
- Hard to maintain consistency
- Hard to debug failures

**Problem 4: Safety and Control**
Hard to guarantee what the LLM will do.

## What Are Structured Inputs?

### Definition

**Structured input:**
Data that is already parsed and organized (typically JSON), rather than raw natural language.

### Example: Weather Request

**Freeform approach:**
```
"What's the weather like in San Francisco tomorrow?"
```

**Structured approach:**
```json
{
  "action": "get_weather",
  "parameters": {
    "location": "San Francisco",
    "date": "2025-07-22",
    "units": "fahrenheit"
  }
}
```

### What This Provides

**For the system:**
- Clear intent
- Precise parameters
- Unambiguous data types
- Validation opportunity

**For the LLM:**
- Less ambiguity to resolve
- Clearer task definition
- Structured context
- Easier reasoning

## Why Structured Inputs Matter

### 1. Reduced Ambiguity

**Problem:**
Natural language is inherently ambiguous.

**Example:**
```
"Next Friday"
- Does it mean 1 week from now?
- Does it mean 1 week from last Friday?
- Does it mean the Friday of next week?
- Different people interpret differently
```

**Structured solution:**
```json
{
  "date_reference": "2025-07-25",
  "date_type": "specific_date"
}
```

**Result:**
No interpretation needed. Data is explicit.

### 2. Improved Reliability

**Benefits:**

```
Validate before sending to LLM
    ↓
Catch errors early
    ↓
Consistent input format
    ↓
Predictable LLM behavior
    ↓
Reusable prompt templates
```

**Practical improvements:**
- Validation prevents garbage input
- Consistent format prevents surprises
- Easy to add rules and constraints
- Easier to debug when something breaks

### 3. Easier for Tool Use and Agents

**Example: Task-based agent**

```json
{
  "task": {
    "title": "Draft quarterly report",
    "due_date": "2025-07-25",
    "priority": "high",
    "assignee": "Sarah",
    "context": {
      "project": "Q3-planning",
      "department": "Engineering"
    }
  }
}
```

**What LLM can do:**
- Reason over structured knowledge
- Make decisions based on fields
- Pass state between steps
- Chain operations together

**Benefit:**
Agent logic becomes clear and testable.

### 4. Better for Chaining and Automation

**Multi-step workflow:**

```
Step 1 Output (structured)
    ↓
Validate and transform
    ↓
Step 2 Input (structured)
    ↓
Process
    ↓
Step 3 Input (structured)
```

**Benefits:**
- Clear contracts between steps
- Easy to transform outputs
- Safe to compose components
- Easier to debug failures

## Structured Inputs vs. Prompt Templates

### The Difference

**Prompt templating:**

```
"Write a polite email to {{name}} about {{topic}}.
Make sure to mention {{key_point}}.
Sign off with {{signature}}"
```

**How it works:**
- Template is fixed
- Dynamic values inserted
- Result is still prose
- Each variation slightly different

**Limitations:**
- Template logic embedded in language
- Hard to validate
- Variations can subtly differ
- Mixing concerns (language + logic)

### Structured Input Approach

**Instead:**

```json
{
  "intent": "compose_email",
  "recipient": {
    "name": "Sam",
    "email": "sam@example.com"
  },
  "subject": "Quarterly Results",
  "tone": "professional",
  "include_points": [
    "Q3 revenue up 15%",
    "New product launch timeline",
    "Team expansion plans"
  ]
}
```

**How it works:**
- Data separated from language
- Validation happens first
- Schema enforcement
- System-level logic applied before LLM

**Advantages:**
- Data is validated before sending to LLM
- Same underlying prompt, different behaviors
- Can add business logic (filtering, transformation)
- Easier to test and debug

### The Separation of Concerns

**Structured inputs enable:**

```
Data layer (validated JSON)
    ↓
Business logic layer (rules, filtering)
    ↓
LLM layer (reasoning, generation)
    ↓
Output validation layer (format, safety)
```

**Each layer has clear responsibility.**

## When Structured Inputs Shine

### 1. APIs and Tool Triggering

**Example:**
```json
{
  "action": "lookup_order",
  "order_id": "ORD-12345",
  "fields": ["status", "tracking", "items"]
}
```

**Why:**
- Clear intent
- Specific parameters
- Unambiguous operation
- Easy validation

### 2. LLM Agents

**Passing state between steps:**

```json
{
  "agent_state": {
    "current_task": "analyze_data",
    "context": {...},
    "memory": {...},
    "available_tools": [...]
  }
}
```

**Why:**
- Agent needs precise state
- Chaining depends on clarity
- Debugging requires visibility
- Multi-step reasoning needs structure

### 3. Enterprise Systems

**Requirements:**
- Consistency across organization
- Auditability and compliance
- Security controls
- Reproducibility

**Structured inputs provide:**
- Clear data contracts
- Validation rules
- Audit trails
- Deterministic behavior

### 4. Multimodal Input

**Combining multiple data types:**

```json
{
  "intent": "analyze_document",
  "text": "...",
  "image": "base64_encoded_image",
  "metadata": {
    "source": "email",
    "priority": "high",
    "sender": "client@company.com"
  }
}
```

**Why:**
- Unified format
- Clear relationships
- Easy validation
- Consistent handling

### 5. Voice Interfaces

**Process:**

```
Voice input
    ↓
Speech recognition
    ↓
Parse to structured intent
    ↓
Validate structure
    ↓
Send to LLM
    ↓
Execute
```

**Benefit:**
Structured intent prevents NLU misinterpretations.

## Trade-Offs and Challenges

### What You Gain

| Benefit | Why |
|---------|-----|
| **Precise intent** | Data is explicit, not interpreted |
| **Schema validation** | Invalid inputs caught early |
| **Easier chaining** | Clear contracts between steps |
| **Safe for production** | Predictable, testable, auditable |
| **Reusable** | Same logic, different inputs |
| **Debuggable** | Clear data, clear flow |

### What You Sacrifice

| Cost | Impact |
|------|--------|
| **Upstream structuring** | Need to parse/organize data first |
| **Less flexibility** | Fuzzy queries harder to handle |
| **Higher complexity** | More setup, more validation |
| **Slower prototyping** | Schema definition takes time |
| **Rigidity** | Can't easily change structure |

### When Each Makes Sense

**Use freeform prompts when:**
- Prototyping quickly
- One-off exploration
- Casual use
- Low stakes

**Use structured inputs when:**
- Building production systems
- Consistency matters
- Scaling across features
- Safety is paramount
- Part of larger workflow

## Practical Implementation

### Basic Structure

```json
{
  "schema_version": "1.0",
  "intent": "action_name",
  "parameters": {
    "required_field": "value",
    "optional_field": "value"
  },
  "context": {
    "user_id": "...",
    "timestamp": "...",
    "metadata": {...}
  }
}
```

### Validation Before LLM

```
1. Receive structured input
2. Validate against schema
3. Apply business rules
4. Transform if needed
5. Send to LLM
6. Validate output
7. Return to user
```

### Error Handling

**Invalid input:**
```json
{
  "error": "validation_failed",
  "reason": "required_field 'location' missing",
  "expected_schema": {...}
}
```

**Clear error → easy debugging.**

## Key Takeaways

1. **Freeform prompts don't scale** — Ambiguous, brittle, hard to maintain
2. **Structured inputs enable reliability** — Validated, consistent, predictable
3. **JSON as default format** — Standard, widely supported, easy to validate
4. **Separation of concerns** — Data layer, logic layer, LLM layer
5. **Ambiguity is eliminated** — Explicit data, no interpretation needed
6. **Validation is gate-keeper** — Bad inputs caught before reaching LLM
7. **Reusable templates** — Same prompt, different inputs, different behaviors
8. **Chaining becomes safe** — Clear contracts between components
9. **Debugging is easier** — Visible data, clear flow, reproducible inputs
10. **Production systems benefit most** — Where consistency and safety matter
11. **Trade-off with flexibility** — Less adaptable to fuzzy queries
12. **Prototyping is slower** — Schema definition takes upfront effort
13. **APIs need structure** — Tool triggering requires precision
14. **Agents need structure** — State passing and chaining require clarity
15. **Enterprise systems need structure** — Compliance, audit, reproducibility
16. **Multimodal benefits** — Unified format for different data types
17. **Voice needs structure** — Parse speech to intent before LLM
18. **Schema validation critical** — Prevent invalid data entering system
19. **Error messages clearer** — Validation tells you what's wrong
20. **LLMs become predictable** — Reduced ambiguity means reduced surprises

## The Bottom Line

Owen Zanzal makes a compelling case that as LLMs move from consumer tools to production systems, structured inputs become essential infrastructure—not optional enhancement.

**The core insight:**
Treating LLMs as programmable functions (via structured inputs) rather than conversational oracles (via freeform prompts) fundamentally changes what you can build reliably at scale.

**The mechanism:**
```
Freeform prompt:
- Flexible
- Ambiguous
- Hard to validate
- Doesn't scale

Structured input:
- Rigid
- Unambiguous
- Easy to validate
- Scales well
```

**The trade-off:**
Upfront complexity and reduced flexibility for production reliability and safety.

**For developers:**
Start with freeform prompts for exploration. Migrate to structured inputs as systems mature and stakes increase.

**For production teams:**
Structured inputs should be the default architecture. They pay for themselves through reliability, debuggability, and reduced surprises.

**For systems:**
Structured inputs enable:
- Clear contracts between components
- Testable, composable pieces
- Audit trails and compliance
- Deterministic behavior
- Safe scaling

**The philosophy:**
LLMs are powerful reasoning engines, not oracles. Give them clear structure and constraints. The results are more reliable, more predictable, and more valuable.

From conversations to code. From prompts to parameters. That's the evolution as LLMs move into production.

