---
summary: Daniel Han (Unsloth) delivers comprehensive workshop on RL breakthroughs—covering reward functions, PPO/GRPO algorithms, why RL is scaling, LLM plateaus, agent construction, quantization techniques, and practical implementation
event_type: video
sources:
    - https://www.youtube.com/watch?v=OkEGJ5G3foU
tags:
    - reinforcement-learning
    - RL
    - LLM
    - agents
    - PPO
    - GRPO
    - reward-modeling
    - quantization
    - model-training
    - Unsloth
---

# Reinforcement Learning, Kernels, Reasoning, Quantization & Agents

**Speaker:** Daniel Han (Founder, Unsloth)
**Conference:** AI Engineer World's Fair
**Location:** San Francisco
**Platform:** YouTube (AI Engineer)
**Duration:** ~2 hours 45 minutes
**Publication Date:** December 20, 2025

## Overview

Daniel Han delivers a comprehensive workshop covering why reinforcement learning has suddenly become central to AI advancement, whether LLMs have plateaued without it, how RL enables agents, reward function design, the PPO and GRPO algorithms, quantization techniques for efficiency, and practical implementation using Unsloth. The talk bridges theory and practice, addressing fundamental questions about where LLMs are headed.

## The Central Question

### Has LLM Progress Plateaued?

**The question:**
Have large language models hit a plateau in terms of intelligence and capabilities without reinforcement learning?

**Traditional view:**
- Scale + data = capability
- More parameters, more data, more training = better models
- Diminishing returns at current scale

**Evidence for RL breakthrough:**
- Models like DeepSeek-R1 showing qualitative improvements
- Better reasoning with RL
- Multi-step problem-solving emerging
- Agent capabilities expanding

**Han's framework:**
RL isn't just an increment—it's a different way of training LLMs that unlocks capabilities scaling alone can't achieve.

## The LLM Training Stages

### Yann LeCun's Cake Analogy

**Three layers of AI capability:**

#### 1. Cake Foundation: Supervised Learning
- Learning from labeled data
- Tokenization, next-token prediction
- "Reading and memorizing"
- Foundation for everything

**Stage in LLMs:**
- Pretraining on vast text
- Learning language patterns
- Building base knowledge
- ~99% of training effort today

**Limitations:**
- Can't reason through novel problems
- Follows patterns from training
- Limited multi-step capability
- Plateau in pure prediction

#### 2. Frosting: Unsupervised Learning
- Learning structure without labels
- Finding patterns
- Building representations
- Self-supervised learning

**Stage in LLMs:**
- Implicit in pretraining
- Learning relationships
- Building semantic understanding

#### 3. Cherry on Top: Reinforcement Learning
- Learning from reward signals
- Optimizing for outcomes
- Problem-solving and reasoning
- Adapting to new domains

**Why it matters:**
- Unlocks reasoning capability
- Enables goal-directed behavior
- Allows agents to learn from experience
- Breaks through prediction plateau

### The Current State

**Reality in 2025:**
- Most training effort on supervised learning (foundation cake)
- Some unsupervised (implicit in pretraining)
- Very little reinforcement learning (yet)

**Opportunity:**
- RL is barely tapped
- Massive scaling potential
- Qualitative improvements possible
- This is where breakthroughs will happen

## Agents and Reinforcement Learning

### Why RL Enables Agents

**Traditional LLM:**
- Responds to prompts
- Generates text
- No feedback loop
- No goal optimization
- No learning from experience

**Agent with RL:**
- Takes actions in environment
- Receives rewards/feedback
- Learns from outcomes
- Optimizes for goals
- Improves through experience

**Key difference:**
RL provides signal (reward) for what's good vs. bad, enabling learning.

### Reward Functions: The Critical Component

**What it is:**
Signal telling agent whether behavior is good or bad.

**Examples:**
```
Coding agent:
- Test passes: +1 reward
- Test fails: -1 reward
- Code is readable: +0.5 reward

Customer support agent:
- Customer satisfied: +1 reward
- Problem resolved: +1 reward
- Time wasted: -0.1 reward per minute
```

