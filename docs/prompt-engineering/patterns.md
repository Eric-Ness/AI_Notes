# Prompt Patterns & Templates

These are reusable structures that work well across many situations. Copy and adapt them for your needs.

## The Basics Pattern

Structure: Context → Task → Format

```
[Context: What you're working on]
[Task: What you need done]
[Format: How you want the output]
```

### Example

```
I'm building a REST API for a todo app.

Write a function that creates a new todo item.

Return just the code with brief comments.
```

## The Role Pattern

Assign the AI a specific role to get expertise-appropriate responses.

```
You are a [role] with [experience].
[Task or question]
```

### Example

```
You are a security engineer reviewing code for vulnerabilities.

Review this authentication function and identify any security issues:

def authenticate(username, password):
    user = db.find_user(username)
    if user.password == password:
        return create_session(user)
    return None
```

## The Template Pattern

Give a template and ask the AI to fill it in.

```
Fill in this template for [subject]:

Title: [descriptive title]
Summary: [1-2 sentences]
Key Points:
- [point 1]
- [point 2]
- [point 3]
Recommendation: [action to take]
```

### Example

```
Fill in this template for the React vs Vue decision:

Title: [descriptive title]
Summary: [1-2 sentences]
Key Points:
- [point 1]
- [point 2]
- [point 3]
Recommendation: [action to take]
```

## The Persona Pattern

Create a specific personality for more tailored responses.

```
Respond as [persona description].
[Your question]
```

### Example

```
Respond as a patient teacher explaining to someone who has
never programmed before.

What is a variable in programming?
```

## The Constraint Pattern

Add specific rules to guide the output.

```
[Task]

Constraints:
- [rule 1]
- [rule 2]
- [rule 3]
```

### Example

```
Write a function to validate email addresses.

Constraints:
- Use only standard library (no regex)
- Handle edge cases
- Return boolean
- Include docstring
```

## The Refinement Pattern

Ask for a first draft, then improve it.

```
First: [initial request]
Then: [refinement request]
```

### Example

```
First: Write a product description for wireless earbuds.
Then: Make it more concise and add urgency.
```

## The Comparison Pattern

Get structured comparisons.

```
Compare [A] vs [B] for [use case].

Consider:
- [aspect 1]
- [aspect 2]
- [aspect 3]

Format as a table, then give a recommendation.
```

### Example

```
Compare PostgreSQL vs MongoDB for a social media app.

Consider:
- Data relationships
- Scalability
- Development speed
- Query flexibility

Format as a table, then give a recommendation.
```

## The Review Pattern

Get feedback on your work.

```
Review this [type of content] for [specific concerns].

[Content to review]

Provide:
1. Issues found (with severity)
2. Suggestions for improvement
3. What works well
```

### Example

```
Review this API design for RESTful best practices.

POST /api/getUsers
POST /api/deleteUser?id=123
GET /api/user/update

Provide:
1. Issues found (with severity)
2. Suggestions for improvement
3. What works well
```

## The Explain Pattern

Get explanations at the right level.

```
Explain [concept] to [audience].

Use [analogy type] if helpful.
Keep it under [length].
```

### Example

```
Explain Kubernetes to a developer who knows Docker
but hasn't used orchestration.

Use real-world analogies if helpful.
Keep it under 200 words.
```

## The Debug Pattern

Structured debugging help.

```
This code should [expected behavior] but instead [actual behavior].

[Code]

Help me debug:
1. What's likely wrong?
2. How can I verify?
3. What's the fix?
```

### Example

```
This code should return the sum of even numbers but returns 0.

def sum_evens(numbers):
    total = 0
    for n in numbers:
        if n % 2 == 0:
            total += n
        return total

Help me debug:
1. What's likely wrong?
2. How can I verify?
3. What's the fix?
```

## The Alternatives Pattern

Get multiple options.

```
I need to [goal].

Give me 3 different approaches:
1. The simple approach
2. The robust approach
3. The creative approach

For each, explain trade-offs.
```

### Example

```
I need to cache API responses in my Node.js app.

Give me 3 different approaches:
1. The simple approach
2. The robust approach
3. The creative approach

For each, explain trade-offs.
```

## The Checklist Pattern

Get verification steps.

```
Create a checklist for [task].

Include:
- Pre-requisites
- Main steps
- Verification steps
- Common gotchas
```

### Example

```
Create a checklist for deploying a Node.js app to production.

Include:
- Pre-requisites
- Main steps
- Verification steps
- Common gotchas
```

## Combining Patterns

You can mix patterns together:

```
You are a senior Python developer (Role Pattern).

Review this code (Review Pattern) with these constraints (Constraint Pattern):
- Focus on performance
- Ignore styling issues
- Consider memory usage

[code]

Format your response as (Template Pattern):
Issue: [description]
Impact: [high/medium/low]
Fix: [suggested change]
```

## Quick Reference

| Pattern | When to Use |
|---------|-------------|
| Basics | Any task (start here) |
| Role | Need expertise |
| Template | Need specific format |
| Persona | Need specific tone |
| Constraint | Need boundaries |
| Refinement | Iterative improvement |
| Comparison | Making decisions |
| Review | Getting feedback |
| Explain | Learning concepts |
| Debug | Fixing issues |
| Alternatives | Exploring options |
| Checklist | Process guidance |

## Next Steps

Learn about [Common Mistakes](mistakes.md) to avoid when prompting.
