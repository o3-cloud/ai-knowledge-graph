---
summary: Introduces ACE (Agentic Context Engineering), a framework treating contexts as evolving playbooks that accumulate and refine strategies through generation, reflection, and curation—achieving +10.6% on agents and +8.6% on finance benchmarks while reducing adaptation latency by 86.9%
event_type: research
sources:
    - https://arxiv.org/pdf/2510.04618
tags:
    - context-engineering
    - agent-memory
    - self-improvement
    - prompt-optimization
    - LLM-agents
    - test-time-adaptation
    - playbooks
---

# Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models

**Authors:** Qizheng Zhang, Changran Hu, Shubhangi Upasani, Boyuan Ma, Fenglu Hong, Vamsidhar Kamanuru, Jay Rainton, Chen Wu, Mengmeng Ji, Hanchen Li, Urmish Thakker, James Zou, Kunle Olukotun
**Affiliations:** Stanford University, SambaNova Systems, UC Berkeley
**ArXiv:** 2510.04618
**Publication Date:** October 6, 2025

## Overview

ACE (Agentic Context Engineering) is a framework for comprehensive context adaptation that treats contexts as **evolving playbooks**—detailed, inclusive repositories of domain insights that accumulate, refine, and organize strategies over time. Unlike prior approaches that compress contexts into concise summaries, ACE preserves detailed knowledge and scales with long-context models.

## Core Problem

Existing context adaptation methods suffer from two key limitations:

### 1. Brevity Bias
Many prompt optimizers prioritize concise, broadly applicable instructions over comprehensive accumulation. GEPA highlights brevity as a strength, but such abstraction omits:
- Domain-specific heuristics
- Tool-use guidelines
- Common failure modes
- Detailed strategies required by agents

### 2. Context Collapse
Methods relying on monolithic LLM rewriting degrade into shorter, less informative summaries over time. In one AppWorld case study:
- Step 60: 18,282 tokens, 66.7% accuracy
- Step 61: 122 tokens, 57.1% accuracy (worse than 63.7% baseline)

This represents catastrophic information loss from end-to-end context rewriting.

## Key Insight: Contexts as Playbooks

**"Contexts should function not as concise summaries, but as comprehensive, evolving playbooks—detailed, inclusive, and rich with domain insights."**

Unlike humans who benefit from concise generalization, LLMs are more effective when provided with long, detailed contexts and can distill relevance autonomously at inference time.

## ACE Framework Architecture

### Three Specialized Components

**Generator:** Produces reasoning trajectories for new queries, surfacing effective strategies and recurring pitfalls.

**Reflector:** Critiques traces to extract lessons, optionally refining them across multiple iterations. Separates evaluation and insight extraction from curation.

**Curator:** Synthesizes lessons into compact delta entries, merged deterministically into existing context by lightweight, non-LLM logic.

### Workflow

```
Query → Generator → Trajectory → Reflector → Insights → Curator → Delta Context Items
                                     ↑                              ↓
                                     └── Iterative Refinement ──────┘
                                                                    ↓
                                                          Context Playbook (Update)
```

## Key Innovations

### 1. Incremental Delta Updates

Context represented as collection of structured, itemized bullets rather than monolithic prompt:

**Bullet structure:**
- Metadata: unique identifier, counters tracking helpful/harmful usage
- Content: small unit (reusable strategy, domain concept, failure mode)

**Properties enabled:**
- **Localization:** Only relevant bullets updated
- **Fine-grained retrieval:** Generator focuses on pertinent knowledge
- **Incremental adaptation:** Efficient merging, pruning, de-duplication

### 2. Grow-and-Refine Mechanism

Balances context expansion with redundancy control:
- New bullets appended with fresh identifiers
- Existing bullets updated in place (incrementing counters)
- De-duplication via semantic embeddings
- Refinement: proactive (after each delta) or lazy (when context window exceeded)

### 3. Dedicated Reflector

Separates evaluation from curation:
- Improves context quality
- Enables iterative refinement rounds
- Better downstream performance than combined approaches

## Results

### Agent Benchmark (AppWorld)

| Method | Test-Normal TGC | Test-Challenge TGC | Average |
|--------|-----------------|---------------------|---------|
| ReAct (base) | 63.7 | 41.5 | 42.4 |
| ReAct + ICL | 64.3 | 46.0 | 46.0 |
| ReAct + GEPA | 64.9 | 46.0 | 46.4 |
| ReAct + DC | 65.5 | 52.3 | 51.9 |
| **ReAct + ACE** | **76.2** | **57.3** | **59.4** |

