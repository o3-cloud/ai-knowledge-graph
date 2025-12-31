---
summary: LinkedIn engineers discuss why AI agents must be treated as platform infrastructure rather than point features, covering MCP, foreground/background agents, intent specification, and secure multi-agent orchestration
event_type: video
sources:
    - https://www.youtube.com/watch?v=Vkp8zQpwDSg
tags:
    - AI-agents
    - platform-engineering
    - MCP
    - infrastructure
    - multi-agent-systems
    - LinkedIn-architecture
    - security-compliance
---

# Why LinkedIn Treats AI Agents as Infrastructure (Not Features)

**Speakers:** Karthik Ramgopal & Prince Valluri (LinkedIn)
**Interviewer:** Wes Reisz (InfoQ)
**Platform:** InfoQ Podcast
**Upload Date:** December 10, 2025

## Overview

In this episode, LinkedIn engineers dismantle myths about AI adoption in software engineering. They reveal how LinkedIn moved beyond siloed proof-of-concepts and hermit developers to build a unified Platform Engineering approach for multi-agentic systems. The conversation emphasizes treating AI agents as infrastructure layer rather than isolated features.

## Core Argument: Infrastructure, Not Features

LinkedIn's thesis: **AI agents require dedicated platform infrastructure**, not ad hoc development by individual teams. This represents architectural shift from:
- Individual developers scripting automation → unified agent orchestration
- Hermit developer model → coordinated multi-agent system
- Feature-based adoption → infrastructure-as-code approaches

## Key Technical Topics

### Model Context Protocol (MCP)

MCP serves as critical infrastructure for agent capability discovery and standardized tool integration. Enables:
- Consistent interface for agents to access external services
- Interoperable tool definitions across heterogeneous systems
- Reduced implementation variance between teams
- Foundation for multi-agent coordination

### Foreground vs. Background Agents

LinkedIn distinguishes two agent execution models:

**Foreground Agents (IDE-based)**
- Interactive, synchronous reasoning within development environment
- Developer-driven, real-time feedback
- Suited for exploratory and iterative tasks
- Lower latency, immediate human interaction

**Background Agents (Asynchronous)**
- Execute on separate infrastructure/runtime
- Handle long-running, multi-step workflows
- Decoupled from developer session
- Enable parallel execution without blocking

This distinction shapes infrastructure design—foreground requires tight IDE integration while background needs robust scheduling, monitoring, and recovery.

### Intent Specification Through Specs

Shift from crafting prompts to **specifying intent via structured specifications**:
- Define what agents should accomplish, not how they should do it
- Specs serve as contract between human requirements and agent execution
- Enable verification and observability
- Future of software delivery moves toward declarative intent specification

Combined with **sandboxes**: Bounded execution environments where agents operate within defined constraints, access controls, and resource limits.

### Human-in-the-Loop Review Process

Even with sophisticated agents, human judgment remains critical. LinkedIn implements structured human review:
- Agents prepare work for human verification
- Humans serve as verifiers, not directors
- Review triggers based on confidence scores, change magnitude, security implications
- Feedback loops train implicit human requirements into system

## Platform Engineering Approach

LinkedIn's unified platform engineering strategy:

1. **Standardized Agent Framework:** Common infrastructure for agent lifecycle management, logging, monitoring
2. **Capability Abstraction:** Tools, services, and knowledge exposed through uniform interfaces (MCP)
3. **Security and Compliance:** Agents operate within enterprise security boundaries with audit trails
4. **Observability:** Full visibility into agent decision-making, context usage, and tool invocations
5. **Resource Governance:** Agents compete for resources fairly; costs tracked and attributed

## Technical Patterns

### Context Management with RAG and Historical Data

Agents require rich context:
- **RAG (Retrieval-Augmented Generation):** Dynamic context assembly from knowledge bases
- **Historical Data:** Agent decisions informed by organization's past patterns and domain knowledge
- **Multi-source Context:** Integration of documentation, code, configuration, telemetry

Proper context engineering critical to agent quality and reliability.

### Security, Compliance, and Observability at Scale

Enterprise requirements for agent adoption:
- **Security:** Agents operate with principle of least privilege; tool access governed by role-based policies
- **Compliance:** Audit trails of all agent actions; data handling conformity
- **Observability:** Comprehensive logging; ability to trace agent reasoning and tool invocations
- **Governance:** Resource limits, cost attribution, approval workflows

## Key Insights for Architects and Leaders

### Moving Beyond Proof-of-Concepts
Single-team POCs lack infrastructure for enterprise adoption. Success requires:
- Platform investment upfront
- Shared infrastructure and tools
- Standardized interfaces (MCP)
- Organizational buy-in

### Foreground vs. Background Trade-offs
- Foreground agents tighter feedback loop but require IDE-specific implementations
- Background agents more scalable but add latency
- Effective systems likely need both

### Intent Over Implementation
Shift from prompt engineering to intent specification:
- Developers declare goals and constraints
- Agents determine execution approach
- More maintainable and auditable long-term

### Human Remains in Critical Loop
Human judgment needed for:
- Verification of agent outputs
- Security and compliance decisions
- Feedback on implicit requirements
- Exception handling and edge cases

## Audience

Key for:
- **Software Architects:** Blueprint for enterprise-scale AI agent adoption
- **Engineering Leaders:** Organizational and technical strategy
- **Platform Engineers:** Infrastructure design patterns
- **Enterprise Development Teams:** Scaling AI safely and securely

## Resources

- **Transcript:** https://bit.ly/4iFRRhe
- **Software Architects' Newsletter:** https://www.infoq.com/software-architects-newsletter
- **QCon AI Events:** Annual conferences on AI in software engineering

## Discussion Prompt

"Do you agree that AI agents require a dedicated platform team, or should they be managed by individual developers?"
