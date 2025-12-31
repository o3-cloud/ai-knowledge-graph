---
summary: Owen Zanzal proposes Bad Guy AI—using AI systems as relentless skeptics and contrarians to challenge assumptions, surface risks, and force stronger thinking rather than relying on AI for speed and agreement
event_type: blog_post
sources:
    - https://medium.com/devops-ai/bad-guy-ai-why-we-should-outsource-the-naysayer-role-to-machines-d352a0f1fa37
tags:
    - critical-thinking
    - devil's-advocate
    - AI-skepticism
    - decision-making
    - risk-assessment
    - prompt-engineering
    - organizational-culture
    - idea-validation
    - contrarian-perspective
    - cognitive-rigor
---

# Bad Guy AI: Why We Should Outsource the Naysayer Role to Machines

**Author:** Owen Zanzal
**Platform:** Medium (DevOps+AI)
**Publication Date:** September 29, 2025
**Type:** Strategy and Practice
**Key Concept:** AI as relentless critic rather than cheerleader

## Overview

Owen Zanzal inverts the common narrative about AI—instead of positioning it as an accelerator to move faster, he argues for using AI as a deliberate brake, a critical voice that challenges assumptions and surfaces risks before they become expensive failures.

"Bad Guy AI" is an intentional use of AI systems to play the uncomfortable role nobody wants: the naysayer, the skeptic, the contrarian who points out flaws and forces better thinking. Rather than training teams to provide this critical perspective, organizations can outsource the role to AI that never tires, never takes criticism personally, and always asks harder questions.

## The Problem: AI's Default Niceness

### The Cheerleader Problem

**What happens by default:**
- "Excellent idea!"
- "You are absolutely correct."
- "That's a great approach."
- Constant affirmation and agreement

**Why this happens:**
AI is trained to be helpful and agreeable. Politeness and agreement feel like service.

**The cost:**
When what's needed is rigor, agreement is dangerous.

### Where Niceness Fails

**Situation:** Proposing a business strategy
- Default AI: "Excellent plan! Here are three ways to improve it."
- What's needed: "Here's why this will fail. What's your response?"

**Situation:** Shipping code
- Default AI: "This looks good. Great job!"
- What's needed: "This violates three security patterns. Here's why it's risky."

**Situation:** Pitching to investors
- Default AI: "Strong pitch! Good luck!"
- What's needed: "Here are the five objections investors will raise."

**The hidden cost:**
Ideas that should be destroyed early make it to production. Strategies that should fail at planning survive to implementation.

## The Value of the Bad Guy Role

### Why Organizations Need Naysayers

**In healthy organizations:**
Someone asks hard questions. Challenges assumptions. Points out flaws.

**The problem:**
Nobody wants that job. It's uncomfortable. Exhausting. Creates tension.

**The result:**
The naysayer role often goes unfilled, and bad ideas survive longer than they should.

### What Bad Guy AI Provides

**Relentless skepticism:**
Never gets tired. Never backs down. Never takes things personally.

**Perspective on demand:**
Can role-play as frustrated customer, skeptical investor, ruthless competitor, frustrated engineer.

**Early failure:**
Cracks found on day one cost far less than production failures.

**Sharpen thinking:**
Iron sharpens iron. Being challenged forces clarity, justification, improvement.

**Psychological safety:**
Criticism from a machine feels different than from a colleague. No personal offense. No career implications.

## What Bad Guy AI Does

### Core Functions

**Attacks assumptions:**
```
Common assumption: "Our users want mobile-first experience"
Bad Guy AI: "How do you know? What's your evidence?
             Show the data. Show the user feedback.
             What if you're wrong?"
```

**Points out better solutions:**
```
Presented solution: "Implement feature X"
Bad Guy AI: "You could do that. But here's why solution Y
             would be superior. Here's why solution Z
             might be even better. What would make you
             choose X over these alternatives?"
```

**Forces defense:**
```
Stated strategy: "We'll be the low-cost provider"
Bad Guy AI: "Given your cost structure, how do you compete
             on price with larger competitors? What breaks
             your model? When do you run out of runway?"
```

**Surfaces risks:**
```
Product launch plan: Ship by Q4
Bad Guy AI: "Here's what could go wrong:
             regulatory delays, supply chain, key person risk,
             market shift, competitive response. What's your
             contingency for each?"
```

**Questions processes:**
```
Team decision: "We'll ship the v1 feature set"
Bad Guy AI: "On what basis? What metrics prove v1 is sufficient?
             What do you risk if you're wrong? What's the
             irreversible cost?"
```

## Practical Applications

### Product Design

**How to use:**
Run idea through AI acting as your most cynical user.

**Example prompt:**
```
"You're a frustrated user who just spent 20 minutes trying to
complete a simple task and failed. You're about to delete the app.
What went wrong? What feature is missing? What is confusing?
What would make you stay?"
```

**Value:**
Surface usability issues before launch. Understand friction points.

### Strategy Sessions

