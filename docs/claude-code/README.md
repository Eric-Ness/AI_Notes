# Claude Code

Claude Code is an agentic coding tool that lives in your terminal or IDE. Unlike chat-based AI, Claude Code can actually *do things* - read your files, write code, run commands, and interact with your development environment.

## What Makes It Different

### Chat AI vs Claude Code

**Chat AI (Claude.ai, ChatGPT):**
- You copy/paste code into the chat
- AI gives you suggestions
- You copy/paste back into your editor
- Repeat for every change

**Claude Code:**
- Claude sees your entire project
- Claude edits files directly
- Claude runs tests and commands
- Claude commits to Git
- You guide, Claude executes

It's the difference between having a consultant who gives advice vs having a developer who does the work.

### The Agent Model

Claude Code is "agentic" - it takes actions, not just gives answers.

When you say "fix the bug in the login function," Claude Code:
1. Searches your codebase to find the login function
2. Reads the code and understands it
3. Identifies the bug
4. Edits the file to fix it
5. Optionally runs tests to verify
6. Reports what it did

You stay in control (approving changes) while Claude does the heavy lifting.

## What Claude Code Can Do

### File Operations
- Read any file in your project
- Create new files
- Edit existing files
- Search across your codebase

### Terminal Commands
- Run builds and tests
- Execute scripts
- Install packages
- Git operations

### GitHub Integration
- Create commits
- Open pull requests
- Manage issues
- Review code

### Extended Capabilities
- Connect to databases (via MCP)
- Fetch web content
- Use external APIs
- Custom tools and workflows

## What You'll Learn

| Guide | What It Covers |
|-------|----------------|
| [Installation](installation.md) | CLI setup + IDE extensions |
| [Basic Usage](basic-usage.md) | How to interact with Claude Code |
| [Slash Commands](slash-commands.md) | Custom reusable workflows |
| [Hooks](hooks.md) | Automate responses to events |
| [MCP Servers](mcp-servers.md) | Extend capabilities |
| [Settings](settings.md) | Configuration and CLAUDE.md |
| [Tips](tips.md) | Best practices and efficiency |

## Quick Example

Here's what a typical interaction looks like:

```
You: There's a bug where users can submit empty forms.
     Add validation to require all fields.

Claude: I'll add form validation. Let me look at your form component.

        [Reads src/components/ContactForm.tsx]

        I found the form. I'll add validation for required fields.

        [Edits ContactForm.tsx - adds validation logic]
        [Edits styles.css - adds error styling]

        Done. I've added:
        - Required field validation for name, email, message
        - Error messages that appear below invalid fields
        - Submit button disabled until form is valid

        Want me to run the tests to verify?
```

One request. Multiple files updated. Tests ready to run. That's the power of agentic coding.

## Start Here

1. **[Installation](installation.md)** - Get Claude Code running in your environment
2. **[Basic Usage](basic-usage.md)** - Learn how to interact effectively
3. Explore the advanced features as needed

## The Big Picture

Claude Code fits into your workflow like this:

```
You (Vision & Direction)
    ↓
Claude Code (Execution)
    ↓
Your Codebase (Results)
    ↓
Git/GitHub (Version Control)
```

You decide what to build. Claude helps you build it. Git keeps everything safe and tracked.
