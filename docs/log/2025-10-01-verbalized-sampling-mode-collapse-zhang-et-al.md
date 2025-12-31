---
summary: Zhang et al. identify typicality bias as root cause of mode collapse in aligned LLMs and propose Verbalized Sampling—training-free prompting technique that generates probability distributions over responses, restoring diversity without sacrificing quality
event_type: research_paper
sources:
    - https://arxiv.org/html/2510.01171v1
tags:
    - mode-collapse
    - diversity
    - prompt-engineering
    - LLM-alignment
    - preference-learning
    - typicality-bias
    - training-free-methods
    - creative-generation
---

# Verbalized Sampling: How to Mitigate Mode Collapse and Unlock LLM Diversity

**Authors:** Jiayi Zhang, Simon Yu, Derek Chong, Anthony Sicilia, Michael R. Tomz, Christopher D. Manning, Weiyan Shi

**Affiliations:** Northeastern University, Stanford University, West Virginia University
**Publication Date:** October 1, 2025
**Type:** Research Paper
**Venue:** arXiv

## Overview

Zhang et al. identify a fundamental problem with aligned language models: typicality bias in preference data causes mode collapse, where models produce repetitive, homogeneous outputs. They propose Verbalized Sampling (VS), a training-free prompting technique that asks models to generate probability distributions over responses rather than single outputs.

The key innovation: by shifting from instance-level to distribution-level prompting, models recover substantial inherent diversity without sacrificing quality or safety.

## The Problem: Mode Collapse in Aligned Models

### What Is Mode Collapse?

**Definition:**
Aligned language models produce repetitive, homogeneous responses lacking diversity.

**Manifestation:**
- Boring outputs
- Lack of creativity
- Similar responses across different prompts
- Loss of personality/variation

### Why It Happens: Typicality Bias

**Root cause:**
Human annotators in preference learning have typicality bias—they favor familiar, typical text over novel text.

**The mechanism:**

```
Training data:
- Human annotators prefer outputs that look "normal"
- Unusual/creative outputs penalized even if good
- Model learns to optimize for "typical-looking" outputs

Result:
- Model collapses to mode (most typical responses)
- Diversity is actively suppressed
- Creativity is lost in favor of familiarity
```

### The Data-Level Problem

**Finding:**
Preference bias is measurable and quantifiable.

**Empirical evidence:**
- HelpSteer dataset analysis showed bias weights (α) of 0.57-0.65
- Consistent across preference datasets
- Not an artifact of specific dataset

**Implication:**
The problem is fundamental to how preference data is created, not how models learn.

## The Theoretical Framework

### Formalizing Typicality Bias

**Mathematical model:**

```
Reward function:
r(x,y) = r_true(x,y) + α log π_ref(y|x)

Where:
- r_true: true utility of response
- π_ref: reference model probability (how "typical" it is)
- α: strength of typicality bias (0.57-0.65 empirically)

Effect:
- Responses favored if they're both good AND typical
- Responses penalized if creative but unusual
- Creates pressure toward mode
```

### The Alignment Optimization Effect

**During alignment training:**

```
Optimization sharpens distribution by factor γ:
γ = 1 + α/β

Where β is temperature parameter

Result:
- Distribution becomes concentrated
- Tail probabilities collapse
- Diversity is suppressed
- Mode becomes dominant
```

**Numerical example:**
```
α = 0.6 (typicality bias)
β = 0.5 (temperature)
γ = 1 + 0.6/0.5 = 2.2

Distribution sharpened by 2.2×
→ Diversity collapses
```

### Why Traditional Approaches Fail

**Fine-tuning approach (traditional):**
- Retrain model with different data
- Expensive computationally
- Requires high-quality diverse data
- Doesn't address underlying bias

**Temperature scaling (naive):**
- Just turns up temperature
- Produces incoherent outputs
- Doesn't recover the constrained diversity
- Sacrifices quality

**Prompting for diversity (naive):**
- "Be creative!" → Still constrained by training
- "Give varied outputs" → Doesn't help
- Models struggle with instruction alone

