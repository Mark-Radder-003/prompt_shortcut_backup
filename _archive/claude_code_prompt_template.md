# Claude Code Prompt Template - LLM ↔ Code Interaction Guide

## 📋 Overview
This template is designed for efficient LLM-code interactions based on Anthropic's prompt engineering best practices. Use this as a foundation for creating prompts that work seamlessly with Claude for coding tasks.

## 🎯 Before You Start - Success Criteria Checklist

### Pre-Prompt Engineering Requirements
- [ ] Clear definition of success criteria for your use case
- [ ] Empirical testing methods established
- [ ] First draft prompt ready to improve

### When to Use This Template
✅ **Use for**: Code generation, debugging, refactoring, documentation, analysis
❌ **Don't use for**: Latency/cost issues (consider different model instead)

## 🏗️ Prompt Structure Framework

### Basic Template Structure
```xml
<context>
[Provide relevant background information]
</context>

<instructions>
[Clear, sequential instructions]
</instructions>

<examples>
[Code examples if needed]
</examples>

<constraints>
[Specific limitations or requirements]
</constraints>

<output_format>
[Specify exact output format needed]
</output_format>
```

## 🎯 Core Techniques (In Order of Effectiveness)

### 1. Be Clear and Direct
**Key Principles:**
- Think of Claude as a brilliant new employee who needs explicit instructions
- Provide contextual information about the task's purpose
- Be specific about what you want Claude to do
- Use sequential steps (numbered lists/bullet points)

**Example Structure:**
```xml
<task_context>
I'm building a [project type] and need to [specific goal].
This code will be used for [purpose] by [audience].
</task_context>

<instructions>
1. Analyze the provided code structure
2. Identify potential improvements
3. Generate optimized code with comments
4. Explain the changes made
</instructions>
```

### 2. Use XML Tags for Structure
**Benefits:**
- **Clarity**: Separate different prompt parts
- **Accuracy**: Reduce misinterpretation errors
- **Flexibility**: Easy to modify without rewriting
- **Parseability**: Easy to extract specific response parts

**Best Practices:**
- Be consistent with tag names
- Nest tags for hierarchical content
- Reference tag names in instructions

**Common Code-Related Tags:**
```xml
<codebase>...</codebase>
<requirements>...</requirements>
<constraints>...</constraints>
<examples>...</examples>
<output_format>...</output_format>
<thinking>...</thinking>
<solution>...</solution>
```

### 3. Multishot Prompting (Examples)
**Why Use Examples:**
- **Accuracy**: Examples reduce misinterpretation of instructions
- **Consistency**: Examples enforce uniform structure and style
- **Performance**: Well-chosen examples boost Claude's ability to handle complex tasks

**Best Practices:**
- **Relevant**: Examples mirror your actual use case
- **Diverse**: Cover edge cases and vary enough to avoid unintended patterns
- **Clear**: Wrap examples in `<example>` tags (multiple in `<examples>` tags)

```xml
<examples>
<example>
<input>
def calculate_area(radius):
    return 3.14 * radius * radius
</input>
<output>
def calculate_area(radius: float) -> float:
    """Calculate the area of a circle given its radius.
    
    Args:
        radius: The radius of the circle
        
    Returns:
        The area of the circle
    """
    import math
    return math.pi * radius ** 2
</output>
</example>
</examples>
```

### 4. Chain of Thought (Let Claude Think)
**When to Use:**
- Complex math, logic, or analysis tasks
- Multi-step reasoning problems
- Tasks requiring structured thinking

**Three Approaches:**
1. **Basic**: Include "Think step-by-step" in your prompt
2. **Guided**: Outline specific steps for Claude to follow
3. **Structured**: Use XML tags like `<thinking>` and `<answer>`

```xml
<instructions>
Analyze this algorithm's time complexity. Think through this step-by-step.
</instructions>

<thinking>
[Claude will work through the problem here]
</thinking>

<answer>
[Claude will provide the final answer here]
</answer>
```

