---
summary: Steve Yegge presents six new tips for agentic coding beyond the Vibe Coding book, including treating software as throwaway, self-critique patterns, and preparing to manage 50-100 agents simultaneously
event_type: article
sources:
    - https://steve-yegge.medium.com/six-new-tips-for-better-coding-with-agents-d4e9c86e42a9
tags:
    - vibe-coding
    - agentic-coding
    - coding-agents
    - software-architecture
    - agent-management
    - Steve-Yegge
    - best-practices
---

# Six New Tips for Better Coding With Agents

**Author:** Steve Yegge
**Publication Date:** December 2025
**Publication:** Medium

## Overview

Steve Yegge shares new tips and strategies for agentic coding that extend beyond his published "Vibe Coding" book (released October 21, 2025, co-authored with Gene Kim). These insights emerged from continued exploration of agent-assisted development, including Yegge's work on tools like the Beads memory system and the Agent-Efrit bridge for Emacs.

## Core Mental Model

**Agents as junior developers:** Treat agents as "unreliable but extremely fast junior devs" who require oversight but deliver massive throughput.

**Future scale:** Engineers will soon manage 50-100 coding agents simultaneously, requiring new coordination and oversight skills.

## The Six Tips

### Tip 1: Software is Now Throwaway

**Expect less than 1 year shelf life for code.**

This represents a fundamental shift from Joel Spolsky's 26-year-old wisdom in "Things You Should Never Do, Part 1" which advised against rewriting software. Anthropic has already begun embracing this mindset internally.

**Implications:**
- Don't over-engineer for longevity
- Embrace rapid iteration and replacement
- Reduce attachment to existing code
- Plan for continuous regeneration

**Impact on SaaS vendors:** Many vendors who've found niches building business automation software face disruption as businesses automate their own processes through vibe coding.

### Tip 2: Self-Critique Pattern

**Request agents critique their own output before trusting it.**

Rather than accepting agent output immediately:
1. Generate initial solution
2. Ask agent to review and critique its work
3. Iterate based on self-identified issues
4. Run 5-6 rounds of improvement

**Why it works:** Agents often catch their own mistakes when explicitly asked to review, but don't spontaneously self-correct.

### Tip 3: Built-in Refactoring Capability

**Agents should have built-in refactoring tools, not just text replacement.**

Text-based code modification is brittle. Effective agent tooling includes:
- Structural refactoring operations
- AST-aware transformations
- Semantic code understanding
- Safe modification patterns

### Tip 4: Codebase Documentation

**Maintain consistent, agent-generated documentation for human comprehension.**

As agent-generated code volumes increase:
- Documentation becomes critical for human understanding
- Agents can generate documentation as they work
- Consistency enables future agents to understand context
- Human oversight requires clear documentation

### Tip 5: Code Quality and Stability

**Build oversight skills to keep codebases secure and high-quality.**

With increased agent output:
- Security review becomes critical
- Quality gates prevent accumulated debt
- Human oversight scales differently than generation
- Stability requires active management

### Tip 6: Agent Memory Systems

**Use persistent memory (like Beads) for agent context.**

Yegge developed Beads, a drop-in memory upgrade for coding agents, going from concept to 1,000+ GitHub stars in six days through vibe coding.

**Benefits:**
- Agents retain context across sessions
- Learning compounds over time
- Reduced re-explanation of codebase
- Better continuity in long projects

## Key Patterns for Success

### Iterative Improvement Rounds

Run 5-6 rounds of asking agents to improve code:
1. Generate initial solution
2. Request critique and improvement
3. Apply improvements
4. Request further critique
5. Iterate until quality threshold met
6. Final review

### Agent and Subagent Focus

Effective agent usage involves:
- Primary agents for orchestration
- Subagents for specialized tasks
- Clear task decomposition
- Coordination patterns

### 100x Super-Programmer Potential

To become a "100x super-engineer":
1. Start learning vibe coding basics now
2. Develop agent coordination skills
3. Build oversight and quality capabilities
4. Master iterative improvement workflows
5. Understand agent limitations and strengths

## Related Work

### Beads Memory System

Yegge introduced Beads after "vibe coding for forty days and nights." The system is designed for users of:
- Claude Code
- Sourcegraph Amp
- OpenAI Codex
- Similar coding agents

### Agent-Efrit Bridge

A tool for Emacs described as "a simple and elegant system" and "a tool made for agents, by agents."

### Vibe Coding Book

Published October 21, 2025 by Gene Kim and Steve Yegge. All advice from the book remains relevant, with these six tips representing additional discoveries.

## Implications

### For Individual Developers

- Embrace throwaway mindset for code
- Develop agent oversight skills
- Learn iterative improvement patterns
- Build agent coordination capabilities
- Prepare for 50-100 agent management

### For Organizations

- Reconsider long-term codebase strategies
- Invest in agent tooling and infrastructure
- Train teams on agent coordination
- Develop quality oversight processes
- Embrace rapid iteration cycles

### For the Industry

- SaaS automation vendors face disruption
- Business process automation democratizes
- Developer productivity multipliers increase
- New coordination skills become essential
- Code longevity expectations shift

## Key Takeaways

1. **Throwaway code is the new normal** — stop over-engineering for longevity
2. **Self-critique before trust** — agents catch their own mistakes when asked
3. **Iterative improvement** — 5-6 rounds of refinement yields quality
4. **Memory matters** — persistent context improves agent effectiveness
5. **Scale is coming** — prepare to manage 50-100 agents
6. **Quality oversight** — human review skills become critical differentiator

## The Bottom Line

Agent-assisted development is evolving rapidly. The Vibe Coding book provides foundations, but practitioners must continuously update their approaches. These six tips represent the current frontier of effective agent coordination—and that frontier moves fast.
