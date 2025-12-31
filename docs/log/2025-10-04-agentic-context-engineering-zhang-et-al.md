---
summary: Zhang et al. introduce agentic context engineering—framework for autonomous prompt and example refinement through iterative agent-based optimization enabling self-improving LLMs without weight modification
event_type: research_paper
sources:
    - https://arxiv.org/pdf/2510.04618
tags:
    - context-engineering
    - self-improvement
    - prompt-optimization
    - in-context-learning
    - agentic-systems
    - LLM-adaptation
    - continuous-improvement
    - feedback-loops
---

# Agentic Context Engineering: Evolving Contexts for Self-Improving Language Models

**Authors:** Qizheng Zhang, Changran Hu, Shubhangi Upasani, Boyuan Ma, Fenglu Hong, Vamsidhar Kamanuru, Jay Rainton, Chen Wu, Mengmeng Ji, Hanchen Li, Urmish Thakker, James Zou, Kunle Olukotun

**Publication Date:** October 4, 2025
**Type:** Research Paper
**Venue:** arXiv

## Overview

Zhang et al. present agentic context engineering—a framework for automatically refining system prompts and in-context examples through iterative agent-based optimization. Rather than fine-tuning model weights, this approach enables language models to progressively enhance their performance by evolving the contextual information they operate within.

The key innovation: agents manage the evolution of prompts and examples through structured feedback cycles, creating self-improving systems without requiring model retraining.

## The Core Problem

### The Challenge with Fine-Tuning

**Current approach:**
Improve model performance by fine-tuning weights on task-specific data.

**Limitations:**
- Computationally expensive
- Requires careful data curation
- Risk of catastrophic forgetting
- Not practical for frequent updates

### The Alternative: Context Engineering

**Insight:**
Model performance depends not just on weights, but on what context the model operates within.

**Approach:**
Instead of modifying weights, evolve the prompts, examples, and context that guide the model.

**Advantage:**
- No retraining required
- Fast iteration cycles
- Easy to experiment with
- Can be automated

## The Agentic Context Engineering Framework

### How It Works

**Iterative cycle:**

```
Analyze task performance
    ↓
Agent identifies weaknesses
    ↓
Agent generates improved prompts/examples
    ↓
Test modifications on benchmark
    ↓
Incorporate feedback
    ↓
Repeat (next iteration)
```

### The Key Components

**1. Initial Context**
- System prompt defining task
- In-context examples showing correct behavior
- Context establishes baseline

**2. Performance Analysis**
- Agent evaluates model outputs
- Identifies failure patterns
- Recognizes systematic errors
- Determines what's not working

**3. Context Refinement**
- Agent modifies system prompt
- Agent improves or replaces examples
- Agent adjusts context structure
- Refinements informed by failure analysis

**4. Evaluation**
- Test refined context on benchmark
- Measure performance improvement
- Compare to previous iteration
- Determine if better

**5. Feedback Integration**
- Agent analyzes evaluation results
- Extracts lessons from this iteration
- Plans next refinement
- Incorporates insights into next round

### The Feedback Loop

**What makes it work:**
- Explicit measurement of performance
- Structured refinement process
- Automated evaluation
- Agent reasoning about improvements

**Result:**
Contexts evolve toward better performance.

## Key Mechanisms

### System Prompt Evolution

**What agents modify:**
- Task description clarity
- Constraint articulation
- Reasoning guidance
- Output format specification

**Example evolution:**

```
Iteration 1:
"Classify sentiment of text"

Iteration 2:
"Classify sentiment of text as positive, negative, or neutral.
Consider both explicit and implicit emotional language.
If mixed signals exist, explain the tension and choose the dominant sentiment."

Iteration 3:
"Classify sentiment of text. Key considerations:
1. Explicit emotional language (strong indicators)
2. Implicit tone (sarcasm, innuendo)
3. Context (question as sarcasm)
4. Mixed signals (explain tension, choose dominant)
Return: [sentiment] [confidence 0-1] [reasoning]"
```

**Progression:**
Clarity increases; reasoning becomes more explicit; edge cases addressed.

### In-Context Example Evolution

**What agents modify:**
- Example selection
- Example quality
- Example diversity
- Example annotation

**Example evolution:**

```
Iteration 1:
3 basic examples showing main cases

Iteration 2:
3 basic examples + 2 edge case examples
Edge cases highlight tricky situations

Iteration 3:
5 core examples with detailed reasoning
Edge cases with explanation of difficulty
Counter-examples showing common mistakes
```

**Progression:**
Coverage increases; reasoning explicit; failure cases addressed.

## Methodology: How They Validated

### Experimental Setup

**Benchmarks tested:**
- AppWorld (application interaction tasks)
- Legal reasoning (specialized domain)
- Other specialized reasoning tasks

**Agent implementation:**
- Agents analyze failure cases
- Generate context improvements
- Propose modifications
- Evaluate results

**Comparison:**
- Baseline (original context)
- After 1 iteration
- After 5 iterations
- After 10 iterations

### Metrics

**Performance measured:**
- Task accuracy
- Reasoning quality
- Generalization to test set
- Consistency of improvements

## Key Findings

### Performance Improvements

**Across domains:**
Consistent gains demonstrated across benchmarks.

**Magnitude:**
Significant improvements possible through context evolution alone.

**Without fine-tuning:**
All gains achieved through prompt/example refinement, not weight modification.

### Domain-Specific Effectiveness

**General tasks:**
Solid improvements; context helps reasoning.

**Specialized reasoning:**
More dramatic improvements; context optimization addresses domain nuances.

