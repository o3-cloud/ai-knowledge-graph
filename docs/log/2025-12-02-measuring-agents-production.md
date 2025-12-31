---
summary: First large-scale systematic study of 306 practitioners and 20 case studies revealing production agent practices, showing 68% execute ≤10 steps before human intervention, 70% use prompting over fine-tuning, and reliability as top challenge
event_type: research
sources:
    - https://arxiv.org/pdf/2512.04123
tags:
    - production-agents
    - agent-deployment
    - empirical-study
    - evaluation-methodology
    - human-oversight
    - reliability
    - case-studies
    - agent-architecture
---

# Measuring Agents in Production

**Authors:** Melissa Z. Pan, Negar Arabzadeh, Riccardo Cogo, Yuxuan Zhu, Alexander Xiong, Lakshya A Agrawal, Huanzhi Mao, Emma Shen, Sid Pallerla, Liana Patel, Shu Liu, Tianneng Shi, Xiaoyuan Liu, Jared Quincy Davis, Emmanuele Lacavalla, Alessandro Basile, Shuyi Yang, Paul Castro, Daniel Kang, Joseph E. Gonzalez, Koushik Sen, Dawn Song, Ion Stoica, Matei Zaharia, Marquita Ellis

**Affiliations:** UC Berkeley, Intesa Sanpaolo, UIUC, Stanford University, IBM Research
**ArXiv:** 2512.04123
**Publication Date:** December 2, 2025

## Overview

First large-scale empirical study of AI agents actually deployed in production environments. Conducted through:
- Online survey: 306 practitioners across 26 domains
- In-depth interviews: 20 case studies with real-world deployments
- Focus: Understanding successful deployment practices vs. research prototypes

## Research Questions

**RQ1:** What are the applications, users, and requirements of agents?
**RQ2:** What models, architectures, and techniques are used to build deployed agents?
**RQ3:** How are agents evaluated for deployment?
**RQ4:** What are the top challenges in building deployed agents?

## Key Findings

### RQ1: Applications and Use Cases

**Motivation for Adoption:**
- 73% deploy agents primarily for productivity gains (increasing task completion speed)
- 64% focus on reducing human task-hours
- 50% aim to automate routine labor
- Harder-to-verify benefits (risk mitigation, novel technology) are less common

**Application Domains (26 total):**
- Finance & Banking: 39.1%
- Technology: 24.6%
- Corporate Services: 23.2%
- Data Analytics, R&D, Healthcare also significant

**User Base:**
- 92.5% serve human end-users directly
- 52.2% serve internal employees
- 40.3% serve external customers
- Only 7.5% serve non-human consumers (other systems/agents)

**Latency Requirements:**
- 66% allow response times of minutes or longer
- Only 34% require sub-minute latency
- Organizations tolerate latency because agents still outperform human baselines by orders of magnitude

### RQ2: Architecture and Implementation

**Model Selection:**
- 85% of case studies use closed-source frontier models
- Only 15% use open-source models
- When open-source used: cost or regulatory constraints drive choice
- Pragmatic approach: test top accessible models, select best-performing regardless of cost

**Model Fine-Tuning:**
- 70% of production systems use off-the-shelf models WITHOUT fine-tuning
- Fine-tuning limited to:
  - Business-specific contexts (5% of studied systems)
  - Selective application for enterprise clients
  - Even then, performance gains don't always justify overhead
- Reinforcement Learning: Only 1 case study uses RL post-trained models

**Multi-Model Orchestration:**
- 40.9% use exactly one model
- 59.1% coordinate multiple models
- Drivers:
  - Cost optimization (route simple subtasks to smaller models)
  - Modality handling (combine general LLMs with specialized models)
  - Operational management (run legacy alongside new versions)

**Prompt Engineering:**
- 79% rely heavily on manual prompt construction
- Production prompts can exceed 10,000 tokens
- 44.6% use hybrid: humans draft, then LLM augments/refines
- Only 8.9% use automated prompt optimizers
- Human dominance reflects desire for control, interpretability, and iteration speed

**Agent Architecture:**

**Bounded Autonomy Pattern:**
- 68% execute at most 10 steps before requiring human intervention
- 47% execute fewer than 5 steps
- Most systems operate within tight bounds—deliberate design choice

**Control Flow:**
- 80% of detailed case studies utilize structured control flow
- Well-scoped, static workflows preferred over open-ended autonomy
- 9 cases use agentic RAG pipelines
- Only 1 case allows unconstrained exploration (sandbox-only)

**Framework Adoption Paradox:**
- Survey: 60.7% use third-party frameworks (LangChain 25%, CrewAI 10.7%)
- Case studies: 85% build custom in-house implementations
- Only 15% use external frameworks
- Motivation for custom: flexibility, simplicity, security/privacy policies, reduced dependency bloat

### RQ3: Evaluation Practices

