# GitHub Basics

Git and GitHub are essential tools for anyone working with code - and especially powerful when combined with AI assistants like Claude Code.

## Why Version Control Matters

### 1. Your Safety Net

Every change you make is saved. Made a mistake? Go back. Broke something that worked yesterday? Restore it. This isn't just convenient - it's liberating. You can experiment freely knowing you can always undo.

### 2. Your Project's Memory

Git remembers everything:
- What changed
- When it changed
- Why it changed (if you write good commit messages)

Six months from now, you can look back and understand exactly how your project evolved.

### 3. Collaboration Made Possible

Whether it's a teammate or an AI assistant, version control lets multiple contributors work on the same project without chaos. Everyone can see what changed and merge work together.

### 4. Claude Code Integration

This is the big one. When you connect GitHub to Claude Code:
- Claude can commit your changes
- Claude can create pull requests
- Claude can manage issues and todos
- Claude can read your project history

Without Git, Claude Code is helpful. With Git, Claude Code becomes a full development partner.

## What You'll Learn

| Guide | What It Covers |
|-------|----------------|
| [GitHub CLI Setup](github-cli-setup.md) | Connect Claude Code to GitHub |
| [Issues & Todos](issues-and-todos.md) | Task tracking with GitHub Issues |
| [Workflows](workflows.md) | Branching, PRs, and code review with Claude |
| [Reverting Changes](reverting-changes.md) | How to undo mistakes |
| [Core Commands](core-commands.md) | Essential Git commands reference |

## Start Here

If you're new to Git:
1. First, read through this page to understand the "why"
2. Then set up the [GitHub CLI](github-cli-setup.md) - this unlocks Claude Code's full potential
3. Learn the [Issues workflow](issues-and-todos.md) for task management

If you already use Git:
- Jump straight to [GitHub CLI Setup](github-cli-setup.md) if you haven't connected it to Claude Code
- Check [Reverting Changes](reverting-changes.md) for when things go wrong

## The Mental Model

Think of Git like this:

```
Your Code (working directory)
    ↓ git add
Staging Area (ready to save)
    ↓ git commit
Local Repository (saved on your machine)
    ↓ git push
GitHub (saved in the cloud, shareable)
```

Each step moves your changes closer to being permanent and shared. You control when and what moves forward.
