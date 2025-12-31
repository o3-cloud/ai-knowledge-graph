---
summary: Gordon Ritter and David Dworsky analyze enterprise AI transformation—contrasting retrofit approaches (adding AI to legacy systems) versus rebuild strategies (AI-native architectures)—with implications for incumbents and startups
event_type: blog_post
sources:
    - https://www.emcap.com/thoughts/two-paths-for-enterprise-ai-retrofit-or-rebuild
tags:
    - enterprise-AI
    - software-strategy
    - incumbent-vs-startup
    - AI-native-architecture
    - business-process-automation
    - system-design
    - vibe-coding
    - digital-transformation
---

# Two Paths for Enterprise AI: Retrofit or Rebuild?

**Authors:** Gordon Ritter, David Dworsky
**Organization:** Emergence Capital
**Publication Date:** October 1, 2025

## Overview

Gordon Ritter and David Dworsky (Emergence Capital) examine a fundamental strategic question facing enterprise software: as AI enables conversational business process customization, will incumbents retrofit AI onto legacy systems, or will new entrants rebuild from scratch with AI-native architectures?

The distinction has profound implications: retrofit approaches inherit the complexity and limitations of existing platforms, while rebuild approaches eliminate legacy constraints but sacrifice established market presence.

## The Core Problem AI Solves

### Current Enterprise Reality

**Today's business process customization:**
- Manual configuration across multiple systems
- Complex proprietary formats (XML, Apex, custom fields)
- Requires deep platform expertise
- Time-consuming and error-prone
- Locks customers into vendor ecosystems

**Customization workflow:**
```
Business need identified
    ↓
IT team designs solution
    ↓
Engineer configures system
    ↓
Multiple system updates
    ↓
Testing and validation
    ↓
Months to deployment
```

**Cost:**
Significant implementation time and expertise required.

### The AI Promise: "Vibe Coding"

**New approach:**
Conversational interfaces enabling business users to customize processes intuitively.

**Example interaction:**
```
User: "When a customer payment is overdue by 30 days,
       automatically send a reminder and flag for review"

AI: Understands requirement, implements workflow logic,
    configures necessary automations

Result: Customization deployed without technical expertise
```

**Timeline:**
Hours instead of months.

**Implication:**
Business process customization becomes accessible to non-technical users.

## Path 1: Retrofit - Adding AI to Legacy Systems

### The Strategy

**Approach:**
Incumbents (Salesforce, SAP, Oracle) add conversational AI interfaces to existing platforms.

**Example - Salesforce approach:**
```
Existing system:
- Complex Apex code
- Custom fields and objects
- XML configurations
- Proprietary data models

Add:
- Natural language interface
- AI understanding layer
- Conversation-to-configuration translator

Result:
Natural language → AI → proprietary format conversion → system update
```

### The Fundamental Challenge

**Problem:**
Legacy systems weren't designed for AI modification.

**Specific obstacles:**

**1. Proprietary Format Opacity**
```
Standard programming language (TypeScript/Python):
User: "Create this workflow"
AI: Understands directly, implements straightforwardly

Proprietary format (XML, Apex, custom field definitions):
User: "Create this workflow"
AI: Must learn proprietary syntax
    Must understand platform conventions
    Must compose valid configurations
    Many paths to same outcome (confusing for AI)
```

**2. Abstraction Layer Complexity**
```
Database schema → Objects → Fields → Relationships
Each level introduces mapping complexity.

AI must navigate:
- How objects relate
- Which fields are appropriate
- What custom logic required
- Validation constraints
```

**3. Long Tail of Special Cases**
```
Platform has evolved over 20+ years.
Legacy customizations, edge cases, special behaviors.
AI must understand entire system to avoid conflicts.
```

### The Retrofit Reality

**What incumbents can do:**
- Add conversational interfaces (UI layer)
- Provide AI-assisted configuration (suggestions)
- Automate templated processes
- Improve documentation with AI

**What's difficult:**
- AI-driven arbitrary customization
- Complex logic synthesis
- Novel workflow design
- Learning from conversation context

**Result:**
Retrofit narrows the AI advantage. It helps users work with the system, but doesn't transform what the system can do or how quickly it can be customized.

### Market Dynamics of Retrofit

**Incumbent advantage:**
- Existing customer base
- Trusted brand
- Sales relationships
- Data lock-in

**Retrofit limitation:**
- Product limitations from legacy architecture
- Slower to AI-native capabilities
- Constrained by backward compatibility
- Must maintain huge codebase

**Risk:**
Customers see AI-native alternatives solving problems faster.

## Path 2: Rebuild - AI-Native Architecture

### The Strategy

**Approach:**
New entrants build systems from scratch using code-first architectures.

**Architecture pattern:**

```
User conversational intent
    ↓
AI converts to standard programming language
    ↓
System executes code natively
    ↓
Visual/natural language interfaces above

Underneath: TypeScript, Python, standard libraries
```

### Why Code-First Matters

**LLMs excel at programming languages:**

