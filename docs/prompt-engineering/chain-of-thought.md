# Chain of Thought Prompting

Chain of thought (CoT) prompting asks the AI to show its reasoning step-by-step before giving a final answer. This dramatically improves accuracy on complex tasks.

## Why It Works

When you ask for just an answer, the AI jumps straight to a conclusion. When you ask it to think through the problem, it catches errors and considers details it would otherwise miss.

## The Simple Version

Add "Think step by step" or "Let's work through this" to your prompt.

### Without CoT

```
Roger has 5 tennis balls. He buys 2 more cans of tennis balls.
Each can has 3 tennis balls. How many tennis balls does he have now?
```

AI might rush and get it wrong.

### With CoT

```
Roger has 5 tennis balls. He buys 2 more cans of tennis balls.
Each can has 3 tennis balls. How many tennis balls does he have now?

Think step by step.
```

Output:
```
Let me work through this:
1. Roger starts with 5 tennis balls
2. He buys 2 cans
3. Each can has 3 balls, so 2 cans = 2 × 3 = 6 balls
4. Total: 5 + 6 = 11 tennis balls

Roger has 11 tennis balls.
```

## When to Use Chain of Thought

### Good For

- Math and logic problems
- Multi-step reasoning
- Code debugging
- Analysis and decision-making
- Anything with multiple parts

### Not Needed For

- Simple factual questions
- Translations
- Basic formatting tasks
- Single-step operations

## Techniques

### "Think Step by Step"

The simplest approach. Just add the phrase:

```
What's the best way to refactor this function? Think step by step.
```

### "Let's Break This Down"

Good for complex problems:

```
I need to migrate my database from MySQL to PostgreSQL.
Let's break this down into steps.
```

### "Before Answering, Consider..."

Directs attention to specific aspects:

```
Should I use React or Vue for this project?

Before answering, consider:
- Team experience
- Project requirements
- Long-term maintenance
- Community support
```

### Show Your Work

Explicitly request the reasoning:

```
Review this code for security issues.
Show your reasoning for each issue you find.
```

## Combining with Few-Shot

You can show examples of chain-of-thought reasoning:

```
Q: Is 17 a prime number?
A: Let me check. A prime number is only divisible by 1 and itself.
   17 ÷ 2 = 8.5 (not whole)
   17 ÷ 3 = 5.67 (not whole)
   17 ÷ 4 = 4.25 (not whole)
   I only need to check up to √17 ≈ 4.1
   None divide evenly, so yes, 17 is prime.

Q: Is 21 a prime number?
A:
```

The AI learns to show the same reasoning pattern.

## Structured Chain of Thought

For complex analysis, give structure:

```
Analyze whether we should build this feature in-house or buy a solution.

Structure your analysis:
1. First, list the requirements
2. Then, evaluate build option (pros, cons, effort)
3. Then, evaluate buy option (pros, cons, cost)
4. Finally, make a recommendation with reasoning
```

## Real-World Examples

### Code Review

```
Review this function for bugs and improvements.

For each issue:
1. Identify what you found
2. Explain why it's a problem
3. Show how to fix it

def get_user(id):
    user = db.query(f"SELECT * FROM users WHERE id = {id}")
    return user[0]
```

### Decision Making

```
I'm choosing between AWS Lambda and a dedicated server for my API.

Walk through the decision:
1. What are my actual requirements?
2. How does each option handle those requirements?
3. What are the cost implications?
4. What are the operational differences?
5. Recommendation?

Context:
- ~10,000 requests/day
- Occasional spikes to 50,000
- Need to process images (takes 2-5 seconds each)
```

### Debugging

```
My code is supposed to calculate the average but returns wrong results.

Debug this step by step:
1. What should happen?
2. Trace through with a simple example
3. Where does actual behavior differ?
4. What's the fix?

def average(numbers):
    total = 0
    for n in numbers:
        total += n
        return total / len(numbers)
```

## Tips

### Let It Think

Don't rush to the answer. The reasoning IS the valuable part.

### Use for Important Decisions

CoT takes more tokens but gives better results. Use it when accuracy matters.

### Combine with Verification

Ask the AI to check its own work:

```
Solve this problem step by step.
Then verify your answer by working backwards.
```

## Next Steps

Learn about [System vs User Prompts](system-vs-user-prompts.md) to understand different ways to structure your prompts.
