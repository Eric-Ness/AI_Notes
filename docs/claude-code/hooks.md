# Hooks

Hooks let you run custom actions automatically when certain events happen in Claude Code. They're like triggers that fire code in response to Claude's actions.

## Why Use Hooks?

- **Validation**: Block dangerous commands before they run
- **Automation**: Auto-format code after edits
- **Notification**: Alert you when certain actions happen
- **Logging**: Track what Claude does
- **Integration**: Connect to external tools

## Hook Types

| Hook | When It Fires |
|------|---------------|
| `PreToolUse` | Before Claude uses a tool (can block) |
| `PostToolUse` | After Claude uses a tool |
| `UserPromptSubmit` | When you send a message |
| `Stop` | When Claude finishes responding |
| `SessionStart` | When a session begins |

## Configuration

Hooks are configured in your settings file.

### Location

- **Project**: `.claude/settings.json`
- **User**: `~/.claude/settings.json`

### Basic Structure

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "command": "node ./scripts/validate-command.js"
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Edit",
        "command": "npm run format"
      }
    ]
  }
}
```

## PreToolUse Hooks

Run before Claude executes a tool. Can block the action.

### Validate Commands

Block dangerous bash commands:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "command": "node ./scripts/check-command.js"
      }
    ]
  }
}
```

`scripts/check-command.js`:

```javascript
const input = JSON.parse(process.argv[2] || '{}');
const command = input.command || '';

const dangerous = ['rm -rf', 'DROP TABLE', 'format c:', 'del /f'];

for (const pattern of dangerous) {
  if (command.includes(pattern)) {
    console.error(`Blocked dangerous command: ${pattern}`);
    process.exit(1); // Non-zero = block the action
  }
}

process.exit(0); // Zero = allow
```

### Require Confirmation for Certain Files

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit",
        "command": "node ./scripts/check-protected-files.js"
      }
    ]
  }
}
```

```javascript
const input = JSON.parse(process.argv[2] || '{}');
const file = input.file_path || '';

const protected = ['.env', 'secrets.json', 'config/production.js'];

if (protected.some(p => file.includes(p))) {
  console.error(`Protected file: ${file}`);
  console.error('This file requires manual editing.');
  process.exit(1);
}

process.exit(0);
```

## PostToolUse Hooks

Run after Claude completes a tool action. Good for post-processing.

### Auto-Format After Edits

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit",
        "command": "npm run format"
      }
    ]
  }
}
```

### Run Linter After Changes

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit",
        "command": "npm run lint:fix"
      }
    ]
  }
}
```

### Log All File Changes

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit",
        "command": "node ./scripts/log-change.js"
      }
    ]
  }
}
```

```javascript
const fs = require('fs');
const input = JSON.parse(process.argv[2] || '{}');

const log = {
  timestamp: new Date().toISOString(),
  file: input.file_path,
  action: 'edit'
};

fs.appendFileSync('claude-changes.log', JSON.stringify(log) + '\n');
```

## UserPromptSubmit Hooks

Run when you submit a message to Claude.

### Log All Prompts

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "command": "node ./scripts/log-prompt.js"
      }
    ]
  }
}
```

### Add Context Automatically

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "command": "node ./scripts/add-context.js"
      }
    ]
  }
}
```

## Stop Hooks

Run when Claude finishes a response.

### Notification

```json
{
  "hooks": {
    "Stop": [
      {
        "command": "node ./scripts/notify.js"
      }
    ]
  }
}
```

### Auto-Test After Changes

```json
{
  "hooks": {
    "Stop": [
      {
        "command": "npm test"
      }
    ]
  }
}
```

## SessionStart Hooks

Run when Claude Code starts.

### Environment Check

```json
{
  "hooks": {
    "SessionStart": [
      {
        "command": "node ./scripts/check-environment.js"
      }
    ]
  }
}
```

```javascript
const required = ['DATABASE_URL', 'API_KEY'];
const missing = required.filter(key => !process.env[key]);

if (missing.length > 0) {
  console.warn(`Warning: Missing environment variables: ${missing.join(', ')}`);
}
```

## Matchers

Matchers specify which tool actions trigger the hook.

### Match Specific Tool

```json
{
  "matcher": "Bash",
  "command": "..."
}
```

### Match Multiple Tools

```json
{
  "matcher": "Edit|Write",
  "command": "..."
}
```

### Match All

Omit matcher to match everything:

```json
{
  "command": "..."
}
```

### Tool Names

Common tools you can match:

| Tool | What It Does |
|------|--------------|
| `Bash` | Terminal commands |
| `Edit` | Edit existing files |
| `Write` | Create new files |
| `Read` | Read file contents |
| `Glob` | Search for files |
| `Grep` | Search file contents |

## Input Data

Your hook script receives JSON data about the action:

### Bash Tool

```json
{
  "tool": "Bash",
  "command": "npm install lodash"
}
```

### Edit Tool

```json
{
  "tool": "Edit",
  "file_path": "/path/to/file.js",
  "old_string": "original code",
  "new_string": "updated code"
}
```

### Access in Script

```javascript
const input = JSON.parse(process.argv[2] || '{}');
console.log(input.tool);
console.log(input.file_path);
```

## Blocking Actions

For PreToolUse hooks, exit code determines if action proceeds:

- **Exit 0**: Allow the action
- **Exit non-zero**: Block the action

```javascript
if (shouldBlock) {
  console.error('Action blocked: reason');
  process.exit(1);  // Block
}
process.exit(0);    // Allow
```

## Practical Examples

### Security: Block rm -rf /

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "command": "node -e \"const cmd = JSON.parse(process.argv[1]).command; if(cmd.match(/rm\\s+-rf\\s+\\//)) { console.error('Blocked'); process.exit(1); }\""
      }
    ]
  }
}
```

### Quality: Auto-format Python

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit",
        "command": "black . --quiet"
      }
    ]
  }
}
```

### Workflow: Run Tests on Changes

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "command": "npm test -- --bail --findRelatedTests"
      }
    ]
  }
}
```

### Audit: Log Everything

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "command": "node ./scripts/audit-log.js pre"
      }
    ],
    "PostToolUse": [
      {
        "command": "node ./scripts/audit-log.js post"
      }
    ]
  }
}
```

## Best Practices

### 1. Keep Hooks Fast

Hooks run synchronously. Slow hooks slow down Claude.

### 2. Handle Errors Gracefully

```javascript
try {
  // Your logic
} catch (error) {
  console.error('Hook error:', error.message);
  process.exit(0); // Don't block on errors unless intended
}
```

### 3. Use Specific Matchers

Match only what you need:

```json
// Good - specific
{ "matcher": "Bash", "command": "..." }

// Avoid - too broad
{ "command": "..." }
```

### 4. Log for Debugging

When developing hooks:

```javascript
console.error('Hook input:', JSON.stringify(input, null, 2));
```

Use stderr so it doesn't interfere with stdout.

### 5. Test Before Deploying

Test your hook scripts manually:

```bash
echo '{"command":"rm -rf /"}' | node ./scripts/check-command.js
echo $?  # Should be 1 (blocked)
```

## Troubleshooting

### Hook Not Firing

1. Check settings.json syntax (valid JSON)
2. Verify file path is correct
3. Check matcher matches the tool name exactly

### Hook Blocking Everything

1. Check your exit codes
2. Add logging to see what's being checked
3. Test the condition logic separately

### Hook Running Slow

1. Move heavy processing to async/background
2. Consider if you really need this hook
3. Optimize the script

## Next Steps

Learn about [MCP Servers](mcp-servers.md) to extend Claude Code's capabilities with external tools.