### 5. Prompt Templates and Variables
**Use Cases:**
- Repeated prompts with changing inputs
- API integrations
- Batch processing tasks

**Template Structure:**
```xml
<context>
Project: {{project_name}}
Language: {{programming_language}}
Framework: {{framework}}
</context>

<requirements>
{{requirements_list}}
</requirements>

<code_to_analyze>
{{user_code}}
</code_to_analyze>
```

**Benefits:**
- **Consistency**: Uniform prompt structure
- **Efficiency**: Easy to swap variable content
- **Testability**: Quick testing of different inputs
- **Scalability**: Simplified prompt management

## 🛠️ Code-Specific Prompt Patterns

### Pattern 1: Code Generation
```xml
<context>
Project: [project description]
Language: [programming language]
Framework: [if applicable]
</context>

<requirements>
- [Functional requirement 1]
- [Functional requirement 2]
- [Non-functional requirement 1]
</requirements>

<constraints>
- Follow [coding standards/style guide]
- Use [specific libraries/patterns]
- Include error handling
- Add inline comments
</constraints>

<output_format>
1. Complete, runnable code
2. Brief explanation of approach
3. Usage example
</output_format>
```

### Pattern 2: Code Review/Debugging
```xml
<codebase>
[Paste your code here]
</codebase>

<issues>
[Description of problems you're experiencing]
</issues>

<instructions>
1. Analyze the code for bugs, performance issues, and best practices
2. Provide specific fixes with explanations
3. Suggest improvements for maintainability
4. Format output as: Problem → Solution → Explanation
</instructions>
```

### Pattern 3: Code Documentation
```xml
<code_to_document>
[Your code here]
</code_to_document>

<documentation_requirements>
- Target audience: [developers/users/maintainers]
- Include: [API docs/usage examples/architectural notes]
- Format: [README/JSDoc/Sphinx/etc.]
- Level of detail: [beginner/intermediate/advanced]
</documentation_requirements>

<output_format>
Generate comprehensive documentation including:
1. Overview and purpose
2. Installation/setup instructions
3. Usage examples
4. API reference (if applicable)
5. Contributing guidelines (if applicable)
</output_format>
```

### Pattern 4: Architecture Design
```xml
<project_context>
Project: [description]
Scale: [user count/data volume/etc.]
Tech stack: [current/preferred technologies]
</project_context>

<requirements>
- [Functional requirements]
- [Performance requirements]
- [Scalability requirements]
- [Security requirements]
</requirements>

<constraints>
- Budget: [if applicable]
- Timeline: [if applicable]
- Team expertise: [technologies team knows]
- Existing systems: [systems to integrate with]
</constraints>

<deliverables>
1. High-level architecture diagram (text-based)
2. Component breakdown with responsibilities
3. Technology recommendations with rationale
4. Implementation phases/roadmap
</deliverables>
```

## 🔧 Advanced Techniques

### System Prompts (Role-Based Prompting)
**Purpose**: Give Claude a specific professional role to enhance accuracy and focus.

**How to Implement:**
```python
# Using the system parameter
system_prompt = "You are a senior software engineer with 10+ years of experience in Python and Django. You write clean, maintainable code following PEP 8 standards and always consider security, performance, and scalability."

# In your API call
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    system=system_prompt,  # Role goes here
    messages=[
        {"role": "user", "content": "Review this Django view for security issues..."}
    ]
)
```

**Role Examples for Code Tasks:**
- "Senior software architect specializing in microservices"
- "DevOps engineer with expertise in CI/CD and containerization"
- "Frontend developer focused on React and accessibility"
- "Data scientist experienced in machine learning pipelines"

### Prefilling for Output Control
**Use Cases:**
- Skip preambles and get straight to code
- Enforce specific output formats (JSON, XML)
- Maintain character consistency in role-play scenarios

