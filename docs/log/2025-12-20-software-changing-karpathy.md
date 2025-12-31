---
summary: Andrej Karpathy argues software is fundamentally changing—Software 3.0 replaces code with natural language, enabling vibe coding, agentic systems, and new programming paradigms with human-AI collaboration at the core
event_type: video
sources:
    - https://www.youtube.com/watch?v=LCEmiRjPEtQ
tags:
    - Software 3.0
    - LLM
    - natural-language-programming
    - agentic-systems
    - autonomy
    - vibe-coding
    - human-AI-collaboration
    - AI-infrastructure
---

# Software Is Changing (Again) – Andrej Karpathy

**Speaker:** Andrej Karpathy (Stanford, OpenAI, Tesla)
**Event:** AI Startup School, Y Combinator
**Platform:** YouTube
**Date:** June 17, 2025
**Duration:** ~40 minutes

## Overview

Andrej Karpathy presents a keynote on Software 3.0—a fundamental shift in how software is built. Drawing from his experience at Stanford, OpenAI, and Tesla, he argues that natural language is becoming the programming interface, LLMs function as operating systems, and we're entering the early days of a completely different software paradigm. We're in the 1960s of LLMs, building the infrastructure for a new era.

## The Evolution of Software

### Software 1.0

**Era:** Traditional programming
- **What:** Hand-written code
- **Interface:** Programming languages (Python, C++, Java)
- **Process:** Write code → Compile → Execute
- **Debugging:** Read code, find bugs, fix explicitly
- **Examples:** All software before 2022

**Characteristics:**
- Precise, explicit instructions
- Every behavior intentional
- Reproducible
- Requires detailed specification

### Software 2.0

**Era:** Deep learning
- **What:** Neural networks trained on data
- **Interface:** Data + loss functions
- **Process:** Collect data → Train → Deploy model
- **Debugging:** Improve data, adjust architecture
- **Examples:** Image recognition, speech-to-text, GPT models

**Characteristics:**
- Implicit behavior from training
- Learned from patterns
- Difficult to understand internals
- Specification through examples

### Software 3.0

**Era:** Natural language + LLMs
- **What:** LLM as OS, natural language as programming language
- **Interface:** Plain English descriptions
- **Process:** Describe behavior → LLM implements → Deploy
- **Debugging:** Refine descriptions, iterate
- **Examples:** ChatGPT plugins, Claude projects, specialized agents

**Key shift:** Programming in English, not code

## LLMs as Operating Systems

### The New Abstraction

**Historical parallel:**
- Assembly → Compilers → High-level languages → Operating systems
- Each layer abstracted lower complexity

**Current shift:**
- Code → LLMs as abstraction
- LLMs handle implementation details
- Humans describe intent in natural language

### Why LLMs Work as OS

| Function | How LLMs Provide |
|----------|-----------------|
| Application execution | Generate and execute code |
| Resource allocation | Decide what models to use |
| API/Tool interface | Access external functions |
| State management | Maintain conversation context |
| Error handling | Fix problems and retry |

### Utilities, Fabs, and OS

**Three models emerging:**

1. **Utilities** — API access (OpenAI, Anthropic APIs)
   - Pay per token
   - Like electricity grid
   - Commodity pricing

2. **Fabs** — Inference infrastructure (companies running models)
   - Like semiconductor fabrication plants
   - Require capital investment
   - Economies of scale

3. **OS** — LLM as platform
   - Like operating system
   - Run multiple applications
   - Manage resources

## Psychology of LLMs

### LLMs as Digital Minds

**Key insight:** LLMs exhibit personality and psychology

### Quirks and Behaviors

- **Goal misspecification** — Models optimize for what you said, not what you meant
- **Edge case weirdness** — Unexpected behaviors in unusual scenarios
- **"People spirits"** — Behaviors resembling human psychology
- **Context sensitivity** — Behavior varies with context and framing

**Implication:** Designing for LLMs requires understanding their psychology, not just their capability.

## Designing LLM Applications

### Partial Autonomy

**The spectrum:**

```
Full human control ←→ Partial autonomy ←→ Full autonomy
```

**Questions to answer:**
- When does the LLM decide?
- When do humans intervene?
- How confident is the LLM?
- What are the consequences?

### Human-AI Collaboration Loops

**The pattern:**

```
Human intent → LLM suggestion → Human review → Human decision → Action
```

**Examples:**
- Drafting documents (human refines)
- Code suggestions (human reviews)
- Decision support (human decides)
- Task automation (human supervises)

