---
summary: Manuel Cossio provides comprehensive taxonomy of LLM hallucinations—framing them as mathematically inevitable rather than bugs, and proposing practical mitigation through hybrid systems with human oversight
event_type: research-paper
sources:
    - https://www.alphaxiv.org/overview/2508.01781v1
tags:
    - hallucinations
    - LLM-limitations
    - taxonomy
    - faithfulness
    - factuality
    - interpretability
    - mitigation
    - reliability
    - computability-theory
---

# A Comprehensive Taxonomy of Hallucinations in Large Language Models

**Author:** Manuel Cossio (Universitat de Barcelona)

**Publication:** AlphaXiv:2508.01781v1
**Publication Date:** August 1, 2025

## Overview

Manuel Cossio establishes a formal classification system for understanding hallucinations in large language models. Rather than treating hallucination as a fixable bug, the paper argues that hallucination is mathematically inherent to any computable language model. The work provides a multi-layered taxonomy of hallucination types, identifies root causes, and proposes practical mitigation strategies beyond seeking elimination.

## The Core Thesis

### Hallucination as Inevitability, Not Bug

**Traditional view:**
- Hallucinations are errors
- Better training eliminates them
- More data prevents them
- Sufficient scale avoids them
- Technical fix exists

**Cossio's argument:**
- Hallucinations are inherent to computation
- Using computability theory: mathematically unavoidable
- Any LLM (computable or otherwise) will hallucinate
- Not a training issue but fundamental property
- Mitigation, not elimination, is realistic goal

### Mathematical Inevitability

**The proof:**
- Language models are computable systems
- Computability theory shows inherent limitations
- Cannot guarantee truth in all cases
- Cannot distinguish true from plausible
- Hallucination is provably inescapable

**The implication:**
Hallucination isn't a problem to solve—it's a constraint to manage.

## Hallucination Taxonomy

### The Classification System

**Cossio's framework distinguishes:**

#### 1. Intrinsic vs. Extrinsic Hallucinations

**Intrinsic hallucinations:**
- Contradict the input context
- Ignore information provided
- Example: Told "John is 25 years old," model says "John is 30"
- Within-conversation inconsistency

**Extrinsic hallucinations:**
- Inconsistent with training data
- Not contradicted by input
- Invented facts not in training
- Example: "The capital of France is Berlin"
- Knowledge/factual inconsistency

#### 2. Factuality vs. Faithfulness

**Factuality errors:**
- Statement doesn't match reality
- Verifiable as false
- "The moon orbits Mars"
- Objective truth violation

**Faithfulness violations:**
- Statement doesn't follow from reasoning
- Logical inconsistency
- "All dogs are animals, therefore some dogs are plants"
- Reasoning validity violation

**Distinction:**
- Factual: Real-world truth
- Faithful: Internal consistency

#### 3. Scope of Hallucination

| Type | Definition | Example |
|------|-----------|---------|
| Complete | Entirely fabricated | Inventing a citation |
| Partial | Mixed true/false | Real person, wrong accomplishment |
| Subtle | Minor inaccuracy | Slight date error |
| Compound | Cascading errors | Wrong assumption leads to wrong answer |

## Root Causes Analysis

### Three Categories of Causes

#### 1. Data Quality Issues

**Problems:**
- Training data contains errors
- Conflicting information in data
- Outdated information
- Biased or incomplete data
- Noisy labeling

**Why it matters:**
- Model learns from what it's fed
- Can't know which data is wrong
- Reproduces data errors at scale

#### 2. Model Architectural Limitations

**Auto-regressive prediction:**
- Models predict next token probabilistically
- No inherent truth-checking mechanism
- High-confidence plausible tokens chosen
- Fluency != truth

**Architectural constraints:**
- No built-in verification
- No access to ground truth during inference
- No mechanism to say "I don't know"
- Biased toward generating text

**Why it matters:**
- Token prediction doesn't require truth
- Fluent language often trumps accuracy
- Architecture incentivizes completion

#### 3. Prompt and Usage Factors

**Problematic prompts:**
- Ambiguous instructions
- Conflicting requirements
- Unsupported assumptions
- Leading questions

**Usage errors:**
- Using model for tasks it can't do
- Trusting without verification
- Out-of-distribution inputs
- Demanding high confidence on uncertain matters

## Human Factors in Hallucination

### Cognitive Biases in Model Use

**Fluency heuristic:**
- If it sounds fluent, assume it's correct
- Models are fluent by design
- Human brains equate fluency with truth
- Dangerous combination

**Automation bias:**
- Over-relying on automated systems
- Assuming AI output is verified
- Skipping human review
- Trusting AI beyond evidence

**Confidence illusions:**
- Model appears confident
- Confidence != correctness
- Users mistake confidence for accuracy
- Leads to over-trust

