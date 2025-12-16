# Core Git Commands

A quick reference for the Git commands you'll use most often. Bookmark this page.

## Daily Workflow

### Check Status

```bash
git status
```

Shows what's changed, what's staged, and what branch you're on. Use this constantly.

### See Changes

```bash
# All changes
git diff

# Changes to specific file
git diff filename.js

# Changes that are staged
git diff --staged
```

### Stage Files

```bash
# Stage specific file
git add filename.js

# Stage all changes
git add .

# Stage parts of a file interactively
git add -p filename.js
```

### Commit

```bash
# Commit with message
git commit -m "Add login validation"

# Commit with longer message (opens editor)
git commit
```

### Push to GitHub

```bash
# Push current branch
git push

# First push of a new branch
git push -u origin branch-name
```

### Pull from GitHub

```bash
# Get latest changes
git pull
```

## Branching

### See Branches

```bash
# Local branches
git branch

# All branches (including remote)
git branch -a
```

### Create Branch

```bash
# Create and switch to new branch
git checkout -b feature-name

# Or with newer Git:
git switch -c feature-name
```

### Switch Branches

```bash
git checkout branch-name

# Or with newer Git:
git switch branch-name
```

### Delete Branch

```bash
# Delete local branch
git branch -d branch-name

# Force delete (if not merged)
git branch -D branch-name
```

## History

### View Commits

```bash
# Recent commits
git log

# One line per commit
git log --oneline

# With graph
git log --oneline --graph

# Last 5 commits
git log -5
```

### See What Changed in a Commit

```bash
git show abc1234
```

### Who Changed This Line?

```bash
git blame filename.js
```

## Remote Operations

### See Remotes

```bash
git remote -v
```

### Fetch Without Merging

```bash
git fetch
```

### Clone a Repository

```bash
git clone https://github.com/user/repo.git
```

## GitHub CLI Commands

These require `gh` to be installed and authenticated.

### Repository

```bash
# List your repos
gh repo list

# Create new repo
gh repo create name --public

# Clone a repo
gh repo clone owner/repo
```

### Issues

```bash
# List issues
gh issue list

# Create issue
gh issue create --title "Bug title" --body "Description"

# View issue
gh issue view 42

# Close issue
gh issue close 42
```

### Pull Requests

```bash
# List PRs
gh pr list

# Create PR
gh pr create --title "Feature" --body "Description"

# View PR
gh pr view 123

# Check out a PR locally
gh pr checkout 123

# Merge PR
gh pr merge 123
```

### Status

```bash
# See status of your PRs, issues, etc.
gh status
```

## Configuration

### Set Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Set Default Branch Name

```bash
git config --global init.defaultBranch main
```

### See Configuration

```bash
git config --list
```

## Quick Combos

### Start of Day

```bash
git pull
git status
gh issue list
```

### End of Day

```bash
git add .
git commit -m "WIP: description of work"
git push
```

### New Feature

```bash
git checkout -b feature-name
# ... do work ...
git add .
git commit -m "Add feature"
git push -u origin feature-name
gh pr create
```

### Quick Fix

```bash
# ... make fix ...
git add .
git commit -m "Fix: description"
git push
```

## Cheat Sheet

| What | Command |
|------|---------|
| Status | `git status` |
| Stage all | `git add .` |
| Commit | `git commit -m "msg"` |
| Push | `git push` |
| Pull | `git pull` |
| New branch | `git checkout -b name` |
| Switch branch | `git checkout name` |
| View log | `git log --oneline` |
| Undo last commit | `git reset HEAD~1` |
| Discard changes | `git checkout -- .` |

## Tips

### Use Tab Completion

Most terminals support Git tab completion. Type `git ch` and press Tab.

### Aliases Save Time

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.st status
```

Now `git co main` works like `git checkout main`.

### Let Claude Help

You don't need to memorize all this. Just tell Claude what you want:

```
"Commit these changes"
"Create a new branch for this feature"
"Show me recent commits"
"Push to GitHub"
```

Claude knows the commands and will use them for you.