**Challenges:**
- Defining good reward is hard
- Reward hacking (optimizing reward not goal)
- Sparse rewards (not enough feedback)
- Misaligned incentives

**Han's insight:**
Good reward functions are as important as good algorithms. Bad rewards ruin everything.

### Reward Model vs. Reward Function

**Reward Function:**
- Hand-coded rule
- "If X then +1 reward"
- Deterministic
- Simple but inflexible

**Reward Model:**
- Learned from data
- LLM learns what's good
- Flexible and contextual
- Complex but powerful

**In practice:**
- Simple tasks: reward functions
- Complex tasks: reward models
- Hybrid approaches: both

## The Algorithms: PPO and GRPO

### PPO (Proximal Policy Optimization)

**What it is:**
Standard RL algorithm for training agents.

**How it works:**
1. Agent takes action
2. Receives reward
3. Updates policy (behavior)
4. Repeats
5. Learns to maximize reward

**Key innovation:**
- Trust region: don't change too much per update
- Prevents catastrophic forgetting
- Stable training

**Why it matters:**
- Enabled practical RL at scale
- Became industry standard
- Trainable with reasonable compute

**In LLMs:**
- Train model to optimize rewards
- Change behavior based on feedback
- Improve reasoning or alignment

### GRPO (Group Relative Policy Optimization)

**What it is:**
Newer algorithm improving on PPO.

**Key improvement:**
- Group rewards together
- Compare relative performance
- More stable training
- Better convergence

**Advantage:**
- Simpler than PPO
- Better performance reported
- Less compute needed
- Used in DeepSeek-R1

**In practice:**
- PPO still common
- GRPO gaining adoption
- Both fundamentally similar
- GRPO likely future standard

### The Math Behind Training

**Reinforce Algorithm:**
- Basic policy gradient
- Update policy to increase reward
- Simple but high variance
- Foundation for PPO

**PPO Improvements:**
- Clip gradients (trust region)
- Multiple epochs
- Reduce variance
- More stable training

**GRPO Improvements:**
- Group comparisons
- Reduce computation
- Better scaling
- Simpler implementation

## Why RL Is Scaling Now

### Three Convergences

**1. Models are capable enough**
- LLMs can understand complex tasks
- Can learn from feedback
- Can follow subtle signals
- Previous models couldn't

**2. Reward signals are clearer**
- Testing works for code
- Evaluation models work for reasoning
- Human feedback scalable
- Clear metrics possible

**3. Compute is available**
- Training infrastructure mature
- Methods optimized
- Tools like Unsloth make it accessible
- Not research-only anymore

### The Breakthrough

**RL isn't new:**
- Decades of research
- Proven in games, robotics
- Standard in industry

**What's new:**
- LLMs + RL combination
- Scale of training
- Accessibility of tools
- Quality of reasoning emerging

**Result:**
- Models like DeepSeek-R1 showing qualitative jumps
- Reasoning capability improving
- Multi-step problem-solving working
- Agents becoming practical

## Quantization: Efficiency Without Loss

### The Challenge

**Current state:**
- Models getting bigger
- Training expensive
- Inference expensive
- GPU limits throughput

**Solution:**
- Quantization (reduce precision)
- 8-bit, 4-bit, or even 1-bit models
- Maintain performance
- Massive efficiency gains

### Techniques

**Standard quantization:**
- Reduce floating-point precision
- 32-bit → 8-bit = 4x compression
- Some accuracy loss
- Good tradeoff often

**Advanced quantization:**
- 4-bit or lower
- Specialized algorithms
- Maintain quality
- Extreme compression

**Extreme quantization:**
- DeepSeek-R1 at 1.58-bits
- Still performs well
- Radical efficiency
- New frontier

### Practical Impact

**What it enables:**
- Run models on consumer GPU
- Inference on edge devices
- Lower compute costs
- Faster inference
- Broader accessibility

**Trade-off:**
- Slightly reduced quality
- But acceptable for many tasks
- Worth it for efficiency
- Enables deployment

## Kernels: Still Worth Your Time?

### The Question

**Kernel methods:**
- Classical ML technique
- Rich feature spaces
- Theoretically grounded
- Pre-deep learning standard