**Implementation:**
```python
# Force JSON output without preamble
messages=[
    {"role": "user", "content": "Extract key info from this code"},
    {"role": "assistant", "content": "{"}  # Prefill starts JSON
]

# Start with specific analysis format
messages=[
    {"role": "user", "content": "Analyze this code"},
    {"role": "assistant", "content": "**Issues Found:**\n1."}  # Prefill format
]
```

**Warning**: Prefilling is not available with extended thinking mode.

### Prompt Chaining for Complex Tasks
**Why Chain Prompts:**
- **Accuracy**: Each subtask gets Claude's full attention
- **Clarity**: Simpler subtasks mean clearer instructions
- **Traceability**: Easy to pinpoint and fix issues

**Chaining Strategy:**
1. **Identify subtasks**: Break complex tasks into sequential steps
2. **Use XML for handoffs**: Structure data passing between prompts
3. **Single-task focus**: Each prompt should have one clear objective

**Example Chain Workflow:**
```xml
<!-- Prompt 1: Analysis -->
<task>Analyze the codebase structure</task>
<output_format>
<analysis>
  <components>...</components>
  <dependencies>...</dependencies>
  <issues>...</issues>
</analysis>
</output_format>

<!-- Prompt 2: Design (uses output from Prompt 1) -->
<previous_analysis>
[Insert output from Prompt 1]
</previous_analysis>
<task>Design refactoring plan based on analysis</task>

<!-- Prompt 3: Implementation (uses outputs from Prompts 1 & 2) -->
<analysis>[From Prompt 1]</analysis>
<plan>[From Prompt 2]</plan>
<task>Implement the refactored code</task>
```

**Advanced: Self-Correction Chains**
```xml
<!-- Step 1: Generate code -->
<task>Write a function to process CSV data</task>

<!-- Step 2: Review own work -->
<code_to_review>
[Output from Step 1]
</code_to_review>
<task>Review the above code for bugs, edge cases, and improvements</task>

<!-- Step 3: Apply corrections -->
<original_code>[From Step 1]</original_code>
<review_feedback>[From Step 2]</review_feedback>
<task>Apply the suggested improvements to create the final version</task>
```

### Long Context Optimization
**Essential Tips for 20K+ Token Prompts:**

1. **Put longform data at the top**: Place large documents/inputs near the top of your prompt, above queries and instructions (can improve performance by up to 30%)

2. **Structure with XML**: Use clear document organization
```xml
<documents>
<document>
<source>filename.py</source>
<document_content>
[Large code file content]
</document_content>
</document>
</documents>

<query>
Analyze the above codebase for security vulnerabilities...
</query>
```

3. **Ground responses in quotes**: Ask Claude to quote relevant parts first
```xml
<instructions>
1. First, identify and quote the relevant code sections
2. Then provide your analysis of each section
3. Finally, summarize your findings
</instructions>
```

### Extended Thinking Mode (Advanced)
**When to Use Extended Thinking:**
- Complex STEM problems
- Detailed code architecture design  
- Multi-step debugging processes
- Constraint optimization problems

**Key Principles:**
1. **Start general, then get specific**: Let Claude choose its approach first
```xml
<!-- Instead of prescriptive steps -->
<instructions>
Please think about this algorithmic problem thoroughly and in great detail.
Consider multiple approaches and show your complete reasoning.
Try different methods if your first approach doesn't work.
</instructions>
```

2. **Use multishot with thinking examples**:
```xml
<examples>
<example>
<problem>Debug this sorting algorithm</problem>
<thinking>
Let me trace through this step by step...
1. First, I'll check the logic flow
2. Then examine edge cases
3. Finally test with sample data
</thinking>
<solution>[Fixed code with explanation]</solution>
</example>
</examples>
```

3. **Have Claude self-verify**:
```xml
<instructions>
Write a function to calculate fibonacci numbers.
Before you finish, please verify your solution with test cases and fix any issues you find.
</instructions>
```

**Technical Considerations:**
- Minimum thinking budget: 1024 tokens
- For 32K+ thinking budgets, use batch processing
- Extended thinking performs best in English
- Don't pass thinking output back as user input

