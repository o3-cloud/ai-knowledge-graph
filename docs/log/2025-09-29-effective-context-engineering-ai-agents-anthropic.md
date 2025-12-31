---
summary: Anthropic's applied AI team explains context engineering for agents—managing limited tokens through strategic system prompts, tool design, retrieval patterns, and long-horizon task architectures to maximize model performance
event_type: blog_post
sources:
    - https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
tags:
    - context-engineering
    - prompt-engineering
    - agent-architecture
    - token-management
    - system-prompts
    - tool-design
    - retrieval-patterns
    - memory-management
    - long-horizon-tasks
---

# Effective Context Engineering for AI Agents

**Authors:** Prithvi Rajasekaran, Ethan Dixon, Carly Ryan, Jeremy Hadfield (Anthropic Applied AI Team)
**Publication Date:** September 29, 2025
**Organization:** Anthropic

## Overview

Anthropic's applied AI team presents a comprehensive framework for context engineering—a critical but often underexplored challenge in agent development. Rather than focusing solely on prompt wording, context engineering addresses the larger problem: how to strategically allocate limited tokens across system instructions, tools, external data, and conversation history to maximize desired model behavior.

The core insight is deceptively simple yet practically profound: "Find the smallest set of high-signal tokens that maximize the likelihood of your desired outcome."

## Defining Context Engineering

### Context vs. Prompt Engineering

**Prompt engineering:**
- Focus: Crafting effective instructions and questions
- Scope: Individual prompts
- Horizon: Single-turn interactions

**Context engineering:**
- Focus: Curating all information available during inference
- Scope: Complete context window across multiple turns
- Horizon: Multi-turn conversations with state management

### What Context Engineering Includes

**System prompts:**
- Agent role and mission
- Behavioral constraints
- Decision frameworks
- Fallback strategies

**Tools and tool descriptions:**
- Tool inventory
- Input/output specifications
- When each tool is appropriate
- Usage examples

**External data:**
- Retrieved documents
- API responses
- Knowledge bases
- Reference materials

**Message history:**
- Conversation records
- Previous decisions
- Learned context
- Accumulated state

### The Scope Problem

**Traditional thinking:**
"Better prompts = better results"

**Context engineering reality:**
"The right allocation of token space = better results"

**Implication:**
Even perfect prompts fail if context space is wasted on irrelevant information.

## The Attention Budget Problem

### Context Rot

**What it is:**
Retrieval accuracy and model performance degrade as context length increases.

**Why it happens:**
- Transformer architecture creates n² pairwise token relationships
- Attention mechanisms spread thin across larger contexts
- Needle-in-haystack problem intensifies at scale
- Later tokens receive weaker attention than earlier ones

**Manifestation:**
Information buried deeper in context becomes less accessible to model reasoning.

### The Practical Implication

**Myth:**
Longer context = better performance

**Reality:**
Token quality matters more than quantity. Strategic allocation beats comprehensive inclusion.

**Consequence:**
Agents require constant curation of context to maintain performance.

## System Prompts: The Goldilocks Zone

### Design Philosophy

**Poor approach:**
Overly specific if-then-else logic that breaks on unexpected inputs.

**Better approach:**
Heuristic guidelines that provide direction without brittleness.

**Target:**
The "Goldilocks zone"—specific enough to guide effectively, flexible enough to handle variation.

### Finding the Optimal Specificity

**Too vague:**
"Be helpful and friendly"
- Problem: No guidance; model guesses at behavior
- Result: Inconsistent, often incorrect responses

**Too specific:**
"If user asks for X, do Y; if user asks for Z, do W; if..."
- Problem: Doesn't generalize; breaks on novel inputs
- Result: Inflexible agent that fails outside programmed scenarios

**Just right:**
"You are a financial advisor. Your role is to help users understand investment options and risks. For any recommendation, explain the reasoning and acknowledge relevant uncertainties. Never suggest specific stock picks without context."

- Provides clear role
- Sets behavioral boundaries
- Offers guidance principles
- Allows flexibility

### System Prompt Structure

**Effective system prompts include:**

1. **Role Definition**
   - Clear agent identity
   - Scope of capabilities
   - Authority limits

2. **Primary Goals**
   - What the agent optimizes for
   - What "success" looks like
   - Trade-off prioritization

3. **Behavioral Constraints**
   - What the agent must not do
   - Safety boundaries
   - Ethical guidelines

4. **Decision Framework**
   - How the agent should approach decisions
   - When to escalate
   - How to handle uncertainty

