---
summary: Research paper on emergent hierarchical reasoning in LLMs through RL, revealing a two-phase learning dynamic and proposing HICRA algorithm for hierarchy-aware credit assignment
event_type: research
sources:
    - https://openreview.net/pdf?id=NlkykTqAId
tags:
    - emergent-reasoning
    - reinforcement-learning
    - hierarchical-reasoning
    - credit-assignment
    - LLM-optimization
---

# Emergent Hierarchical Reasoning in LLMs Through Reinforcement Learning

**Status:** Under review for ICLR 2026
**Authors:** Anonymous (double-blind review)

## Core Discovery

RL training creates an emergent functional reasoning hierarchy in LLMs, mirroring human cognition's separation of high-level strategic planning from low-level procedural execution. This explains puzzling phenomena like "aha moments," "length-scaling," and entropy dynamics.

## Two-Phase Learning Dynamic

### Phase ① - Procedural Consolidation
- Models first master low-level execution skills
- Marked by sharp decrease in perplexity and token entropy of execution tokens
- Model builds reliable "toolbox" of procedural abilities (calculations, substitutions, formula application)

### Phase ② - Strategic Exploration
- Learning frontier shifts to high-level strategic planning
- Marked by increasing semantic diversity of planning tokens
- Model explores diverse reasoning strategies (logical deduction, branching, backtracing)
- Sustained performance improvements driven by strategic planning mastery

## Key Concept: Strategic Grams (SGs)

N-grams that function as semantic units guiding logical flow, including:
- **Deduction**: "we can use the fact that"
- **Branching**: "let's try a different approach"
- **Backtracing**: "but the problem mentions that"

Automated pipeline identifies SGs with 86% precision (validated via human annotation).

## Proposed Algorithm: HICRA

**Hierarchy-Aware Credit Assignment** concentrates optimization on high-impact planning tokens rather than applying pressure indiscriminately across all tokens (as in GRPO).

### Mechanism
- Amplifies credit for planning tokens in successful trajectories
- Dampens penalties for planning tokens in unsuccessful ones
- Creates anisotropic reshaping of policy toward strategic dimensions
- Enables faster discovery and reinforcement of effective reasoning patterns

## Experimental Results

- Tested across 8 text-only and vision-language models (Qwen, Llama, MiMO-VL, etc.)
- Evaluated on multiple benchmarks: AIME24, AIME25, Math500, AMC23, Minerva, Olympiad, MathVista, MathVverse, EMMA
- **HICRA consistently outperforms GRPO baselines** across text and multimodal reasoning tasks
- Performance gains range from +0.7% to +8.4% across benchmarks

## Critical Insights

1. **Semantic Entropy vs. Token Entropy**: Token-level entropy is misleading for tracking exploration because it's dominated by vast low-level tokens. Semantic entropy accurately reflects diversity of strategic planning.

2. **Planning Tokens vs. High-Entropy Tokens**: While most planning tokens are high-entropy, most high-entropy tokens are NOT planning tokens. Entropy alone is insufficient for strategic credit assignment.

3. **Boundary Condition**: HICRA is most effective when applied to models with foundational procedural competence; less effective on models still consolidating basic skills.

## Key Takeaways

- RL improves reasoning by rediscovering hierarchical reasoning structure from pre-training
- Strategic planning mastery is the primary bottleneck for advanced reasoning
- Current agnostic RL algorithms dilute learning signal across all tokens
- Semantic understanding of reasoning function matters more than statistical uncertainty
