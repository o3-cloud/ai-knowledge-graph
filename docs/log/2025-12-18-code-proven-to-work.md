---
summary: Simon Willison argues developers must prove their code works before submission, emphasizing manual testing, automated testing, and human accountability in professional development
event_type: article
sources:
    - https://simonwillison.net/2025/Dec/18/code-proven-to-work/
tags:
    - code-quality
    - testing
    - code-review
    - developer-responsibility
    - AI-generated-code
---

# Your Job Is to Deliver Code You Have Proven to Work

## The Core Argument

Developers must take responsibility for demonstrating their code functions before submitting it for review. The burden of validation should not fall on reviewers to discover whether code actually works.

## The Problem

Junior engineers using LLMs increasingly generate large, untested pull requests and pass the validation burden to reviewers. This shifts responsibility and creates inefficiencies in the review process.

## Two Essential Proof Methods

### 1. Manual Testing

Developers should personally verify changes work by:
- Recreating initial conditions
- Exercising the modification
- Documenting results

Ideally demonstrated through:
- Terminal commands showing the fix in action
- Screen recordings proving the behavior works
- Step-by-step reproduction showing before/after

### 2. Automated Testing

Contributors should bundle implementations with tests that:
- Would fail if the changes were reverted
- Validate the specific fix or feature
- Serve as regression prevention

Testing is a critical skill that distinguishes senior engineers from junior ones.

## Accountability and AI Agents

Willison emphasizes that coding agents like Claude Code must also demonstrate their changes work through testing before submission. The key principle: **"A computer can never be held accountable."**

This makes human oversight crucial for ensuring code quality and reliability in professional development workflows.

## Key Takeaway

Professional development is not just about writing code—it's about taking responsibility for proving that code works, protecting both yourself and your reviewers through adequate testing and documentation.