## Verbalized Sampling: The Solution

### The Core Idea

**Shift perspective:**
Instead of asking for single "best" response, ask model to generate distribution.

**Prompt format:**

```
Original prompt: "Write a poem about nature"
Single output approach: "Generate the best poem"

Verbalized Sampling:
"Generate 5 poems about nature with their probabilities"

Model generates:
- Poem 1 (probability: 0.3)
- Poem 2 (probability: 0.25)
- Poem 3 (probability: 0.2)
- Poem 4 (probability: 0.15)
- Poem 5 (probability: 0.1)
```

### Why This Works

**Mechanism:**
By asking for distribution, model:
1. Accesses responses across range of probabilities
2. Includes high-probability (good) responses
3. Also includes lower-probability (diverse) responses
4. Weights by probability (maintains quality preference)

**Result:**
Recovers diversity from model's underlying distribution without degrading quality.

### VS Implementation Variants

**VS-Standard:**
- Basic: "Generate k responses with probabilities"
- Straightforward
- Works in most cases

**VS-CoT (Chain-of-Thought):**
- "Reason about different approaches, then generate k responses"
- Improves quality of diverse responses
- Helps model think through variations
- Better for complex tasks

**VS-Multi (Multiple Rounds):**
- Multiple turns of distribution generation
- Iteratively explores space
- Can discover unusual combinations
- More thorough exploration

## Empirical Results

### Creative Writing Performance

**Test tasks:**
- Poems
- Stories
- Jokes

**Diversity improvements:**
- Poems: 1.6× diversity increase
- Stories: 1.7× diversity increase
- Jokes: 2.1× diversity increase

**Human evaluation:**
- 25.7% improvement in diversity ratings
- Recovered 66.8% of base model diversity
- Compared to 23.8% for direct prompting

**Quality maintained:**
- Coherence preserved
- Creativity improved
- Appropriateness maintained

### Dialogue Simulation

**Test:**
Simulating donation distribution decisions in dialogue.

**Result:**
Model with VS generated distributions matching human behavior more closely than baseline.

**Implication:**
Not just diversity for sake of it, but meaningful variation in behavior.

### Open-Ended Question Answering

**Test:**
Multiple valid answers to open-ended questions.

**Result:**
- Achieved KL divergence of 0.12 from pretraining distribution
- Better coverage of answer space
- Maintained factual accuracy

### Synthetic Data Generation

**Application:**
Generating diverse math problem solutions.

**Results:**
- Baseline accuracy: 32.8%
- With VS: 37.5%
- Diversity enabled finding better solutions

## Scaling Properties

### The Surprising Scaling Trend

**Finding:**
Larger models show GREATER benefits from VS.

**Data:**
- GPT-4 benefits: 1.5-2× compared to
- GPT-4-Mini benefits
- Trend continues to larger models

**Implication:**
Bigger models have MORE constrained diversity distribution (stronger mode collapse), so VS benefit is bigger.

**Practical significance:**
VS becomes more valuable as models scale.

## Safety and Quality Preservation

### Quality Metrics

**Testing:**
- Factual accuracy (commonsense reasoning)
- Coherence (writing quality)
- Safety (harmful content detection)

**Results:**
- No degradation in factual accuracy
- Writing quality maintained
- Safety evaluations show no problems
- Quality-diversity tradeoff resolved

### Why Quality Is Preserved

**Mechanism:**
- Model still generates probabilities
- Higher-probability responses favored
- Lower-probability responses diverse but sampled with lower weight
- Quality and diversity balanced

## Practical Implications

### For Creative Applications

**Applications:**
- Creative writing assistance
- Brainstorming tools
- Content generation
- Design exploration

**Benefit:**
Users get diverse, creative options without sacrificing quality.

### For Social Simulation

**Applications:**
- Simulating diverse behaviors
- Modeling populations
- Testing against varied scenarios
- Behavioral modeling

**Benefit:**
More realistic diversity in simulated behaviors.