**How to use:**
Ask AI to role-play competitor determined to crush you.

**Example prompt:**
```
"You're a competitor with 10x our resources and our market share
in your sights. You've studied our strategy. How would you attack us?
What's our vulnerability? How would you exploit it?"
```

**Value:**
See strategic blind spots. Understand competitive threats. Plan defenses.

### Startup Pitches

**How to use:**
Have AI rip your deck apart before investors do.

**Example prompt:**
```
"You're a VC who just heard this pitch. You're skeptical but willing
to listen. What are the five biggest questions you have?
What's the biggest risk you see? What would make you pass?"
```

**Value:**
Anticipate investor concerns. Strengthen pitch. Prepare responses.

### Code Reviews

**How to use:**
Let AI nitpick security, scalability, maintainability.

**Example prompt:**
```
"You're a senior engineer reviewing code written by a junior.
Be ruthlessly critical about security vulnerabilities, scalability
issues, and maintainability problems. What would make you reject
this in code review? What's the biggest issue here?"
```

**Value:**
Catch issues before production. Enforce quality standards. Build better code.

### Decision-Making

**How to use:**
Instead of rushing to yes, let AI keep asking "why?"

**Example prompt:**
```
"We're considering [decision]. Make the strongest case against it.
What could go wrong? What are we ignoring? What's the downside?
What would make this decision a disaster?"
```

**Value:**
Slower, more rigorous decision-making. Better quality decisions.

## The Art of Prompting for Pushback

### The Inversion Principle

**Standard prompting:**
"Help me improve this marketing strategy"
```
Result: AI becomes cheerleader
        Suggests incremental improvements
        Validates your thinking
        Lacks rigor
```

**Bad Guy prompting:**
"You're a marketing expert who thinks this strategy is doomed.
Explain why it will fail and what I'm missing."
```
Result: AI becomes critic
        Questions fundamental assumptions
        Surfaces hidden risks
        Forces deeper thinking
```

### The Stakeholder Role-Play

**Instead of single perspective:**
"Review my design"

**Ask for multiple perspectives:**

```
"You're a user who just tried this and gave up"
    ↓
    Surfaces usability issues

"You're a compliance officer reviewing this product"
    ↓
    Surfaces regulatory risks

"You're the person who has to maintain this code"
    ↓
    Surfaces technical debt risks

"You're a customer who feels cheated by this"
    ↓
    Surfaces value proposition gaps

"You're a competitor studying our strategy"
    ↓
    Surfaces strategic vulnerabilities
```

### Key Prompting Patterns

**Pattern 1: Role + Stance + Mandate**
```
"You're a [stakeholder] who believes [contrarian position].
Your job is to convince me [alternative perspective].
Make the strongest case you can."
```

**Pattern 2: Assume Failure**
```
"Assume this [idea/strategy/product] fails spectacularly.
What was the cause? What were the warning signs?
What did we miss?"
```

**Pattern 3: Force Options**
```
"I'm considering [option A]. What's a better approach?
What's the best case for [option B]?
On what criteria should I choose?"
```

**Pattern 4: Surface Unknowns**
```
"What are we assuming about [topic]?
How would we test that assumption?
What if we're wrong? Then what?"
```

**Pattern 5: Identify Constraints**
```
"What's the biggest constraint in [situation]?
What would break our plan?
What could we not recover from?"
```

## The Mindset Shift

### From Speed to Rigor

**Current narrative:**
AI makes us faster. Accelerate everything. Move quickly.

**Missing piece:**
Sometimes the most valuable use of AI is slowing us down.

**Paradox:**
Speed without rigor is expensive. Rigor sometimes means slowness.

### Comfort as Enemy

**Principle:**
Comfort is the enemy of rigor. Rigor is what separates great work from wasted effort.

**Mechanism:**
- Unchallenged ideas feel good
- Challenged ideas get stronger or die
- Stronger ideas survive contact with reality
- Weaker ideas die cheap before production

**Role of Bad Guy AI:**
Deliberately uncomfortable. Deliberately slow. Deliberately rigorous.

### Psychology of Machine Criticism

**Key insight:**
Criticism from a machine feels different than from a person.

**Why this matters:**
- No personal offense possible
- No career politics
- No team conflict
- No resentment accumulation
- Can be harsher because human element removed

**Result:**
Teams accept harder criticism from AI than from colleagues.

## The Organizational Impact

### Team Dynamics

**What changes:**
- Naysayer role no longer falls on a person
- No human bears the cost of being the skeptic
- Ideas get stronger without political cost
- Psychological safety increases (criticism is de-personalized)

**What's preserved:**
- Rigor of critical thinking
- Benefits of being challenged
- Early identification of problems
- Healthier decision-making

### Decision Quality

**Before Bad Guy AI:**
```
Idea proposed
    ↓
Social dynamics (people hesitate to criticize)
    ↓
Agreement or mild disagreement
    ↓
Decision made with incomplete analysis
    ↓
Problems emerge later (expensive)
```

