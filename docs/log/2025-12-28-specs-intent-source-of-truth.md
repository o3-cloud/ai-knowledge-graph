---
summary: Exploration of how intent expressed in natural language may become the source of truth over code itself, driven by generative AI capabilities and specs-driven development practices.
event_type: research
sources:
    - https://it20.info/2025/12/specs-intent-and-the-source-of-truth/
    - Article by Massimo Re Ferrè
tags:
    - generative-ai
    - developer-tools
    - software-engineering
    - ai-assisted-development
    - source-of-truth
    - intent-driven-development
---

# Specs, Intent, and the Source of Truth

## Question/Goal

How will the role of code and intent shift as AI-assisted development becomes mainstream? What does the future architecture of development look like when specifications and natural language intent become primary artifacts?

## Evolution of Developer Tools

The article traces a trajectory of developer tooling:
- **Past**: Basic editors → IDEs with linters, autocomplete
- **Present**: Generative AI tools enabling code generation from specifications
- **Pace**: "One year in generative AI is like three dog years" - rapid transformative change

## Current State (Today)

**Current Practice:**
- Developers employ "vibe coding" and "specs-driven development"
- AI writes code based on software specifications
- Source code remains the primary asset checked into repositories
- Process and prompts are typically discarded

**Key Insight:** The code itself is treated as the source of truth, but the intent and specifications driving it are ephemeral.

## Future Vision

**Paradigm Shift:**
- Intent expressed in natural language may become the source of truth
- Generated code becomes a downstream artifact (like CloudFormation templates)
- Development workflow inverts: Intent → Code Generation → Deployment

**Analogy:**
Just as CloudFormation templates are infrastructure-as-code that generates cloud resources, future development might treat natural language intent as the primary artifact that generates deployable code.

## Challenges Ahead

**Technical & Conceptual Obstacles:**
- **Expression**: Accurately expressing complex behavior in natural language
- **Verification**: Ensuring generated code matches declared intent
- **Security**: Validating that AI-generated code meets security requirements
- **Traceability**: Maintaining auditability and change tracking

## Timeline

Author's perspective:
- Lightheartedly suggests this transformation may only occur after retirement
- Acknowledges accelerated AI pace could bring it sooner than expected
- Uncertainty about feasibility reflects genuine technical and organizational challenges

## Implications for AI-Assisted Development

This represents a fundamental shift in how developers think about artifacts:
- **Current Model**: Code is the primary deliverable; specifications support it
- **Future Model**: Intent is the primary deliverable; code is a generated consequence

This aligns with observations about:
- Disciplined LLM coding workflows favoring specification-first approaches
- The increasing importance of prompt engineering and specification clarity
- Potential shift toward "intent verification" over "code review"

## Open Questions

- How would version control work with intent as source of truth?
- What tooling would enable effective intent expression and modification?
- How would organizations audit compliance when code is generated?
- What role remains for developers in a specs-driven model?

## Related Concepts

See also:
- LLM coding workflow best practices
- Knowledge-Graph-First design paradigm
- Disciplined approaches to AI-assisted development