5. **Communication Style**
   - Tone and formality
   - Level of detail
   - Format preferences

### Token Efficiency in System Prompts

**Principle:**
Heuristics beat exhaustive rule lists.

**Example:**

**Inefficient (token waste):**
```
If user asks about weather, use weather tool
If user asks about news, use news tool
If user asks about finance, use finance tool
[100+ more if-then rules]
```

**Efficient (same information, fewer tokens):**
```
You have access to specialized tools: weather, news, finance.
For user requests, select the tool most relevant to their question.
When uncertain, ask clarifying questions before choosing a tool.
```

**Result:**
Fewer tokens, clearer guidance, more robust decision-making.

## Tool Design: Minimization and Clarity

### The Tool Ambiguity Problem

**What happens:**
With many tools, models struggle with selection and may mis-apply tools.

**Why it matters:**
- Token budget includes tool descriptions
- More tools = longer descriptions
- Longer descriptions = less clarity
- Poor clarity = tool misuse

### Minimization Principle

**Strategy:**
Minimize tool sets to reduce ambiguity.

**Not minimum possible:**
Tools should still cover needed functionality.

**But remove:**
- Redundant tools
- Rarely-used tools
- Conceptually overlapping tools
- Tools with unclear purposes

### Tool Clarity Requirements

**Each tool should be:**

1. **Self-contained**
   - Can understand tool from description alone
   - Doesn't require external context
   - Has clear input/output contract

2. **Well-understood by models**
   - Description matches common understanding
   - Not overly technical
   - Examples illustrate behavior clearly

3. **Token efficient**
   - Description is concise
   - Avoids redundancy
   - Covers necessary information only

### Tool Description Best Practices

**Poor tool description:**
```
"search: Search for stuff. Can search the web. Takes a query string. Returns results."
```

**Better description:**
```
"search: Search the public web for current information.
Input: query string (what to search for)
Output: list of relevant results with titles, URLs, summaries
Use when: you need recent information not in your training data"
```

**Why better:**
- Clear purpose
- Specifies inputs/outputs
- Indicates when to use
- No ambiguity about functionality

## Retrieval Strategies: Just-In-Time Loading

### Traditional Retrieval Approach

**Naive strategy:**
Pre-load all potentially relevant data into context.

**Problems:**
- Bloats context with irrelevant information
- Reduces space for reasoning
- Increases context rot effects
- Wastes tokens on low-signal data

### Just-In-Time Retrieval Pattern

**Strategy:**
Maintain lightweight references and dynamically load information via tools.

**Implementation:**
```
Agent context includes:
- File paths (not file contents)
- Database query patterns
- API endpoints
- Knowledge base indices

When needed:
- Agent uses tools to retrieve specific data
- Retrieved data temporarily added to context
- Data discarded after use
- Context stays clean
```

**Analogy:**
Humans keep contact information, not all details about every contact. You retrieve details when needed, not upfront.

### Benefits

1. **Token efficiency**
   - Only relevant data in context
   - Lightweight references
   - No data bloat

2. **Cognitive clarity**
   - Agent focuses on reasoning, not data browsing
   - Reduced context rot
   - Better attention distribution

3. **Scalability**
   - Can work with large knowledge bases
   - Handles dynamic data
   - Adapts to new information

## Example Implementations

**E-commerce customer service agent:**

```
System prompt: [Role and guidelines]
Tools: search_products, retrieve_order_history, check_return_policy
Tool descriptions: [Clear, concise descriptions]
Context: Empty or minimal (no pre-loaded product data)

When customer asks about products:
→ Agent uses search_products tool
→ Retrieves relevant products
→ Answers question with live data
→ Removes data from context after responding

When customer asks about order status:
→ Agent uses retrieve_order_history tool
→ Gets relevant order details
→ Provides status information
→ Clean context afterward
```

**Research assistant agent:**

```
System prompt: [Research guidelines, how to evaluate sources]
Tools: search_web, retrieve_from_knowledge_base, query_academic_database
Context: Lightweight index of available sources (not full documents)

When user asks research question:
→ Agent formulates search strategy
→ Uses tools to retrieve relevant papers/articles
→ Cites and synthesizes retrieved information
→ Removes full documents from context
→ Maintains only key insights
```

## Using Examples Effectively

### Examples as High-Signal Tokens

**Key principle:**
"For an LLM, examples are the pictures worth a thousand words."

