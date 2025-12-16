# Basic Usage

This guide covers how to interact with Claude Code effectively - from simple questions to complex multi-file tasks.

## Starting a Session

### CLI

```bash
# Start in current directory
claude

# Start in specific directory
claude /path/to/project
```

### IDE

Open the Claude Code panel from:
- Sidebar icon (VS Code)
- Tool window (JetBrains)
- View menu (Visual Studio)

## The Conversation Model

Claude Code works through conversation. You describe what you want, Claude takes action, you provide feedback or approval.

### Basic Pattern

```
You: [Describe what you want]
Claude: [Shows what it will do, asks for approval if needed]
You: [Approve, modify, or redirect]
Claude: [Takes action, reports results]
```

### Example

```
You: Add a dark mode toggle to the settings page

Claude: I'll add a dark mode toggle. Let me first look at your
        settings page to understand the current structure.

        [Reads src/pages/Settings.tsx]

        I see you're using React with Tailwind. I'll:
        1. Add a toggle component
        2. Create a theme context
        3. Update your tailwind config

        Should I proceed?

You: Yes, go ahead

Claude: [Creates/edits files]

        Done. I've added:
        - ThemeContext.tsx - manages dark mode state
        - Toggle component in Settings.tsx
        - Dark mode classes in tailwind.config.js

        Refresh your app to see the changes.
```

## What You Can Ask Claude to Do

### Read and Understand

```
What does the auth module do?
Explain this function to me
Find where user validation happens
What dependencies does this project use?
```

### Write and Edit

```
Create a new React component for user profiles
Add error handling to this function
Refactor this class to use composition
Fix the bug where dates display incorrectly
```

### Search and Navigate

```
Find all files that import the database module
Where is the API rate limiting configured?
Show me all TODO comments in the codebase
Which components use the Button component?
```

### Run Commands

```
Run the tests
Build the project
Install lodash
Start the dev server
```

### Git Operations

```
Commit these changes
Create a branch for this feature
Show me the recent commits
What changed in the last commit?
```

## The Permission Model

Claude Code asks for permission before taking significant actions.

### Auto-Approved (Safe)

- Reading files
- Searching code
- Explaining code
- Listing directories

### Requires Approval

- Writing/editing files
- Running terminal commands
- Creating commits
- Deleting files

### How Approval Works

```
Claude: I'll edit src/utils/validate.js to add email validation.

        [Shows diff of proposed changes]

        Apply this change? (y/n)

You: y

Claude: [Applies change]
```

### Trust Modes

You can adjust how much approval is required:

- **Default**: Approve each action
- **Trust session**: Auto-approve for this session
- **Trust project**: Auto-approve for this project

Configure in settings or via CLI flags.

## Effective Communication

### Be Specific

Bad:
```
Fix the bug
```

Good:
```
The login form accepts empty passwords. Add validation
to require at least 8 characters.
```

### Provide Context

Bad:
```
Make it faster
```

Good:
```
The user list page is slow with 1000+ users.
Add pagination to load 50 users at a time.
```

### Iterate

Don't try to do everything in one message. Build incrementally:

```
1. "Create a basic user registration form"
2. "Add email validation"
3. "Add password strength requirements"
4. "Style it to match our other forms"
```

## Multi-File Operations

Claude Code excels at changes that span multiple files.

### Example: Adding a Feature

```
You: Add a "last login" timestamp to users

Claude: This will require changes to:
        1. Database schema (add column)
        2. User model (add field)
        3. Auth controller (update on login)
        4. User profile page (display it)

        Should I proceed with all of these?

You: Yes

Claude: [Makes all changes across files]
```

### Example: Refactoring

```
You: Move all API calls into a dedicated services folder

Claude: I'll create a services folder and extract API calls from:
        - UserComponent.tsx
        - ProductList.tsx
        - OrderPage.tsx

        [Creates services/userService.ts]
        [Creates services/productService.ts]
        [Creates services/orderService.ts]
        [Updates imports in all components]

        Done. All API calls are now in src/services/
```

## Using Context Effectively

### Current File

In IDE, Claude sees your open file. Reference it naturally:

```
Explain what this function does
Add error handling here
Refactor this to be more readable
```

### Specific Files

Point Claude to files:

```
Look at src/auth/login.ts and fix the validation
Compare package.json with package-lock.json
```

### Project-Wide

Ask about the whole project:

```
What testing framework does this project use?
Find all hardcoded strings that should be constants
Show me the API route structure
```

## Session Management

### Continuing Work

Within a session, Claude remembers context:

```
You: Create a Button component
Claude: [Creates Button.tsx]

You: Now add a loading state to it
Claude: [Updates the Button it just created]

You: Add tests for it
Claude: [Creates Button.test.tsx]
```

### Starting Fresh

New sessions start without memory of previous ones. Provide context:

```
I'm continuing work on the user dashboard feature.
Yesterday we created the layout. Today let's add the data fetching.
```

Or reference issues:

```
Let's work on issue #42 - the date formatting bug
```

## Common Workflows

### Bug Fix

```
1. "There's a bug where [description]"
2. Claude investigates, proposes fix
3. Approve the fix
4. "Run the tests to verify"
5. "Commit with message 'Fix: [description]'"
```

### New Feature

```
1. "I want to add [feature]"
2. Discuss approach with Claude
3. "Let's start with [first piece]"
4. Build incrementally
5. "Add tests for what we built"
6. "Commit this feature"
```

### Code Review

```
1. "Review the changes in this branch"
2. Claude analyzes diffs
3. "Fix the issues you found"
4. "Run tests"
```

## Keyboard Shortcuts (CLI)

| Shortcut | Action |
|----------|--------|
| Ctrl+C | Cancel current operation |
| Ctrl+D | Exit Claude Code |
| Up/Down | Navigate history |
| Tab | Autocomplete |

## Tips for Getting Started

1. **Start small** - Simple questions and tasks first
2. **Watch what Claude does** - Learn by observing its approach
3. **Don't be afraid to say no** - Reject changes that don't look right
4. **Iterate** - Refine results through conversation
5. **Use file references** - Point Claude to specific files when relevant

## Next Steps

Learn about [Slash Commands](slash-commands.md) to create reusable workflows.
