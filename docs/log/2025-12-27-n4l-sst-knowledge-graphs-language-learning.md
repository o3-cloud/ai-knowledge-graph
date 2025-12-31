---
summary: Framework for using Semantic Spacetime (SST) knowledge graphs with N4L notes to make foreign language learning practical and personal, emphasizing active process-driven knowledge building over traditional structured approaches.
event_type: research
sources:
    - https://mark-burgess-oslo-mb.medium.com/using-n4l-notes-and-sst-knowledge-graphs-for-foreign-language-learning-ac4c0731320d
    - https://github.com/markburgess/SSTorytime/tree/main
tags:
    - knowledge-graphs
    - language-learning
    - semantic-spacetime
    - note-taking
    - learning-tools
    - n4l-notes
    - knowledge-representation
---

# Using N4L Notes and SST Knowledge Graphs For Foreign Language Learning

**Author:** Mark Burgess (40+ years educator, SSTorytime Project developer)
**Date:** December 5, 2025
**Medium:** Article + Practical Examples

## Core Philosophy

Knowledge graphs aren't just for enterprise databases and formal ontologies—they're powerful tools for personal learning. The critical insight: **"It never actually becomes knowledge unless you actually know it."**

Key principle: Learning requires **personal intent**. Outsourcing knowledge to tools (including "AI") is no substitute for understanding something yourself.

## The Problem with Current Approaches

### RDF/OWL Limitations
- Industry standard since 1990s, but overly bureaucratic
- Forces difficult formats onto users rather than simplifying
- Compounds learning difficulty (learning subject + learning complex tool)
- Piles cognitive quicksand instead of providing bird's-eye view

### Why Traditional Language Learning Fails
- Teaches official language, not what people actually say
- Rote memorization without personal relevance
- Lacks personal context and scenarios
- No efficient search or recall mechanism

**Example:** "Jean-Paul plays with the ball" teaches grammar but is useless in actual conversation.

## The N4L + SST Method

### Core Principle: Three Simple Elements

1. **Events, Things, Concepts** (nodes) - the material itself
2. **Arrows** (relationships) - joining relevant nodes
3. **Context** (grouping) - organizing for easy recall

Everyone can collect these at their own pace. No need for perfect systems upfront—that's how writer's block begins.

### The Gardening Mantra

```
JOT IT DOWN WHEN YOU THINK OF IT...
TYPE IT INTO N4L AS SOON AS YOU CAN...
ORGANIZE AND TIDY YOUR N4L NOTES EVERY DAY...
UPLOAD AND BROWSE THEM ONLINE...
REMEMBER, IT ISN'T KNOWLEDGE IF YOU DON'T ACTUALLY KNOW IT!!
```

The notes are the goal. The graph is merely a navigational structure to help you find things by meaning.

## Practical Implementation

### Stage 1: Capture (Informal)
- Take photos/screenshots of unfamiliar text
- Jot down phrases and examples on paper, phone, or computer
- Don't stress about organization yet
- Focus on what interests you or feels important

### Stage 2: Transcribe (Semi-Structured)
- Transfer captures into N4L format
- Add arrows showing relationships:
  - Translation arrows: `(eng for fr)`, `(hanzi to english)`, `(pinyin to pinyin)`
  - Context arrows: `(means)`, `(example)`, `(origin)`
  - Usage arrows: `(airport scenario)`, `(formal vs colloquial)`

**Example:**
```
Jean-Paul played with the ball (eng for fr) Jean-Paul joué avec le ballon
Jean-Paul plays with the ball (eng for fr) Jean-Paul joue avec le ballon
```

