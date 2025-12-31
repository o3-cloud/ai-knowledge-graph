---
summary: Kurt Cagle proposes Knowledge-Graph-First (KGF) design—a paradigm shift where knowledge graphs are queried first to retrieve only relevant data before passing results to LLMs, rather than loading entire taxonomies into limited context windows, minimizing token consumption while maintaining consistency
event_type: blog_post
sources:
    - https://ontologist.substack.com/p/knowledge-graph-first-kgf-design
tags:
    - knowledge-graphs
    - KGF-design
    - LLM-architecture
    - ontologies
    - context-windows
    - RAG-reversal
    - semantic-search
    - metalabel-matching
    - Kurt-Cagle
---

# Knowledge-Graph-First (KGF) Design: Querying Graphs Before LLMs

**Author:** Kurt Cagle
**Publication:** The Ontologist (Substack)
**Publication Date:** December 21, 2025
**Type:** Architectural Pattern and Knowledge Organization
**Key Concept:** Reversing RAG paradigm to query graphs first, minimizing LLM context consumption

## Overview

Kurt Cagle introduces Knowledge-Graph-First (KGF) design as a fundamental paradigm shift in how large language models interact with knowledge structures. Rather than attempting to load entire ontologies and taxonomies into limited LLM context windows, KGF proposes querying knowledge graphs first to retrieve only relevant data, then passing those focused results to the model. The approach minimizes token consumption, maintains consistency with real-time updates, and treats knowledge graphs as orchestrators rather than loading them as raw input. The core insight: stop overloading contexts—use graph query capabilities intelligently.

## The Problem: Context Overload

### The Reality of LLM Context Windows

**Modern LLM constraints:**
- Typical context windows: 100K-1M tokens
- Large knowledge graphs (extensive taxonomies): often 500K-5M+ tokens
- Gap: Insufficient space for complete knowledge base

### What Teams Currently Do

