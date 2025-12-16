# Reverting Changes

Things go wrong. Code breaks. Features don't work as expected. Git's ability to undo changes is one of its most valuable features - and knowing how to use it will save you countless hours.

## The Safety Net Mindset

Before we dive in, remember: if you've committed your work, it's almost impossible to truly lose it. Git keeps everything. Even "deleted" commits can usually be recovered.

This means you can experiment freely. Try things. Break things. Git has your back.

## Three Levels of "Undo"

### 1. Uncommitted Changes (Working Directory)

You've edited files but haven't committed yet.

### 2. Staged Changes (Added but not committed)

You've run `git add` but haven't committed yet.

### 3. Committed Changes (In history)

You've committed and want to undo that commit.

Each level has different undo strategies.

## Undoing Uncommitted Changes

### Discard Changes to One File

```bash
git checkout -- filename.js
```

This restores the file to its last committed state. **Changes are lost permanently.**

### Discard All Uncommitted Changes

```bash
git checkout -- .
```

Nuclear option - restores everything. Use carefully.

### See What Would Be Lost First

```bash
git diff
```

Always check before discarding.

## Undoing Staged Changes

You ran `git add` but changed your mind.

### Unstage One File

```bash
git reset HEAD filename.js
```

The file is now unstaged but your changes are still there.

### Unstage Everything

```bash
git reset HEAD
```

All files unstaged, all changes preserved.

## Undoing Commits

This is where it gets interesting. There are several approaches depending on your situation.

### Option 1: git revert (Safest)

Creates a NEW commit that undoes a previous commit. History is preserved.

```bash
# Undo the most recent commit
git revert HEAD

# Undo a specific commit
git revert abc1234
```

**When to use:**
- The commit is already pushed to GitHub
- You want to keep a record of the undo
- You're working with others

**Example:**

```
Before:  A -- B -- C (HEAD)
After:   A -- B -- C -- D (HEAD)
                        ↑
                    "Revert C"
```

Commit C still exists, but D undoes its changes.

### Option 2: git reset (Rewrites History)

Moves HEAD back to a previous commit. Can "erase" commits.

```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes unstaged
git reset HEAD~1

# Undo last commit, discard changes completely
git reset --hard HEAD~1
```

**When to use:**
- Commit hasn't been pushed yet
- You want to redo the commit differently
- You're the only one working on this branch

**Example:**

```
Before:  A -- B -- C (HEAD)
After:   A -- B (HEAD)
               ↑
           C is "gone" (but recoverable)
```

### Option 3: Amend Last Commit

Fix the most recent commit without creating a new one.

```bash
# Make your fixes, then:
git add .
git commit --amend
```

This replaces the last commit. Use only if you haven't pushed yet.

## Common Scenarios

### "I committed to the wrong branch"

```bash
# Save the commit hash first
git log -1  # Note the commit hash

# Switch to correct branch
git checkout correct-branch

# Apply the commit here
git cherry-pick abc1234

# Go back and remove from wrong branch
git checkout wrong-branch
git reset --hard HEAD~1
```

### "I need to undo the last 3 commits"

```bash
# Keep the changes, just uncommit
git reset HEAD~3

# Or discard everything
git reset --hard HEAD~3
```

### "I pushed a bad commit to GitHub"

```bash
# Create a revert commit
git revert HEAD

# Push the revert
git push
```

Don't use `reset` on pushed commits - it causes problems for anyone who pulled.

### "I want to see what a file looked like before"

```bash
# View file at specific commit
git show abc1234:path/to/file.js

# Restore file from specific commit
git checkout abc1234 -- path/to/file.js
```

### "I accidentally deleted a branch"

```bash
# Find the commit hash
git reflog

# Recreate the branch
git checkout -b recovered-branch abc1234
```

## The Reflog: Your Emergency Recovery

Git keeps a log of everywhere HEAD has been. Even after resets, you can recover.

```bash
# See the reflog
git reflog

# Output looks like:
# abc1234 HEAD@{0}: reset: moving to HEAD~1
# def5678 HEAD@{1}: commit: Add feature
# ghi9012 HEAD@{2}: commit: Fix bug

# Recover to any point
git reset --hard def5678
```

The reflog is your ultimate safety net.

## Quick Reference

| Situation | Command |
|-----------|---------|
| Discard uncommitted changes | `git checkout -- .` |
| Unstage files | `git reset HEAD` |
| Undo commit, keep changes | `git reset HEAD~1` |
| Undo commit, discard changes | `git reset --hard HEAD~1` |
| Undo pushed commit (safe) | `git revert HEAD` |
| Fix last commit message | `git commit --amend` |
| See where HEAD has been | `git reflog` |

## Using Claude for Reverts

You can ask Claude to help:

```
I need to undo my last commit but keep the changes
```

```
Revert to how the code looked 3 commits ago
```

```
I pushed a bug to main, help me revert it safely
```

Claude will use the appropriate strategy based on your situation.

## Golden Rules

1. **Check before discarding** - Use `git diff` and `git status` first
2. **Use revert for pushed commits** - Never reset public history
3. **When in doubt, branch first** - Create a backup branch before dangerous operations
4. **The reflog remembers** - Even "deleted" commits can be recovered

## Next Steps

For a quick reference of everyday Git commands, see [Core Commands](core-commands.md).