**With LLMs:**
- Neural networks dominant
- Kernel methods less common
- Still useful in niches
- Different strengths

### Han's Take

**When kernels matter:**
- Small datasets
- Interpretability needed
- Safety-critical applications
- Mathematical guarantees needed

**When deep learning wins:**
- Large datasets
- End-to-end learning
- Complex patterns
- Practical applications

**Reality:**
- Kernels not dead
- Just less central
- Hybrid approaches work
- Use right tool for job

## Practical Implementation

### Unsloth Contributions

**What Unsloth provides:**
- RL training made accessible
- Code optimizations
- Community tools
- Simplified APIs

**Key innovations:**
- 2x faster training
- Lower memory usage
- Easier implementation
- Works with standard libraries

**Impact:**
- Enables broader adoption
- Makes RL practical
- Reduces barriers to entry
- Democratizes access

### Implementation Patterns

**For coding agents:**
- Define test cases as rewards
- Train on code generation
- Iterate on performance
- Deploy with tests

**For reasoning tasks:**
- Specify success criteria
- Train on multi-step problems
- Reward correct solutions
- Learn to reason

## The Future Vision

### Where This Is Heading

**Short term (6-12 months):**
- More RL in model training
- Better reasoning from RL
- Agent systems maturing
- Quantization improving

**Medium term (1-3 years):**
- RL standard in training pipeline
- Specialized agents common
- Edge deployment widespread
- Open-source accessibility

**Long term (3+ years):**
- RL enables continuous learning
- Models adapt post-deployment
- Agents solve complex problems
- Specialized systems proliferate

### Key Insights

1. **RL is the breakthrough** — Not bigger models, but better training
2. **Reasoning emerges** — RL enables multi-step problem-solving
3. **Agents become practical** — With RL, agents actually work
4. **Quantization enables access** — Efficiency democratizes deployment
5. **This is early** — RL in LLMs barely started
6. **Scale matters** — RL compounds benefits of scale
7. **Reward design is critical** — Good rewards are everything
8. **Computation improving** — Making RL accessible
9. **Open source essential** — Democratizing these advances
10. **Integration happening** — RL becoming standard practice

## Key Takeaways

1. **RL suddenly everywhere** — Convergence of model capability, signal clarity, and compute
2. **LLMs not plateau yet** — But RL is how they progress further
3. **Yann's cake analogy useful** — Supervised (foundation) + Unsupervised (implicit) + RL (breakthrough)
4. **Reward functions critical** — Well-designed rewards are essential
5. **PPO still standard** — GRPO improving but both core
6. **Algorithms well-understood** — Execution is bottleneck, not theory
7. **Quantization works** — 1-bit models maintaining quality
8. **Agents enabled by RL** — Cannot work without it
9. **Kernels have niches** — Not dead, just less central
10. **This is early innings** — Massive opportunity ahead

## The Bottom Line

Daniel Han's workshop reveals why reinforcement learning has suddenly become central to AI advancement. It's not that RL is new—it's that three factors converged: (1) LLMs are capable enough to learn from reward signals, (2) reward signals can be made clear and scalable, (3) compute and tools have improved enough to make RL practical.

The implications are profound. LLMs may not have hit a plateau, but scaling raw parameters shows diminishing returns. RL provides a different dimension of improvement—teaching models to reason through problems, optimize for goals, and learn from feedback. Models like DeepSeek-R1 demonstrate the breakthrough in reasoning capability from RL.

Agents become possible with RL because they need to optimize for outcomes in an environment. Traditional LLM prompting lacks that optimization signal. Agents need reward functions defining what success looks like, RL algorithms to learn those objectives, and infrastructure to execute actions based on learned policies.

Quantization techniques enable practical deployment—reducing model size dramatically while maintaining quality. Combined with RL improvements, efficiency gains, and open-source tools like Unsloth, these advances are becoming accessible to broader practitioners.

The workshop positions RL not as incremental improvement but as fundamental shift in how LLMs train and operate. The future is models that learn from reward signals, agents that optimize for outcomes, and systems that continuously improve through RL. This is the frontier of AI progress, and early adoption of these techniques will compound over time.
