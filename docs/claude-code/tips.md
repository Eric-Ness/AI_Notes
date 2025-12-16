# Tips & Best Practices

Practical tips for getting the most out of Claude Code, based on real usage patterns.

## Communication Tips

### Be Specific About What You Want

Bad:
```
Make this better
```

Good:
```
Refactor this function to:
1. Handle null inputs
2. Add TypeScript types
3. Split into smaller functions
```

### Tell Claude What NOT to Do

```
Add error handling to the API calls.
Don't change the existing function signatures.
Don't add new dependencies.
```

### Give Context Upfront

```
I'm working on the checkout flow. Users are reporting that
the payment sometimes fails silently. The relevant code is in
src/checkout/payment.ts. Let's investigate and fix this.
```

### Use "Let's" for Collaboration

```
Let's review the authentication flow
Let's refactor this to use hooks
Let's debug why tests are failing
```

This frames it as working together, not just giving orders.

## Workflow Tips

### Start Small, Then Expand

Instead of:
```
Build a complete user management system with registration,
login, profiles, roles, and admin dashboard
```

Do:
```
1. "Create a basic user registration form"
2. "Add validation to the form"
3. "Connect it to the API"
4. "Add login functionality"
...
```

### Review Before Approving

Always look at the diff Claude shows before approving changes. You'll catch:
- Unintended changes
- Missing edge cases
- Style inconsistencies

### Use Todo Lists

Tell Claude to track work:
```
Let's create a todo list for this feature:
1. Create the component
2. Add styling
3. Write tests
4. Update documentation
```

Claude will track progress and you can see what's done.

### Save Context with Issues

Before ending a session:
```
Create a GitHub issue with our progress and remaining tasks
```

This preserves context for the next session.

## Efficiency Tips

### Use Slash Commands for Repetitive Tasks

If you do something often, make it a command:
- `/review` - Code review
- `/test` - Generate tests
- `/doc` - Add documentation
- `/commit` - Commit changes

### Let Claude Search

Instead of telling Claude where something is:
```
Bad: "Edit the function in src/utils/helpers.js line 45"
Good: "Find and fix the date formatting bug"
```

Claude is good at searching. Let it find things.

### Batch Related Changes

Instead of:
```
1. "Add a name field to User"
2. "Add name to the registration form"
3. "Add name to the profile page"
4. "Add name to the API response"
```

Do:
```
"Add a name field to User and update all places that
need to use it - registration, profile, and API"
```

Claude handles multi-file changes well.

### Use Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Up arrow | Previous message |
| Ctrl+C | Cancel operation |
| Tab | Autocomplete |
| `/` | Start command |

## Quality Tips

### Ask for Tests

```
Add tests for the code you just wrote
```

Or better:
```
Add tests covering:
- Happy path
- Empty input
- Invalid input
- Edge cases
```

### Request Explanations

```
Explain why you made these changes
What are the trade-offs of this approach?
Are there any risks with this implementation?
```

### Verify Critical Changes

For important code:
```
Walk me through this logic step by step
What happens if the database is unavailable?
How does this handle concurrent requests?
```

### Use Claude for Code Review

```
Review the code I just wrote for:
- Bugs
- Security issues
- Performance problems
- Better approaches
```

## Project Setup Tips

### Create a Good CLAUDE.md

Spend time on CLAUDE.md upfront. It saves time on every future session.

Include:
- Tech stack
- Project structure
- Conventions
- Important commands

### Set Up .claudeignore

Exclude what Claude shouldn't see:
```
node_modules/
dist/
*.log
.env*
```

### Configure Auto-Approve

For trusted operations:
```json
{
  "permissions": {
    "autoApprove": ["Read", "Glob", "Grep", "Bash(npm test)"]
  }
}
```

### Use Git From the Start

Even for small projects. Claude works best with version control.

## Debugging Tips

### Give Error Context

```
I'm getting this error:
[paste full error]

It happens when I:
[describe steps]

Here's the relevant code:
[point to file or paste snippet]
```

### Ask for Debug Strategy

```
Help me debug this. Don't just fix it -
show me how to investigate so I can learn.
```

### Use Incremental Verification

```
1. "Add a console.log to verify the input"
2. [run and check]
3. "Now log the output of processData"
4. [run and check]
5. "Found it - the bug is in processData. Fix it."
```

## Safety Tips

### Don't Approve Blindly

Always review diffs, especially for:
- File deletions
- Configuration changes
- Database operations
- Anything with `rm`, `delete`, `drop`

### Keep Secrets Out

Never paste:
- API keys
- Passwords
- Tokens
- Private keys

Use environment variables instead.

### Commit Frequently

Small, frequent commits let you revert easily:
```
After each working change: "Commit this progress"
```

### Test Before Deploying

```
Run all tests before we commit
Check that the build succeeds
```

## Common Patterns

### The Exploration Pattern

```
1. "What does this codebase do?"
2. "Show me the main entry point"
3. "How does authentication work?"
4. "Now let's make changes..."
```

Understand before changing.

### The Fix-Verify Pattern

```
1. "Fix the bug"
2. "Write a test that would have caught this"
3. "Run the tests"
4. "Commit"
```

### The Refactor Pattern

```
1. "Write tests for current behavior"
2. "Run tests to verify they pass"
3. "Now refactor"
4. "Run tests again"
5. "Commit"
```

Tests protect refactors.

### The Learning Pattern

```
1. "Explain how [concept] works in this codebase"
2. "Show me an example"
3. "Now let me try - I'll write code and you review"
```

Use Claude to learn, not just produce.

## What to Avoid

### Don't Fight Claude's Approach

If Claude suggests a different way, hear it out. It might be better.

### Don't Paste Huge Files

Instead of pasting 1000 lines:
```
Look at src/bigfile.js and find the problematic section
```

### Don't Rush

Taking time to communicate clearly saves time overall.

### Don't Skip Reviews

Even when you trust Claude, review changes. You'll learn and catch issues.

## When Claude Struggles

### Break Down the Problem

If Claude seems stuck:
```
Let's step back. What's the simplest version of this we can build first?
```

### Provide More Context

```
Here's more context:
- This runs in a Docker container
- The database is PostgreSQL 14
- We're using Express 4.x
```

### Try a Different Angle

```
That approach isn't working. Let's try [alternative approach] instead.
```

### Ask for Options

```
Give me 3 different ways we could solve this, with trade-offs for each.
```

## Summary

1. **Be specific** - Clear requests get clear results
2. **Iterate** - Build incrementally
3. **Review** - Always check before approving
4. **Use tools** - Slash commands, CLAUDE.md, .claudeignore
5. **Commit often** - Small commits, easy reverts
6. **Learn** - Ask Claude to explain, not just do

The best results come from treating Claude as a capable collaborator, not a magic solution. Guide it, work with it, and verify its output.