**Natural language:**
```
"Create a workflow that..."
Ambiguous, multiple interpretations, context-dependent
```

**Standard programming language:**
```
JavaScript/TypeScript/Python
Clear syntax, unambiguous semantics, LLMs trained extensively
```

**Proprietary format:**
```
XML, Apex, custom DSL
Limited training data, unclear conventions, steep learning curve
```

### Implementation Pattern

**Architecture:**

```
Frontend:
- Visual builder
- Natural language interface
- No-code workflow editor

Conversational layer:
- Understands user intent
- Asks clarifying questions
- Translates to code

Execution layer:
- Standard programming language
- Native libraries
- Direct data access

Persistence:
- Code-based configuration
- Version control friendly
- Human-readable

Result:
"Vibe coding" that produces maintainable, understandable solutions
```

### The Rebuild Advantage

**1. AI Comprehension**
LLMs understand standard programming languages deeply.

**2. Flexibility**
No abstraction layer limits; users can do anything the language allows.

**3. Developer-First**
If technical users want to refine AI outputs, they can (code is standard language).

**4. Integrability**
Standard languages integrate easily with other systems.

**5. Verifiability**
Code is auditable and testable.

### The Rebuild Challenge

**Disadvantage:**
No existing customer base, trusted brand, sales relationships, or data lock-in.

**Must:**
- Solve customer problems faster than incumbents
- Build market trust
- Acquire customers without existing relationships
- Achieve feature parity with incumbents (eventually)

## The "Trojan Horse" Strategy

### How New Entrants Win

**Key insight:**
New entrants succeed by starting narrow, expanding over time.

**Pattern:**

```
Phase 1: Narrow Focus
- Target specific workflow (e.g., sales pipeline)
- Solve that problem exceptionally well
- Become system of record for that workflow
- Build strong customer relationships

Phase 2: Expansion
- Gradually add adjacent workflows
- Leverage existing data and relationships
- Become more central to customer operations
- Increase switching costs

Phase 3: Dominance
- Broadest workflows integrated
- Primary system of record for multiple areas
- Data concentration and network effects
- Difficult for customers to switch
```

**Example - Sales pipeline expansion:**
```
Start: Sales pipeline management (CRM-like, but AI-native)
    ↓
Expand: Quote generation and approval workflows
    ↓
Expand: Contract management
    ↓
Expand: Revenue recognition
    ↓
Expand: Reporting and forecasting
```

**Each expansion:**
- Leverages data already in system
- Improves with more data
- Increases customer value
- Raises switching costs

### Why This Strategy Works

**Against incumbents:**
- Start in areas where retrofit is weakest
- Prove superior AI-native capabilities
- Build loyalty with better user experience
- Gradually capture broader business logic

**Customer perspective:**
- Exceptional experience in primary workflow
- Expanding value from one system
- Decreasing need for separate tools
- Network effects as more processes integrated

## Startup Recommendations

### For Companies Pursuing AI-Native Path

**1. Target Specific Workflows**
- Don't try to be everything
- Pick a workflow where AI advantage is clear
- Solve it extremely well

**2. Capture Workflow Data as Processes Operate**
- Every interaction creates learning opportunity
- Data improves AI over time
- Becomes defensible moat
- Customers generate value through use

**3. Become System of Record Gradually**
- Start as tool for one workflow
- Become data hub for that domain
- Expand to adjacent workflows
- Eventually primary system of record

**4. Use Code-First Architecture**
- Standard programming languages
- Opinionated SDKs (constrain choices helpfully)
- API-first design
- Visual and natural language on top

**5. Provide Multiple Interaction Modes**
- Conversational (most users)
- Visual builder (power users)
- Code (developers)
- Programmatic API

### Market Timing Considerations

**Window of opportunity:**
- Retrofit implementations will disappoint
- Customers will be frustrated by limitations
- AI-native alternatives will look attractive
- Timing: Next 2-3 years critical

**Risk:**
- Incumbents may move faster than expected
- Incumbents may acquire promising startups
- Multiple AI-native entrants competing
- Need speed to market and capital

## Key Distinctions

### Retrofit (Incumbent Path)

**Strengths:**
- Existing customer base
- Trusted brand
- Sales relationships
- Implementation expertise
- Data already in system
- Huge resources

**Weaknesses:**
- Legacy architecture constraints
- Complex proprietary formats
- AI struggles with system design
- Backward compatibility requirements
- Slow iteration cycles
- Organizational inertia

**Best for:**
- Customers already in ecosystem
- Incremental improvement scenarios
- Process assistance (not transformation)
- Ease of adoption (existing users)

**Limitations:**
- Won't fully realize AI potential
- Constrained by architecture
- Slower innovation
- Reduced flexibility

### Rebuild (Startup Path)

**Strengths:**
- Clean architecture from start
- AI-native design
- Standard programming languages
- Rapid innovation
- Superior AI integration
- Flexible and extensible

