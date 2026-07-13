# Class 2 - LLMs' Prompts & Smart Agents

## Overview
This class covered Large Language Models (LLMs) and how they can be guided through **prompt engineering** — the skill of crafting inputs to get accurate, useful, or creative outputs from AI systems.

## What is Prompt Engineering?
Prompt engineering is the practice of designing and structuring prompts (instructions/cues given to an AI) in a way that significantly impacts the quality and accuracy of the AI's responses. It's a key skill for effectively interacting with LLMs.

## Types of Prompts

1. **Zero-shot prompts**
   - Asking the AI to perform a task without giving any examples.
   - The AI relies purely on its trained knowledge to figure out what's needed.

2. **Few-shot prompts**
   - Providing a few examples within the prompt to guide the AI's behavior.
   - Helps the AI understand the expected format, tone, or pattern before generating a response.

3. **Role-based prompts**
   - Assigning the AI a specific role or persona (e.g., "You are a lawyer...", "You are a fitness coach...").
   - Influences the tone, vocabulary, and depth of the AI's output.

4. **Negative prompts**
   - Telling the AI what *not* to do.
   - Helps narrow down or refine the output by excluding unwanted behavior or content.

5. **Structured prompts (XML/JSON)**
   - Using format-based inputs (like XML or JSON) to organize the output.
   - Especially useful for communicating with APIs and agents, since structured formats are easier for systems to parse and use programmatically.
   - Covered in more detail below.

## Structured Prompting: XML vs JSON

Structured prompts matter most when the AI's output needs to be **read by another system** (an API, an agent, a script) rather than just read by a human. Instead of getting a paragraph of text back, you get data in a predictable shape that code can reliably parse.

### XML-style Prompting

**Syntax basics:**
- Content is wrapped in opening and closing tags: `<tag>content</tag>`
- Tags can be nested to represent structure/hierarchy
- Tag names are custom — you define whatever makes sense for your task

**Example — asking an LLM to structure a prompt using XML tags:**
```xml
<instructions>
Summarize the following article in 3 bullet points.
</instructions>

<article>
Paste the full article text here.
</article>

<output_format>
Return the summary as plain bullet points, no extra commentary.
</output_format>
```

**Example — asking the model to respond in XML:**
```xml
<response>
  <summary>Short summary of the article</summary>
  <key_points>
    <point>First key point</point>
    <point>Second key point</point>
    <point>Third key point</point>
  </key_points>
</response>
```

**Why XML is useful:**
- Clear visual separation between sections (instructions vs. data vs. examples)
- Nesting makes hierarchy explicit (e.g., multiple `<point>` tags inside `<key_points>`)
- Many LLMs (including Claude) are specifically trained to follow XML-tagged instructions well

### JSON-style Prompting

**Syntax basics:**
- Data is structured as key-value pairs: `"key": "value"`
- Curly braces `{}` define an object; square brackets `[]` define a list/array
- Keys are always strings in double quotes; values can be strings, numbers, booleans, objects, or arrays

**Example — asking the model to return JSON:**
```json
{
  "summary": "Short summary of the article",
  "key_points": [
    "First key point",
    "Second key point",
    "Third key point"
  ],
  "word_count": 245
}
```

**Example — a prompt instructing structured JSON output:**
```
Analyze the sentiment of this review and respond ONLY in JSON format, 
with no extra text, using this structure:

{
  "sentiment": "positive | negative | neutral",
  "confidence": 0.0,
  "reason": "short explanation"
}
```

**Why JSON is useful:**
- It's the standard format most APIs and programming languages parse natively
- Easy to convert directly into objects/variables in code (e.g., JavaScript, Python)
- Compact and widely supported across tools, databases, and agent frameworks

### XML vs JSON — When to Use Which

| | XML | JSON |
|---|---|---|
| Best for | Long-form or nested instructions, separating prompt sections | Data meant to be directly consumed by code/APIs |
| Readability | Easier for humans to scan visually | More compact, less visual noise |
| Common use case | Structuring a *prompt* (instructions, context, examples) | Structuring a *response* (data to be parsed programmatically) |
| LLM handling | Many models (like Claude) are trained to respect XML tags precisely | Very reliable for models trained on code/data-heavy tasks |

**Key rule of thumb from the lecture:** use structured prompting whenever the output needs to be handed off to another system (an API call, a database, another agent) rather than just read by a person — structure removes ambiguity and prevents the AI from "wandering" in its response.

## Smart Agents

**Smart agents** are autonomous or semi-autonomous systems powered by LLMs that can:
- Understand instructions
- Make decisions
- Take actions across digital environments (e.g., calling APIs, using tools, navigating apps)

Smart agents rely heavily on **well-designed prompts** to function accurately and contextually — the quality of the prompt directly affects how well the agent understands its task and executes it.

## Key Takeaway

Structured thinking and clarity are essential when working with language models. The way a prompt is designed shapes:
- How accurate the response is
- How well an agent understands its task
- How reliably an agent can take the right action

This lecture set the foundation for designing smarter, more intentional interactions with AI tools and agents going forward.

---
*Part of the "AI Agents" course repository — Master AI Agents by Tech7Academy.*