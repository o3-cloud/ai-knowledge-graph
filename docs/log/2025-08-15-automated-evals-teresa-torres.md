---
summary: Teresa Torres (PM) shares her journey building an AI Interview Coach—from manual "vibe checking" to sophisticated automated evaluation framework, covering practical tools (Airtable, Jupyter, Claude, VS Code), LLM-as-Judge vs. code-based assertions, and PM-engineer collaboration on AI products
event_type: video
sources:
    - https://www.youtube.com/watch?v=N-qAOv_PNPc
tags:
    - evaluations
    - evals
    - AI-products
    - product-management
    - LLM-as-judge
    - testing-AI
    - AI-interview-coach
    - annotations
    - evaluation-frameworks
---

# From Noob to Automated Evals In A Week (as a PM) w/ Teresa Torres

**Speaker:** Teresa Torres (Product Management Expert)
**Host:** Hamel Husain
**Platform:** YouTube
**Duration:** ~70 minutes
**Publication Date:** August 15, 2025

## Overview

Teresa Torres shares her journey building an "AI Interview Coach" and developing a sophisticated automated evaluation framework—starting from manual "vibe checking" responses and evolving into a production evaluation system. The talk covers practical tools, evaluation strategies, PM-engineer collaboration, and key learnings about building AI products without deep technical background.

## The Origin Story

### The Problem

**What Teresa was doing:**
- Manually reviewing AI interview coaching responses
- Subjectively assessing quality ("vibe checking")
- Making decisions based on feel
- No systematic approach to quality
- Difficult to scale evaluation

**The realization:**
This manual process won't work for production. Need systematic, automated way to evaluate AI outputs.

### The Goal

**What she built:**
An automated evaluation framework that can assess AI responses systematically at scale.

**Timeline:**
Built from scratch to production-ready in approximately one week.

**Key insight:**
A product manager with no ML background built sophisticated evals using standard tools and clever thinking.

## Building an AI Interview Coach

### The Product Vision

**What it does:**
Provides AI-powered coaching for interview preparation—helping people practice and improve their interview skills.

**How it works:**
1. User responds to interview question
2. AI coach provides feedback
3. User can ask follow-up questions
4. System tracks improvement

**Quality matters because:**
Bad feedback actually hurts user development
Good feedback improves interview performance

### Evaluation Challenge

**The question:**
How do you know if your AI coach is actually helpful?

**Why it's hard:**
- No single "right" answer to interview questions
- Quality is subjective and contextual
- Varies by role, company, culture
- Need to assess helpfulness, not just correctness

**Solution:**
Build evaluation framework that captures quality dimensions.

## From Manual to Automated

### Phase 1: Manual Vibe Checking

**Approach:**
- Read responses manually
- Assess subjectively
- Make notes
- Compare examples

**Problems:**
- Doesn't scale
- Inconsistent criteria
- Time-consuming
- Hard to track changes
- Difficult to identify patterns

### Phase 2: Structured Traces

**Tool:** Airtable

**What she did:**
- Created Airtable base for traces
- Stored request, response, metadata
- Annotated results manually
- Tracked patterns

**Benefits:**
- Organized data
- Easy to reference
- Enables manual annotation
- Visible patterns emerge

**Limitation:**
Still manual annotation work

### Phase 3: Systematic Evaluation

**Realization:**
Need structured, repeatable evaluation process.

**Approach:**
1. Define what "good" means
2. Create test cases
3. Build evals
4. Run systematically
5. Iterate on results

## Design and Evaluation Tools

### Airtable for Annotation

**Structure:**
- Column for each evaluation dimension
- Checkboxes for pass/fail
- Comments for notes
- Tags for categorization

**Benefits:**
- Easy to view all results
- Can sort and filter
- Non-technical team can use
- Tracks history

**Use case:**
Initial data collection and manual annotation.

### Jupyter Notebooks for Analysis

**What Teresa used:**
Jupyter for analyzing evaluation results.

**Capabilities:**
- Load data from Airtable
- Compute statistics
- Visualize patterns
- Develop understanding

**Key insight:**
Jupyter provides executable analysis that can be shared and documented.

### Python for Analysis

**Learning journey:**
- No prior Python experience
- Learned while building
- Used ChatGPT to help
- Focused on practical analysis

**Key learnings:**
- Python is accessible
- ChatGPT makes it faster
- Practical need drives learning
- PM can do analysis

## Evaluation Strategies

### Type 1: LLM-as-Judge

**What it is:**
Use another LLM to evaluate outputs from your LLM.

**Process:**
```
User Response → Your AI Coach
    ↓
Your AI Coach Response → Judge LLM
    ↓
Judge LLM Assessment → Score/Feedback
```

