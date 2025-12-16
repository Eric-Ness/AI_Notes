# Issues & Todos

GitHub Issues is more than a bug tracker - it's a powerful task management system that integrates directly with your code. When combined with Claude Code, it becomes your project's central nervous system.

## Why Use GitHub Issues?

### 1. Everything in One Place

Your code, your tasks, your discussions - all in the same repository. No context switching between tools.

### 2. Persistence Across Sessions

When you close Claude Code or start a new conversation, your todo list disappears. But GitHub Issues persist forever. They're your project's long-term memory.

### 3. Claude Can Manage Them

With the GitHub CLI set up, you can tell Claude:
- "Create an issue for this bug"
- "Add these tasks to GitHub"
- "What issues are open on this repo?"

### 4. Links to Code

Issues can reference commits, pull requests, and specific lines of code. Everything stays connected.

## The Workflow

### During a Session

1. You're working with Claude on a feature
2. You discover bugs or identify future tasks
3. Instead of forgetting them, tell Claude: "Add this to our issues"
4. Claude creates the issue on GitHub
5. Continue working on the current task

### Between Sessions

1. Start a new Claude Code session
2. Ask: "What issues are open on this repo?"
3. Pick one to work on
4. Claude has context from the issue description
5. Work, then close the issue when done

### The Big Picture

```
Discover Task → Create Issue → (later) Work on Issue → Close Issue
     ↓                              ↓
  Never forgotten              Full context preserved
```

## Creating Issues with Claude

### Quick Issue

```
Create a GitHub issue: "Add input validation to login form"
```

### Detailed Issue

```
Create a GitHub issue with this info:

Title: Login form lacks input validation
Labels: bug, security

Description:
The login form accepts any input without validation.
We need to:
- Validate email format
- Check password minimum length
- Sanitize inputs before database query

Found in: src/auth/login.js
```

### From Your Todo List

```
I have these tasks remaining:
1. Add unit tests for user service
2. Fix date formatting bug
3. Update API documentation

Add these as GitHub issues.
```

## Managing Issues

### View Open Issues

```
What issues are open on this repo?
```

Or via command line:

```bash
gh issue list
```

### View Specific Issue

```bash
gh issue view 42
```

### Close an Issue

After completing work:

```
Close issue #42 - we've implemented the fix
```

Or:

```bash
gh issue close 42
```

### Add Comments

```bash
gh issue comment 42 --body "Started working on this, ETA tomorrow"
```

## Issue Best Practices

### Write Good Titles

Bad: "Bug"
Good: "Login fails when email contains plus sign"

Bad: "Add feature"
Good: "Add password reset functionality"

### Include Context

A good issue has:
- **What**: Clear description of the task or bug
- **Where**: File/function/line if known
- **Why**: Why this matters (for features) or how to reproduce (for bugs)

### Use Labels

Common labels:
- `bug` - Something is broken
- `enhancement` - New feature or improvement
- `documentation` - Docs need updating
- `good first issue` - Simple task, good starting point

### Keep Issues Focused

One issue = one task. If an issue grows too big, split it:

```
This issue has become too large. Let's split it:

1. Create issue: "Add user registration endpoint"
2. Create issue: "Add email verification flow"
3. Create issue: "Add registration UI form"

Close this issue and reference the new ones.
```

## Linking Issues to Work

### Reference in Commits

When you commit, reference the issue:

```
git commit -m "Add email validation, fixes #42"
```

The magic words (`fixes`, `closes`, `resolves`) automatically close the issue when merged.

### Reference in PRs

Pull request descriptions can reference issues:

```markdown
## Summary
Implements user registration flow

Closes #42
Closes #43
Related to #38
```

## The Claude Code + Issues Workflow

### Starting a Session

```
I'm starting work on this project. What issues are open?
Let's work on issue #15 today.
```

Claude will:
1. Fetch the issue details
2. Understand the context
3. Start working with that context in mind

### During Development

```
We found a bug - the date picker doesn't work in Safari.
Create an issue for this so we don't forget, but let's
keep working on the current task.
```

### Ending a Session

```
We're stopping for today. Let's:
1. Commit what we have
2. Create issues for the remaining tasks
3. Close any issues we completed
```

This ensures nothing is lost between sessions.

## Quick Reference

| Task | Command |
|------|---------|
| List issues | `gh issue list` |
| Create issue | `gh issue create --title "Title" --body "Description"` |
| View issue | `gh issue view 42` |
| Close issue | `gh issue close 42` |
| Reopen issue | `gh issue reopen 42` |
| Add comment | `gh issue comment 42 --body "Comment"` |
| Add labels | `gh issue edit 42 --add-label "bug"` |

## Next Steps

Learn about [Reverting Changes](reverting-changes.md) for when you need to undo mistakes.