**Key finding:** ACE outperforms baselines by average of **10.6%** on agents.

### Domain-Specific Benchmarks (Finance)

| Method | FINER (Acc) | Formula (Acc) | Average |
|--------|-------------|---------------|---------|
| Base LLM | 70.7 | 67.5 | 69.1 |
| ICL | 72.3 | 67.0 | 69.6 |
| GEPA | 73.5 | 71.5 | 72.5 |
| DC | 74.2 | 69.5 | 71.8 |
| **ACE** | **78.3** | **85.5** | **81.9** |

**Key finding:** ACE outperforms baselines by average of **8.6%** on finance.

### AppWorld Leaderboard Performance

ACE matches the top-ranked production-level agent IBM CUGA (powered by GPT-4.1) on average, and **surpasses it on harder test-challenge split** while using smaller open-source model (DeepSeek-V3.1).

## Efficiency Gains

### Cost and Speed Analysis

**Offline (AppWorld):**
| Method | Latency (s) | # Rollouts |
|--------|-------------|------------|
| ReAct + GEPA | 53,898 | 1,434 |
| ReAct + ACE | 9,517 (-82.3%) | 357 (-75.1%) |

**Online (FiNER):**
| Method | Latency (s) | Token Cost ($) |
|--------|-------------|----------------|
| DC | 65,104 | $17.7 |
| ACE | 5,503 (-91.5%) | $2.9 (-83.6%) |

**Average latency reduction: 86.9%**

## Self-Improvement Without Labels

ACE constructs effective contexts **without labeled supervision** by leveraging:
- Execution feedback (code success/failure)
- Environment signals
- Natural execution outcomes

This enables self-improving agents that adapt reliably without ground-truth annotations.

## Playbook Structure

ACE-generated playbooks contain organized sections:

**STRATEGIES AND HARD RULES**
Domain-specific guidelines and constraints

**USEFUL CODE SNIPPETS AND TEMPLATES**
Reusable code patterns discovered during execution

**TROUBLESHOOTING AND PITFALLS**
Common failure modes and workarounds

**APIs TO USE FOR SPECIFIC INFORMATION**
Correct API usage patterns and output schemas

**VERIFICATION CHECKLIST**
Quality checks and validation steps

## Ablation Studies

| Component | Impact |
|-----------|--------|
| Without Reflector | -4.3% average |
| Without multi-epoch | -2.6% average |
| Without offline warmup | -3.4% average |

Each design choice contributes substantial performance gains.

## When ACE Works Best

ACE is most beneficial in settings that demand:
- Detailed domain knowledge
- Complex tool use
- Environment-specific strategies
- Knowledge beyond what's embedded in model weights

**Less beneficial for:**
- Tasks requiring only concise, high-level instructions (e.g., HotPotQA)
- Games with fixed strategies (e.g., Game of 24)

## Implications

### Longer Context ≠ Higher Serving Cost

Modern serving infrastructures optimize for long-context workloads through:
- KV cache reuse
- Compression
- Offload mechanisms

Amortized cost of handling long contexts continues to decrease.

### Online and Continuous Learning

ACE offers flexible alternative to model fine-tuning:
- Adapting contexts cheaper than updating weights
- Human-interpretable contexts enable selective unlearning
- Supports privacy/legal constraints (GDPR, CCPA)

## Key Takeaways

1. **Contexts as playbooks:** Comprehensive, evolving contexts outperform concise summaries
2. **Incremental updates:** Delta-based updates prevent context collapse
3. **Separation of concerns:** Dedicated Reflector improves quality
4. **Self-improvement:** Execution feedback enables adaptation without labels
5. **Efficiency:** 86.9% latency reduction with higher accuracy
6. **Scalability:** Smaller open-source models match production-level proprietary agents

## Comparison to Related Work

| Approach | Key Difference |
|----------|----------------|
| Dynamic Cheatsheet | ACE adds Reflector, incremental updates, grow-and-refine |
| GEPA | ACE avoids brevity bias, preserves detailed knowledge |
| Reflexion | ACE structures knowledge persistently, not just per-episode |
| A-MEM | ACE focuses on comprehensive playbooks, not just memory entries |

## The Bottom Line

ACE demonstrates that **comprehensive, evolving contexts enable scalable, efficient, and self-improving LLM systems with low overhead**. The key insight is treating contexts as detailed playbooks that accumulate domain knowledge rather than compressing into concise summaries—letting the model decide what matters at inference time.