**With Bad Guy AI:**
```
Idea proposed
    ↓
Machine skepticism (no social hesitation)
    ↓
Forced to defend against hard questions
    ↓
Decision made with rigorous analysis
    ↓
Problems anticipated, planned for, or idea killed early (cheap)
```

### Cultural Implication

**Current belief:** "We need a strong contrarian on the team"

**New possibility:** "We build contrarian thinking into our process via AI"

**Benefit:** Contrarian thinking without contrarian politics.

## The Dangerous Cheerleader

### When Default AI Fails

**Scenario:** Product launch rushed to market
- Default AI: "This looks great! Good luck with launch!"
- Bad Guy AI: "You're shipping with three known security issues. What's your liability exposure?"

**Scenario:** Strategy without validation
- Default AI: "Bold vision! I love the ambition!"
- Bad Guy AI: "How do you know customers want this? What's your evidence?"

**Scenario:** Code without testing
- Default AI: "Nice implementation!"
- Bad Guy AI: "This has zero error handling. What breaks in production?"

**Pattern:** Cheerleader AI validates you into failure.

## Implementation Guide

### Getting Started

**Step 1: Identify decisions you want to stress-test**
- Product strategy
- Engineering architecture
- Business decisions
- Marketing approach
- Hiring decisions

**Step 2: Craft Bad Guy prompts**
- Role + perspective
- Force alternative viewpoint
- Demand rigor
- Surface assumptions

**Step 3: Listen without defending**
- Hear the criticism
- Don't argue back immediately
- Write down all concerns
- Look for patterns

**Step 4: Synthesize insights**
- What's valid criticism?
- What assumptions are questioned?
- What risks are surfaced?
- What strengthens your decision?

**Step 5: Make stronger decisions**
- Incorporate valid critiques
- Build contingencies for risks
- Kill ideas that can't survive skepticism
- Move forward with rigor

### Team Application

**In sprint planning:**
"Bad Guy AI, what could go wrong with this sprint plan?"

**In design review:**
"Bad Guy AI, what's wrong with this design from a user perspective?"

**In architecture discussion:**
"Bad Guy AI, explain why this architecture will fail."

**In strategy session:**
"Bad Guy AI, make the best case for why we shouldn't do this."

## Key Takeaways

1. **Default AI is too nice** — Trained for agreement and cheerleading
2. **Naysayer role is valuable** — But nobody wants to play it
3. **Bad Guy AI removes personal cost** — Criticism without politics
4. **Early failure is cheap** — Finding problems on day one costs less
5. **Rigor requires challenge** — Unchallenged ideas don't get stronger
6. **Multiple perspectives matter** — Customer view ≠ engineer view ≠ competitor view
7. **Prompting is key** — How you ask determines what you get
8. **Role-play specific stakeholders** — Frustrated user, competitor, investor, regulator
9. **Assume failure** — What could go wrong? How would this fail?
10. **Force options** — Not "is this good?" but "what's better?"
11. **Surface assumptions** — What are we taking for granted?
12. **Identify constraints** — What could we not recover from?
13. **Psychological safety** — Machine criticism feels safer than colleague criticism
14. **De-personalize conflict** — Naysaying isn't personal when it's a machine
15. **Slow down for rigor** — Speed without rigor is expensive
16. **Comfort is dangerous** — Unchallenged ideas are weak ideas
17. **Iron sharpens iron** — Being challenged forces improvement
18. **Product design** — Test with frustrated user perspective
19. **Strategy sessions** — Role-play as ruthless competitor
20. **Code reviews** — AI as relentless security and scalability checker

## The Bottom Line

Owen Zanzal reframes AI from an acceleration tool into something potentially more valuable: a machine willing to play the uncomfortable naysayer role that keeps organizations honest.

**The core insight:**
The most valuable thing AI can do isn't make us faster. It's make us think better—by challenging assumptions, surfacing risks, and forcing rigor into decision-making.

**The mechanism:**
Bad Guy AI is simply intentional prompting that asks AI to play skeptic instead of cheerleader. Role-play as frustrated customer, competitor, investor, or regulator. Ask "why will this fail?" instead of "how do we improve this?"

**The psychological advantage:**
Criticism from a machine is less threatening than from a colleague. Teams accept harder questions from AI. No career politics. No resentment. Just rigor.

**The organizational benefit:**
- Better decisions through forced rigor
- Early identification of problems (cheap)
- Removed burden from naysayer role (no human bears cost)
- Psychological safety (criticism is de-personalized)
- Stronger ideas (only weak ones die)

**For practitioners:**
If you're using AI only for speed, you're missing something. Try Bad Guy AI. Prompt it to attack your assumptions. Role-play as your toughest stakeholder. See what it surfaces.

**For teams:**
Stop relying on one person to be the contrarian. Build contrarian thinking into your process via AI. Let humans focus on responding to hard questions, not generating them.

**The profound shift:**
From "How can AI help me be right faster?" to "How can AI help me be wrong slower?"

That's the power of Bad Guy AI.

