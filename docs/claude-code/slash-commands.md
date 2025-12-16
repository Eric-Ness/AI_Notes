# Slash Commands

Slash commands are reusable prompts you can invoke with a simple `/command` syntax. They're perfect for workflows you repeat often.

## Why Use Slash Commands?

Instead of typing the same complex prompt repeatedly:

```
Review this code for bugs, security issues, and performance problems.
Format your response with severity levels and specific line numbers.
Focus on the files I've changed in this branch.
```

Create a command and just type:

```
/review
```

Same result, every time, with consistent formatting.

## Built-in Commands

Claude Code comes with several built-in commands:

| Command | What It Does |
|---------|--------------|
| `/help` | Show available commands |
| `/clear` | Clear conversation history |
| `/compact` | Summarize and compress context |
| `/config` | Open settings |
| `/cost` | Show token usage |
| `/doctor` | Diagnose issues |
| `/init` | Initialize project settings |

Type `/` to see all available commands.

## Creating Custom Commands

Custom commands live in your project's `.claude/commands/` folder as Markdown files.

### Basic Structure

```
.claude/
└── commands/
    └── review.md
```

The filename becomes the command: `review.md` → `/review`

### Simple Example

Create `.claude/commands/review.md`:

```markdown
Review the code changes in this branch for:
- Bugs and logic errors
- Security vulnerabilities
- Performance issues
- Code style violations

Format findings as:
## [Severity] Issue Title
**File:** filename:line
**Problem:** Description
**Fix:** Suggested solution
```

Now `/review` runs this prompt.

### Command with Description

Add YAML frontmatter for metadata:

```markdown
---
description: Review code for bugs, security, and performance
---

Review the code changes in this branch for:
- Bugs and logic errors
...
```

The description shows up in `/help` and autocomplete.

## Command Arguments

Commands can accept arguments using `$ARGUMENTS`.

### Example: Commit Command

Create `.claude/commands/commit.md`:

```markdown
---
description: Create a commit with the given message
---

Create a git commit with this message: $ARGUMENTS

If no message provided, analyze the changes and suggest an appropriate message.
```

Usage:

```
/commit Add user authentication
/commit Fix date parsing bug in reports
/commit    (will auto-generate message)
```

## Dynamic Context

Commands can reference files and use variables.

### Reference Current File

Use `@file` to include file contents:

```markdown
---
description: Explain the current file
---

@file

Explain what this code does:
- Purpose and main functionality
- Key functions/classes
- Dependencies
- Any notable patterns
```

### Reference Specific Files

```markdown
---
description: Compare two files
---

Compare these files and explain the differences:

@src/old-implementation.ts
@src/new-implementation.ts
```

### Project Context

Reference project files for consistent context:

```markdown
---
description: Generate code following project conventions
---

@CLAUDE.md
@src/types/index.ts

Generate code that follows our project conventions as documented above.

$ARGUMENTS
```

## Practical Examples

### /test - Generate Tests

```markdown
---
description: Generate tests for current file or specified function
---

@file

Generate comprehensive tests for this code:
- Unit tests for each public function
- Edge cases and error conditions
- Use the existing test framework in this project
- Follow the testing patterns already established

Focus on: $ARGUMENTS
```

### /doc - Add Documentation

```markdown
---
description: Add documentation to code
---

@file

Add documentation to this code:
- JSDoc/docstrings for all public functions
- Inline comments for complex logic
- README section if this is a module

Keep documentation concise but complete.
```

### /fix - Quick Bug Fix

```markdown
---
description: Fix a bug based on description
---

There's a bug: $ARGUMENTS

Steps:
1. Find the relevant code
2. Identify the root cause
3. Implement a fix
4. Verify with tests if applicable

Show me the fix before applying it.
```

### /refactor - Improve Code

```markdown
---
description: Refactor code for better quality
---

@file

Refactor this code to improve:
- Readability
- Maintainability
- Performance (if obvious wins)

Don't change functionality. Show proposed changes before applying.

Focus on: $ARGUMENTS
```

### /pr - Create Pull Request

```markdown
---
description: Create a PR for current branch
---

Create a pull request:
1. Summarize all commits on this branch
2. List files changed
3. Write a clear description
4. Note any breaking changes
5. Create the PR using gh cli
```

### /standup - Daily Summary

```markdown
---
description: Summarize recent work for standup
---

Summarize my recent work:
1. Look at commits from the last 24 hours
2. Check recently modified files
3. List open issues assigned to me

Format as:
## Yesterday
- [list of completed items]

## Today
- [planned items based on open issues]

## Blockers
- [any issues or questions]
```

## Organization

### Project-Specific Commands

Put in your project:

```
your-project/
└── .claude/
    └── commands/
        ├── review.md
        ├── deploy.md
        └── test.md
```

These only work in this project.

### Global Commands

Put in your home directory for commands that work everywhere:

```
~/.claude/
└── commands/
    ├── explain.md
    ├── improve.md
    └── ask.md
```

### Naming Conventions

- Use lowercase: `review.md` not `Review.md`
- Use hyphens for multi-word: `code-review.md` → `/code-review`
- Keep names short but descriptive
- Prefix related commands: `git-commit.md`, `git-pr.md`, `git-status.md`

## Best Practices

### 1. Be Specific

Bad:
```markdown
Review the code
```

Good:
```markdown
Review the code changes in this branch for:
- Security vulnerabilities (especially SQL injection, XSS)
- Performance regressions
- Breaking API changes

Ignore: formatting, typos, minor style issues
```

### 2. Define Output Format

```markdown
Format your response as:

## Summary
[1-2 sentence overview]

## Findings
### [Critical/High/Medium/Low] Issue Name
- **Location:** file:line
- **Problem:** What's wrong
- **Solution:** How to fix
```

### 3. Include Context When Needed

```markdown
@CLAUDE.md
@package.json

Use our project conventions and dependencies as context.
```

### 4. Make It Idempotent

Commands should be safe to run multiple times:

```markdown
Check if tests exist before creating new ones.
Don't duplicate existing documentation.
```

### 5. Handle Missing Arguments

```markdown
$ARGUMENTS

If no arguments provided:
- Analyze the current file
- Focus on the most important issues
```

## Debugging Commands

### Test Your Command

Run it and see what happens:

```
/my-command test input
```

### Check It Loaded

```
/help
```

Your command should appear in the list.

### Common Issues

| Problem | Solution |
|---------|----------|
| Command not found | Check file is in `.claude/commands/` |
| Wrong behavior | Check Markdown syntax, especially frontmatter |
| Arguments not working | Use `$ARGUMENTS` (uppercase) |
| File references failing | Check `@file` paths are correct |

## Next Steps

Learn about [Hooks](hooks.md) to automate actions based on events.