**Weaknesses:**
- No existing customer base
- No brand recognition
- No distribution relationships
- Must build trust
- Limited resources
- Chicken-egg problem

**Best for:**
- Companies starting fresh
- Customers not in incumbent ecosystem
- Radical transformation (not incremental)
- Technical audiences

**Risk:**
- Must execute flawlessly
- Capital-intensive
- Competitive timing pressures
- Incumbents may respond aggressively

## Market Implications

### For Customers

**Question:**
Should I wait for incumbent retrofit or switch to AI-native startup?

**Factors to consider:**
- How soon do you need AI capabilities?
- How much is workflow transformation worth?
- Can you work with startup reliability?
- Do you need broad feature coverage or deep single-workflow excellence?

**Timeline:**
- Retrofit: 1-2 years minimum for meaningful AI capabilities
- AI-native: Available now, but may lack breadth

### For Investors

**The opportunity:**
- AI-native startups could challenge massive incumbents
- Timing is critical (window before retrofits mature)
- Multiple winners possible (different verticals)
- But requires flawless execution and capital

**Risk factors:**
- Incumbent responses
- Execution challenges
- Market adoption risk
- Competitive dynamics

## Key Insights

### 1. Retrofit Inherits Limitations
Legacy architecture constrains AI capabilities.

### 2. Code-First Is the Differentiator
Standard programming languages make AI comprehension straightforward.

### 3. LLM Performance on Code Is Exceptional
Training data and clear semantics enable superior AI performance.

### 4. Vibe Coding Becomes Possible
Conversational business process customization is achievable with right architecture.

### 5. Incumbent Position Is Vulnerable
Retrofit won't compete with purpose-built AI-native systems.

### 6. Trojan Horse Strategy Works
Start narrow, expand gradually, become indispensable.

### 7. Data Gravity Matters
Once data is in system, customers hesitant to leave.

### 8. Timing Is Critical
Window before incumbents mature retrofit approaches is limited.

### 9. Multiple Winners Possible
Different verticals and workflows can support different leaders.

### 10. Integration Becomes Moat
Systems of record with integrated workflows are sticky.

## Key Takeaways

1. **AI enables conversational business customization** — "Vibe coding" for business processes
2. **Two fundamentally different paths exist** — Retrofit (add AI to legacy) vs. Rebuild (AI-native)
3. **Retrofit approach inherits complexity** — Proprietary formats hinder AI comprehension
4. **Code-first architecture is the key difference** — LLMs excel at standard programming languages
5. **Proprietary formats limit AI** — XML, Apex, custom DSLs are harder for AI to work with
6. **AI-native systems have fundamental advantage** — Direct LLM integration without abstraction
7. **Incumbents benefit from existing positions** — Customer base, trust, relationships, data
8. **Incumbents face retrofit limitations** — Legacy architecture constrains AI capabilities
9. **Startups must pursue trojan horse strategy** — Start narrow, expand gradually
10. **Workflow data becomes competitive moat** — System of record advantages accumulate
11. **Multiple interaction modes needed** — Conversational, visual, code, API
12. **Timing is critical** — Window before retrofits mature is limited
13. **Opinionated design is advantage** — Constrain choices to enable better AI
14. **API-first architecture enables extensibility** — Can integrate with other systems
15. **Standard languages are underrated advantage** — Game-changing for AI comprehension
16. **Customer lock-in increases over time** — Expanded workflows raise switching costs
17. **Retrofit won't fully solve AI potential** — Constrained by architectural decisions
18. **Adjacent workflow expansion is scalable** — Each expansion leverages existing data
19. **Feature parity less important than differentiation** — AI advantages matter more
20. **Market transformation is coming** — Business customization will become conversational

## The Bottom Line

Gordon Ritter and David Dworsky identify a crucial fork in enterprise software evolution: as AI enables "vibe coding" for business processes, incumbents must choose between retrofitting AI onto legacy systems or rebuilding with AI-native architectures.

**The core strategic insight:**
Retrofit approaches inherit the complexity of legacy systems, while rebuild approaches eliminate constraints but sacrifice market position.

**For incumbents:**
Retrofit adds value but doesn't fundamentally transform customization. AI-native startups will prove to be formidable competitors because standard programming languages are far more natural for LLMs than proprietary formats.

**For startups:**
The opportunity is real and substantial, but requires:
- Code-first architecture
- Focused initial workflow
- Gradual expansion strategy
- Exceptional execution
- Sufficient capital for multi-year journey

**The critical insight:**
Success comes from starting narrow (workflow-specific), capturing workflow data, and gradually expanding. Over time, the system becomes the system of record for those domains, creating network effects and switching costs that protect against incumbent responses.

**Market timing:**
The next 2-3 years are critical. Retrofit implementations will disappoint customers. AI-native alternatives will look attractive. The window for new entrants to establish beachheads is open now, but won't last indefinitely.

For customers: the decision is whether to wait for incumbent retrofit to mature (slow) or adopt startup solutions (fast but less proven). For startups: the opportunity is substantial, but execution must be flawless.

