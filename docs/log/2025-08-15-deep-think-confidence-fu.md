---
summary: Fu, Wang, Tian, and Zhao investigate confidence scores as reliable indicators of reasoning quality in LLM extended thinking, introducing techniques for filtering reasoning paths and validating on challenging mathematics problems (AIME/HMMT)
event_type: research_paper
sources:
    - https://arxiv.org/pdf/2508.15260
tags:
    - reasoning
    - confidence
    - extended-thinking
    - LLM
    - mathematical-reasoning
    - AIME
    - reasoning-quality
    - inference-optimization
---

# Deep Think with Confidence

**Authors:** Yichao Fu, Xuewei Wang, Yuandong Tian, Jiawei Zhao
**Source:** arXiv
**Paper ID:** 2508.15260
**Publication Date:** August 15, 2025 (estimated based on ID)

## Overview

This research paper investigates a fundamental question about Large Language Models: can we use confidence scores as reliable indicators of reasoning quality during extended thinking processes? The authors demonstrate that confidence naturally serves as a proxy for sound reasoning, introducing practical techniques for leveraging confidence signals to improve performance on challenging mathematical problems.

## The Core Problem

### Extended Thinking Challenge

**What's being studied:**
Modern LLMs can perform extended reasoning—thinking through problems step-by-step before responding.

**The question:**
How can we determine if the reasoning is actually good without explicit verification?

**Why it matters:**
- Extended reasoning is computationally expensive
- Not all reasoning paths are equally valuable
- Need efficient way to rank or filter reasoning
- Can't always verify correctness before committing

### Traditional Approach

**Limitation:**
Requires explicit verification of correctness.

**Problem:**
For complex problems, verification is as hard as solving.

**Example:**
For AIME-level mathematics, you can't easily verify if reasoning is correct without solving the problem yourself.

## Key Insight: Confidence as Signal

### The Hypothesis

**Core claim:**
LLMs naturally express higher confidence when their reasoning is on track.

**Intuition:**
- Well-calibrated models recognize when they're on solid ground
- Reasoning paths with fewer logical gaps feel more certain
- Models can assess their own reasoning quality internally

**Implication:**
Confidence might be a usable proxy for reasoning quality.

## Research Methodology

### Experimental Setup

**Benchmark problems:**
- AIME (American Invitational Mathematics Examination)
- HMMT (Harvard-MIT Mathematics Tournament)
- Other challenging mathematics problems

**What they measured:**
- Confidence scores during reasoning
- Actual correctness of solutions
- Correlation between confidence and success

### Key Findings

#### 1. Confidence Correlates with Correctness

**Finding:**
Higher confidence during reasoning predicts better solutions.

**Evidence:**
Models consistently assign higher confidence to reasoning steps that lead to correct answers.

**Implication:**
Confidence is not random—it reflects something meaningful about reasoning quality.

#### 2. Internal Reasoning Quality Assessment

**Finding:**
LLMs can assess their own reasoning quality without external feedback.

**Mechanism:**
Through self-evaluation during thinking process.

**Significance:**
Models possess intrinsic signals about reasoning reliability.

#### 3. Confidence-Based Filtering Works

**Finding:**
Can rank multiple reasoning paths by confidence.

**Performance:**
Selecting paths with higher confidence improves solution quality.

**Practical value:**
Enables computational efficiency—run reasoning, rank by confidence, keep best paths.

## Practical Applications

### Filtering Multiple Reasoning Paths

**Scenario:**
Generate multiple reasoning attempts for difficult problem.

**Process:**
1. Generate N reasoning paths
2. Score each by confidence
3. Select top-K highest confidence
4. Use best path as answer

**Result:**
Better answers without needing to verify all paths.

**Efficiency gain:**
Filter out low-quality reasoning without manual verification.

### Computational Resource Optimization

**Challenge:**
Extended thinking is expensive (many tokens).

**Solution:**
Use confidence to determine when to stop thinking.

**Implementation:**
- Monitor confidence during reasoning
- Stop when confidence stabilizes
- Continue if confidence is increasing

**Benefit:**
Use tokens more efficiently on actually useful reasoning.

### Ranking Reasoning Attempts

**Application:**
Multiple attempts at same problem.

**Approach:**
1. Generate multiple reasoning chains
2. Score by confidence
3. Rank for final response
4. Use highest-confidence solution

**Outcome:**
Better solutions with better calibration.

## Mathematical Reasoning Case Study

### AIME Problem Characteristics

**Why these matter:**
- Extremely challenging (only top students solve)
- Require multi-step reasoning
- No obvious shortcuts
- Verification nearly as hard as solving

**Relevance:**
Ideal test case for confidence as quality signal.

### HMMT Problem Characteristics

**Similar difficulty:**
Harvard-MIT level competition math.

**Additional challenges:**
- Creative insight needed
- Multiple valid approaches
- Timing pressures in competition

**Testing scope:**
Validates approach across problem types.

### Performance Improvements

**Key results:**
- Confidence-based filtering improves accuracy
- Computational savings from early stopping
- Better calibration of model uncertainty

