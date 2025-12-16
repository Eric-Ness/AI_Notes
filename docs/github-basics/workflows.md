# Git Workflows with Claude

This guide covers practical workflows for using Claude Code with Git - branching, pull requests, and code review.

## Branching Workflow

### Why Use Branches?

Never work directly on `main`. Branches let you:
- Experiment without breaking working code
- Work on multiple features at once
- Review changes before merging
- Easily abandon failed experiments

### Creating a Feature Branch

```
You: Create a new branch for adding user authentication

Claude: I'll create a feature branch for this work.

        git checkout -b feature/user-auth

        Created and switched to branch 'feature/user-auth'.
        Ready to start working on user authentication.
```

### Branch Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Feature | `feature/description` | `feature/user-auth` |
| Bug fix | `fix/description` | `fix/login-redirect` |
| Hotfix | `hotfix/description` | `hotfix/security-patch` |
| Experiment | `experiment/description` | `experiment/new-ui` |

### The Branch Workflow

```
1. Create branch from main
2. Make changes, commit frequently
3. Push branch to GitHub
4. Create pull request
5. Review and merge
6. Delete branch
```

## Pull Requests with Claude

### Creating a PR

After you've made commits on your feature branch:

```
You: Create a pull request for this branch

Claude: I'll create a PR for your changes. Let me analyze
        what we've done on this branch.

        [Reads commit history and changed files]

        Creating PR with:
        - Title: Add user authentication
        - Summary of changes
        - List of files modified

        [Creates PR via gh cli]

        Done. PR #42 created: https://github.com/you/repo/pull/42
```

### What Claude Includes in PRs

Claude automatically generates:
- **Title**: Based on branch name and commits
- **Summary**: What the changes accomplish
- **Changed files**: List of what was modified
- **Testing notes**: If applicable

### Customizing the PR

```
You: Create a PR but emphasize that this needs security review

Claude: [Creates PR with security review callout]

        Added note: "⚠️ Security Review Requested -
        This PR modifies authentication logic."
```

## Code Review with Claude

### Reviewing Your Own Code

Before creating a PR:

```
You: Review the changes on this branch before I create a PR

Claude: I'll review all changes since branching from main.

        [Analyzes diffs]

        Found 3 items to address:

        1. **Bug** (high): SQL injection risk in user lookup
           - File: src/auth/users.js:45
           - Fix: Use parameterized query

        2. **Improvement** (medium): Missing error handling
           - File: src/auth/login.js:23
           - Consider: Add try/catch for API call

        3. **Style** (low): Inconsistent naming
           - File: src/auth/utils.js
           - Consider: Rename `usr` to `user`

        Want me to fix these before we create the PR?
```

### Reviewing a PR from GitHub

```
You: Review PR #38 on this repo

Claude: [Fetches PR details via gh cli]

        PR #38: "Add caching layer"
        Author: teammate
        Files changed: 5

        [Analyzes the diff]

        Review findings:

        ✅ Good: Clean separation of cache logic
        ✅ Good: Proper TTL handling

        ⚠️ Concern: Cache invalidation on user update
           might miss edge cases

        ❌ Issue: Memory leak potential in cache cleanup

        Want me to add these as review comments on the PR?
```

### Adding Review Comments

```
You: Yes, add those as review comments

Claude: [Uses gh cli to add comments]

        Added 2 comments to PR #38:
        - Line comment on src/cache.js:67 about invalidation
        - Line comment on src/cache.js:89 about memory leak

        PR is now marked as "Changes Requested"
```

## Handling Merge Conflicts

### When Conflicts Happen

Merge conflicts occur when the same code was changed in both branches.

```
You: Merge main into my branch to get latest changes

Claude: git merge main

        CONFLICT: Merge conflict in src/config.js

        I found a conflict. Let me show you what happened:

        Your version (feature branch):
        ```
        const API_URL = 'https://api.newservice.com';
        ```

        Main branch version:
        ```
        const API_URL = process.env.API_URL || 'https://api.default.com';
        ```

        The main branch added environment variable support.

        Recommendation: Keep main's version but use your new URL
        as the default:
        ```
        const API_URL = process.env.API_URL || 'https://api.newservice.com';
        ```

        Should I apply this resolution?
```

### Resolving with Claude's Help

```
You: Yes, that makes sense. Apply it.

Claude: [Edits file to resolve conflict]
        [Stages the resolved file]

        Conflict resolved. Ready to complete the merge.

        git add src/config.js
        git commit -m "Merge main, resolve config conflict"

        Done. Your branch now includes the latest from main.
```

## Common Workflows

### Feature Development

```
1. "Create branch for [feature]"
2. [Build the feature with Claude]
3. "Review changes before PR"
4. [Fix any issues]
5. "Create a pull request"
6. [Get human review if needed]
7. "Merge the PR"
8. "Delete the feature branch"
```

### Bug Fix

```
1. "Create a fix branch for [bug]"
2. "Find where [bug] is happening"
3. [Fix with Claude]
4. "Write a test that would catch this"
5. "Create PR for the fix"
```

### Keeping Branch Updated

```
You: My branch is behind main. Update it.

Claude: I'll pull the latest main and merge it into your branch.

        git fetch origin
        git merge origin/main

        [Handles any conflicts]

        Your branch is now up to date with main.
```

## Quick Reference

| Task | What to Ask Claude |
|------|-------------------|
| New branch | "Create a branch for [feature]" |
| See branches | "What branches exist?" |
| Switch branch | "Switch to [branch]" |
| Create PR | "Create a pull request" |
| Review PR | "Review PR #[number]" |
| Merge PR | "Merge PR #[number]" |
| Delete branch | "Delete the [branch] branch" |
| Handle conflict | "Help me resolve the merge conflict" |
| Update branch | "Merge main into my branch" |

## Best Practices

### 1. Branch Early

Create a branch before making changes, not after.

### 2. Keep Branches Focused

One branch = one feature or fix. Don't mix unrelated changes.

### 3. Commit Often

Small commits are easier to review and revert.

```
You: Commit what we have so far

Claude: [Commits with descriptive message]
```

### 4. Pull Main Regularly

Stay up to date to avoid big conflicts:

```
You: Pull latest main into my branch
```

### 5. Review Before PR

Always have Claude review your changes before creating a PR:

```
You: Review this branch for issues before I create the PR
```

### 6. Write Good PR Descriptions

Claude does this automatically, but you can guide it:

```
You: Create a PR. Emphasize that this changes the database schema
     and requires a migration.
```

## Next Steps

Return to [GitHub Basics](README.md) or explore [Core Commands](core-commands.md) for quick reference.
