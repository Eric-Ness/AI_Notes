# Prompt Engineering

Prompt engineering is the skill of communicating effectively with AI. It's not magic - it's about being clear, specific, and structured in how you ask for things.

## Why It Matters

The same AI can give you a useless response or an incredibly helpful one depending entirely on how you ask. A small change in wording can transform the output.

## What You'll Learn

| Guide | What It Covers |
|-------|----------------|
| [My Prompt Examples](mypromptexamples.md) | My examples / quick guide |
| [Basics](basics.md) | Zero-shot vs few-shot prompting |
| [Chain of Thought](chain-of-thought.md) | Getting AI to reason step-by-step |
| [System vs User Prompts](system-vs-user-prompts.md) | Different prompt types and when to use them |
| [Patterns & Templates](patterns.md) | Reusable structures that work |
| [Common Mistakes](mistakes.md) | What to avoid |

## Quick Start

**The #1 rule:** Be specific about what you want.

Bad:
```
Help me with my code
```

Good:
```
Review this Python function for bugs. Focus on edge cases
and error handling. Here's the code:

def calculate_average(numbers):
    return sum(numbers) / len(numbers)
```

The second prompt tells the AI exactly what to do, what to focus on, and provides the context needed.

## Key Principles

1. **Be specific** - Say exactly what you want
2. **Provide context** - Give background information
3. **Show examples** - Demonstrate the format you want
4. **Break it down** - Complex tasks need step-by-step instructions
5. **Iterate** - Refine based on what you get back

Start with [Basics](basics.md) to learn the fundamental techniques.
