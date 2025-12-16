# Common Prompting Mistakes

These are the most frequent mistakes people make when prompting AI. Avoiding them will immediately improve your results.

## 1. Being Too Vague

### The Mistake

```
Help me with my code.
```

The AI doesn't know:
- What language?
- What's the problem?
- What have you tried?
- What do you want it to do?

### The Fix

```
I have a Python function that should return the largest number
in a list, but it returns None for empty lists instead of
raising an error.

Here's my code:
[code]

How should I handle the empty list case?
```

## 2. Not Providing Context

### The Mistake

```
Why isn't this working?

const x = getData()
console.log(x.name)
```

What is getData()? What error are you seeing? What should happen?

### The Fix

```
I'm getting "Cannot read property 'name' of undefined" on line 2.

getData() is an async function that fetches user data from an API.
It should return { name: "John", email: "..." }

const x = getData()
console.log(x.name)

What's wrong?
```

## 3. Asking Multiple Questions at Once

### The Mistake

```
How do I set up React with TypeScript and what's the best
state management and should I use CSS modules or styled-components
and how do I deploy to Vercel?
```

The AI will give shallow answers to all, or miss some entirely.

### The Fix

Ask one thing at a time:

```
How do I set up a new React project with TypeScript?
```

Then follow up with the next question.

## 4. Not Specifying Output Format

### The Mistake

```
Explain how to use git.
```

You might get a 2000-word essay when you wanted bullet points, or vice versa.

### The Fix

```
Explain the basic git workflow in 5 bullet points.
Focus on: clone, add, commit, push, pull.
```

## 5. Assuming Context Carries Over

### The Mistake

In a new conversation:

```
Can you fix the bug we discussed?
```

New conversations start fresh. The AI doesn't remember previous sessions.

### The Fix

Provide context each time:

```
I have a bug in my authentication code where users
stay logged in after clicking logout.

Here's the relevant code:
[code]

The issue is the session isn't being cleared.
```

## 6. Not Showing What You've Tried

### The Mistake

```
How do I center a div?
```

There are many ways. What have you tried? What didn't work?

### The Fix

```
I'm trying to center a div horizontally and vertically.

I tried margin: auto but it only centers horizontally.
I tried text-align: center but it doesn't work on the div itself.

Here's my current CSS:
[code]

Using flexbox is fine if that's the best approach.
```

## 7. Over-Constraining

### The Mistake

```
Write a function to validate emails.
- Must be exactly 15 lines
- Must use only a single loop
- Cannot use any string methods except charAt
- Must work in ES3
```

Arbitrary constraints lead to bad code.

### The Fix

Constrain what matters:

```
Write a function to validate emails.
- No external libraries
- Handle common edge cases
- Return boolean
```

## 8. Accepting the First Response

### The Mistake

Taking the first answer and using it without verification.

### The Fix

- Test the code
- Ask follow-up questions
- Request alternatives
- Ask "Is there a simpler way?"

```
That works, but is there a more efficient approach
for large datasets?
```

## 9. Not Iterating

### The Mistake

Getting a response that's 80% right and starting over with a new prompt.

### The Fix

Refine the response:

```
Good, but can you:
- Remove the error handling for now
- Use arrow functions instead
- Add a brief comment explaining the algorithm
```

## 10. Treating AI as Infallible

### The Mistake

Assuming every AI response is correct.

### The Fix

- Verify important information
- Test all code
- Ask for sources when accuracy matters
- Use AI as a starting point, not the final answer

```
Are you sure about that version number?
Please double-check.
```

## 11. Not Providing Examples

### The Mistake

```
Format the data nicely.
```

"Nicely" means different things to different people.

### The Fix

```
Format the data like this:

Input: {name: "John", age: 30}
Output:
Name: John
Age: 30

Now format this: {name: "Jane", age: 25, city: "NYC"}
```

## 12. Using AI for Real-Time Information

### The Mistake

```
What's the current price of Bitcoin?
What's the weather in New York right now?
```

AI models have knowledge cutoffs and can't access real-time data (unless they have web access enabled).

### The Fix

- Use AI for concepts, not current data
- Ask "As of your knowledge cutoff..." for dated info
- Use actual APIs/services for real-time data

## Quick Checklist

Before sending a prompt, check:

- [ ] Is my request specific?
- [ ] Did I provide necessary context?
- [ ] Is it one question/task at a time?
- [ ] Did I specify the format I want?
- [ ] Did I include relevant code/examples?
- [ ] Did I mention what I've already tried?

## Summary Table

| Mistake | Fix |
|---------|-----|
| Too vague | Be specific about what you need |
| No context | Explain the situation |
| Multiple questions | One at a time |
| No format specified | Say how you want the output |
| Assuming context | Re-state important details |
| Not showing work | Share what you've tried |
| Over-constraining | Only constrain what matters |
| Accepting first answer | Verify and iterate |
| Not iterating | Refine responses |
| Treating as infallible | Test and verify |
| No examples | Show what you want |
| Asking for real-time data | Use appropriate tools |

## Next Steps

Return to the [Prompt Engineering overview](README.md) or explore other sections of the AI Notes.
