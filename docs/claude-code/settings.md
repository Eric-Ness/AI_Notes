# Settings & Configuration

Claude Code can be customized through settings files and CLAUDE.md project files. This guide covers all the ways to configure your environment.

## Configuration Hierarchy

Settings cascade from general to specific:

```
Default Settings (built-in)
    ↓
User Settings (~/.claude/settings.json)
    ↓
Project Settings (.claude/settings.json)
    ↓
CLAUDE.md (project instructions)
```

More specific settings override general ones.

## Settings File

### Location

| Scope | Path |
|-------|------|
| User (global) | `~/.claude/settings.json` |
| Project | `.claude/settings.json` |

### Creating Settings

```bash
# Global settings
mkdir -p ~/.claude
touch ~/.claude/settings.json

# Project settings
mkdir -p .claude
touch .claude/settings.json
```

### Basic Structure

```json
{
  "permissions": {
    "autoApprove": ["Read", "Glob", "Grep"],
    "deny": []
  },
  "hooks": {},
  "mcpServers": {}
}
```

## Permissions

Control what Claude can do without asking.

### Auto-Approve Safe Actions

```json
{
  "permissions": {
    "autoApprove": [
      "Read",
      "Glob",
      "Grep",
      "Bash(git status)",
      "Bash(git diff)",
      "Bash(npm test)"
    ]
  }
}
```

### Deny Dangerous Actions

```json
{
  "permissions": {
    "deny": [
      "Bash(rm -rf)",
      "Bash(sudo)",
      "Write(.env)"
    ]
  }
}
```

### Permission Patterns

| Pattern | Matches |
|---------|---------|
| `Read` | All file reads |
| `Bash(npm test)` | Specific command |
| `Bash(npm *)` | Commands starting with npm |
| `Write(.env)` | Writing to .env files |
| `Edit(src/*)` | Editing files in src/ |

## CLAUDE.md - Project Instructions

CLAUDE.md is a special file that gives Claude context about your project. It's like a README specifically for Claude.

### Location

- Project root: `CLAUDE.md`
- Or in: `.claude/CLAUDE.md`

### What to Include

```markdown
# Project: My Awesome App

## Overview
This is a React application for managing tasks. Built with TypeScript,
using Zustand for state management and Tailwind for styling.

## Tech Stack
- React 18
- TypeScript 5
- Zustand (state)
- Tailwind CSS
- Vitest (testing)

## Project Structure
```
src/
  components/   # React components
  hooks/        # Custom hooks
  store/        # Zustand stores
  utils/        # Helper functions
  types/        # TypeScript types
```

## Conventions
- Use functional components with hooks
- Name files in PascalCase for components
- Use absolute imports from 'src/'
- Write tests alongside components (*.test.tsx)

## Commands
- `npm run dev` - Start dev server
- `npm test` - Run tests
- `npm run build` - Production build

## Important Notes
- Never commit to main directly
- All API calls go through src/api/client.ts
- Environment variables must be prefixed with VITE_
```

### Why CLAUDE.md Helps

Without it, Claude has to figure out your project by reading code. With it, Claude:
- Knows your conventions immediately
- Uses the right patterns
- Understands your tech stack
- Follows your rules

### CLAUDE.md Best Practices

**Do include:**
- Tech stack and versions
- Project structure
- Naming conventions
- Important commands
- Things to avoid
- Key architecture decisions

**Don't include:**
- Sensitive information
- API keys or secrets
- Personal data
- Lengthy documentation (link to it instead)

## Multiple CLAUDE.md Files

You can have CLAUDE.md files in subdirectories for specific context:

```
project/
├── CLAUDE.md              # General project info
├── src/
│   └── api/
│       └── CLAUDE.md      # API-specific conventions
└── tests/
    └── CLAUDE.md          # Testing conventions
```

Claude reads the relevant CLAUDE.md based on what you're working on.

## Environment-Specific Settings

### Development vs Production

Create separate setting files:

```
.claude/
├── settings.json           # Base settings
├── settings.dev.json       # Dev overrides
└── settings.prod.json      # Prod overrides
```

Reference in your workflow or use environment detection.

### Team Settings

Share common settings via version control:

```json
// .claude/settings.json (committed)
{
  "hooks": {
    "PostToolUse": [
      { "matcher": "Edit", "command": "npm run lint:fix" }
    ]
  }
}
```

Keep personal settings in user config (`~/.claude/settings.json`).

## Model Configuration

### Select Model

```json
{
  "model": "claude-sonnet-4-20250514"
}
```

Available models vary by subscription.

### Context Settings

```json
{
  "context": {
    "maxTokens": 100000
  }
}
```

## Trust Settings

Control how much approval Claude needs.

### Trust Levels

```json
{
  "trust": {
    "level": "default"  // "default", "trusted", "full"
  }
}
```

| Level | Behavior |
|-------|----------|
| `default` | Approve each significant action |
| `trusted` | Auto-approve most actions in this project |
| `full` | Auto-approve everything (use carefully) |

### Per-Session Trust

You can also set trust for a session via CLI:

```bash
claude --trust
```

## Ignore Files

Tell Claude to skip certain files/folders.

### .claudeignore

Create `.claudeignore` in your project root:

```
# Dependencies
node_modules/
vendor/

# Build output
dist/
build/
.next/

# Large files
*.zip
*.tar.gz

# Sensitive
.env
secrets/
*.pem
```

Similar syntax to `.gitignore`.

### Why Ignore Files

- **Performance**: Don't scan node_modules
- **Relevance**: Skip build artifacts
- **Security**: Exclude sensitive files
- **Focus**: Help Claude focus on your code

## Customizing Appearance (CLI)

### Theme

```json
{
  "appearance": {
    "theme": "dark"  // "dark", "light", "auto"
  }
}
```

### Verbosity

```json
{
  "output": {
    "verbose": true,
    "showToolCalls": true
  }
}
```

## Complete Example

```json
{
  "permissions": {
    "autoApprove": [
      "Read",
      "Glob",
      "Grep",
      "Bash(git *)",
      "Bash(npm test)",
      "Bash(npm run lint)"
    ],
    "deny": [
      "Bash(rm -rf /)",
      "Bash(sudo *)",
      "Write(.env*)"
    ]
  },
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit",
        "command": "npm run format"
      }
    ]
  },
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-postgres"],
      "env": {
        "DATABASE_URL": "${DATABASE_URL}"
      }
    }
  },
  "trust": {
    "level": "default"
  }
}
```

## Viewing Current Settings

### CLI

```bash
claude /config
```

### Check Effective Settings

```bash
cat ~/.claude/settings.json
cat .claude/settings.json
cat CLAUDE.md
```

## Troubleshooting

### Settings Not Applied

1. Check JSON syntax (use a JSON validator)
2. Verify file location
3. Restart Claude Code after changes

### Permissions Not Working

1. Check pattern syntax
2. More specific patterns override general ones
3. Deny takes precedence over autoApprove

### CLAUDE.md Not Read

1. Check file is in project root or .claude/
2. Verify filename is exactly `CLAUDE.md`
3. Check file isn't empty

## Next Steps

Read [Tips](tips.md) for best practices and efficiency tricks.