### For Synthetic Data Generation

**Applications:**
- Generating training data
- Creating diverse examples
- Data augmentation
- Exploring solution spaces

**Benefit:**
Higher-quality, more diverse synthetic data.

## Training-Free Nature: A Key Advantage

### Why This Matters

**Traditional approach:**
Retraining required → weeks of compute, data curation, validation.

**VS approach:**
Prompting change → immediate, no retraining needed.

### Deployment Advantages

- Works with any existing model
- No fine-tuning infrastructure needed
- Can be enabled/disabled with prompting
- Easy A/B testing
- Fast iteration

### Accessibility

- Works with API-accessed models
- No model weight access needed
- Can be applied to any LLM
- No specialized hardware

## The Deeper Insight

### Mode Collapse Is Data, Not Algorithm

**Previous belief:**
"Aligned models inherently produce homogeneous outputs; it's unavoidable."

**This research shows:**
Mode collapse comes from typicality bias in preference data, not fundamental algorithmic limitation.

**Implication:**
The diversity exists in the model; it's just suppressed by training signal.

### Models Retain Underlying Diversity

**Finding:**
By accessing the model's probability distribution, we can recover substantial diversity.

**Meaning:**
Models know how to be diverse; alignment training just teaches them not to be.

## Key Takeaways

1. **Mode collapse is real problem** — Aligned models produce repetitive outputs
2. **Root cause is typicality bias** — Preference data favors typical/familiar text
3. **Bias is quantifiable** — Weights (α) measured at 0.57-0.65 across datasets
4. **Problem is data-level** — Not algorithmic; comes from how preferences collected
5. **Verbalized Sampling is solution** — Ask for distributions, not single outputs
6. **VS is training-free** — Just change prompting; no retraining required
7. **Diversity improvements substantial** — 1.6-2.1× for creative writing
8. **Quality preserved** — No sacrifice of accuracy or safety
9. **Scales to larger models** — Benefits increase with model size
10. **Works across domains** — Creative writing, dialogue, QA, synthetic data
11. **Human evaluation validates** — 25.7% improvement in diversity ratings
12. **Multiple variants available** — Standard, CoT, Multi approaches
13. **Can sample from distribution** — Weight responses by probability
14. **Immediately deployable** — Works with existing models
15. **No specialized training needed** — Anyone can use it
16. **Models retain diversity** — Suppressed by training, not absent
17. **Theoretical framework solid** — Mathematical modeling of typicality bias
18. **Empirical validation comprehensive** — Tested across multiple models and tasks
19. **Scaling trend positive** — Benefits grow with model capability
20. **Broader implications significant** — Suggests need to rethink preference data collection

## The Bottom Line

Zhang et al.'s identification of typicality bias as the root cause of mode collapse—and the proposed Verbalized Sampling solution—represents an important insight into aligned language model behavior.

**The key finding:**
Mode collapse isn't an algorithmic inevitability. It stems from typicality bias in preference data. Models actually retain substantial diversity; alignment training just teaches them to suppress it.

**The practical solution:**
By asking models to generate probability distributions rather than single outputs, we can recover diversity while maintaining quality. No retraining needed; just change the prompting.

**The implications:**

1. **For practitioners:** Use VS for applications requiring diversity
2. **For researchers:** Typicality bias in preference data is fundamental challenge
3. **For training:** Preference data collection needs rethinking to reduce typicality bias
4. **For deployment:** Can immediately improve diversity of existing models

**The broader insight:**
This research suggests that many properties of aligned models come from training signals, not fundamental model limitations. By understanding and modifying those signals, we can unlock different behaviors.

**For the field:**
As we continue aligning models for safety and reliability, this research reminds us to be intentional about what preferences we encode in training data. Typicality bias might be preserving safety in some cases, but it's also unnecessarily restricting diversity and creativity.

The solution—Verbalized Sampling—offers a practical, immediate way to recover diversity for applications where it matters, while maintaining quality and safety where it counts.

