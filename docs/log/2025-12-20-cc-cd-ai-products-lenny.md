---
summary: Reganti & Badam introduce CC/CD (Continuous Calibration/Continuous Development)—a framework for AI products that acknowledges non-determinism and agency-control tradeoffs, replacing traditional software development cycles
event_type: article
sources:
    - https://www.lennysnewsletter.com/p/why-your-ai-product-needs-a-different
tags:
    - AI-products
    - product-development
    - CC/CD-framework
    - continuous-calibration
    - AI-versioning
    - agency
    - non-determinism
    - evaluation-metrics
---

# Why Your AI Product Needs a Different Development Lifecycle: The CC/CD Framework

**Authors:** Aishwarya Reganti, Kiriti Badam
**Publication:** Lenny's Newsletter
**Publication Date:** December 20, 2025

## Overview

Aishwarya Reganti and Kiriti Badam introduce the Continuous Calibration/Continuous Development (CC/CD) framework—a development approach specifically designed for AI-powered products. They argue that AI products fundamentally differ from traditional software, requiring different development, testing, and deployment strategies. The CC/CD framework provides methodology for building reliable AI products while managing unpredictability and autonomy.

## The Problem: AI Products Are Different

### Why Traditional Development Breaks Down

**Traditional software (CI/CD):**
- Deterministic behavior
- Tests verify correctness
- Version by features
- Deploy with confidence
- Bug → Fix → Done

**AI products:**
- Non-deterministic behavior
- Tests can't guarantee correctness
- Agency level unknown
- Deploy with uncertainty
- Behavior emerges unpredictably

### Two Fundamental Differences

#### 1. Non-Determinism

**Input side:**
- Users provide open-ended prompts
- Same input sometimes yields different outputs
- Behavior varies based on state and context
- No single "correct" behavior

**Output side:**
- Systems generate varied responses
- Multiple valid answers possible
- Quality subjective and contextual
- Not reducible to pass/fail

**Implication:**
Traditional testing (deterministic inputs → expected outputs) doesn't work.

#### 2. Agency-Control Tradeoff

**More agency means:**
- Fewer human constraints
- Faster execution
- More autonomy
- Less control

**More control means:**
- Human oversight required
- Slower execution
- Less autonomy
- More safety

**The reality:**
Every increase in autonomy sacrifices control. Must be earned through demonstrated reliability.

**Key principle:**
"Agency is earned over time, not granted all at once."

## The CC/CD Framework

### Two Phases, Six Steps

```
Continuous Development (Planning)
├─ Step 1: Scope capability & curate data
├─ Step 2: Minimal viable application
└─ Step 3: Design evaluation metrics
    ↓
Continuous Calibration (Operations)
├─ Step 4: Run evaluations on live data
├─ Step 5: Analyze behavior patterns
└─ Step 6: Apply targeted fixes
```

### Phase 1: Continuous Development

#### Step 1: Scope Capability and Curate Reference Data

**What:**
Define exactly what the AI system will do and gather reference examples.

**Process:**
- Define specific capability
- Gather reference data (examples of desired behavior)
- Document decision criteria
- Establish success baseline

**Why it matters:**
- Clarity on scope prevents drift
- Reference data enables evaluation
- Success criteria are explicit
- Baseline enables measurement

**Example:**
```
Capability: Summarize customer feedback
Reference data: 50 feedback items with good summaries
Success criteria: Summary preserves key issues, <100 words
Baseline: Acceptable summary quality 75% of time
```

#### Step 2: Set Up Minimal Viable Application

**What:**
Build the simplest version of your product with highest control, lowest agency.

**Characteristics:**
- High human involvement
- Clear guardrails
- Explicit rules where possible
- Human approval for important decisions
- Conservative defaults

**Why it matters:**
- Test system safely before autonomy
- Establish baseline quality
- Identify edge cases
- Build user trust
- Manage risk

