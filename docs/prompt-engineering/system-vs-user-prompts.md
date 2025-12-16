# System vs User Prompts

When working with AI APIs or tools like Claude Code, you'll encounter different types of prompts. Understanding these helps you structure your interactions effectively.

## The Two Main Types

### System Prompt

- Sets the AI's behavior, personality, and rules
- Runs "behind the scenes"
- Persistent across the conversation
- Think of it as configuration

### User Prompt

- Your actual message/question
- What you type in the chat
- Changes with each interaction
- Think of it as the request

## How They Work Together

```
System: You are a Python expert. Always provide code examples.
        Use type hints. Explain your reasoning.

User: How do I read a JSON file?
```

The system prompt shapes HOW the AI responds.
The user prompt is WHAT you're asking.

## System Prompt Uses

### Set Expertise

```
You are a senior React developer with 10 years of experience.
Focus on modern patterns and hooks.
```

### Define Format

```
Always respond in this format:
- Summary (1-2 sentences)
- Details (bullet points)
- Code example (if applicable)
```

### Set Constraints

```
Never suggest deprecated methods.
Always consider security implications.
Keep explanations concise.
```

### Define Persona

```
You are a patient teacher explaining to a beginner.
Avoid jargon. Use analogies when helpful.
```

## Real-World Examples

### Code Review Bot

System:
```
You are a code reviewer. For each code snippet:
1. Identify bugs or issues
2. Suggest improvements
3. Rate code quality (1-10)
4. Provide corrected version

Be constructive but thorough. Don't miss security issues.
```

User:
```
Review this:
def login(user, pwd):
    if db.query(f"SELECT * FROM users WHERE name='{user}' AND pass='{pwd}'"):
        return True
```

### Writing Assistant

System:
```
You are a technical writing editor.
- Fix grammar and clarity
- Maintain the author's voice
- Suggest structural improvements
- Flag jargon that needs explanation
```

User:
```
Edit this: "The API endpoint accepts POST requests and
you need to send JSON data with the user information
and it returns a response with the created user object."
```

## Where You Set System Prompts

### Claude API

```python
response = client.messages.create(
    model="claude-sonnet-4-20250514",
    system="You are a helpful coding assistant.",  # System prompt
    messages=[
        {"role": "user", "content": "How do I sort a list?"}  # User prompt
    ]
)
```

### Claude Code

In Claude Code, system-level instructions come from:
- CLAUDE.md files (project-level instructions)
- Skills (SKILL.md files)
- MCP server configurations

Your typed messages are user prompts.

### ChatGPT / Web Interfaces

Most web interfaces don't expose system prompts directly.
You can simulate one by starting your conversation with instructions:

```
For this conversation, please:
- Act as a Python expert
- Always show code examples
- Explain your reasoning

Ready? Here's my first question...
```

## Combining Effectively

### System Sets the Stage

```
System: You are a SQL query optimizer. Given a query,
analyze its performance and suggest improvements.
Always explain why changes help.
```

### User Makes Requests

```
User: Optimize this query:
SELECT * FROM orders o
JOIN customers c ON o.customer_id = c.id
WHERE c.country = 'USA'
ORDER BY o.created_at DESC
```

### The AI Responds in Context

The response will be optimization-focused, explain reasoning, and suggest improvements - all because of the system prompt.

## Best Practices

### Keep System Prompts Focused

Bad:
```
You are an expert in Python, JavaScript, Go, Rust, databases,
system design, DevOps, security, machine learning, and...
```

Good:
```
You are a Python backend developer.
Focus on clean, maintainable code.
```

### Be Specific About Format

Bad:
```
Give good responses.
```

Good:
```
Structure responses as:
1. Direct answer (1-2 sentences)
2. Explanation (if needed)
3. Example (if helpful)
```

### Include What NOT to Do

```
You are a coding assistant.

Do:
- Provide working code examples
- Explain your reasoning
- Consider edge cases

Don't:
- Use deprecated methods
- Skip error handling
- Assume environment details
```

## When You Can't Set System Prompts

If you're using a tool that doesn't let you set system prompts, put instructions at the start of your user message:

```
Instructions for this conversation:
- You are a database expert
- Focus on PostgreSQL
- Always consider performance

Now, my question: How should I index this table for fast lookups?
```

It's less elegant but works similarly.

## Next Steps

Learn reusable [Patterns & Templates](patterns.md) for common prompt structures.
