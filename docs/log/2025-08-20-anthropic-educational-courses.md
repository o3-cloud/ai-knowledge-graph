---
summary: Anthropic's five educational courses teaching Claude API, prompt engineering, real-world applications, evaluations, and tool use through progressive hands-on learning via Jupyter notebooks and interactive tutorials
event_type: learning_resource
sources:
    - https://github.com/anthropics/courses
tags:
    - Claude-API
    - prompt-engineering
    - educational-courses
    - tool-use
    - evaluations
    - real-world-prompting
    - hands-on-learning
    - Jupyter-notebooks
---

# Anthropic's Educational Courses

**Source:** Anthropic GitHub Repository (anthropics/courses)
**Repository Stats:** 17.8k stars, 1.7k forks, 16 contributors
**Format:** Jupyter Notebooks with Python code
**Model Focus:** Claude 3 Haiku (cost-efficient for learning, other models substitutable)
**Free:** Yes, all courses publicly available

## Overview

Anthropic offers five structured educational courses designed to progressively build expertise with Claude API, from fundamentals through production applications. The courses combine theoretical knowledge with hands-on exercises, using Jupyter notebooks for interactive learning. Recommended completion order provides a logical progression from foundational to advanced concepts.

## Learning Path Overview

### Recommended Sequence

```
1. API Fundamentals (Foundation)
    ↓
2. Prompt Engineering Interactive Tutorial (Core Concepts)
    ↓
3. Real World Prompting (Application)
    ↓
4. Prompt Evaluations (Quality Assurance)
    ↓
5. Tool Use (Advanced Integration)
```

**Time investment:** Progressive; can be completed at own pace.

**Prerequisites:** Basic Python knowledge, access to Claude API.

## Course 1: Anthropic API Fundamentals

### Purpose

**Objective:**
Master essentials of working with Claude SDK and setting up production-ready API access.

**Target audience:**
Developers new to Claude API.

### Learning Objectives

1. Obtain and configure API keys
2. Understand SDK setup and authentication
3. Configure model parameters effectively
4. Write multimodal prompts (text + images)
5. Implement streaming responses
6. Work with core SDK functionality

### Topics Covered

**API Key Management**
- Getting API key from Anthropic console
- Environment variable configuration
- Security best practices
- Key rotation and management

**SDK Installation and Setup**
- Install Claude SDK (`pip install anthropic`)
- Initialize client
- Configure endpoints
- Set up authentication

**Model Parameters**
- Model selection (Claude 3 Haiku, Sonnet, Opus)
- Temperature and randomness control
- Max tokens and context windows
- Stop sequences and safety settings

**Multimodal Prompts**
- Text input handling
- Image input integration
- Multiple content types
- Media format handling

**Streaming Responses**
- Streaming vs. non-streaming
- Handling streamed output
- Real-time response processing
- Error handling in streams

**SDK Capabilities**
- Message creation
- Response parsing
- Error handling
- Retry logic

### Hands-On Elements

- Write first Claude API call
- Configure model parameters
- Build multimodal prompt
- Implement streaming
- Handle errors gracefully

### Key Takeaway

**Foundation established:**
Developers comfortable with basic Claude API usage and ready to move toward optimization.

## Course 2: Prompt Engineering Interactive Tutorial

### Purpose

**Objective:**
Learn key prompting techniques through hands-on, step-by-step guide.

**Target audience:**
Developers ready to optimize their prompts.

### Learning Objectives

1. Understand fundamental prompting principles
2. Learn specific prompting techniques
3. Practice techniques through interactive exercises
4. Develop intuition about what works
5. Apply techniques to own use cases

### Topics Covered

**Fundamental Principles**
- How LLMs process prompts
- Token efficiency considerations
- Context window management
- Best practices overview

**Key Prompting Techniques**

**1. Clarity and Specificity**
- Clear instructions
- Specific examples
- Explicit outputs
- Avoiding ambiguity

**2. Few-Shot Prompting**
- Providing examples
- Structuring examples effectively
- Optimal number of examples
- When to use few-shot

**3. Chain-of-Thought Prompting**
- Step-by-step reasoning
- Intermediate outputs
- Explaining reasoning
- Improving complex tasks

**4. Role and Persona**
- Assigning roles to Claude
- Personality and tone
- Expert personas
- Context-setting roles

**5. System Prompts**
- Setting system-level context
- Behavioral guidelines
- Constraints and rules
- Custom instructions

**6. Output Formatting**
- Structured outputs (JSON, XML, etc.)
- Specifying format requirements
- Validation instructions
- Parsing output programmatically

**7. Prompt Refinement**
- Iterating on prompts
- A/B testing approaches
- Measuring effectiveness
- Continuous improvement