### Stage 3: Organize (Iterative)
- Group by context/scenario (airport, hotel, restaurant, work)
- Look for patterns and cross-references
- Tidy incrementally (don't wait for perfection)
- N4L compiler automatically handles deduplication and structure

### Stage 4: Review/Rehearse (Active Learning)
- Read notes systematically via `\notes` mode (not random lookup)
- Use tick boxes to track progress
- Employ spaced repetition: notes "cool off" from red → yellow → green → blue based on review frequency
- Use `\new \notes \context [topic]` to see items not reviewed in past 4 hours

## Why Semantic Spacetime Fits Language Learning

Language is fundamentally a **process**, not a taxonomy:
- **Worldly process**: The actual conversation or scenario happening
- **Observation timeline**: Your notes about what you're learning
- **Learner's timeline**: Your review and study of those notes
- **Progress timeline**: Tracking when notes were last read (more important than when written)

SST's four arrow types capture this naturally:
- **LEADSTO**: Sequence in conversations/scenarios
- **CONTAINS**: Hierarchical relationships
- **EXPRESSES PROPERTY**: Meaning and usage
- **NEARNESS/SIMILARITY**: Related concepts, synonyms, homonyms

## Case Study: Learning Mandarin

### Challenges Addressed
- **Multiple writing systems**: Hanzi (simplified/traditional), Pinyin (romanization), English
- **Semantic density**: Characters encode meaning graphically (like hieroglyphics)
- **Homophones**: Same sound, different meanings, different characters
- **Context dependency**: Words have multiple meanings depending on context

### Structured Approach
```
hanzi ↔ pinyin ↔ english
Traditional/Simplified characters
Character composition (which character carries meaning)
Paired character patterns (one main meaning, one refinement)
```

### Example: Yin and Yang
The hidden message: actually means "hot and cold" (from sun and moon) encoded in the characters themselves. This "aha" moment creates lasting memory.

## Scenario-Based Organization

Instead of abstract exercises, anchor learning in real situations:

**Airport scenario sequence:**
- Arrive at airport
- Check in (luggage)
- Passport/visa
- Security
- Board plane
- Land
- Passport/customs
- Find taxi to hotel

Each step triggers natural vocabulary needs and memorable associations.

**Implementation in N4L:**
```
context :: airport check-in ::
  I need to check in (english to mandarin) 我需要办理登机手续
  Passport (english to mandarin) 护照
  ...
```

Results in structured but natural knowledge graph that mirrors the actual scenario flow.

## Application Beyond Languages

The method works for any domain knowledge system:

### Mathematics
- Notation and symbols (like LaTeX for Chinese characters)
- Grammar and structure
- Worked examples and derivations
- Cross-linked concepts

### Specialized Domains
- Medical/legal terminology
- Programming languages
- Job-specific jargon
- Academic subjects (History, Geography, etc.)

## Comparison to Other Tools

| Tool | Strengths | Limitations |
|------|-----------|------------|
| Duolingo | Accessible, engaging initially | No search function, gameification, juvenile, doesn't capture real usage |
| Phrase books | Practical, situational | Static, no connections, no context for understanding |
| Dictionaries | Comprehensive lookup | Word-by-word, no narrative or relationship |
| Courses | Structured, comprehensive | Often irrelevant examples, all-at-once cognitive load |
| **N4L + SST** | Personal, searchable, narrative-driven, scenario-based | Requires self-discipline and consistent review |

## Key Design Principles

### 1. Personal Intent is Primary
- Real learning requires personal reasons to learn
- Company training courses without intent produce zero retained knowledge
- Success depends on jeopardy (needing to actually communicate)

### 2. Process Over Structure
- Don't force perfect organization upfront
- Iterative tidying is more effective than perfect initial design
- The process of review is what moves knowledge from short-term to long-term memory

### 3. Knowledge ≠ Information
- Information is passive consumption ("info-tainment")
- Knowledge requires active engagement and repeated rehearsal
- Just having intent to solve a problem is "half the battle to remembering"

### 4. Narrative Over Taxonomy
- Stories and scenarios stick better than abstract categories
- Context is more important than rigid ontology
- Repetition across multiple contexts is fine (don't force single-box organization)

## Against AI as Knowledge Replacement

Tech capitalism promotes AI as a solution to everything. Important clarification:
- **Tools are tools**: AI can help at appropriate moments
- **Knowledge must be personal**: Outsourcing understanding won't work
- **Probability vs. precision**: Language models are probabilistic; knowledge graphs are precise
- **Supplement, not replacement**: AI can accelerate learning, not replace it
- **Keys to knowledge lie in our real intentions**: Tools amplify intent; they don't create it

## Critical Success Factors

1. **Self-discipline in review schedule** - Notes cool if not regularly rehearsed
2. **Willingness to iterate** - Organization improves with use, not upfront planning
3. **Scenario grounding** - Anchor vocabulary in real situations you care about
4. **Personal relevance** - Learn what you actually need or want to know
5. **Active note-making** - The act of writing is part of the learning process

## Related Concepts

This approach connects to:
- `2025-12-27-death-and-rebirth-of-programming.md` - Knowledge as the scarce resource, not production
- `2025-12-27-agent-readiness-framework.md` - Making systems comprehensible and documented
- `2025-12-27-llm-coding-workflow-best-practices.md` - Active engagement over passive consumption

## Practical Next Steps

1. **Start with one scenario** (airport, restaurant, daily work tasks)
2. **Capture freely** without worrying about structure
3. **Transcribe to N4L daily** with simple arrow patterns
4. **Organize iteratively** as patterns emerge
5. **Review on schedule** using spaced repetition and color-cooling
6. **Expand to related scenarios** as vocabulary grows
7. **Cross-link advanced concepts** as you discover deeper patterns

## Open Questions

1. How does N4L + SST scale to very large knowledge domains (thousands of concepts)?
2. What are optimal review schedules for different types of learners?
3. How can SST be integrated with other learning modalities (video, conversation, text)?
4. Could this approach improve formal education if adopted in schools?
5. How does personal knowledge graph compare to collaborative/shared graphs for group learning?