**Example:**
```
AI suggests action → Human reviews → Human approves → Action takes
(No autonomous action until system proven reliable)
```

#### Step 3: Design Evaluation Metrics

**What:**
Create metrics to assess AI behavior quality and safety.

**Metrics to design:**
- Quality metrics (does it work well?)
- Safety metrics (is it reliable?)
- User metrics (do users trust it?)
- Business metrics (does it create value?)

**Characteristics:**
- Automatable evaluation
- Realistic scenarios
- Edge cases included
- Measurable
- Actionable

**Why it matters:**
- Enables continuous assessment
- Detects degradation
- Guides improvement
- Justifies autonomy increase

### Phase 2: Continuous Calibration

#### Step 4: Run Evaluations on Live Data

**What:**
Continuously test system behavior against real usage patterns.

**Process:**
- Use real user interactions
- Evaluate against metrics
- Gather failure cases
- Identify patterns
- Compare to baseline

**Why it matters:**
- Real data reveals issues
- Production patterns differ from test
- Continuous monitoring catches regressions
- Live feedback informs improvement

#### Step 5: Analyze Behavior Patterns

**What:**
Understand why system behaves as it does—successes and failures.

**Analysis:**
- Success patterns (what works well)
- Failure patterns (what goes wrong)
- Edge cases (unusual scenarios)
- Systematic issues (reoccurring problems)
- Root causes (why failures happen)

**Why it matters:**
- Understand before fixing
- Target improvements effectively
- Prevent common mistakes
- Build system intuition

#### Step 6: Apply Targeted Fixes

**What:**
Make focused improvements based on analysis.

**Types of fixes:**
- Prompt refinement
- Data curation
- Guardrail addition
- Process adjustment
- Feature restriction
- Capability expansion

**Why it matters:**
- Targeted fixes are efficient
- Continuous improvement loops
- Avoid major redesigns
- Preserve working aspects
- Incrementally increase capability

## Versioning by Agency Level

### Rethinking Versions

**Traditional versioning:**
```
v1.0 → v1.1 → v1.2 → v2.0
(Feature → Feature → Feature → Major Feature)
```

**AI product versioning:**
```
V1 (Low Control)   → V2 (Medium Control) → V3 (High Autonomy)
(User decides)       (Suggestions+Review)  (Autonomous action)
```

### Agency Progression Example

**Capability: Content Moderation**

**V1 - High Control, Low Agency:**
- AI flags potentially problematic content
- Human reviewer makes decision
- Human takes action

**V2 - Medium Control, Medium Agency:**
- AI flags and applies low-risk actions
- Human reviews edge cases
- AI handles clear-cut cases

**V3 - Low Control, High Agency:**
- AI handles all cases autonomously
- Human monitoring only
- Escalation for unusual situations

### Why This Matters

**Risk management:**
- Start safe
- Build confidence
- Prove reliability
- Earn autonomy

**User trust:**
- Visible human control
- Gradual autonomy increase
- Predictable behavior
- Safety assurance

**System improvement:**
- Identify failures early
- Fix before scaling
- Establish patterns
- Optimize systematically

## Key Operational Practices

### Continuous Evaluation

**What:**
Ongoing assessment of system behavior.

**Frequency:**
- Daily for critical systems
- Weekly for standard systems
- Real-time for important metrics

**Actions:**
- Alert on regressions
- Track improvement
- Celebrate successes
- Escalate issues

### Targeted Calibration

**What:**
Focused improvements based on evaluation findings.

**Process:**
1. Identify failure patterns
2. Understand root cause
3. Apply targeted fix
4. Re-evaluate
5. Iterate

**Avoid:**
- Major rewrites
- Overcomplication
- Losing working functionality
- Stopping iteration

### User Feedback Integration

**What:**
Incorporate user experience into evaluation and calibration.

**Mechanisms:**
- Explicit feedback tools
- Usage pattern analysis
- Support tickets
- Surveys
- Qualitative research