**Traditional approach:**
1. Load entire knowledge base into context
2. Hope it fits (it usually doesn't)
3. Compress and summarize (loses information)
4. Accept degraded performance (trades off accuracy)

**The result:**
Inefficiency, incomplete information, poor decisions.

### Why This Doesn't Scale

**Graph size vs. context window:**

| Graph Size | Tokens | Max Context | Fits? |
|-----------|--------|-------------|--------|
| Small (100 entities) | 10K | 1M | ✓ |
| Medium (1000 entities) | 100K | 1M | ✓ |
| Large (10K entities) | 1M | 1M | ✓ (barely) |
| Enterprise (100K+ entities) | 10M+ | 1M | ✗ |
| Complex domain (multi-domain) | 50M+ | 1M | ✗ |

**The gap widens as domains become more complex.**

### The Cost of Compression

Attempting to fit large graphs by:
- Summarizing
- Abbreviating
- Truncating
- Selecting subsets randomly

Results in:
- Lost context
- Missing relationships
- Degraded reasoning
- Incorrect conclusions

**Solution: Stop trying to fit everything.**

## The KGF Paradigm: Query First, Pass Results

### The Core Idea

**Reverse the traditional flow:**

```
Traditional:
LLM Input: [entire knowledge base] → Model processes → Output

KGF:
LLM Query → Graph Query → Relevant results → Model processes → Output
```

**Key shift:**
Let the graph do the filtering, not the LLM.

### The Architecture

**Step 1: Query the Graph**
- User request arrives
- Translate to graph queries
- Query knowledge graph (unlimited size)
- Retrieve only relevant nodes and relationships

**Step 2: Format Results**
- Serialize relevant subgraph
- Use compact format (Turtle RDF)
- Include schema metadata
- Minimize token count

**Step 3: Pass to LLM**
- Only relevant data in context
- Complete picture of that domain
- Schema information explicit
- Model can reason clearly

**Step 4: Generate Response**
- LLM operates on focused context
- All necessary information present
- No missing relationships
- Clear structure and constraints

### Why This Works

**Advantages:**

| Aspect | Traditional | KGF |
|--------|------------|-----|
| **Context size** | Entire graph (too large) | Relevant subgraph (optimal) |
| **Token efficiency** | Poor (loses information) | Excellent (focused) |
| **Update capability** | Static (needs retraining) | Real-time (graph updates instantly) |
| **Consistency** | Variable (depends on compression) | High (structure enforced) |
| **Reasoning quality** | Degraded (incomplete info) | Superior (complete relevant context) |
| **Scalability** | Poor (doesn't scale) | Excellent (handles any size) |

## The Five Molecular Types in Ontologies

### Understanding Graph Structure

Cagle identifies five fundamental molecular types—distinct structural patterns that appear in ontologies and knowledge graphs.

### Type 1: Entities

**Definition:**
Physical or conceptual things with identifiable properties.

**Characteristics:**
- Few inbound properties
- Generally independent
- Can exist alone
- Examples: Person, Product, Company, Location

**In graphs:**
Leaf nodes or relatively independent nodes.

**Properties:**
- Identifiers (ID, name)
- Attributes (physical properties)
- Relationships (connections to other entities)

### Type 2: Connectors

**Definition:**
Relationships that bind interactions between entities.

**Characteristics:**
- Represent associations
- Don't exist independently
- Connect two or more entities
- Examples: "owns", "manages", "employs", "uses"

**In graphs:**
Edges or relationship nodes.

**Properties:**
- Source entity
- Target entity
- Relationship type
- Temporal properties (when, duration)
- Strength or confidence

**Use in KGF:**
Critical for understanding how entities relate.

### Type 3: Components

**Definition:**
Subordinate or abstract entities that are parts of larger entities.

**Characteristics:**
- Exist as parts of wholes
- Help decompose complex entities
- Can be abstract or concrete
- Examples: "department" (part of company), "chapter" (part of book), "organ" (part of body)

**In graphs:**
Can be modeled as hierarchical relationships.

**Importance in KGF:**
Allow breaking down complex domains into manageable pieces.

### Type 4: Classifiers

**Definition:**
Qualifying properties or enumerated values that categorize or describe entities.

**Characteristics:**
- Often represent choices
- Enumerated (limited set)
- Can be hierarchical
- Examples: Status (active/inactive), Priority (high/medium/low), Category (type classification)

**In graphs:**
Can be nodes themselves or properties of other nodes.

**In KGF search:**
Critical for filtering (show only "high priority" items).

### Type 5: Schemes

**Definition:**
Sets or collections of classifiers that work together.

**Characteristics:**
- Group related classifiers
- Define vocabulary for classification
- Can be hierarchical
- Examples: Color scheme, status scheme, priority scheme

**In graphs:**
Collections or categories of classifiers.

**In KGF:**
Define what classifications are available for filtering and search.

## Metalabel Matching: Beyond Simple Keywords

### The Problem with Simple Keyword Matching

**Basic keyword matching:**
```
User query: "What is the manager?"
Graph lookup: Exact field name match
Result: Fails if field is "manages", "supervisor", "overseer"
```

Multiple valid labels for same concept confuse simple matching.

### The Metalabel Solution

**Metalabel strategy:**
Enrich each classifier with multiple label vectors capturing different aspects of the same concept.

### Multiple Label Vectors

**For a single concept, include:**

**1. Primary Label**
- Official name
- Standard terminology
- Example: "manages"

**2. Alternative Labels**
- Synonyms
- Related terms
- Examples: "oversees", "supervises", "leads"

**3. Phonetic Representation**
- Double Metaphone algorithm
- Handles pronunciation variations
- Enables sound-alike matching
- Example: "manages" → phonetic code

**4. Acronyms and Abbreviations**
- Common shorthand
- Industry abbreviations
- Examples: "MGR", "supervisor abbrev"

**5. Stems and Variations**
- Morphological forms
- Root forms
- Examples: "manage", "manager", "managed", "management"

### How Metalabel Matching Works

**Process:**

```
1. User query arrives: "Who supervises this team?"
2. Analyze query for concepts: "supervise", "team"
3. Look up metalabels for supervision concept:
   - Primary: "manages"
   - Alternatives: "oversees", "supervises"
   - Phonetic: [algorithm output]
   - Acronyms: ["MGR", "SUPV"]
   - Stems: ["manage", "supervise"]
4. Match against input: "supervises" matches Alternative label
5. Retrieve correct graph relationship
6. Return semantically appropriate result
```

**Benefits:**
- Tolerates user terminology variations
- Handles abbreviations and acronyms
- Works across linguistic variations
- Improves semantic matching accuracy

## KGF Architecture in Practice

### The Flow

```
User Query
    ↓
Query Parser
    ↓
Graph Query (SPARQL, Cypher, etc.)
    ↓
Knowledge Graph (unlimited size)
    ↓
Subgraph Retrieval (relevant nodes only)
    ↓
Serialize to Turtle RDF
    ↓
Include Schema Metadata
    ↓
Format for LLM Context
    ↓
LLM Processing
    ↓
Response Generation
```

### Query Languages

**For retrieving from knowledge graphs:**
- SPARQL (standard for RDF graphs)
- Cypher (for property graphs)
- Gremlin (for graph traversal)
- Custom query logic

**Selection depends on:**
- Graph type (RDF vs property vs other)
- Query complexity
- Performance requirements
- Team expertise

### Serialization Format

**Turtle RDF recommended because:**
- Compact (saves tokens)
- Human-readable (debugging)
- Standard format (tools support)
- Schema can be included

**Example:**

```turtle
@prefix ex: <http://example.org/> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

ex:person1 foaf:name "John Doe" .
ex:person1 foaf:knows ex:person2 .
ex:person2 foaf:name "Jane Smith" .
```

### Schema Metadata

Include with results:
- What properties mean
- What relationships are valid
- Data types and constraints
- Hierarchies and classifications

Enables LLM to:
- Understand structure
- Make valid inferences
- Avoid nonsensical conclusions
- Follow data integrity rules

## Comparison: Traditional RAG vs. KGF

### Traditional RAG (Vector-based)

**Process:**
1. Embed documents into vectors
2. Query with user question
3. Find similar vectors
4. Retrieve documents
5. Pass to LLM

**Limitations:**
- Retrieves by semantic similarity, not logical relevance
- May include irrelevant results
- Loses structural relationships
- Cannot enforce constraints
- Works with unstructured data

### KGF (Graph Query First)

**Process:**
1. Parse user query for concepts
2. Query knowledge graph directly
3. Retrieve logically relevant nodes
4. Pass focused results to LLM

**Advantages:**
- Retrieves by logical relevance
- Precise subgraph extraction
- Preserves relationships and structure
- Can enforce constraints
- Works with structured knowledge

### Hybrid Approach

**Best practice might combine:**
- KGF for structured knowledge
- Vector RAG for unstructured content
- Federated search across both

## Real-World Advantages

### 1. Token Efficiency

**Impact:**
- Only relevant data in context
- Dramatically reduced token count
- Enables larger, more complex queries
- Reduces cost (fewer tokens = cheaper)

### 2. Real-Time Updates

**Advantage:**
- Graph updates instantly
- No need to retrain embeddings
- New knowledge immediately available
- Semantic relationships preserved

**vs. Vector RAG:**
- Requires re-embedding
- Takes time to propagate
- May miss recent changes

### 3. Consistency and Correctness

**Knowledge graphs enforce:**
- Schema constraints
- Relationship types
- Data types
- Cardinality rules

**LLM benefits:**
- Cannot violate structure
- Stays within valid values
- Respects relationships
- Generates more correct outputs

### 4. Explainability

**Graph structure provides:**
- Clear provenance (where did this come from?)
- Relationship tracing (why are these connected?)
- Schema compliance (is this valid?)
- Constraint verification (is this consistent?)

### 5. Scalability

**Traditional approach:**
- Doesn't scale (can't fit large graphs)
- Compression loses information
- Degradation with size

**KGF approach:**
- Scales to any graph size
- Query efficiency independent of total size
- No information loss
- Consistent quality regardless of scale

## Implementation Considerations

### When to Use KGF

**Best for:**
- Large, complex domains
- Highly structured knowledge
- Consistency-critical applications
- Real-time update requirements
- Enterprise knowledge systems

**Less ideal for:**
- Unstructured text
- Ambiguous or loosely structured data
- Rapid prototyping (setup overhead)
- Simple domains (overkill)

### Knowledge Graph Requirements

**Necessary:**
- Clear entity definitions
- Well-defined relationships
- Schema documentation
- Relationship constraints

**Helpful:**
- Metalabel enrichment
- Temporal properties
- Confidence scores
- Audit trails

### Tool Ecosystem

**Graph databases:**
- Neo4j (property graphs)
- RDF4J, Apache Jena (RDF)
- Amazon Neptune
- ArangoDB

**Query languages:**
- SPARQL
- Cypher
- Gremlin

**LLM integration:**
- Custom query builders
- Semantic routing
- Context formatting

## Key Takeaways

1. **Context overload problem** — Graphs exceed LLM context windows
2. **KGF paradigm** — Query graph first, pass results to LLM
3. **Reverses RAG** — Graph queries precede LLM processing
4. **Five molecular types** — Entities, Connectors, Components, Classifiers, Schemes
5. **Entity definition** — Physical/conceptual things with identifiable properties
6. **Connectors** — Relationships binding entities together
7. **Components** — Subordinate entities, parts of wholes
8. **Classifiers** — Qualifying properties or enumerated values
9. **Schemes** — Collections/vocabularies of classifiers
10. **Metalabel matching** — Multiple label vectors for semantic matching
11. **Double Metaphone** — Phonetic representation for sound-alike matching
12. **Alternative labels** — Synonyms and related terms
13. **Token efficiency** — KGF dramatically reduces token consumption
14. **Real-time updates** — Graph changes immediately available
15. **Consistency enforced** — Schema constraints prevent invalid outputs
16. **Scalability unlimited** — Works with any graph size
17. **Explainability improved** — Clear provenance and reasoning trails
18. **Hybrid approach** — Combine KGF (structured) and vector RAG (unstructured)
19. **Implementation requirements** — Clear entities, relationships, and schema
20. **Enterprise ideal** — KGF excels for complex, consistency-critical domains

## The Bottom Line

Kurt Cagle introduces Knowledge-Graph-First (KGF) design as a fundamental paradigm shift in how LLMs interact with knowledge structures. Rather than attempting to load entire ontologies into limited context windows, KGF proposes querying knowledge graphs first to retrieve only relevant subgraphs, then passing focused results to the model.

**The core insight:**
Stop overloading contexts—use graphs as orchestrators, not as raw input.

**Key advantages:**
- **Token efficiency** — Only relevant data in context
- **Real-time updates** — Graph changes instantly available
- **Consistency** — Schema constraints enforce correctness
- **Explainability** — Clear provenance and relationship tracing
- **Scalability** — Handles any graph size without degradation

**The five molecular types:**
Knowledge graphs consist of distinct structural patterns:
1. **Entities** — Physical or conceptual things
2. **Connectors** — Relationships between entities
3. **Components** — Subordinate parts of larger entities
4. **Classifiers** — Enumerated qualifying properties
5. **Schemes** — Collections of classifiers

**Metalabel matching:**
Enrich classifiers with multiple label vectors (primary, alternatives, phonetic, acronyms, stems) to enable intelligent semantic lookup that handles variations in user terminology.

**The architecture:**
Query the knowledge graph → Retrieve relevant subgraph → Serialize to Turtle RDF → Include schema metadata → Pass focused results to LLM → Generate response.

**For enterprise systems:**
KGF excels when knowledge is large, complex, highly structured, and consistency-critical. It enables real-time updates without retraining, scales to any domain size, and maintains data integrity.

**The comparison:**
Traditional RAG retrieves by semantic similarity. KGF retrieves by logical relevance. Hybrid approaches combine both: KGF for structured knowledge, vector RAG for unstructured content.

This represents a fundamental rethinking of how LLMs should interact with knowledge: not by loading everything into limited context, but by letting knowledge graphs do intelligent filtering and retrieval, passing only the relevant subgraph that the model needs to reason well.