**Baseline Comparisons:**
- Only 38.7% compare against non-agentic baselines
- 25.8% report systems are "truly novel" with no meaningful baseline
- Baseline comparison often challenging when non-agentic solutions are complex multi-component systems

**Benchmarking:**
- 75% of teams evaluate without formal benchmarks
- Rely instead on: A/B testing, user feedback, production monitoring
- 25% build custom benchmarks from scratch
- Common pattern: establish golden QA set, collect user feedback, work with subject matter experts

**Evaluation Methods (Primary Focus):**
- 74.2% rely on human-in-the-loop evaluation
- 51.6% use LLM-as-a-judge (but ALWAYS combined with human review)
- 41.9% use cross-referencing (RAG, knowledge graphs)
- 38.7% use rule-based checks

**Critical Pattern:** Human judgment dominates—automated methods are complementary, not replacement. Production agents handle complex tasks requiring nuanced judgment beyond classification/pattern matching.

### RQ4: Top Challenges

**Reliability: Unsolved Challenge (Primary Focus)**
- 37.9% rank "Core Technical Focus" (reliability, robustness, scalability) as top challenge
- Far outweighs governance (3.4%) or compliance (17.2%)

**Three Challenge Dimensions:**

**Evaluation Challenges:**
- Creating benchmarks: Data scarcity in regulated fields (insurance), resource-intensive scaling (months to create 100 examples), client-specific customization complexity
- Integrating with CI/CD: Agent non-determinism and difficulty judging outputs programmatically
- Verification mechanisms: Coding-related agents have fast correctness signals; insurance agents receive delayed feedback through real consequences
- Benefit quantification: Easier to measure productivity gains than risk mitigation or cross-domain expertise reduction

**Latency Challenges (Manageable for Most):**
- Only 14.8% identify latency as critical deployment blocker
- 59.3% report suboptimal but deployable
- 15/20 cases use asynchronous execution (decoupling from session)
- Exception: Real-time interactive agents (voice, chat) face continuous engineering effort

**Security and Privacy (Secondary):**
- 69% of systems retrieve confidential/sensitive data
- Primary mitigation: Read-only operations, sandboxed execution, abstraction layers, RBAC (though challenging)
- Teams address through organizational legal methods, contractual agreements with providers

## Architectural Pattern: Reliability Through Constraint

**Paradox Resolution:** Agents reach production despite reliability being unsolved challenge through:

1. **Deployment Environment Constraints:**
   - Read-only mode (no production state modification)
   - Internal deployment (lower consequences, human oversight available)
   - Sandboxed execution (output verification before production)
   - Abstraction layers hiding internal function details

2. **Bounded Autonomy:**
   - 68% execute <10 steps before human intervention
   - Structured workflows with predetermined subtasks
   - RAG with predetermined retrieval steps

3. **Outcome Verification:**
   - Shift reliability burden from "correct every step" to "verify final output meets threshold"
   - Enables higher error tolerance with strong final gates

## Emerging Pattern: Agents as Augmentation Tools

Rather than full autonomy, production agents function as **domain expert augmentation**:
- Most systems require domain-specific expertise to operate
- Agents augment rather than replace domain experts
- Humans remain as final verifiers of agent outputs
- Enables acceptable error rates through final quality gates

## Model Capabilities Already Sufficient

**Key Insight:** Current frontier models provide sufficient capabilities for productive deployment across diverse industries without:
- Fine-tuning
- Weight modification
- Reinforcement learning
- Autonomous decision-making

Success depends on:
- Architectural constraints ensuring controllability
- Human oversight at critical points
- Realistic problem scoping
- Clear evaluation criteria

## Data Handling

- 89.7% ingest from databases (internal infrastructure)
- 65.5% ingest real-time user input
- 69% retrieve confidential/sensitive data
- Only 34.5% retrieve public data

## Future Modality Support

**Growth Areas:**
- 93% of current systems process text/speech
- Strong interest in expanding to: images, videos, scientific data, geospatial/temporal data
- Most future growth planned for non-textual modalities

## Key Insights for Practitioners

1. **Simple, Controllable Methods Succeed:** Bounded autonomy, human oversight, and structured workflows enable reliable production deployment

2. **Reliability Through Architecture:** Solve reliability not through perfect agent behavior but through environmental constraints and final quality gates

3. **Human Judgment Central:** Even with sophisticated evaluation, human verification remains irreplaceable

4. **Frontier Models Sufficient:** State-of-the-art model capabilities already enable diverse production use cases without specialized tuning

5. **Productive with Current Technology:** Organizations are already delivering measurable value across 26+ domains using practical, proven patterns

## Implications

- Production agent development is emerging engineering discipline distinct from research
- Success requires disciplined architecture and evaluation, not chasing capability frontiers
- Reliability solutions are architectural, not merely algorithmic
- Human oversight isn't limitation—it's essential production practice
