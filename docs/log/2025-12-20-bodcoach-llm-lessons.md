---
summary: Justin Schroeder shares five critical lessons from building Bod.Coach (AI-powered fitness trainer)—output format engineering, managing model eagerness, tool stratification, economic stratification with model routing, and building custom infrastructure for reliability
event_type: article
sources:
    - https://dev.to/justinschroeder/building-bodcoach-llm-lessons-learned-the-hard-way-59kf
tags:
    - LLM-applications
    - AI-product-development
    - practical-engineering
    - prompt-engineering
    - system-design
    - cost-optimization
    - reliability
    - model-routing
---

# Building Bod.Coach: LLM Lessons Learned the Hard Way

**Author:** Justin Schroeder
**Platform:** Dev.to
**Publication Date:** December 20, 2025

## Overview

Schroeder shares five hard-won lessons from developing Bod.Coach, a text-message-based AI fitness trainer app. The insights challenge conventional wisdom about LLM applications and reveal the gap between research and production systems. Building reliable AI products requires different intuitions than traditional software engineering.

## The Five Critical Lessons

### Lesson 1: Output Format Matters More Than You Think

**The Problem:**
LLMs naturally produce lower-quality structured data (JSON, CSV, etc.) compared to natural text. Attempts to force structured output lead to format errors and parsing failures.

**The Solution: Chaining**
Use a two-pass approach:
1. First pass: Generate detailed, comprehensive response in natural language
2. Second pass: Restructure the response into required format

**Impact:** Higher accuracy, fewer formatting errors, more reliable downstream processing

**Example:**
```
Instead of: "Generate workout as JSON"
Use: "First describe workout in detail, then format as JSON"
```

### Lesson 2: LLMs Rush to Conclusions

**The Problem:**
Models behave as if each interaction is their last opportunity to impress the user. This causes:
- Premature conversation termination
- Skipped steps
- Incomplete explanations
- Rushing to final recommendations

**The Root Cause:**
Models optimize for immediate satisfaction rather than conversation flow, treating each turn as potentially final.

**The Solution: Explicit Sequencing**
Tell the LLM exactly how many questions/steps remain before completion:

```
"You have 3 more questions to ask before providing the final workout plan."
```

**Impact:** More thoughtful interactions, better information gathering, higher-quality outputs

### Lesson 3: Too Many Tools Degrade Accuracy

**The Problem:**
Offering comprehensive tool sets and options sounds beneficial but actually:
- Increases decision complexity
- Leads to worse choices
- Overloads the model's reasoning
- Reduces reliability

**The Solution: Routers with Limited Choice Sets**
Use decision trees to narrow options:
1. Create router prompts that guide selection to ~6 maximum options
2. Use hierarchical decision-making
3. Route complex scenarios through progressive refinement

**Architecture:**
```
Complex problem → Router → Narrow to 6 options → Specialized handler
```

**Impact:** More reliable choices, better performance, higher user satisfaction

### Lesson 4: Economics Require Model Stratification

**The Challenge:**
Premium models (GPT-4, Claude 3 Opus) are expensive. Consumer apps like Bod.Coach ($11.99/month) cannot sustain costs of premium model for every request.

**The Solution: Cost-Aware Routing**
Implement intelligent model selection based on task complexity:

| Task Complexity | Recommended Model | Cost Consideration |
|-----------------|-------------------|-------------------|
| Simple responses | Cheaper model (GPT-3.5, Haiku) | 95% of requests |
| Medium complexity | Mid-tier model | 4% of requests |
| Complex (workouts, planning) | Premium model (GPT-4, Opus) | 1% of requests |

**Implementation:**
- Classify incoming requests by complexity
- Route simple requests to cost-effective models
- Reserve premium models for genuinely complex reasoning
- Monitor and adjust thresholds based on quality/cost metrics

**Impact:** 80-90% cost reduction while maintaining quality for high-value requests

### Lesson 5: Build Custom Infrastructure

**The Problem:**
Third-party frameworks (LangChain, etc.) optimize for flexibility and feature richness, not production reliability. They become bottlenecks as your needs evolve.

**Why This Matters:**
- AI capabilities change rapidly
- Your requirements become increasingly specific
- Frameworks lock you into predetermined patterns
- Custom solutions adapt faster

**What to Build:**
- Logging and observability systems
- Provider compatibility layers (switch between OpenAI, Anthropic, etc.)
- Fault tolerance and retry logic
- Flow control and rate limiting
- Custom decision trees and routers

**Philosophy:**
"Build what you actually need, not what's theoretically possible."

**Impact:** Better control, faster iteration, ability to adapt to model changes

## The Broader Insight

### No Shortcut Beyond Hands-On Experience

**Traditional Software Intuition ≠ LLM Application Intuition**

What works in software engineering:
- Premature optimization is evil
- DRY (Don't Repeat Yourself)
- Maximize flexibility and options
- Generic solutions > custom code

What works with LLMs:
- Output format requires explicit engineering
- Models need guidance on interaction length
- Limited tool sets > comprehensive options
- Specific solutions > generic frameworks
- Cost stratification is mandatory

**The Implication:**
Success requires time spent in production, observing failures, and iterating on actual user experiences.

## Practical Applications

### For AI Product Builders

**Immediate Actions:**
1. Implement output chaining for structured data
2. Add explicit sequence counts to conversations
3. Audit your tool/option sets—can you reduce?
4. Analyze request patterns for model stratification opportunity
5. Evaluate framework dependencies vs. custom solutions

### For LLM Integration Teams

**Testing and Monitoring:**
- Monitor output format consistency
- Track conversation length and quality
- Measure accuracy by tool count
- Calculate cost per successful request
- Measure framework overhead

### For Cost-Constrained Projects

**Model Stratification Strategy:**
1. Profile your actual request distribution
2. Identify high-value requests requiring premium models
3. Implement classifier for request complexity
4. Route accordingly
5. Validate quality metrics don't suffer

## Key Takeaways

1. **Output format is engineering work** — Two-pass chaining produces better results than forcing structure
2. **Models rush conclusions** — Explicit sequencing prevents premature termination
3. **Limited tools > comprehensive tools** — Decision trees with ~6 options outperform large tool sets
4. **Economics force stratification** — Route by complexity to maintain affordability
5. **Framework flexibility has costs** — Custom infrastructure beats flexible frameworks in production
6. **Different intuitions required** — LLM reliability engineering differs fundamentally from software engineering
7. **Hands-on experience is mandatory** — No theoretical understanding replaces production learning
8. **Cost optimization is strategic** — Model routing enables sustainable consumer AI products

## The Bottom Line

Building reliable AI applications requires unlearning software engineering intuitions and acquiring new ones through production experience. Schroeder's five lessons—output format engineering, managing model eagerness, tool stratification, economic model routing, and custom infrastructure—reveal that LLM application development is fundamentally different from traditional software. The most successful products aren't built with the most flexible frameworks or comprehensive tool sets, but with deliberate simplifications driven by production constraints and real user behavior. The path to reliability isn't theoretical but empirical: hands-on iteration, careful monitoring, and willingness to reject both software engineering conventional wisdom and AI research best practices in favor of what actually works in production.
