---
summary: Proposes a file system abstraction for context engineering in GenAI systems, implementing a persistent infrastructure for managing heterogeneous context through the AIGNE framework with structured Constructor-Updater-Evaluator pipeline
event_type: research
sources:
    - https://arxiv.org/pdf/2512.05470
tags:
    - context-engineering
    - file-system-abstraction
    - GenAI-architecture
    - agentic-systems
    - memory-management
    - AIGNE-framework
---

# Everything is Context: Agentic File System Abstraction for Context Engineering

**Authors:** Xiwei Xu, Xuewu Gu, Robert Mao, Yechao Li, Quan Bai, Liming Zhu
**Affiliations:** CSIRO's Data61, ArcBlock Inc, University of Tasmania, UNSW
**ArXiv:** 2512.05470
**Upload Date:** December 5, 2025

## Core Problem

Current GenAI systems treat context engineering as ad hoc and fragmented. Existing practices like prompt engineering, RAG, and tool integration produce transient artefacts that limit traceability and accountability. The real challenge is not model fine-tuning but how systems capture, structure, and govern external knowledge, memory, tools, and human input.

## Key Innovation: File System as Context Infrastructure

Inspired by Unix philosophy ("everything is a file"), the paper proposes a **file system abstraction** as architectural foundation for context engineering. This provides:

- **Persistent governance** of heterogeneous context sources (memory, tools, external knowledge, human contributions)
- **Uniform mounting and access** through standard file operations
- **Structured metadata** enabling traceability and accountability
- **Verifiable infrastructure** replacing ad hoc prompting practices

## Architectural Principles

The file system abstraction implements five core SE principles:

### 1. Abstraction
Uniform interface hiding heterogeneity of underlying context sources. Regardless of whether a resource is a knowledge graph, vector store, or human-curated note, it's represented through standardized file interface. Schema-driven design automatically projects REST/OpenAPI, GraphQL, MCP tools, and external APIs into the namespace.

### 2. Modularity and Encapsulation
Decomposition into independently manageable context resources. Each resource encapsulated as mounted component with well-defined boundaries and metadata. Changes in one component don't propagate across system.

### 3. Separation of Concerns
Distinction between data, tools, and governance layers. Non-executable files (config.yaml, experiment_results.csv) serve as data/knowledge resources. Executable artefacts (analyser.py, simulate.sh) represent active tools. Governance mechanisms (access control, logging, metadata) handled independently.

### 4. Traceability and Verifiability
Every interaction logged as transaction in persistent context repository. Enables reconstruction of context provenance and accountability of actions. Coupled with structured metadata, logs support auditing of changes, reasoning steps, and tool invocations.

### 5. Composability and Evolvability
Consistent namespace and interoperable metadata schema across all mounted resources. Context elements combined, queried, or integrated without additional integration code. Plugin architecture allows new backends (full-text indexers, vector databases, knowledge graphs) mounted seamlessly.

## Persistent Context Repository: History, Memory, Scratchpad Lifecycle

Addresses statelessness of LLMs by maintaining external persistent memory repository.

### History: Immutable Source of Truth
Records all raw interactions between users, agents, and environment. Each input, output, and intermediate reasoning step logged immutable with metadata (timestamp, origin, model version). Spans multiple agents and sessions as shared global data record.

### Memory: Structured and Indexed Views
Multiple memory types coexist along temporal, structural, and representational dimensions:

- **Scratchpad:** Temporary, task-bounded dialogue turns and reasoning states
- **Episodic Memory:** Medium-term session summaries and case histories
- **Fact Memory:** Long-term atomic factual statements
- **Experiential Memory:** Cross-task observation-action trajectories
- **Procedural Memory:** System-wide functions, tools, and definitions
- **User Memory:** Long-term personalized user attributes and preferences

Each memory item maintains reference to historical source, ensuring traceability. Indexed logs and embeddings enable selective recall without re-scanning entire history.

### Scratchpad: Temporary Workspace
Ephemeral workspaces where agents compose intermediate hypotheses and computations during reasoning. Scoped to specific task or reasoning episode. Upon session conclusion, relevant artefacts may be inserted into memory or appended to history.

### Governance
Explicit policies govern lifecycle: versioning, aging, retention. Obsolete scratchpads pruned automatically; historical logs compressed but never deleted. System remains both scalable and auditable.

## Context Engineering Pipeline: Three-Component Architecture

Built on three design constraints intrinsic to GenAI models:

### Design Constraints

**1. Token Window:** Hard architectural constraint defining maximum tokens model can attend to during single inference. Bounded reasoning capacity sets upper limit on active context available at runtime (e.g., 128K for GPT-5, 200K for Claude Sonnet 4.5). Quadratic complexity of self-attention increases computational cost with input length.

**2. Statelessness:** GenAI models don't retain conversational history or memory across sessions. Requires external persistent context repository. Stateless nature drives need for session memory mechanisms to restore continuity and avoid redundant computation.

