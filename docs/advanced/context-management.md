# Context Management

Claude Code has a context window—a limit on how much information it can hold in a single conversation. Understanding how context works helps you get better results and avoid degraded responses.

## How Context Works

### The Basics

Every conversation has a context limit (measured in tokens). This includes:
- Your messages
- Claude's responses
- File contents that were read
- Tool outputs
- System instructions

As you work, context fills up. When it approaches the limit, quality can degrade.

### The Quality Curve

Context usage affects response quality:

| Context Used | Quality |
|--------------|---------|
| 0-30% | Peak quality - comprehensive, thorough |
| 30-50% | Good quality - engaged, focused |
| 50-70% | Degrading - efficiency mode, less thorough |
| 70%+ | Poor - rushed, may miss details |

The key insight: degradation starts around 40-50%, not at the limit. Claude begins "compression mode" when it senses context getting full.

## Signs of Context Pressure

Watch for these indicators:

### Response Quality Changes
- Shorter, less detailed responses
- Skipping verification steps
- Missing edge cases
- Less thorough explanations

### Behavioral Changes
- Rushing to finish
- Not asking clarifying questions
- Making assumptions instead of checking
- Summarizing instead of showing work

### Explicit Warnings
Claude may mention context is getting full. Take this seriously.

## Strategies for Managing Context

### 1. Start Fresh for New Topics

Don't stretch one conversation forever. Start new sessions when:
- Switching to a different feature
- The current task is complete
- You notice quality degrading
- The conversation has gone very long

### 2. Use the Compact Command

```
/compact
```

This summarizes the conversation, reducing context usage while preserving key information.

### 3. Be Efficient with File Reads

Every file Claude reads adds to context.

**Less efficient**:
```
Read all the files in src/
Then tell me about the auth module
```

**More efficient**:
```
Find and read only the files related to authentication
```

### 4. Don't Repeat Large Contexts

If Claude already read a file, don't paste it again. Reference it:
```
Using the auth.js file you already read...
```

### 5. Break Large Tasks into Sessions

Instead of one massive session:

Session 1: "Plan the authentication feature"
Session 2: "Implement user registration"
Session 3: "Implement login flow"
Session 4: "Add password reset"

Each session starts fresh with focused context.

## Handoffs Between Sessions

When you need to continue work in a new session, preserve context with handoffs.

### Manual Handoff

Before ending:
```
Summarize our progress and what's left to do.
Format it so I can paste it into a new session.
```

### GitHub Issues

```
Create a GitHub issue documenting where we are
and what's remaining.
```

Next session:
```
Let's work on issue #42 - the authentication feature
```

### Planning Artifacts

Planning skills can produce artifacts (PLAN.md, SUMMARY.md) that carry context between sessions.

### Handoff Format

A good handoff includes:
1. **What was done** - Completed work
2. **Current state** - Where things stand
3. **What's next** - Remaining tasks
4. **Key decisions** - Important choices made
5. **Gotchas** - Things to remember

## When to Start Fresh

### Good Reasons to Start Fresh
- Task is complete
- Switching to unrelated work
- Quality is noticeably degraded
- You want a "clean slate" perspective

### Bad Reasons to Start Fresh
- Minor topic shift within same feature
- You hit a snag (work through it)
- Out of habit (continuity has value)

## Context-Efficient Practices

### Ask Targeted Questions

**Context heavy**:
```
Read all my code and tell me everything about it
```

**Context light**:
```
What testing framework does this project use?
Look at package.json and any test files.
```

### Incremental File Reading

**Heavy**:
```
Read the entire src/ directory
```

**Light**:
```
Read src/auth/login.ts
[work on it]
Now read src/auth/register.ts
[work on it]
```

### Use Search Over Read

```
Find where the database connection is configured
```

Better than reading every file looking for it.

### Reference, Don't Repeat

```
In the file you just edited...
Using the pattern from the previous component...
Apply the same fix to the other handlers...
```

## Monitoring Context

### Ask About Status

```
How much context are we using?
Are we approaching limits?
```

### Watch for Warnings

Claude may proactively mention context concerns. Don't ignore these.

### Notice Behavior Changes

If Claude's responses become noticeably shorter or less thorough, consider context pressure as a cause.

## The Compact Workflow

When you need to continue but context is high:

1. **Verify state**: "Summarize what we've accomplished"
2. **Compact**: `/compact`
3. **Verify retention**: "What are we working on?"
4. **Continue**: Resume work

This preserves essential context while freeing space.

## Multi-Session Workflows

For large projects, plan for multiple sessions:

### Phase-Based

```
Session 1: Phase 1 - Database setup
Session 2: Phase 1 - API routes
Session 3: Phase 2 - Authentication
...
```

### Feature-Based

```
Session 1: User registration
Session 2: User login
Session 3: Password reset
...
```

### Role-Based

```
Session 1: Planning and architecture
Session 2: Implementation
Session 3: Testing
Session 4: Documentation
```

## Context and Quality Trade-offs

### Longer Sessions

**Pros**:
- Continuity
- Accumulated context
- No re-explanation needed

**Cons**:
- Quality degradation over time
- Risk of confusion
- Harder to recover from mistakes

### Shorter Sessions

**Pros**:
- Fresh, high-quality responses
- Clean mental model
- Easy to course-correct

**Cons**:
- Context re-establishment needed
- May lose nuance
- More overhead

### The Balance

Most effective: Medium-length sessions with clear handoffs.

## Quick Reference

| Situation | Action |
|-----------|--------|
| Starting new feature | New session |
| Continuing same feature | Same session (if quality good) |
| Quality degrading | `/compact` or new session |
| Task complete | New session for next task |
| Long conversation | Consider handoff |
| Switching topics | New session |

## Key Takeaways

1. **Context affects quality** - Full context = degraded responses
2. **Fresh starts are powerful** - Don't fear new sessions
3. **Handoffs preserve continuity** - Document before switching
4. **Efficiency matters** - Read what you need, not everything
5. **Monitor quality** - Watch for degradation signs

Effective context management is about working WITH the limits, not fighting them.
