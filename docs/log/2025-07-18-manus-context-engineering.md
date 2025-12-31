---
summary: Manus shares six production context engineering techniques—KV-cache optimization (10x cost difference), action space masking via token logits, file system as unlimited memory, todo.md for attention manipulation, preserving error evidence, and variation to prevent few-shot degradation
event_type: article
sources:
    - https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus
tags:
    - context-engineering
    - AI-agents
    - production-systems
    - KV-cache
    - Manus
    - in-context-learning
    - prompt-engineering
---

# Context Engineering for AI Agents: Lessons from Building Manus

**Author:** Yichao 'Peak' Ji
**Publication:** Manus Blog
**Publication Date:** July 18, 2025

## Overview

The Manus team shares lessons learned from building production AI agents, focusing on context engineering—the discipline of shaping what information enters the model's context window and how it's structured.

## The Core Decision

### In-Context Learning vs End-to-End Training

**Manus chose in-context learning with frontier models.**

Why:
- Ship improvements within hours, not weeks
- Product independent from model architecture
- Leverage frontier model capabilities directly
- Iterate rapidly on agent behavior

Trade-off: More emphasis on context engineering as the primary lever for agent quality.

## Six Key Techniques

### 1. KV-Cache Optimization

**The most critical metric for production agents: KV-cache hit rate.**

**Cost difference (Claude Sonnet):**
- Cached tokens: $0.30/MTok
- Uncached tokens: $3.00/MTok
- **10x cost difference**

**Best practices:**
- Maintain stable prompt prefixes
- Implement append-only contexts
- Explicitly mark cache breakpoints
- Avoid prefix modifications mid-conversation

**Why it matters:** At production scale, cache efficiency dominates cost structure.

### 2. Action Space Masking

**Problem:** Dynamically removing tools breaks cache and complicates logic.

**Solution:** Mask token logits during decoding to constrain available actions.

**Implementation:**
- Name tools with consistent prefixes (`browser_`, `shell_`, etc.)
- Enforce selection constraints at decoding level
- Keep tool definitions stable
- Preserve cache while constraining choices

**Result:** Dynamic action constraints without prompt modification.

### 3. File System as Extended Context

**Problem:** Even 200k token windows aren't enough for complex tasks.

**Solution:** Treat file system as externalized memory.

**Characteristics:**
- Unlimited size
- Persistent by nature
- Agent reads/writes on demand
- Actual context stays manageable

**Pattern:**
```
Agent → writes intermediate results to files
Agent → reads from files when needed
Context → contains only active working set
```

### 4. Attention Manipulation Through Recitation

**Problem:** "Lost-in-the-middle" degradation across extended task sequences.

**Context:** Complex tasks require ~50 tool calls on average.

**Solution:** Create and update `todo.md` files.

**How it works:**
- Agent maintains objectives in todo.md
- Regular updates keep goals in recent context
- Recent attention span holds current objectives
- Combats attention decay over long sequences

**Key insight:** What's recent in context gets more attention weight.

### 5. Preserving Error Evidence

**Counter-intuitive approach:** Don't hide failures.

**Traditional approach:**
- Remove failed attempts
- Show only successful paths
- Clean up error messages

**Manus approach:**
- Retain failed actions in context
- Keep error observations visible
- Enable implicit belief updating
- Model learns from mistakes in-context

**Result:** Model shifts priors away from similar mistakes without explicit training.

### 6. Preventing Few-Shot Degradation

**Problem:** Models fall into repetitive patterns with similar sequential tasks.

**Solution:** Controlled variation in:
- Serialization formats
- Phrasing of similar content
- Formatting choices
- Structural presentation

**Why:** Variation breaks pattern lock-in, maintains model flexibility.

## Architecture Philosophy

### "Stochastic Graduate Descent"

Context engineering remains experimental:
- No established best practices
- Requires iterative framework redesigns
- Models and techniques evolve together
- What works today may need revision

### The Core Principle

**How context is shaped determines:**
- Agent performance
- Recovery capability
- Scalability
- Cost efficiency

## Practical Implications

### For Production Agents

| Aspect | Recommendation |
|--------|----------------|
| Cost | Optimize KV-cache hit rate first |
| Constraints | Use logit masking, not prompt modification |
| Memory | Externalize to file system |
| Attention | Use recitation for objective persistence |
| Errors | Preserve, don't hide |
| Variation | Prevent few-shot degradation |

### Cost Breakdown Impact

With 10x cost difference between cached and uncached tokens:
- 90% cache hit rate → $0.57/MTok effective cost
- 50% cache hit rate → $1.65/MTok effective cost
- 0% cache hit rate → $3.00/MTok effective cost

Cache optimization can cut costs by 80%+.

### Memory Architecture

```
┌─────────────────────────────────────┐
│         Actual Context              │
│  - System prompt (cached)           │
│  - Recent observations              │
│  - Current task state               │
│  - todo.md contents                 │
└─────────────────────────────────────┘
              ↕
┌─────────────────────────────────────┐
│      File System (Extended)         │
│  - Historical results               │
│  - Intermediate artifacts           │
│  - Reference documents              │
│  - Overflow memory                  │
└─────────────────────────────────────┘
```

## Key Takeaways

1. **KV-cache is critical** — 10x cost difference, optimize first
2. **Logit masking** — constrain actions without breaking cache
3. **File system = memory** — unlimited, persistent external storage
4. **Recitation beats decay** — keep objectives in recent attention
5. **Preserve errors** — enables implicit belief updating
6. **Vary presentation** — prevents few-shot pattern lock-in
7. **Context shapes everything** — performance, recovery, scalability
8. **Iterate constantly** — "Stochastic Graduate Descent"

## The Bottom Line

Context engineering is the primary lever for production agent quality when using in-context learning with frontier models. Manus's six techniques address the practical challenges: cost (KV-cache), constraints (logit masking), memory limits (file system), attention decay (recitation), error recovery (evidence preservation), and pattern rigidity (variation). The 10x cost difference from cache optimization alone justifies treating context engineering as a core discipline, not an afterthought. The approach remains experimental—"Stochastic Graduate Descent"—but these patterns represent hard-won production lessons.
