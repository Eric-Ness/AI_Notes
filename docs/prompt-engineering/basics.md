# Prompting Basics

There are two fundamental approaches to prompting: **zero-shot** and **few-shot**. Understanding these gives you a foundation for everything else.

## Zero-Shot Prompting

Zero-shot means asking the AI to do something without providing examples. You're relying on the AI's training to understand what you want.

### When It Works Well

- Simple, common tasks
- Clear instructions
- Standard formats

### Example

```
Translate this to Spanish: "Hello, how are you?"
```

Output:
```
"Hola, ¿cómo estás?"
```

No examples needed - the task is straightforward.

### When It Falls Short

- Unusual formats
- Specific styles
- Complex or ambiguous tasks

## Few-Shot Prompting

Few-shot means providing examples of what you want. The AI learns the pattern from your examples and applies it.

### When to Use It

- Custom formats
- Specific tone or style
- Non-obvious transformations
- When zero-shot gives wrong format

### Example

```
Convert these sentences to past tense:

"I walk to the store" -> "I walked to the store"
"She runs every morning" -> "She ran every morning"
"They eat lunch together" -> "They ate lunch together"

Now convert: "He writes code all day"
```

Output:
```
"He wrote code all day"
```

The examples teach the AI exactly what transformation you want.

## Few-Shot Best Practices

### Use 2-5 Examples

Too few and the pattern isn't clear. Too many wastes tokens and can confuse.

```
# Good: 3 clear examples
Input: happy -> Output: sad
Input: hot -> Output: cold
Input: fast -> Output: slow

Input: big -> Output: ?
```

### Make Examples Representative

Cover the variations you expect:

```
# Shows the AI how to handle different cases
"hello world" -> "Hello World"
"ALREADY CAPS" -> "Already Caps"
"mixed CASE here" -> "Mixed Case Here"

Now convert: "this is a TEST"
```

### Keep Format Consistent

Use the same structure for every example:

```
# Consistent format
Q: What is 2+2?
A: 4

Q: What is the capital of France?
A: Paris

Q: Who wrote Hamlet?
A:
```

## Zero-Shot vs Few-Shot Decision

| Situation | Use |
|-----------|-----|
| Standard task (translate, summarize) | Zero-shot |
| Custom output format | Few-shot |
| Getting wrong format | Add examples (few-shot) |
| Specific style or tone | Few-shot |
| Simple question | Zero-shot |

## Practical Tips

### Start Zero-Shot, Add Examples If Needed

Don't over-engineer. Try the simple approach first:

1. Write a clear zero-shot prompt
2. If output is wrong format, add 2-3 examples
3. If still wrong, check if your examples are clear

### Use Examples to Fix Problems

If the AI keeps getting something wrong, show it:

```
# AI kept using bullet points when I wanted numbered lists

Format these as a numbered list:

Items: apple, banana, cherry
Output:
1. apple
2. banana
3. cherry

Items: red, blue, green
Output:
1. red
2. blue
3. green

Items: cat, dog, bird
Output:
```

### Examples Are Worth a Thousand Words

Instead of explaining a complex format, just show it:

```
# Hard to explain in words, easy to show

Format user data like this:

Input: John Smith, john@email.com, Engineer
Output:
---
Name: John Smith
Email: john@email.com
Role: Engineer
---

Input: Jane Doe, jane@email.com, Designer
Output:
```

## Next Steps

Once you're comfortable with zero-shot and few-shot, learn [Chain of Thought](chain-of-thought.md) prompting for complex reasoning tasks.
