---
summary: Research showing code architecture significantly impacts AI coding tool effectiveness—centralized architectures see 4x productivity gains vs 2x for distributed systems
event_type: article
sources:
  - https://jellyfish.co/blog/ai-coding-tools-not-paying-off-your-code-architecture-might-be-to-blame/
tags:
  - ai-coding-tools
  - code-architecture
  - productivity
  - monorepo
  - microservices
  - developer-tools
  - context-window
  - code-organization
---

# AI Coding Tools and Code Architecture

## Key Finding

Jellyfish's analysis of 3.8 million pull requests across 321 companies reveals that **code architecture is the critical—but overlooked—factor** determining whether AI coding tools deliver ROI. The relationship is stark:

- **Centralized architectures** (monorepos, monolithic services): ~4x improvement in PR throughput with AI
- **Distributed architectures** (microservices): ~2x improvement in PR throughput with AI
- **Highly distributed architectures**: Slight negative correlation between AI adoption and throughput

## The Architecture-Context Problem

AI coding tools perform better when they can easily access relevant code context. This is the crux:

- **Centralized systems** naturally provide broad context—all code is readily available
- **Distributed systems** force AI tools to search across many repositories, degrading context quality and tool effectiveness
- **Highly distributed systems** may actually slow teams due to the complexity of cross-repository coordination

## Implications

1. **Organizations should evaluate repository strategy before scaling AI investments**—don't just roll out tools blindly
2. **Consolidation might be worth reconsidering** even if not popular—the ROI on AI tooling could justify architectural changes
3. **Future AI agents** capable of intelligent cross-repository coordination could unlock distributed architectures
4. **Context window limitations** are a real constraint for distributed teams

## Relevance to Our Project

This research suggests that our codebase organization directly impacts our ability to leverage AI tools effectively. Monorepo structures with clear module boundaries will likely outperform highly fragmented microservices in terms of AI tool productivity.
