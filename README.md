<h1 align="center">
  <br>
  <img src="https://i.imgur.com/wjJF9wP.png" alt="Piñata Renter App" width="250">
  <br>
    Practical Prompt Engineering
  <br>
</h1>

<div align="center">
  :rocket:
</div>
<div align="center">
Your practical guide to <code>mastering prompt engineering</code> with LLMs. Build better AI apps with proven patterns and techniques.

</div>
<br />

<div align="center">
  <sub>Shared by created by
  <a href="https://github.com/elbrodelche">
  Juan Carlos Migliavacca
  </a>
</div>




## Table of Contents

- [Technique Summary](#-1-technique-summary)
- [Core Prompting Techniques](#-2-core-prompting-techniques)
- [Advanced Prompting Techniques](#-3-advanced-prompting-techniques)
- [Combined Prompt Examples](#-4-combined-prompt-examples)
- [Best Practices for Production](#-5-best-practices-for-production)
- [Common Pitfalls](#%EF%B8%8F-6-common-pitfalls)
- [Tips for Developers](#%EF%B8%8F-tips-for-developers)

---

## 📘 1. Technique Summary

| Technique | Purpose | Best For | Complexity |
|-----------|---------|----------|------------|
| Standard Prompt | Direct instruction | Simple tasks | ⭐ |
| Zero-Shot | No examples | General Q&A | ⭐ |
| One-Shot | One example | Basic formatting | ⭐⭐ |
| Few-Shot | Multiple examples | Structured outputs, custom logic | ⭐⭐ |
| Context Placement | Organizing information | Tasks with background context | ⭐⭐ |
| Structured Output | Machine-readable format | APIs, automation, data extraction | ⭐⭐ |
| Chain-of-Thought | Step-by-step reasoning | Logic, math, complex reasoning | ⭐⭐⭐ |
| Delimiters | Clear separation | Code, logs, long prompts, security | ⭐⭐ |
| Persona Prompting | Control style/expertise | Domain-specific tasks | ⭐⭐ |
| Self-Consistency | Multiple reasoning paths | High-accuracy requirements | ⭐⭐⭐ |
| ReAct | Reasoning + Acting | Agent systems, tool use | ⭐⭐⭐⭐ |

---

## 📌 2. Core Prompting Techniques

### 2.1 Standard Prompt

A direct instruction to the model. No examples or special formatting.

**Use when:** The task is simple and self-contained.

**Example:**

```text
Convert this article into a 50-word summary.
```

---

### 2.2 Zero-Shot Prompting

The model receives *no examples* — only the instruction.

**Use when:**

- The model already understands the task
- You want a fast, general answer

**Example:**

```text
Describe how neural networks work using everyday language.
```

---

### 2.3 One-Shot Prompting

You provide **one** example before giving the real task.

**Use when:**

- You want a specific output format
- Only one example is enough to illustrate the task

**Example:**

```text
Input: "This movie was absolutely fantastic."
Sentiment: Positive

Now classify:
Input: "The app crashes constantly."
Sentiment:
```

---

### 2.4 Few-Shot Prompting

Provide **multiple examples** to teach the model an input/output pattern.

**Use when:**

- Output must follow a strict format
- You need better consistency
- The task requires custom logic or domain-specific knowledge
- Zero-shot performance is insufficient

**Example:**

```text
Label each comment as "Positive" or "Negative".

Comment: "Exceeded my expectations, highly recommend."
Label: Positive

Comment: "Complete waste of money and time."
Label: Negative

Comment: "Decent product, nothing special though."
Label:
```

---

### 2.5 Context Placement

Structuring your prompt so the model understands what information is important.

**Best practices:**

- Put instructions at the top
- Add long context inside delimiters
- Keep the question at the end
- Place most relevant information close to the instruction

**Example:**

```text
Context:
You are reviewing customer support tickets for urgent issues.

Task:
Identify critical problems and list them by priority.

Tickets:
[insert ticket data here]
```

---

## 🚀 3. Advanced Prompting Techniques

### 3.1 Structured Output

Tell the model to return data in a strict format (JSON, YAML, tables, XML).

**Use when:**

- Integrating with APIs
- Doing data extraction
- Using LLMs inside automation / pipelines
- You need to parse output programmatically

**Example:**

```bash
Extract the following data and return as valid JSON:
{
  "product_name": "",
  "price": 0.0,
  "features": [],
  "rating": 0.0
}
```

**Pro tip:** Many modern LLMs support native JSON mode or structured output APIs for guaranteed valid JSON.

---

### 3.2 Chain-of-Thought (CoT)

Ask the model to think step-by-step before providing the final answer.

**Use when:**

- Reasoning is required
- Solving math or logic problems
- The model is prone to hallucinating an answer
- You need explainable/auditable decisions
- Complex multi-step tasks

**Example:**

```text
Solve step-by-step:

A library has 120 books on a shelf.
35 books were checked out.
18 new books were added.
How many books are on the shelf now?

Show your reasoning before providing the final answer.
```

**Variation:** Use "Let's think step by step" as a prompt suffix to trigger CoT reasoning.

---

### 3.3 Delimiters

Use symbols to clearly separate instructions, data, or context.

**Common delimiters:**

- Triple quotes `"""`
- Backticks ``` ` ` ` ```
- XML tags `<data>...</data>`
- Brackets `[[ ... ]]`
- Triple dashes `---`

**Use when:**

- Handling long prompts
- Embedding code or logs
- Reducing model confusion
- Preventing prompt injection attacks
- Working with user-generated content

**Example:**

```text
Review the content enclosed in the XML tags.

<content>
Your data goes here.
</content>

Extract the key insights and themes.
```

---

### 3.4 Persona / Role Prompting

Assign the model a specific role or expertise level.

**Use when:**

- Controlling tone and style
- Applying domain knowledge
- Simulating a specialist or advisor
- You need responses at a specific skill level

**Example:**

```text
You are an experienced DevOps engineer with extensive Kubernetes expertise.
Explain the concept of container orchestration to a beginner.
Use relatable comparisons and keep technical terms minimal.
```

---

### 3.5 Self-Consistency

Generate multiple reasoning paths and select the most consistent answer.

**Use when:**

- You need high accuracy on critical tasks
- Working with reasoning-heavy problems
- You can afford multiple API calls

**Example:**

```text
Solve this problem using three different approaches and compare results:

A cyclist covers 45 miles in 3 hours, while a runner covers
20 miles in 2 hours. Who has the higher average speed?

Show all three reasoning methods, then provide the final conclusion.
```

---

### 3.6 ReAct (Reasoning + Acting)

Combine reasoning with tool/API calls in an iterative loop.

**Use when:**

- Building agents that need to interact with external systems
- The model needs to gather information before answering
- Multi-step tasks requiring validation

**Example:**

```text
You can use these tools: [web_search, math_calculator, data_lookup]

Task: Find the GDP of Germany and compute what 12% of that value equals.

Determine which tools are needed, execute them, then deliver the final result.
```

---

## 🧩 4. Combined Prompt Examples

### 4.1 Few-Shot + Structured Output

```bash
You categorize user feedback into groups.
Respond ONLY in JSON.

Examples:
Feedback: "The checkout process is broken."
Category: "Technical Issue"

Feedback: "Where can I find my order history?"
Category: "Support Question"

Now categorize:
Feedback: "Amazing new features, very impressed!"

Output format:
{
  "category": "",
  "confidence": 0.0,
  "reasoning": ""
}
```

---

### 4.2 Role + CoT

```text
Act as an experienced database administrator.

Describe step-by-step how you would optimize the performance of this query:

---QUERY---
[query content here]
---END QUERY---

Include:
1. Your methodology
2. Techniques you'd apply
3. Why this strategy is effective
```

---

### 4.3 Delimiters + Context Placement

```text
Task: Fix spelling errors in the text between the --- markers.

---
The compnay has achived remarkble sucess in recnt years.
---

Provide only the corrected version.
```

---

### 4.4 Persona + Few-Shot + Structured Output

```bash
You are a network security specialist.

Categorize the following events as: HIGH, MEDIUM, or LOW priority.

Examples:
Event: "Multiple authentication failures detected"
Priority: MEDIUM

Event: "System memory critically low"
Priority: HIGH

Event: "Routine backup completed successfully"
Priority: LOW

Now categorize:
Event: "Suspicious file download from external source"

Return as JSON:
{
  "priority": "",
  "recommended_action": ""
}
```

---

## 🎯 5. Best Practices for Production

### 5.1 Prompt Design

- **Be specific and explicit** - Don't assume the model knows your intent
- **Use constraints** - Specify length, format, and style requirements
- **Test iteratively** - Start simple, then add complexity
- **Version your prompts** - Track changes like you would code
- **Include edge cases** - Add examples for ambiguous inputs

### 5.2 Output Handling

- **Always specify format** when output is consumed programmatically
- **Request confidence scores** for classification tasks
- **Use validation** - Parse and verify structured outputs
- **Handle errors gracefully** - Plan for malformed responses
- **Set temperature appropriately** - Lower (0.0-0.3) for deterministic tasks, higher (0.7-1.0) for creative tasks

### 5.3 Performance & Cost

- **Keep prompts concise** - Remove unnecessary verbosity
- **Use prompt caching** when available (for repeated context)
- **Batch requests** when possible
- **Choose appropriate model size** - Don't use GPT-4 when GPT-3.5 suffices
- **Monitor token usage** - Track costs and optimize

### 5.4 Security

- **Use delimiters** to prevent prompt injection
- **Sanitize user inputs** - Never trust user-provided content
- **Validate outputs** - Check for unexpected content
- **Rate limit** - Protect against abuse
- **Log and monitor** - Track unusual patterns

### 5.5 Evaluation & Testing

- **Create test suites** - Build a set of input/output pairs
- **Measure metrics** - Accuracy, latency, cost per request
- **A/B test prompts** - Compare versions objectively
- **Use human evaluation** - For subjective quality assessment
- **Monitor in production** - Track real-world performance

---

## ⚠️ 6. Common Pitfalls

### 6.1 Vague Instructions

❌ **Bad:**

```text
Explain this function.
```

✅ **Good:**

```text
Review this JavaScript function and describe:
1. Its purpose
2. Performance characteristics
3. Possible error scenarios
```

### 6.2 Inconsistent Examples

❌ **Bad:**

```text
Input: "excellent quality"
Output: positive

Input: "poor performance"
Output: Negative  # Inconsistent casing
```

✅ **Good:**

```text
Input: "excellent quality"
Output: positive

Input: "poor performance"
Output: negative
```

### 6.3 Missing Context

❌ **Bad:**

```text
Debug this code.
[code snippet]
```

✅ **Good:**

```text
This JavaScript function should filter out duplicate entries,
but it's removing all items instead.

[code snippet]

Locate the error and supply the fixed version.
```

### 6.4 Over-Reliance on Model Knowledge

❌ **Bad:**

```text
Show me the contents of the 'products' table.
```

✅ **Good:**

```text
Given this database structure:
[schema details]

Write a SQL query to fetch all items with inventory below 10 units added in the past week.
```

### 6.5 Ignoring Token Limits

- Always check model context windows
- Summarize or truncate long inputs
- Use retrieval-augmented generation (RAG) for large knowledge bases

---

## 🛠️ Tips for Developers

### Quick Wins

1. **Always specify format** when output is consumed by code (JSON, CSV, etc.)
2. **Use delimiters** for logs, markdown, JSON, or long text to prevent confusion
3. **Add few-shot examples** when consistency matters more than flexibility
4. **Use CoT** when correctness matters more than speed
5. **Keep prompts short + deterministic** for production systems
6. **Test with edge cases** - empty inputs, special characters, extreme values
7. **Version control your prompts** - treat them like code
8. **Set appropriate temperature** - 0 for deterministic, 0.7+ for creative
9. **Use streaming** for better UX in chat applications
10. **Implement fallbacks** - graceful degradation when LLM fails

### Developer Workflow

```python
# Example: Production-ready prompt with validation
import json
from typing import Dict, Optional

def classify_sentiment(review: str) -> Optional[Dict]:
    prompt = f"""
    Analyze the sentiment of the review below.
    Return ONLY valid JSON with no additional text.
    
    Format:
    {{
        "sentiment": "",
        "confidence": 0.0,
        "key_phrases": []
    }}
    
    Review:
    ---
    {review}
    ---
    """
    
    response = llm.generate(prompt, temperature=0.0)
    
    try:
        return json.loads(response)
    except json.JSONDecodeError:
        # Handle malformed output
        return None
```

---

## 📚 Additional Resources

### Learn More

- [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering)
- [Anthropic Prompt Engineering Documentation](https://docs.anthropic.com/claude/docs/prompt-engineering)
- [Google's Prompting Best Practices](https://ai.google.dev/docs/prompt_best_practices)
- [LangChain Prompt Templates](https://python.langchain.com/docs/modules/model_io/prompts/)

### Papers

- "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models" (Wei et al., 2022)
- "ReAct: Synergizing Reasoning and Acting in Language Models" (Yao et al., 2022)
- "Self-Consistency Improves Chain of Thought Reasoning in Language Models" (Wang et al., 2022)

---

## 🤝 Contributing

Found a technique that works well? Have improvements to suggest?

Feel free to open an issue or submit a pull request!

---

## 📄 License

You may freely copy, modify, or embed this README in your internal or public repositories.

---

Happy Prompting! 🚀
