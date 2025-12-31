---
summary: Comprehensive framework for effective AI-assisted coding that emphasizes structured discipline, human oversight, and maintaining developer accountability while leveraging LLM capabilities across the development lifecycle.
event_type: research
sources:
    - https://addyo.substack.com/p/my-llm-coding-workflow-going-into
tags:
    - llm-coding
    - ai-workflow
    - developer-practices
    - code-quality
    - ai-assisted-development
    - automation
---

# My LLM Coding Workflow Going Into 2025

**Author:** Addy Osmani
**Source:** Substack
**Context:** Best practices for AI-assisted development at scale

## Core Insight

Successful AI-assisted coding requires **structured discipline rather than autonomous automation**. Despite impressive capabilities, AI coding assistants remain fundamentally tools requiring human verification and oversight.

**Key observation:** At Anthropic, ~90% of Claude Code's codebase is written by Claude Code itself, yet the process remains "difficult and unintuitive" and demands constant human judgment.

## The 10-Step Workflow

### 1. Planning First
- Create detailed specifications before touching code
- Define requirements, constraints, and acceptance criteria
- Establish clear success metrics
- **Why:** AI performs better with explicit intent than vague exploration

### 2. Break Into Chunks
- Divide projects into focused, manageable tasks
- Each task should be completable in one AI interaction
- Avoids cognitive overload and easier verification
- **Why:** Smaller scopes = better AI reasoning and human review

### 3. Provide Context
- Feed AI relevant code, documentation, and constraints
- Include architectural patterns and style guides
- Share existing implementations as reference patterns
- **Why:** Context determines output quality; poor context = poor outputs

### 4. Choose Right Tools
- Select models appropriate to task complexity
- Use faster models for routine work, advanced models for reasoning
- Consider cost/latency tradeoffs
- **Why:** Every task has optimal tooling; matching matters

### 5. Leverage Automation
- Deploy AI agents across development lifecycle
- Use for code generation, testing, refactoring, documentation
- Automate repetitive scaffolding work
- **Why:** Agents can handle volume that overwhelms human developers

### 6. Maintain Human Oversight
- Verify all AI-generated code before shipping
- Review for correctness, security, and style alignment
- Challenge AI assumptions when needed
- **Why:** Developers own the code; AI assistance doesn't transfer responsibility

### 7. Version Control Discipline
- Commit frequently with clear, descriptive messages
- Use branching strategies for AI experiments
- Track what changed and why
- **Why:** Accountability and traceability for AI-generated changes

### 8. Customize Behavior
- Provide explicit style guides and preferences
- Define architectural constraints and patterns
- Create AI personas for specific roles (reviewer, architect, etc.)
- **Why:** AI adapts to explicit guidance; consistency improves quality

### 9. Integrate Testing
- Embed automated checks throughout the pipeline
- Use CI/CD to catch AI mistakes automatically
- Maintain strong test suites as safety nets
- **Why:** Automation is faster and more reliable than human verification

### 10. Continuous Learning
- Treat each AI interaction as a learning opportunity
- Refine prompts and context based on results
- Document what works and what doesn't
- **Why:** Skill with AI tools is learnable; iteration improves outcomes

## The Mental Model: "Over-Confident Junior Developer"

Frame AI coding assistants as intelligent but sometimes wrong. Like a junior developer:
- They need direction and context
- They make plausible but incorrect decisions
- They require verification and oversight
- They improve with feedback
- They should not be trusted without review

**Contrast:** Don't treat AI as a "finished product" or as a replacement for developer judgment.

## Practical Techniques

### Git Worktrees for Experimentation
- Create parallel branches to explore AI suggestions
- Compare different approaches before committing
- Enables safe experimentation without main branch pollution

### CI/CD as Safety Net
- Automated tests catch AI mistakes faster than humans
- Linting enforces style consistency automatically
- Build failures prevent bad code from shipping
- Coverage reports show untested AI-generated paths

### Code Review Practices
- Review AI code the same way you'd review human code
- Look for logical correctness, not just syntax
- Verify security implications
- Challenge performance assumptions
- Ask: "Would I accept this from a human junior?"