**Why examples work:**
- Demonstrate desired behavior concretely
- More effective than abstract description
- Reduce ambiguity about expectations
- Show edge case handling

### Diversity Over Exhaustiveness

**Inefficient approach:**
Include every possible edge case with examples.

**Effective approach:**
Include diverse, canonical examples showing representative patterns.

**Better use of tokens:**
```
Instead of 20 examples of special characters in names:
[2-3 diverse examples showing how to handle names with special characters]

Model generalizes from pattern, handles variation.
```

### Example Selection Criteria

**Good examples:**
- Representative of common cases
- Show variation in approach
- Demonstrate edge case handling
- Concise and clear

**Poor examples:**
- Too many (token waste)
- Overly specific (don't generalize)
- Redundant (same pattern repeated)
- Unclear context

## Long-Horizon Task Management

### The Challenge

**Problem:**
Agents need to maintain context and make progress over many turns.

**Constraints:**
- Context window is finite
- Each turn adds tokens
- Eventually, context fills up
- Original system information gets squeezed out

### Compaction: Conversation Summarization

**Strategy:**
When context approaches limit, summarize conversation and reinitiate with compressed context.

**Implementation:**

```
Phase 1: Normal operation
- Agent operates with full history
- Context window fills gradually
- Model still has space for reasoning

Phase 2: Approaching limit
- Agent notes when context reaches 70-80% capacity
- Asks language model to summarize conversation so far
- Extracts key facts, decisions, progress

Phase 3: Reinitiation
- New context starts with summarized history
- Includes key facts, not full dialogue
- Agent continues from summarized state
- Retains continuity while freeing space

Example:
Original: [4000 tokens of conversation history]
Summarized: [200 tokens of key facts and decisions]
Freed space: [3800 tokens for continued reasoning]
```

**Benefits:**
- Maintains context across long interactions
- Prevents context explosion
- Preserves decision continuity
- Efficient token use

### Structured Note-Taking: External Memory

**Strategy:**
Agent maintains persistent notes outside the context window.

**Pattern:**

```
As agent operates:
- Maintains internal context window (for immediate reasoning)
- Writes key information to external notes/database
- Notes contain decisions, facts, progress
- When needed, retrieves relevant notes via tools
- Notes persist across context resets
```

**Example:**
```
Customer service agent helping with product issue
Context window: Current conversation
External notes:
- Customer profile (name, ID, order history)
- Problem description
- Steps already attempted
- Next steps planned

Agent can:
- Maintain casual conversation
- Reference notes when needed
- Update notes with new information
- Hand off to other agent with complete context
```

**Benefit:**
Agents can handle long-running cases while maintaining token efficiency.

### Sub-Agent Architectures

**Strategy:**
Decompose long-running tasks into focused sub-agents.

**Pattern:**

```
Manager Agent:
- Understands big picture
- Routes to specialists
- Compiles final answer

Specialist Agents:
- Handle focused tasks
- Use optimized tools
- Return condensed summaries

Flow:
Manager → routes to specialist A → gets summary
       → routes to specialist B → gets summary
       → synthesizes summaries → responds to user
```

**Benefits:**
- Each agent keeps focused context
- Specialists optimize their tool use
- Manager aggregates cleanly
- Scalable to complex problems

**Example: Financial analysis**

```
Manager: "Analyze this company's financial health"

Specialist A (Revenue): Analyzes revenue trends, returns 3-sentence summary
Specialist B (Risk): Analyzes risk factors, returns 3-sentence summary
Specialist C (Valuation): Analyzes valuation metrics, returns 3-sentence summary

Manager: Receives three concise summaries, synthesizes into comprehensive analysis
User gets: Complete analysis without any agent having bloated context
```

## Key Principles

### 1. Quality Over Quantity

**Principle:**
High-signal tokens outperform large context windows.

**Implication:**
Spend effort curating tokens, not accumulating them.

### 2. Strategic Allocation

**Principle:**
Different tokens serve different functions; allocate space intentionally.

**Allocation pattern:**
- System prompt: 5-10% of context
- Tools/references: 10-20%
- External data/retrieval: 30-40%
- Conversation history: 30-50%
- Reasoning space: Always reserve 10-20%

**Flexibility:**
Adjust allocation based on task type.

### 3. Heuristics Over Rules

**Principle:**
Flexible heuristics beat brittle if-then logic.

**Application:**
System prompts provide direction, not deterministic behavior.

### 4. Minimization Is Efficiency

**Principle:**
Remove tokens that don't increase performance.

**Practice:**
- Redundant tool descriptions: remove
- Comprehensive rule lists: replace with heuristics
- Irrelevant examples: exclude
- Low-signal data: don't pre-load

### 5. Retrieval Over Pre-loading

**Principle:**
Load data just-in-time, not all upfront.

**Benefit:**
Cleaner context, better attention, more scalability.

## Key Takeaways

1. **Context engineering differs from prompt engineering** — Broader scope including tools, data, history
2. **Token quality matters more than quantity** — Strategic allocation beats comprehensive inclusion
3. **Context rot affects all long contexts** — Attention degrades with length; curation essential
4. **System prompts need Goldilocks specificity** — Specific enough to guide, flexible enough to generalize
5. **Heuristics beat exhaustive rules** — Token-efficient, more robust guidance
6. **Tool minimization reduces ambiguity** — Fewer tools, clearer choices, better performance
7. **Tool descriptions require clarity** — Self-contained, understandable, token-efficient
8. **Just-in-time retrieval improves efficiency** — Load data only when needed
9. **Lightweight references replace pre-loading** — File paths, not contents; APIs, not results
10. **Examples are high-signal tokens** — Few diverse examples beat exhaustive edge cases
11. **Compaction handles long conversations** — Summarize and reinitiate when approaching limits
12. **Structured note-taking provides memory** — External persistence for long-running tasks
13. **Sub-agent architectures scale complexity** — Decompose into focused specialists, aggregate results
14. **Reserve reasoning space** — Always keep 10-20% context for actual thinking
15. **Measure context impact** — Track performance against context size and composition
16. **Dynamic allocation by task** — Adjust system prompt / tools / data ratio by task type
17. **Clarity prevents tool misuse** — Well-described tools used correctly
18. **Abstraction through tools** — Tools hide complexity, expose clean interfaces
19. **Redundancy is waste** — Remove duplicate information, consolidate overlapping tools
20. **Find high-signal tokens** — The smallest set that maximizes desired outcome

## Patterns by Scenario

### Short, Focused Tasks
```
Higher %: System prompt (detailed instructions matter more)
Higher %: Tools (will be used intensively)
Lower %: History (conversation is brief)
Approach: Pre-load everything relevant, keep context focused
```

### Long-Running Tasks
```
Lower %: System prompt (can be brief; refer to persistent notes)
Medium %: Tools (selective use)
Medium %: History (maintain key context only)
Higher %: External memory (notes, summaries, retrieved data)
Approach: Compaction, external note-taking, sub-agents as needed
```

### Knowledge-Intensive Tasks
```
Low %: System prompt (basic instructions)
Low %: History (each conversation fresh)
Medium %: Tools (retrieval tools essential)
High %: Retrieval capability (must access knowledge)
Approach: Just-in-time retrieval, no pre-loading, lightweight indices
```

### Complex Multi-Step Tasks
```
Medium %: System prompt (clear architecture)
Higher %: Tools (many specialized tools)
Lower %: Single conversation history (use sub-agents)
Higher %: Routing logic (which sub-agent for which step)
Approach: Sub-agent architecture, manager orchestration
```

## The Bottom Line

Context engineering is the often-overlooked complement to prompt engineering. While prompts capture how you communicate with models, context engineering captures what information you make available and when.

The core insight is simple but powerful: "Find the smallest set of high-signal tokens that maximize the likelihood of your desired outcome."

**Key implications:**

1. **Token space is limited and valuable** — Treat it like real estate; allocate strategically
2. **More context doesn't mean better performance** — Quality and relevance matter more
3. **System prompts should guide, not dictate** — Heuristics over rules
4. **Tools should be clear and minimal** — Quality descriptions, focused set
5. **Retrieval beats pre-loading** — Just-in-time access to data
6. **Long-horizon tasks need external memory** — Compaction, note-taking, sub-agents
7. **Examples show patterns better than rules** — Diverse examples, not exhaustive lists
8. **Reserve context for reasoning** — Don't fill window with data; leave space for thinking

For teams building agents, context engineering is where significant performance gains hide. The difference between an agent that struggles and one that excels often comes down to how well its context is curated and strategically allocated.

Start by examining your agent's token allocation: Are you pre-loading unnecessary data? Can tools handle retrieval instead? Is your system prompt optimally specific? Do you have external memory for long-running tasks?

The answers reveal significant optimization opportunities—without changing any prompting or model, just through better context engineering.