**Why it matters:**
- Users experience system differently
- Real pain points emerge
- Priorities clarified
- Trust built through responsiveness

## Non-Determinism: Managing Unpredictability

### Accepting Variability

**Reality:**
- Same input may yield different outputs
- Multiple correct answers exist
- Quality varies contextually
- Perfect consistency impossible

**Not a bug:**
- This is inherent to LLMs
- Can't be "fixed" away
- Must be designed for

**Design approach:**
- Set acceptable variance range
- Monitor distribution
- Provide human review for edge cases
- Accept some variability as feature, not bug

### Evaluation Strategy for Non-Determinism

**Not:**
- Expecting deterministic behavior
- Testing specific outputs
- Demanding consistency

**But:**
- Testing behavior distribution
- Evaluating quality ranges
- Accepting variation
- Monitoring for degradation

### Example: Customer Service AI

**Deterministic thinking (wrong):**
"Input X → Output Y" (always)

**Non-deterministic thinking (right):**
"Input X → Various good responses" (varies)
Success = quality distribution acceptable

## Agency-Control Tradeoff in Practice

### Defining Control Levels

**High Control (Low Agency):**
- User makes decision
- AI provides support
- System suggests action
- Human approves action

**Medium Control (Medium Agency):**
- AI decides with guardrails
- Humans review edge cases
- Clear rules for autonomy
- Escalation for uncertain cases

**Low Control (High Agency):**
- AI decides autonomously
- Limited human oversight
- Exception-based review
- Trust in system reliability

### Testing Before Autonomy

**Must test:**
- System reliability at current level
- Edge case handling
- Error recovery
- User experience
- Safety and security

**Before advancing to:**
- Higher autonomy
- Fewer controls
- Larger scale
- More critical decisions

**Process:**
- Prove reliability → Increase agency
- Failure → Fix → Re-test → Retry
- Never rush autonomy increase

## Key Takeaways

1. **AI products differ fundamentally** — Non-determinism and agency-control tradeoffs
2. **CC/CD framework designed for AI** — Six steps across development and calibration
3. **High control first** — Start with high human oversight
4. **Agency earned not granted** — Prove reliability before increasing autonomy
5. **Continuous evaluation essential** — Ongoing assessment of behavior
6. **Version by agency level** — Progress from control to autonomy
7. **Targeted calibration** — Focused improvements based on data
8. **Accept variability** — Non-determinism is inherent, not bug
9. **User feedback critical** — Real experience informs improvement
10. **Manage tradeoffs explicitly** — Control vs. autonomy is fundamental choice

## The Bottom Line

Aishwarya Reganti and Kiriti Badam's CC/CD framework acknowledges a fundamental truth: AI products require different development approaches than traditional software. Non-deterministic behavior and agency-control tradeoffs make traditional testing and versioning inadequate.

The CC/CD approach addresses this through six steps spanning continuous development (scope capability, build MVP, design metrics) and continuous calibration (evaluate live, analyze patterns, apply fixes). Rather than deploying finished features, AI products must start with high control, build confidence through evaluation, and gradually increase autonomy as reliability is proven.

The key insight is versioning by agency level rather than features. A capability progresses from high-control low-agency (human decides, AI supports) to medium-control medium-agency (AI decides on clear cases, human reviews edge cases) to low-control high-agency (autonomous operation with monitoring). This progression allows systematic de-risking while building user trust.

The framework doesn't eliminate the challenges of non-determinism and agency-control tradeoffs—it acknowledges them and provides methodology for managing them. Success requires accepting variability as inherent, evaluating behavior distribution rather than specific outputs, proving reliability before increasing autonomy, and maintaining continuous evaluation and improvement cycles.

Organizations that adopt CC/CD thinking will build more reliable, trustworthy AI products than those applying traditional software development practices to inherently different systems.