### Style Guides and Preferences
- Provide explicit formatting rules
- Define naming conventions
- Specify architectural patterns
- Give examples of preferred vs. discouraged approaches

## What This Is NOT

- **Not magic:** AI doesn't replace developer skill; it amplifies it
- **Not autonomous:** Human judgment remains essential at every stage
- **Not faster by default:** Poor workflows can slow you down significantly
- **Not about code generation speed:** Real productivity is about understanding + quality
- **Not a substitute for fundamentals:** You still need to understand what you're building

## What This IS

- **A disciplined practice:** Requires structured approach, not freestyle prompting
- **A way to amplify capability:** Leverage AI for volume while maintaining quality
- **Developer-centric:** Human judgment remains central to decision-making
- **Evolutionary:** Improves through iteration and learning
- **Quality-first:** Speed comes from smart automation, not corner-cutting

## Developer Accountability

The critical point: **Developers remain fundamentally accountable for shipped code.**

- AI can generate code faster than humans can write it
- But humans must verify that code works, is secure, and aligns with architecture
- This responsibility can't be delegated to the AI
- It can only be accelerated by better tools and processes

## Connection to Engineering Discipline

This workflow aligns with core software engineering principles:

1. **Planning before implementation** (not reactive coding)
2. **Breaking complex work into smaller pieces** (decomposition)
3. **Providing clear specifications** (requirements discipline)
4. **Continuous verification** (testing and review)
5. **Version control and accountability** (traceability)
6. **Learning from results** (iteration and improvement)

AI doesn't eliminate these principles; it makes them more important. Tools that generate code faster require *more* discipline, not less.

## Related Concepts

This workflow connects directly to:
- `2025-12-27-death-and-rebirth-of-programming.md` - Understanding and architecture become the bottleneck, not code writing
- `2025-12-27-agent-readiness-framework.md` - Environments must support AI collaboration with explicit context and intent
- `2025-12-27-ai-changes-software-engineering.md` - The engineering loop (Plan → Implement → Verify) remains constant; AI accelerates latency
- `2025-12-27-how-chatgpt-influences-language.md` - Awareness that tools shape output; need intentional practices to maintain control

## Key Metrics for Success

Instead of measuring:
- Lines of code generated per hour
- Time from prompt to code

Measure:
- Code quality (bugs caught in review/testing)
- Shipping velocity (complete features working in production)
- Team satisfaction (is AI helping or adding friction?)
- Maintainability (can the team understand and modify the code?)
- Developer skill growth (are team members getting better at using AI tools?)

## Practical Starting Points

**For solo developers:**
1. Start with one task: refactor an existing function with AI assistance
2. Practice the 10-step workflow on small scope
3. Reflect on what worked and what didn't
4. Expand to larger tasks as confidence grows

**For teams:**
1. Establish shared style guides and architectural patterns
2. Set up CI/CD pipelines to catch quality issues
3. Create code review practices for AI-generated code
4. Document what works for your codebase
5. Build organizational knowledge about effective AI use

**Against common pitfalls:**
- Don't use AI for things you don't understand (it's code, you own it)
- Don't skip planning phase (context determines everything)
- Don't treat AI as finished product (always verify)
- Don't let speed pressure eliminate quality checks
- Don't forget that humans remain accountable

## The Uncomfortable Truth

The easiest way to use AI is recklessly (generate fast, ship without review). The right way is more disciplined (plan carefully, generate thoughtfully, verify thoroughly). Speed comes from discipline, not from skipping steps.

## Open Questions

1. How do we train developers to maintain this discipline as AI capabilities improve?
2. What team structures and processes work best for AI-assisted development?
3. How do we prevent speed pressure from undermining quality discipline?
4. How does this scale to distributed teams with varying skill levels?
5. What role should organizational culture play in defining AI coding practices?

## One Last Insight

"~90% of code for Claude Code is written by Claude Code itself" sounds like autonomous development. But the reality is: "the process remains difficult and unintuitive." This paradox reveals the actual truth: **AI can generate vast amounts of code, but human judgment about whether that code is right remains irreplaceable.**

The future of AI-assisted development isn't about removing humans; it's about equipping humans with tools that let them reason faster and build bigger things while maintaining full accountability for quality.