### Prompt Improver Integration
**What the Prompt Improver Provides:**
- Detailed chain-of-thought instructions
- Clear XML tag organization  
- Standardized example formatting
- Strategic prefills

**How to Use:**
1. Submit your basic prompt template
2. Add feedback about current issues
3. Include example inputs and ideal outputs
4. Review and customize the improved prompt

**Best For:**
- Complex tasks requiring detailed reasoning
- High-accuracy requirements (vs. speed)
- Situations where current outputs need significant improvement

## 📝 Quick Reference Checklist

### Before Sending Your Prompt:
- [ ] Success criteria defined
- [ ] Context provided (purpose, audience, workflow)
- [ ] Instructions are sequential and specific
- [ ] XML tags used for structure
- [ ] Output format specified
- [ ] Examples included (if needed)
- [ ] Constraints clearly stated

### Golden Rule Test:
> Show your prompt to a colleague with minimal context. If they're confused, Claude will be too.

## 🎨 Template Examples by Use Case

### Web Development
```xml
<project_context>
Building a [type] web application using [framework]
Target users: [description]
Key features: [list]
</project_context>

<technical_requirements>
- Responsive design
- Performance optimization
- Accessibility compliance
- SEO considerations
</technical_requirements>

<instructions>
1. Create the component structure
2. Implement core functionality
3. Add styling and responsive behavior
4. Include error handling and loading states
5. Write unit tests
</instructions>
```

### Data Analysis
```xml
<dataset_context>
Data source: [description]
Format: [CSV/JSON/database/etc.]
Size: [approximate volume]
Purpose: [analysis goal]
</dataset_context>

<analysis_requirements>
- Clean and preprocess data
- Identify key patterns/insights
- Create visualizations
- Provide statistical summary
</analysis_requirements>

<output_format>
1. Data cleaning code with explanations
2. Analysis code with step-by-step comments
3. Visualization code
4. Summary of findings
5. Recommendations for next steps
</output_format>
```

### API Development
```xml
<api_context>
Service purpose: [description]
Expected load: [requests/day or concurrent users]
Data sources: [databases/external APIs/etc.]
Authentication: [method if required]
</api_context>

<endpoint_requirements>
[List each endpoint with method, path, parameters, response format]
</endpoint_requirements>

<technical_constraints>
- Framework: [Express/FastAPI/etc.]
- Database: [if applicable]
- Rate limiting: [if needed]
- Error handling: [standard format]
- Documentation: [OpenAPI/Swagger/etc.]
</technical_constraints>
```

## 🚀 Pro Tips for Code Interactions

1. **Version Control Integration**: Always ask Claude to include git commit messages for changes
2. **Testing Strategy**: Request both unit tests and integration test approaches
3. **Performance Considerations**: Explicitly ask for performance analysis when relevant
4. **Security Review**: Include security considerations in your constraints
5. **Code Style**: Reference specific style guides (PEP 8, Airbnb, Google, etc.)
6. **Dependency Management**: Ask Claude to explain why it chose specific libraries
7. **Refactoring Requests**: Provide the current code and specific refactoring goals

## 📚 Additional Resources

- [Anthropic Prompt Library](https://docs.anthropic.com/en/resources/prompt-library/library)
- [Interactive Tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial)
- [Google Sheets Tutorial](https://docs.google.com/spreadsheets/d/19jzLgRruG9kjUQNKtCg1ZjdD6l6weA6qRXG5zLIAhC8)

---

## 🎯 Meta-Template for Creating New Prompts

When creating a new coding prompt, follow this meta-structure:

1. **Define the coding task clearly**
2. **Provide relevant context** (project, tech stack, constraints)
3. **Structure with XML tags** for clarity
4. **Include examples** if the pattern isn't obvious
5. **Specify output format** exactly as needed
6. **Test with a colleague** before using with Claude
7. **Iterate based on results** and improve for next time

Remember: The best prompts are clear, specific, and structured. Treat Claude like a highly skilled developer who needs complete context to deliver exactly what you need.