**Real-world applications:**
Improvements translate to practical performance gains.

## The Self-Improvement Cycle

### How Models Improve

**Mechanism:**
1. Model operates within context
2. Agent observes performance
3. Agent modifies context based on failures
4. Model operates within improved context
5. Performance increases
6. Cycle repeats

**Key insight:**
Model performance improves without the model being retrained.

### Continuous Adaptation

**Implication:**
Models can continuously adapt to new tasks or domain shifts without retraining.

**Application:**
- Shift to new domain: refine context
- New task variant: evolve examples
- Performance degradation: diagnose and fix through context

## Advantages Over Fine-Tuning

### 1. No Retraining Required

**Speed:**
Hours or days for context refinement vs. weeks for fine-tuning.

**Cost:**
Minimal computational cost; no GPU hours for training.

### 2. Transparent and Interpretable

**What changed:**
Can see exactly what prompts/examples evolved.

**Why it changed:**
Agent reasoning is visible.

**How to revert:**
Easy to rollback if change makes things worse.

### 3. Iterative and Flexible

**Pace:**
Can run many iterations quickly.

**Responsiveness:**
Can adapt rapidly to performance issues.

**Experimentation:**
Easy to test ideas.

### 4. Generalizable

**Across models:**
Same context works with different models.

**Across tasks:**
Framework applies to any task.

**Across domains:**
No domain-specific retraining.

## Challenges and Limitations

### Search Space

**Challenge:**
Many possible contexts; which to try?

**Approach:**
Agents use reasoning to guide search intelligently.

**Limitation:**
May miss optimal contexts.

### Convergence

**Challenge:**
How many iterations needed?

**Observation:**
Often 5-10 iterations show significant gains; returns diminish.

**Practical:**
Can stop when improvements plateau.

### Generalization

**Challenge:**
Contexts optimized for benchmark; do they generalize?

**Finding:**
Generally good generalization; domain-specific contexts work well.

**Consideration:**
Validate on held-out test set.

## Practical Implications

### For Model Deployment

**Rather than:**
- Retrain on new data
- Fine-tune for task variant
- Build new model version

**Do this:**
- Use agentic context engineering
- Iterate prompts and examples
- Deploy improved context

**Benefit:**
Much faster adaptation cycle.

### For Research

**Enables:**
- Better understanding of what helps models
- Systematic exploration of prompt space
- Reproducible context improvements

### For Production Systems

**Advantage:**
- Quick response to performance issues
- A/B test different contexts
- Continuous improvement without downtime

## Real-World Use Cases

### Case 1: Application World Tasks

**Challenge:**
Models need to navigate application interfaces and perform tasks.

**Solution:**
Agentic context engineering optimizes prompts for navigation and action execution.

**Result:**
Performance improvements through better context.

### Case 2: Legal Reasoning

**Challenge:**
Legal reasoning requires specialized knowledge and careful reasoning.

**Solution:**
Agents evolve contexts with legal-specific examples and constraints.

**Result:**
Dramatic improvements in legal task performance.

## Key Takeaways

1. **Context engineering is learnable** — Agents can autonomously improve prompts/examples
2. **No fine-tuning required** — Improvements without model retraining
3. **Iterative process works** — Multiple rounds converge to better performance
4. **Feedback loops drive improvement** — Agent reasoning guides refinement
5. **Self-improvement is achievable** — Models improve through context evolution
6. **Prompt evolution is systematic** — Agents rationally modify prompts
7. **Example improvement matters** — Better examples drive performance gains
8. **Generalization is strong** — Improved contexts generalize to test sets
9. **Speed advantage significant** — Context refinement much faster than fine-tuning
10. **Transparency is benefit** — Can see what changed and why
11. **Flexibility high** — Easy to adapt contexts for new tasks/domains
12. **Convergence reasonable** — Usually 5-10 iterations sufficient
13. **Applicable broadly** — Works across task types and domains
14. **Cost effective** — Minimal computational cost compared to fine-tuning
15. **Easy to experiment** — Quick iterations enable hypothesis testing
16. **Rollback simple** — Can revert bad changes instantly
17. **Production ready** — Can deploy improved contexts immediately
18. **Continuous improvement** — Can keep refining indefinitely
19. **Model agnostic** — Same context works across models
20. **Domain adaptable** — Framework works for any domain

## The Bottom Line

Zhang et al.'s agentic context engineering presents a paradigm shift in how we think about model improvement.

**The key insight:**
Model performance isn't determined solely by weights. The context within which a model operates—prompts, examples, constraints—profoundly shapes what it can do.

**The innovation:**
Rather than fine-tuning weights through expensive retraining, use agents to autonomously evolve the context that guides the model.

**The mechanism:**
Iterative feedback loops where agents observe failures, propose context improvements, evaluate results, and iterate toward better performance.

**The implications:**
- Models improve without retraining
- Adaptation cycles compress from weeks to days/hours
- Transparency into why improvements happen
- Easy experimentation and rollback
- Continuous improvement without deployment downtime

**For practitioners:**
When model performance on a task is suboptimal, before considering fine-tuning:
1. Try agentic context engineering
2. Let agents improve prompts and examples
3. Evaluate results on test set
4. Iterate as needed
5. Deploy improved context

**For research:**
This framework enables systematic study of what makes prompts work, how examples influence reasoning, and how to optimize context for specific tasks.

**The broader vision:**
Models that continuously improve themselves by evolving the contexts they operate within—self-improving systems without weight modification.

This represents a practical, efficient path toward increasingly capable AI systems.