### The Human Role

**Users amplify hallucination risk by:**
- Not reading critically
- Accepting without verification
- Using for tasks requiring absolute accuracy
- Trusting beyond model capability
- Skipping human judgment

## Mitigation Strategies

### Moving Beyond Elimination

**Why elimination won't work:**
- Mathematically impossible
- Would require solving halting problem
- Any practical language model will hallucinate
- Better to accept and manage

### Practical Mitigation Framework

**Multi-layered approach:**

#### 1. Retrieval-Augmented Generation (RAG)

**How it helps:**
- Retrieves relevant documents before generation
- Grounds response in actual sources
- Provides citation sources
- Limits to retrievable knowledge

**Limitations:**
- Only helps with factual hallucinations
- Doesn't prevent intrinsic hallucinations
- Requires good retrieval
- Adds latency and complexity

#### 2. Guardrails and Constraints

**Structural approaches:**
- Limit response space
- Require citation format
- Enforce consistency checks
- Reject low-confidence outputs
- Predefined response templates

**Benefits:**
- Prevents certain hallucinations
- Makes failures obvious
- Reduces risk surface
- Enables verification

#### 3. Continuous Human Oversight

**Not one-time review:**
- Sampling of outputs monitored
- Feedback loops built in
- Users empowered to report
- Continuous improvement

**Why important:**
- Catches novel failure modes
- Adapts to new use cases
- Maintains accountability
- Grounds system in reality

### Context-Aware Systems

**Key principle:**
Different contexts need different mitigation levels.

**High-stakes mitigation:**
- Medical diagnosis → Full human review
- Legal opinions → Expert verification
- Financial advice → Multiple sources
- Factual claims → Retrievable sources

**Low-stakes acceptance:**
- Brainstorming → Ideation fine
- Creative writing → Fabrication acceptable
- Casual chat → Accuracy less critical
- Initial drafting → Editing follows

## Implications for LLM Deployment

### What This Means for Users

**Accept the constraint:**
- LLMs will hallucinate
- No amount of prompting eliminates this
- Assume some outputs are wrong
- Verify for critical matters

**Design for hallucination:**
- Expect errors in outputs
- Build verification systems
- Use guardrails appropriate to stakes
- Plan for human review

**Use appropriately:**
- High-stakes decisions → Don't rely on LLM alone
- Creative tasks → Hallucination acceptable
- Factual queries → Verify against sources
- Unknown reliability → Assume hallucination possible

### What This Means for Builders

**Don't promise elimination:**
- Can't eliminate hallucinations
- Can't guarantee factuality
- Must be honest about limitations
- Build user understanding

**Design systems carefully:**
- Match mitigation to stakes
- Build verification into workflows
- Make limitations visible
- Enable user judgment

**Invest in mitigation:**
- RAG systems
- Fact-checking
- Source attribution
- Human oversight
- User education

## Key Takeaways

1. **Hallucinations are inevitable** — Mathematically unavoidable, not fixable bugs
2. **Taxonomy clarifies types** — Intrinsic/extrinsic, factual/faithful distinctions matter
3. **Root causes are identified** — Data, architecture, usage all contribute
4. **Human factors amplify risk** — Fluency heuristics and automation bias
5. **Elimination impossible** — But mitigation is practical
6. **Context determines approach** — Different stakes need different strategies
7. **RAG helps but doesn't solve** — Useful for factual accuracy, not all hallucinations
8. **Guardrails essential** — Structural constraints limit damage
9. **Human oversight irreplaceable** — No substitute for critical review
10. **User understanding crucial** — Education about limitations matters more than false certainty

## The Bottom Line

Manuel Cossio's taxonomy reframes hallucinations in LLMs from bugs-to-fix to inherent constraints-to-manage. Using computability theory, he demonstrates that hallucination is mathematically inevitable in any computable language model. Rather than promising impossible elimination, the realistic approach is pragmatic mitigation: retrieval-augmented generation for factuality, guardrails for consistency, continuous human oversight, and context-aware risk assessment.

The key insight is that hallucinations aren't failures of training or scale—they're fundamental properties of token-prediction-based language generation. The goal shifts from "eliminate hallucinations" to "design systems where hallucinations matter less." For high-stakes applications, this means building in verification, human review, and source attribution. For lower-stakes uses, hallucination is often acceptable if understood and managed.

The implication for LLM deployment is clear: users and builders must design systems with the assumption that some outputs will be wrong. Rather than trusting improvement in models to solve the problem, focus on mitigation strategies appropriate to the domain and the stakes. This honest framing—hallucinations as inevitable, mitigation as practical, understanding as essential—enables responsible deployment of powerful language models in the real world.