### Hands-On Elements

- Interactive exercises for each technique
- Build prompts for different scenarios
- Compare different approaches
- Measure prompt effectiveness
- Experiment with variations

### Available Formats

**Standard version:** GitHub repository

**AWS Workshop:** [AWS Hosted Workshop](https://catalog.us-east-1.prod.workshops.aws/workshops/0644c9e9-5b82-45f2-8835-3b5aa30b1848/en-US)

### Key Takeaway

**Prompting mastery:**
Developers understand specific techniques and when to apply each for optimal results.

## Course 3: Real World Prompting

### Purpose

**Objective:**
Apply prompting techniques to complex, production-grade scenarios.

**Target audience:**
Intermediate developers ready to build real applications.

### Learning Objectives

1. Understand production prompt requirements
2. Combine multiple techniques effectively
3. Handle complex use cases
4. Optimize for real-world constraints
5. Scale prompting approaches

### Topics Covered

**Real-World Use Cases**
- Customer support automation
- Content generation
- Code analysis and generation
- Data extraction and processing
- Complex reasoning tasks

**Technique Integration**
- Combining multiple techniques
- Knowing when to use each
- Avoiding anti-patterns
- Performance optimization

**Production Considerations**
- Prompt versioning
- A/B testing strategies
- Quality metrics
- Cost optimization
- Latency requirements

**Complex Prompt Design**
- Multi-step prompts
- Conditional logic
- Context management
- Error handling in prompts

**Real-World Examples**
- Complete working examples
- Production code patterns
- Integration patterns
- Deployment considerations

### Hands-On Elements

- Build complete production prompts
- Optimize for real constraints
- Measure and improve performance
- Handle edge cases
- Deploy working systems

### Available Versions

**Standard GitHub version:** Full tutorial

**Google Vertex AI version:** Cloud-specific implementation

### Key Takeaway

**Production readiness:**
Developers can build and deploy real-world applications using Claude effectively.

## Course 4: Prompt Evaluations

### Purpose

**Objective:**
Develop measurement and evaluation frameworks for production prompts.

**Target audience:**
Developers building production systems requiring quality assurance.

### Learning Objectives

1. Design effective evaluation metrics
2. Build automated testing frameworks
3. Measure prompt quality systematically
4. Implement continuous evaluation
5. Optimize based on metrics

### Topics Covered

**Evaluation Frameworks**
- Defining success metrics
- Quantifiable vs. qualitative measures
- Metric selection criteria
- Baseline establishment

**Evaluation Types**

**1. Automated Evaluation**
- Code-based assertions
- LLM-as-judge evaluation
- Metric calculation
- Threshold setting

**2. Human Evaluation**
- Expert review processes
- Consistency metrics
- Feedback integration
- Sampling strategies

**3. A/B Testing**
- Comparative testing
- Statistical significance
- Sample size determination
- Result interpretation

**4. Continuous Monitoring**
- Production metrics
- Regression detection
- Alerting systems
- Performance tracking

**Writing Quality Metrics**
- Relevance metrics
- Accuracy metrics
- Safety metrics
- Cost metrics
- Latency metrics

**Production Quality Assurance**
- Version control for prompts
- Change impact analysis
- Rollback procedures
- Quality gates

### Hands-On Elements

- Design evaluation metrics
- Build evaluation code
- Run automated tests
- Analyze results
- Iterate based on data

### Key Takeaway

**Quality assurance capability:**
Developers can measure and ensure prompt quality in production systems.

## Course 5: Tool Use

### Purpose

**Objective:**
Master tool use functionality and external integrations with Claude.

**Target audience:**
Advanced developers building complex agent systems.

### Learning Objectives

1. Understand tool use concepts
2. Define tools for Claude
3. Implement function calling
4. Build multi-step workflows
5. Handle tool errors and edge cases

### Topics Covered

**Tool Use Fundamentals**
- What tool use is
- When to use tools
- Tool vs. prompt approaches
- Design principles

**Tool Definition**
- JSON schema definition
- Clear tool descriptions
- Parameter specification
- Return value documentation

**Function Calling**
- How Claude calls tools
- Handling tool requests
- Executing functions
- Returning results

**Tool Integration Patterns**

**1. Single Tool Call**
- Simple API calls
- Structured data retrieval
- One-step operations

**2. Multi-Step Workflows**
- Sequential tool calls
- Conditional logic
- Iterative processes
- Complex workflows

**3. Tool Composition**
- Combining multiple tools
- Orchestrating workflows
- Managing state
- Error recovery

**4. Agentic Loops**
- Autonomous agent behavior
- Goal-directed tool use
- Iterative improvement
- Stopping criteria

**Advanced Topics**
- Tool validation
- Error handling
- Timeout management
- Security considerations
- Cost optimization

### Hands-On Elements

- Define tools in JSON schema
- Build tool handlers
- Implement multi-step workflows
- Create agentic loops
- Deploy integrated systems

### Key Takeaway

**Advanced integration:**
Developers can build sophisticated multi-tool systems with Claude handling coordination.

## Repository Structure

### Organization

**Top-level folders:**
- `api_fundamentals/` - API course
- `prompt_engineering_interactive_tutorial/` - Prompting course
- `real_world_prompting/` - Real-world course
- `prompt_evaluations/` - Evaluation course
- `tool_use/` - Tool use course

### Each Course Contains

**README.md:**
- Overview and learning objectives
- Prerequisites
- How to use the course
- Time estimate

**Jupyter Notebooks:**
- Interactive lessons
- Code examples
- Exercises
- Solutions

**Supporting Files:**
- Code snippets
- Configuration examples
- Sample data
- Helper functions

## How to Use These Courses

### Getting Started

**Prerequisites:**
- Python 3.8+
- Git
- Anthropic API key
- Jupyter Notebook or JupyterLab

### Setup Steps

```bash
# Clone repository
git clone https://github.com/anthropics/courses.git
cd courses

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Start Jupyter
jupyter notebook
```

### Working Through Courses

**Recommended approach:**
1. Read course README
2. Open first notebook
3. Read explanations
4. Run code cells
5. Complete exercises
6. Move to next notebook

**Pacing:**
- Can complete at own pace
- Recommend blocks of focused time
- Each course: 2-4 hours typically
- Practice and experimentation important

## Key Features

### Jupyter Notebook Format

**Advantages:**
- Interactive learning
- Code execution alongside explanation
- Easy experimentation
- Shareable and reproducible

**Requires:**
- Jupyter environment
- Python installation
- Comfort with notebooks

### Cost-Efficient Learning

**Claude 3 Haiku default:**
- Lowest cost model
- Sufficient for learning
- Easy to substitute other models
- Keeps API costs minimal

### Multi-Platform Support

**Standard versions:** Standard GitHub
**AWS Workshop:** AWS-hosted interactive workshop
**Google Vertex:** Google Cloud-specific version

### Community and Support

**GitHub features:**
- Issues for questions
- Discussions for community
- Contributors welcome
- Regular updates

## Advanced Path Suggestions

### After Completing All Five Courses

**Specialization paths:**

**Path 1: Production Systems**
- Focus on evaluations
- Study production best practices
- Build complete systems
- Implement monitoring

**Path 2: Advanced Agents**
- Deep dive into tool use
- Study complex workflows
- Implement agentic loops
- Explore multi-agent systems

**Path 3: Prompt Optimization**
- Focus on prompt engineering
- Master A/B testing
- Implement evaluation frameworks
- Optimize for specific domains

**Path 4: Domain-Specific Applications**
- Apply to specific industry
- Build domain models
- Create specialized tools
- Evaluate domain-specific metrics

## Key Takeaways

1. **Sequential learning effective** — Build from fundamentals to advanced
2. **Hands-on format essential** — Interactive notebooks enable deep learning
3. **Cost-conscious** — Haiku default minimizes learning costs
4. **Production-focused** — Covers real-world considerations
5. **Comprehensive coverage** — From API basics to advanced agents
6. **Free and open** — No cost, publicly accessible
7. **Active community** — 17.8k stars, ongoing contributions
8. **Multiple formats** — Standard, AWS, Google Cloud versions
9. **Jupyter convenience** — Learn interactively without complex setup
10. **Practical focus** — Theory combined with working code
11. **Evaluation emphasis** — Quality assurance covered thoroughly
12. **Tool integration complete** — Multi-step workflows and agents taught

## The Bottom Line

Anthropic's educational courses represent a comprehensive, well-structured path to mastery of Claude API and prompting. The progression from fundamentals through real-world prompting, evaluations, and tool use mirrors professional development path. Jupyter notebook format enables interactive learning with immediate feedback.

Key strength is practical focus: not just theory, but working code and complete examples applicable immediately. Evaluation course distinguishes this from competitor offerings—quality assurance built in from start, not afterthought.

For developers building with Claude, this represents authoritative learning path directly from Anthropic. Five courses, progressive complexity, hands-on exercises, production-ready knowledge. Cost-efficient via Haiku default, easily adapted to other models.

Recommended approach: work through in order, complete all exercises, build projects applying knowledge. The combination of prompting, evaluation, and tool use creates foundation for building sophisticated Claude-powered systems.

The free, open nature and 17.8k stars indicate community validation and active use. Whether you're starting fresh or improving existing prompts, these courses provide systematic path to improvement.