**Advantages:**
- Flexible evaluation
- Can assess subjective qualities
- Captures nuance
- Works for open-ended tasks

**Challenges:**
- Judge can be inconsistent
- Prompt-dependent results
- Requires validation
- Can be expensive

**Example:**
"Given this interview question and response, rate how helpful the coaching feedback is on a 1-5 scale."

### Type 2: Code-Based Assertions

**What it is:**
Hard-coded rules that check for specific conditions.

**Examples:**
```python
# Check length
assert len(response) > 100, "Response too short"

# Check for keywords
assert "example" in response.lower(), "No concrete examples"

# Check structure
assert response.count("\n") > 2, "Not well-structured"
```

**Advantages:**
- Deterministic
- Fast
- Cheap
- Easy to understand
- Highly reliable

**Challenges:**
- Only captures explicit criteria
- Misses subjective quality
- Brittle (easily broken by minor variations)
- Limited to rule-based checks

**When to use:**
- Clear, objective criteria
- Speed critical
- Cost sensitive

### Type 3: Hybrid Approach

**Best practice:**
Combine LLM-as-Judge with code-based assertions.

**Pattern:**
```
Code assertions (objective criteria)
    ↓
Pass? → Fast path (done)
Fail? → Manual review or LLM-as-Judge
    ↓
LLM assessment (subjective criteria)
```

**Benefits:**
- Fast for obvious cases
- Thorough for edge cases
- Cost-effective
- Reliable results

## Building Evaluation Examples

### Define Quality Dimensions

**For interview coaching:**
- Helpfulness: Does feedback improve performance?
- Relevance: Is feedback on-topic?
- Constructiveness: Is it actionable?
- Specificity: Does it include examples?
- Tone: Is it encouraging?

**For each dimension:**
- Define what good looks like
- Create evaluation rules
- Test against examples

### Create Test Cases

**Approach:**
1. Collect diverse examples
2. Manually evaluate
3. Identify patterns
4. Create test cases

**Example test case:**
```
Input: "I froze during my technical interview"
Expected output should:
- Acknowledge the challenge
- Provide coping strategies
- Suggest practice approaches
- End encouragingly
```

### Implement Evals

**In code:**

```python
def eval_helpfulness(response):
    # Check for actionable advice
    actionable_keywords = ["practice", "try", "consider", "approach"]
    has_action = any(keyword in response.lower()
                     for keyword in actionable_keywords)

    # Check for specificity
    has_examples = "example" in response.lower()

    return has_action and has_examples

def eval_tone(response):
    # Check for encouraging language
    positive_indicators = ["great", "progress", "improve", "strength"]
    positivity = sum(1 for word in positive_indicators
                     if word in response.lower())

    return positivity >= 2
```

### Iterate and Improve

**Process:**
1. Run evals on current system
2. Analyze failures
3. Refine evaluation logic
4. Re-run and compare
5. Deploy improved system

## Custom Tooling

### VS Code and Extensions

**What Teresa used:**
VS Code as development environment.

**Useful extensions:**
- Python extension
- Jupyter extension
- Git integration
- Code formatting

**Benefits:**
- Familiar to engineers
- Powerful debugging
- Good integration
- Easy collaboration

### Custom Annotation Tool

**Problem:**
Need efficient way for team to review and annotate eval results.

**Solution:**
Built custom annotation tool using Claude.

**Process:**
1. Defined requirements
2. Used Claude to generate code
3. Customized for use case
4. Team used for annotation

**Benefits:**
- Tailored to workflow
- Easy for team
- Captures structured feedback
- Enables collaboration

### Investigation Notebook

**Purpose:**
Systematic investigation of eval failures.

**Contents:**
- Load failure cases
- Analyze patterns
- Visualize distribution
- Identify root causes
- Test hypotheses

**Benefits:**
- Executable analysis
- Shareable with team
- Documents thinking
- Enables iteration

## Key Learnings

### Learning Python as PM

**Journey:**
- No prior experience
- Learned while building
- Used ChatGPT extensively
- Focused on practical problems

**Key insights:**
1. **ChatGPT is a great teacher** — Ask specific questions, learn interactively
2. **Practical motivation drives learning** — Learning to solve real problems
3. **Start small** — Build understanding incrementally
4. **PMs can absolutely code** — At least data analysis and automation
5. **Tools are accessible** — No need to be "real programmer"

### Building with Claude

**Experience:**
Used Claude to generate and refine code.

**Benefits:**
- Fast prototyping
- Customizable output
- Interactive refinement
- Learn from generated code

### From Personal to Production