**3. Non-Deterministic and Probabilistic Output:** LLMs produce probabilistic outputs conditioned on sampling parameters (e.g., temperature). Identical prompts yield varying responses. Introduces challenges for traceability, testing, and verification.

### Three-Component Pipeline

**Context Constructor**
- Selects, prioritizes, and compresses relevant context from persistent repository
- Transforms unbounded knowledge into curated subset suitable for token window
- Enforces privacy, access control, and data governance constraints
- Manages trade-off between completeness and boundedness
- Interfaces directly with file system mount points, generates context manifest recording what was selected, excluded, and why

**Context Updater**
- Manages transfer and refresh of constructed context into bounded reasoning space
- Synchronizes token window state, persistent context repository state, and runtime dialogue
- Ensures active context reflects most relevant and authorized information
- At beginning: static snapshot fed to model for single reasoning task
- During extended reasoning: incremental streaming progressively loads context
- Dynamic/interactive: adaptive refresh replaces outdated or less relevant fragments
- Records all context loading/replacement actions as metadata events for traceability

**Context Evaluator**
- Verifies model outputs against source context and provenance metadata
- Detects hallucinations, contradictions, or context drift through semantic comparison, factual consistency checking, cross-referencing
- Records evaluation metrics (confidence scores, factual alignment, human override rates) as structured metadata
- Transforms verified outputs into structured memory elements, updating persistent context repository
- Triggers human review when confidence below threshold or contradictions detected
- Stores human annotations as explicit context elements, elevating tacit knowledge to first-class component

## Implementation: AIGNE Framework

The proposed file system and context engineering pipeline implemented in **AIGNE Framework**—open-source functional development framework for GenAI agents.

### Key Components

**AFS (Agentic File System) Module**
- Primary file system interface
- SystemFS provides virtual file system with:
  - List, read, write, search commands for mounted directories
  - Navigation across nested subdirectories with depth limits
  - ripgrep integration for efficient content search
  - File metadata (timestamps, sizes, types) and user-defined metadata
  - Sandboxed access restricted to mounted directories

**Programmable Resolvers**
- Implement declarative mappings (similar to GraphQL/OpenAPI schemas)
- Translate internal structures into AFS nodes without changing underlying storage format
- Enable seamless integration of heterogeneous systems

**Typed Resources**
- Context elements represented as typed resources under AFS namespace
- Modules expose list/read/write/search APIs through standard asynchronous methods
- Abstraction enables agents to access heterogeneous data (files, chat histories, structured memory) through uniform interface

**Functions as Tools**
- Agents perform reasoning while delegating execution to modular Functions
- Implemented as executable files (e.g., Node.js modules)
- Export default asynchronous function with metadata descriptors (description, input_schema, output_schema)
- Enable agents to discover, validate, and invoke with structured arguments

## Exemplars

### Exemplar 1: Memory-Enabled Context Construction
Agents maintain contextual coherence across multiple dialogue turns through DefaultMemory module. Conversation history persists as retrievable context with storage location specified as file path (e.g., file:./memory.sqlite3). Each dialogue round automatically incorporated into subsequent reasoning, enabling long-term stateful interaction.

### Exemplar 2: MCP with GitHub
Any MCP (Model Context Protocol) server can be mounted as AFS module, exposing capabilities through unified file system interface. GitHub MCP server example shows AI agents interacting with GitHub as if simply accessing files. Agent invokes all GitHub tools directly through afs_exec on mounted paths like /modules/github-mcp/search_repositories.

## Key Insights

- Context engineering is central architectural concern—not secondary prompt optimization
- File system abstraction transforms context management from ad hoc practice into systematic discipline
- Persistent context repository bridges long-term knowledge with bounded reasoning window
- Pipeline enforces traceability, governance, and verifiability throughout context lifecycle
- Human roles embedded in architecture as curators, verifiers, and co-reasoners
- Standard file operations and metadata enable systematic orchestration of heterogeneous context

## Architectural Advantages

1. **Systematic Governance:** Transforms fragmented practices into verifiable infrastructure
2. **Composability:** Enables seamless integration of diverse backends (databases, APIs, vector stores)
3. **Scalability:** Token window constraints handled explicitly through modular context management
4. **Auditability:** All interactions logged for post-hoc analysis, debugging, compliance verification
5. **Human-AI Co-work:** Architecture embeds human judgment as integral component
6. **DevOps Integration:** Context versioning, review, deployment through familiar DevOps practices

## Future Directions

- **Agentic Navigation:** Enable agents to autonomously browse, construct indices, and evolve data structures in mounted space
- **Living Knowledge Fabric:** Allow agents to function as self-organizing processes that observe and modify own context
- **Strengthened Human-AI Co-work:** Empower humans to oversee, correct, contribute to, curate, and contextualise knowledge as active participants
