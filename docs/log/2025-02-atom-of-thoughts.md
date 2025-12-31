---
summary: Proposes Atom of Thoughts (AOT), a Markovian reasoning framework that minimizes historical dependencies during LLM inference through decomposition-contraction cycles, achieving superior test-time scaling efficiency
event_type: research
sources:
    - https://arxiv.org/pdf/2502.12018
tags:
    - test-time-scaling
    - markov-reasoning
    - attention-efficiency
    - reasoning-frameworks
    - inference-optimization
---

# Atom of Thoughts for Markov LLM Test-Time Scaling

**Status:** Submitted to NeurIPS 2025
**Authors:** Fengwei Teng, Quan Shi, Zhaoyang Yu, Jiayi Zhang, Yuyu Luo, Chenglin Wu, Zhijiang Guo
**ArXiv:** 2502.12018

## Core Problem

Existing test-time scaling methods (CoT, ToT, GoT) incur redundant computations by accumulating extensive historical context during inference. This creates inefficiency in the reasoning process.

## Key Innovation: Markovian Reasoning Process

Leverages the memoryless property of Markov processes to minimize reliance on historical context. Each reasoning state encapsulates self-contained information, reducing historical dependencies.

### Two-Phase State Transition Mechanism

**Phase 1 - Decomposition:** Convert current state into a Directed Acyclic Graph (DAG) representing internal dependencies among reasoning steps.

**Phase 2 - Contraction:** Transform the DAG into the next Markov state by:
- Solving independent nodes (those without incoming edges)
- Reformulating dependent nodes into answer-equivalent independent questions
- Creating simplified intermediate questions requiring fewer reasoning steps

## Emergent Atomic Reasoning Structure

When scaling up the Markovian chain through tree search and reflective refinement, complex reasoning trajectories converge into atomic structures—indivisible, self-contained reasoning units with stable, low token requirements.

Key characteristics:
- **Self-contained:** Problems are solvable independently
- **Answer-equivalent:** Each state preserves equivalence with original problem
- **Complexity-reduced:** Each transition reduces reasoning complexity (74-82% reduction)

## Quality Safeguards

**Termination Strategy:** After each transition, an LLM-as-a-judge selects the best answer from {solve(Q_i), solve(G_i), solve(Q_{i+1})}, implicitly enforcing answer equivalence through selection-based filtering.

**Metrics:**
- Answer Equivalence Maintenance: >99% across datasets
- Test-time Complexity Reduction: 74-82%
- LLM-as-a-Judge Selection Rate: 83-96%

## Experimental Results

Evaluated on:
- **Math:** MATH, GSM8K, AIME, AMC23, Minerva, Olympiad
- **Code:** MBPP, LiveCodeBench
- **Multi-hop QA:** LongBench (HotpotQA, MuSiQue, 2WikiMultiHopQA)

**Key Findings:**
- AOT consistently outperforms CoT, ToT, GoT, FoT baselines
- Works with both non-reasoning (GPT-4o-mini, DeepSeek-V3) and reasoning models (O3-mini, DeepSeek-R1)
- Scaling behavior improves with additional reasoning iterations without linear cost increase
- Modular integration enables seamless composition with existing methods

## Architecture Advantages

1. **Efficiency:** Reduces token overhead by concentrating on current state transformations rather than accumulating history

2. **Modularity:** Each Markov state serves as an optimized entry point for other reasoning methods, enabling flexible composition

3. **Interpretability:** DAG-based decomposition makes dependencies explicit, improving transparency of reasoning process

4. **Scalability:** Integrates seamlessly with tree search, self-consistency, and reflective refinement approaches

## Implementation Details

- Temperature: 1.0 for all sampling
- Default maximum transition count: 3 (empirically justified by MATH dataset structure analysis)
- Adaptive setting possible using initial DAG depth as upper bound
- Domain-specific prompts for math, code, and multi-hop QA tasks

## Key Insights

1. Most problems naturally decompose into 2-5 subquestions (3-4 most common)
2. Solution depths typically range 2-4 (depth 3 most frequent)
3. Structural complexity correlates with difficulty—higher depth/subquestion count shows lower accuracy
4. Complexity reduction is not "one-shot"—iterative transitions progressively simplify problems toward atomic states

## Limitations

- Fixed maximum transition count may not be optimal for all problem types
- Decomposition process adds computational overhead versus direct inference
- Quality depends heavily on underlying LLM's capability for generating valid dependency graphs
- No explicit training-time optimization for Markovian patterns
