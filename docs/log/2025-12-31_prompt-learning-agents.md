---
summary: Aparna Dhinakaran presents a system-prompt learning loop that uses RL techniques to automatically tune agent.md files based on PR feedback and evaluations, improving Claude Code and Cline behavior
event_type: video
sources:
  - https://www.youtube.com/watch?v=pP_dSNz_EdQ
tags:
  - prompt-engineering
  - agents
  - reinforcement-learning
  - system-prompts
  - claude-code
  - cline
  - agent-tuning
  - feedback-loops
  - pr-feedback
---

# System Prompt Learning for Agents

**Speaker**: Aparna Dhinakaran, Co-founder & CPO at Arize
**Duration**: 11 minutes
**Conference**: AI Engineer (2025-12-23)

## Core Problem

Coding agents write code differently than development teams expect. Traditional approaches rely on:
- Hand-edited system prompts
- Brittle style guides (e.g., `agent.md`)
- Manual tuning that doesn't scale

These static approaches can't adapt to team preferences or evolving requirements.

## Solution: System-Prompt Learning Loop

Aparna presents a reinforcement learning technique applied to **prompts, not model weights**. The system:

1. **Captures runtime signals** from agent interactions
2. **Learns from PR feedback** and code reviews
3. **Auto-tunes system prompts** based on team preferences
4. **Updates agent.md continuously** as feedback arrives

### Key Insight

Instead of trying to build perfect initial prompts or retraining models, treat the system prompt itself as a learnable artifact. Teams' feedback on PRs becomes training data for improving agent behavior.

## Practical Benefits

- **Scalable**: Works across enterprises without model retraining
- **Transparent**: Changes to prompts are visible and auditable
- **Adaptive**: Agent behavior improves as team context accumulates
- **Generalizable**: Applicable to any agent type (Claude Code, Cline, custom agents)

## Implementation Recipe

The talk provides a concrete recipe for:
1. Collecting runtime signals from agent execution
2. Extracting feedback from PR reviews and evaluations
3. Using RL-style techniques to update prompts
4. Measuring improvement over time

## Related Concepts
- Agent customization
- Prompt optimization
- Feedback-driven learning
- Enterprise AI adoption
- Agent.md file patterns