**Scale:**
Tested on difficult problems where single-sample reasoning is insufficient.

## Theoretical Implications

### Confidence as Intrinsic Signal

**Insight:**
Models don't just generate text—they have internal sense of reasoning quality.

**Mechanism:**
Through token prediction probabilities and attention patterns, models track whether reasoning is coherent.

**Significance:**
Suggests models have meaningful self-assessment capabilities.

### Self-Evaluation Without Feedback

**Finding:**
Models evaluate their own reasoning without external guidance.

**How:**
Through inherent language model properties—probability distributions over next tokens contain confidence information.

**Implication:**
We may have underutilized intrinsic model signals.

### Bridging Internal and External Quality

**Question addressed:**
Do models' internal certainty match external correctness?

**Answer:**
Yes, meaningfully so.

**Importance:**
Connects what models internally know to what they externally produce.

## Methodological Contributions

### Confidence Extraction

**Technique:**
Extract confidence scores from model reasoning process.

**Sources:**
- Token probabilities
- Attention patterns
- Internal representations
- Explicit confidence statements

**Validation:**
Show extracted confidence correlates with correctness.

### Filtering Algorithms

**Approaches tested:**
- Simple thresholding
- Ranking by confidence
- Ensemble methods
- Multi-stage filtering

**Results:**
Multiple approaches work; simpler is often sufficient.

### Evaluation on Competition Math

**Challenge:**
Hard problems require sophisticated metrics.

**Solution:**
Use formal verification (exact match for numerical answers).

**Benefit:**
No subjective evaluation needed.

## Practical Implementation Insights

### Confidence Score Calibration

**Finding:**
Raw model confidence may not be perfectly calibrated.

**Solution:**
Calibration techniques to improve reliability.

**Importance:**
Enables threshold-based filtering decisions.

### Multi-Attempt Strategies

**Approach 1: Best-of-N**
Generate N attempts, select highest confidence.

**Approach 2: Ensemble**
Combine multiple attempts using confidence weights.

**Approach 3: Sequential**
Stop thinking when confidence stabilizes.

### Integration with Extended Thinking

**Pattern:**
Works naturally with step-by-step reasoning.

**Benefit:**
Can monitor confidence throughout thinking process.

**Application:**
Dynamic allocation of computation resources.

## Connection to Broader Research

### Related Work

**Alignment with:**
- Work on model calibration
- Research on reasoning transparency
- Studies of self-evaluation

**Novel contribution:**
Application to extended reasoning in mathematics.

### Implications for AI Safety

**Relevance:**
If models can assess reasoning quality internally, might inform interpretability work.

**Caution:**
Confidence doesn't necessarily indicate truthfulness in all domains.

**Future work:**
Investigate domain-specific reliability of confidence signals.

## Limitations and Future Work

### Current Limitations

**Scope:**
Tested primarily on mathematics problems.

**Question:**
How well does this generalize to other domains?

**Future work:**
Extend to coding, writing, factual reasoning.

### Calibration Questions

**Issue:**
Confidence may not be equally reliable across problem types.

**Research needed:**
Understand when confidence is trustworthy.

### Domain Specificity

**Observation:**
Mathematics may be ideal for this approach.

**Reason:**
Clear right/wrong answers, stable problem structure.

**Question:**
Does this work for open-ended tasks?

## Key Takeaways

1. **Confidence as quality signal** — Models express confidence aligned with reasoning quality
2. **No verification needed** — Can rank paths without explicit correctness checking
3. **Practical application** — Filter multiple attempts to get better answers
4. **Computational benefit** — Use confidence to optimize token usage
5. **Mathematical focus** — Validated on AIME/HMMT competition problems
6. **Self-assessment capability** — Models can evaluate their own reasoning
7. **Intrinsic signals** — We may underutilize internal model information
8. **Generalizable approach** — Principles likely extend beyond math
9. **Calibration matters** — Need to understand when confidence is reliable
10. **Enables efficiency** — Support better inference strategies

## The Bottom Line

Fu, Wang, Tian, and Zhao's research demonstrates that confidence scores can serve as reliable indicators of reasoning quality in LLMs performing extended thinking. Rather than requiring explicit verification (which is computationally expensive), models naturally express higher confidence when their reasoning is sound.

This insight enables practical improvements: filter multiple reasoning paths by confidence, allocate computation adaptively, and select better solutions without verification. Tested on challenging mathematics competitions (AIME, HMMT), the approach shows consistent benefits.

The broader significance is that this work suggests LLMs possess intrinsic signals about reasoning reliability that we may currently underutilize. By leveraging confidence information already generated during inference, we can improve accuracy and efficiency simultaneously.

For practitioners building systems with extended reasoning, this suggests a simple strategy: generate multiple reasoning paths and rank by confidence. For researchers, it opens questions about self-evaluation capabilities in language models and whether confidence signals can be leveraged across other domains beyond mathematics.

The research bridges an important gap between what models internally know (confidence) and what they externally produce (correctness), suggesting that future improvements in reasoning may come not just from better models, but from better utilization of signals they already generate.