**Evolution:**
```
Personal project (manual)
    ↓
Structured traces (Airtable)
    ↓
Automated evals (code)
    ↓
Custom tooling (production)
    ↓
Team workflow (scaled)
```

**Key transition points:**
- When manual annotation becomes burden
- When patterns become clear
- When code-based evals emerge
- When team needs to participate

## PM-Engineer Collaboration

### Different Perspectives

**PM perspective:**
- User value
- Product decisions
- Quality assessment
- Success metrics

**Engineer perspective:**
- Implementation
- Scalability
- Infrastructure
- Technical feasibility

### Effective Collaboration on AI Products

**What works:**
1. **Clear evaluation criteria** — PMs define what "good" means
2. **Shared ownership** — Both own quality
3. **Iterative development** — Build together, learn together
4. **Engineer input on feasibility** — Technical constraints matter
5. **PM input on value** — User need matters

**Example workflow:**
```
PM: "AI should be more constructive"
Engineer: "How do we measure constructive?"
PM: "Does it suggest next steps?"
Engineer: "Let's build eval for that"
Run eval, analyze results, iterate
```

### Communication Patterns

**Good:**
- PM describes desired user outcome
- Engineer suggests technical approach
- Both validate against success criteria
- Iterate based on data

**Avoid:**
- PM dictates implementation
- Engineer makes product decisions alone
- Guessing instead of measuring
- Not involving team in problem definition

## Practical Insights

### Don't Need Deep ML Knowledge

**Key insight:**
Building effective AI products doesn't require ML expertise.

**Why:**
- Standard tools are sufficient
- Problem-solving > algorithms
- Measurement > theory
- Iteration > perfection

**Implication:**
Talented PMs and engineers can build sophisticated AI products without ML specialization.

### Evaluation is Product Work

**Realization:**
Evaluation isn't research—it's core product development.

**Why:**
- Determines if product works
- Guides improvement
- Informs decisions
- Defines quality bar

**Result:**
Both PMs and engineers should be comfortable with evaluation design.

### Tooling Matters

**Observation:**
Right tools make work much easier.

**Examples:**
- Airtable for structured annotation
- Jupyter for exploration
- Claude for code generation
- Custom tools for workflows

**Principle:**
Invest in tooling that fits your workflow.

## Question and Answer Insights

### Capturing User Feedback

**Challenge:**
How do you collect feedback from end users?

**Approaches:**
- In-app feedback mechanisms
- User surveys
- Observation of usage patterns
- Direct interviews
- Support ticket analysis

**Key:**
Make it easy for users to provide feedback.

### Technical Background Necessity

**Answer:**
No. You can build sophisticated AI products without it.

**What matters:**
- Problem-solving skills
- Learning ability
- Clear thinking
- Persistence
- Collaboration

**Learning happens:**
On the job, with mentorship, through practice.

### Next Steps for Teresa

**Future direction:**
Helping other PMs learn to build evals.

**Why:**
- Critical skill
- Often missing
- Learnable
- High impact

## Key Takeaways

1. **Start simple, evolve systematically** — Manual to automated progression
2. **Measurement drives improvement** — You can't improve what you don't measure
3. **Both LLM-as-Judge and code assertions have roles** — Use both where appropriate
4. **PMs can build sophisticated systems** — Doesn't require deep ML knowledge
5. **Right tools amplify productivity** — Choose based on workflow
6. **Clear evaluation criteria matter** — Define what "good" means explicitly
7. **Documentation in code is shareable** — Jupyter notebooks, custom tools
8. **User feedback is critical** — Build evaluation from user experience
9. **Collaboration requires clear communication** — PM and engineer perspectives both matter
10. **This is learnable** — Anyone motivated can build evals

## The Bottom Line

Teresa Torres' journey from manual "vibe checking" to automated evaluation framework demonstrates that sophisticated AI product development is accessible to skilled PMs without deep ML expertise. The key insights are:

**Evaluation progression:** Start with manual assessment, move to structured traces, implement code-based and LLM-as-Judge evals, and build custom tooling for team workflows.

**Tool selection:** Use accessible tools (Airtable, Jupyter, Claude) that fit your workflow rather than specialized ML infrastructure.

**Measurement focus:** Define what quality means, build evals to measure it, run systematically, and improve based on data.

**Collaboration model:** PMs and engineers bring different perspectives. PM defines user value; engineer suggests technical approaches. Both own quality.

**Accessibility:** Building sophisticated AI products doesn't require ML degrees. It requires clear thinking, good tools, and systematic iteration.

The broader implication is that as AI products become central to business, PM and engineer competency in evaluation becomes table-stakes. This isn't specialized research work—it's core product development. Organizations that elevate evaluation from afterthought to central practice will build better AI products faster.
