# MCP Servers

MCP (Model Context Protocol) servers extend Claude Code's capabilities by connecting it to external tools, databases, APIs, and services. Think of them as plugins that give Claude new abilities.

## What MCP Does

Without MCP, Claude Code can:
- Read/write files
- Run terminal commands
- Search your codebase

With MCP, Claude Code can also:
- Query databases directly
- Fetch web pages
- Access APIs
- Use specialized tools
- Connect to services like GitHub, Slack, etc.

## How It Works

```
You → Claude Code → MCP Server → External Service
                  ↓
              Response
```

MCP servers are programs that translate between Claude Code and external services. They expose "tools" that Claude can use.

## Finding MCP Servers

### Official Servers

Anthropic maintains servers for common use cases:
- Filesystem (enhanced file operations)
- GitHub (repository operations)
- PostgreSQL (database queries)
- SQLite (local databases)
- Fetch (web requests)

### Community Servers

The community has built servers for:
- Slack
- Notion
- Google Drive
- AWS services
- Docker
- And many more

Check the MCP server registry or search GitHub for "mcp-server-[service]".

## Configuration

MCP servers are configured in your settings.

### Location

- **Project**: `.claude/settings.json`
- **User**: `~/.claude/settings.json`

### Basic Structure

```json
{
  "mcpServers": {
    "server-name": {
      "command": "command-to-start-server",
      "args": ["arg1", "arg2"],
      "env": {
        "API_KEY": "your-key"
      }
    }
  }
}
```

## Common MCP Servers

### Filesystem Server

Enhanced file operations beyond basic read/write:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-filesystem", "/path/to/allowed/directory"]
    }
  }
}
```

### PostgreSQL Server

Direct database access:

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://user:pass@localhost:5432/mydb"
      }
    }
  }
}
```

Now Claude can:
```
Query the users table to find all admins
Show me the schema for the orders table
```

### SQLite Server

For local databases:

```json
{
  "mcpServers": {
    "sqlite": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-sqlite", "./database.db"]
    }
  }
}
```

### Fetch Server

Web requests and scraping:

```json
{
  "mcpServers": {
    "fetch": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-fetch"]
    }
  }
}
```

Now Claude can:
```
Fetch the API documentation from https://api.example.com/docs
Get the current weather from the weather API
```

### GitHub Server

Enhanced GitHub operations:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-github"],
      "env": {
        "GITHUB_TOKEN": "ghp_your_token_here"
      }
    }
  }
}
```

## Using MCP Tools

Once configured, Claude automatically has access to the tools. Just ask naturally:

### Database Queries

```
You: Show me all users who signed up in the last week

Claude: I'll query the database for recent signups.

        [Uses postgres.query tool]

        Found 47 users who signed up in the last 7 days:
        ...
```

### Web Fetching

```
You: What's the latest version of React?

Claude: Let me check the npm registry.

        [Uses fetch tool]

        The latest version of React is 18.2.0, released...
```

### Combined Operations

```
You: Fetch the API spec from our docs site and create
     database tables to match

Claude: [Uses fetch to get API spec]
        [Uses postgres to create tables]

        Done. I've created 5 tables matching the API spec...
```

## Installing MCP Servers

Most MCP servers are npm packages that run via `npx`:

```bash
# Test that a server works
npx -y @anthropic/mcp-server-postgres --help
```

If it runs, add it to your config.

### From Source

Some servers need to be cloned and built:

```bash
git clone https://github.com/example/mcp-server-custom
cd mcp-server-custom
npm install
npm run build
```

Then reference the built file:

```json
{
  "mcpServers": {
    "custom": {
      "command": "node",
      "args": ["/path/to/mcp-server-custom/dist/index.js"]
    }
  }
}
```

## Environment Variables

Keep secrets out of your config by using environment variables:

### In Config

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-postgres"],
      "env": {
        "DATABASE_URL": "${DATABASE_URL}"
      }
    }
  }
}
```

### In Your Environment

```bash
# .bashrc, .zshrc, or Windows environment
export DATABASE_URL="postgresql://..."
```

### Using .env Files

Some setups support loading from `.env`:

```
DATABASE_URL=postgresql://user:pass@localhost/mydb
GITHUB_TOKEN=ghp_xxxxx
```

## Security Considerations

### Principle of Least Privilege

Only give servers the access they need:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@anthropic/mcp-server-filesystem",
        "./src",  // Only src folder, not entire system
        "./tests"
      ]
    }
  }
}
```

### Read-Only When Possible

If you only need to query, don't give write access:

```json
{
  "env": {
    "DATABASE_URL": "postgresql://readonly_user:pass@localhost/db"
  }
}
```

### Token Scopes

Use minimal GitHub token scopes:
- `repo` for repository access
- `read:org` for organization info
- Don't use tokens with admin/delete permissions

### Audit What's Configured

Regularly review your MCP configs:

```bash
cat ~/.claude/settings.json | jq '.mcpServers'
```

## Troubleshooting

### Server Not Starting

1. Test manually:
   ```bash
   npx -y @anthropic/mcp-server-postgres
   ```
2. Check for missing dependencies
3. Verify environment variables are set

### Tools Not Appearing

1. Restart Claude Code after config changes
2. Check JSON syntax in settings
3. Look for error messages on startup

### Connection Errors

1. Verify credentials/tokens
2. Check network connectivity
3. Ensure services are running (database, API, etc.)

### Permission Denied

1. Check file/directory permissions
2. Verify database user has required grants
3. Check API token scopes

## Building Custom MCP Servers

You can build your own MCP servers for custom integrations.

### Basic Structure (Node.js)

```javascript
import { Server } from '@modelcontextprotocol/sdk/server';

const server = new Server({
  name: 'my-custom-server',
  version: '1.0.0'
});

// Define a tool
server.tool('my_tool', {
  description: 'Does something useful',
  parameters: {
    type: 'object',
    properties: {
      input: { type: 'string' }
    }
  }
}, async (params) => {
  // Tool implementation
  return { result: `Processed: ${params.input}` };
});

server.start();
```

### When to Build Custom

- Internal APIs not covered by existing servers
- Proprietary systems
- Specialized workflows
- Combining multiple services

## Practical Examples

### Full-Stack Development Setup

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-postgres"],
      "env": { "DATABASE_URL": "${DATABASE_URL}" }
    },
    "fetch": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-fetch"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-github"],
      "env": { "GITHUB_TOKEN": "${GITHUB_TOKEN}" }
    }
  }
}
```

### Data Analysis Setup

```json
{
  "mcpServers": {
    "sqlite": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-sqlite", "./data/analysis.db"]
    },
    "fetch": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-fetch"]
    }
  }
}
```

## Next Steps

Learn about [Settings](settings.md) to configure Claude Code's behavior and customize your experience.