**Lesson from Tesla:** Autonomy sliders let users control human-AI balance.

### The Iron Man Analogy

**Two approaches:**

1. **Iron Man (Augmentation)**
   - Human in control
   - AI as tool/assistant
   - Human makes decisions
   - Lower autonomy but high control

2. **Agents (Full Autonomy)**
   - LLM in control
   - Human oversight
   - LLM makes decisions
   - Higher autonomy but requires oversight

**Choice determines system design.**

## Vibe Coding

### Everyone Is Now a Programmer

**Insight:** Natural language interface democratizes programming

**Before Software 3.0:**
- Only trained programmers could code
- Steep learning curve
- Specialized skill

**With Software 3.0:**
- Anyone can describe what they want
- LLM implements details
- Democratized capability

### What Vibe Coding Means

**Process:**
1. Describe desired behavior conversationally
2. LLM generates implementation
3. Refine based on results
4. Iterate toward desired system

**Advantages:**
- Lower barrier to entry
- Faster iteration
- Focus on problem, not syntax
- Immediate feedback

## Building for Agents

### Future-Ready Infrastructure

**Systems should support:**
- Agent decision-making
- Tool/API access
- State management
- Observability

### Agent Capabilities

**What agents need:**
- Clear objectives
- Tool access (APIs, queries, computations)
- Information retrieval
- Decision authority
- Feedback loops

### Infrastructure Implications

**Applications should:**
- Expose APIs for agent access
- Support agent reasoning patterns
- Provide observability
- Enable human oversight

## Historical Context

### We're in the 1960s of LLMs

**Parallel to early computing:**
- 1960s: Computing emerging but not ubiquitous
- Limited applications understood
- Infrastructure being built
- Future uses unclear

**Current LLM era:**
- Capabilities emerging
- Killer apps being discovered
- Infrastructure maturing
- Potential largely unknown

**Implication:** Now is the time to build.

## Key Insights from Tesla Experience

### Autonomy Sliders

**Pattern from Tesla Autopilot:**
- Users control automation level
- Adapt to comfort/capability
- Gradual autonomy increase
- Human remains engaged

**Applicable to LLM systems:**
- Give users control over autonomy
- Match human comfort
- Maintain oversight
- Build trust through transparency

### Iterative Improvement

**Tesla approach:**
- Deploy in limited form
- Collect data
- Improve
- Expand gradually

**For LLM systems:**
- Start with human in loop
- Remove humans from routine decisions
- Keep oversight for risky operations
- Expand autonomy as confidence grows

## Practical Framework

### Design Decisions

**For each LLM application:**
1. Define autonomy level (human ↔ agent spectrum)
2. Identify decision points
3. Design collaboration loops
4. Build observability
5. Plan for human oversight

### Implementation Patterns

| Pattern | When to Use | Example |
|---------|------------|---------|
| Tool access | Need external actions | API calls to databases |
| Multi-step reasoning | Complex problems | Writing articles |
| Collaborative review | High-risk decisions | Medical recommendations |
| Full autonomy | Low-risk, high-volume | Content categorization |

## Key Takeaways

1. **Software is fundamentally changing** — Natural language replacing code as interface
2. **LLMs as operating systems** — Abstraction layer above traditional computing
3. **Psychology matters** — Designing for LLMs requires understanding their quirks
4. **Partial autonomy is key** — Human-AI collaboration beats full automation or full control
5. **Vibe coding democratizes** — Anyone can now program at description level
6. **Agents require infrastructure** — Systems need APIs and oversight designed in
7. **We're in the 1960s** — LLM era is just beginning, infrastructure being built
8. **Tesla lessons apply** — Autonomy sliders, iterative deployment, continuous improvement

## The Bottom Line

Software is entering a new era. Software 3.0 replaces explicit code with natural language descriptions and LLM-powered implementation. LLMs function as operating systems—abstractions that handle implementation details while humans specify intent. The key design insight is partial autonomy: systems work best when humans and AI collaborate, with adjustable autonomy levels based on risk and capability. Vibe coding—describing behavior in English and letting LLMs implement—democratizes programming beyond trained engineers. We're building infrastructure for this transition now, in the early days (1960s) of LLMs. The successful software of the next decade will embrace this shift, design human-AI collaboration loops deliberately, and build agents with thoughtful oversight. The transformation is not about replacing programmers with AI, but about shifting what programmers do—from writing implementation details to specifying intent and designing human-AI systems.
