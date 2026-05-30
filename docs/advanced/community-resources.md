# Community Resources

The Claude Code community has built impressive tools that extend what's possible. This guide highlights the best resources available and how to use them.

## Why Use Community Resources?

You don't have to build everything yourself. The community has already solved many common problems:
- Project planning and breakdown
- Persistent learning across sessions
- Debugging methodologies
- Domain-specific expertise
- Workflow automation

These resources represent hundreds of hours of iteration and refinement.

## Featured Resources

### Sequential Thinking MCP Server

**What it is**: An MCP server that enables structured, step-by-step reasoning for complex problems.

**Resources**:

- [Official GitHub](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking)
- [MCP Servers Directory](https://mcpservers.org/servers/camilovelezr/server-sequential-thinking)
- [Playbooks Guide](https://playbooks.com/mcp/anthropic-sequential-thinking)

**Why it's valuable**: Instead of trying to solve complex problems all at once, Sequential Thinking breaks them down into manageable steps with the ability to revise, branch, and course-correct as understanding evolves.

#### What It Does

The server provides a `sequentialthinking` tool that enables:

- **Dynamic problem decomposition** - Break complex challenges into smaller steps
- **Revision capability** - Reconsider and update earlier conclusions as you learn more
- **Branching logic** - Explore alternative approaches when needed
- **Flexible depth** - Adjust the number of thinking steps as the problem requires
- **Context preservation** - Maintain coherence across extended reasoning chains

#### Best For

- Complex multi-step analysis
- Planning tasks that may need revision
- Problems with unclear scope
- Tasks requiring context across many thinking steps

#### Sequential Thinking: Installation

**Claude Code** (simple):

```bash
claude mcp add sequential-thinking -- npx -y @anthropic/mcp-server-sequential-thinking
```

**Claude Code** (JSON format):

```bash
claude mcp add-json "sequential-thinking" '{"command":"npx","args":["-y","@modelcontextprotocol/server-sequential-thinking"]}'
```

**Claude Desktop** (add to config):

```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-sequential-thinking"]
    }
  }
}
```

#### Sequential Thinking: From Source

Clone and run the server directly:

```bash
git clone https://github.com/camilovelezr/server-sequential-thinking.git
cd server-sequential-thinking
npm install
```

Start the server (uses Streamable HTTP transport on port 3000):

```bash
npm start
```

Change the port with the `PORT` environment variable:

```bash
PORT=8080 npm start
```

#### Sequential Thinking: Docker

Build and run in a containerized environment:

```bash
# Build the image
docker build -t mcp-server-sequential-thinking .

# Run the container
docker run -p 3000:3000 mcp-server-sequential-thinking
```

#### When to Use It

| Situation | Sequential Thinking Helps? |
|-----------|---------------------------|
| Quick simple tasks | No - overkill |
| Complex debugging | Yes - systematic investigation |
| Architecture decisions | Yes - explore trade-offs |
| Multi-step planning | Yes - revise as you learn |
| Research tasks | Yes - branch and explore |

---

## Other Notable Resources

### Domain Expertise Collections

Search GitHub for Claude Code skills in your tech stack:
- `claude-code-react` - React/Next.js expertise
- `claude-code-python` - Python development patterns
- `claude-code-[framework]` - Framework-specific skills

### Prompt Libraries

Collections of effective prompts:
- Code review prompts
- Documentation generation
- Test writing strategies

### Integration Tools

- Database connectors (MCP servers)
- CI/CD integrations
- IDE-specific enhancements

## Finding More Resources

### GitHub Search

```
"claude code" skills
"claude code" commands
mcp-server-[service]
```

### Community Channels

- Claude Code Discord/Forums
- Reddit r/ClaudeAI
- Twitter/X #ClaudeCode

### Evaluation Criteria

When evaluating community resources:

| Criterion | Why It Matters |
|-----------|----------------|
| Stars/Forks | Community validation |
| Recent updates | Active maintenance |
| Documentation | Usability |
| Issue responses | Author engagement |
| Scope | Focused vs. bloated |

## Installing Community Resources

### Plugins (Easiest)

```bash
claude plugins list
claude plugins install [name]
```

### Manual Installation

```bash
# Clone repository
git clone https://github.com/user/resource-repo

# Copy skills
cp -r resource-repo/skills/* ~/.claude/skills/

# Copy commands
cp -r resource-repo/commands/* ~/.claude/commands/
```

### Selective Installation

You don't have to install everything. Pick what you need:

```bash
# Just the skill you want
cp -r resource-repo/skills/skill-name ~/.claude/skills/
```

## Best Practices

### Start with One Resource

Don't install everything at once. Start with one tool, use it for a week, then expand.

### Read the Documentation

Good resources have documentation. Read it before installing—you'll get more value.

### Customize After Learning

Use resources as-is first. Once you understand them, customize for your workflow.

### Keep Updated

Resources improve over time:

```bash
cd ~/.claude/skills/resource-name
git pull
```

### Contribute Back

Found a bug? Have an improvement? Community resources thrive on contributions.

## Combining Resources

Resources can work together:

1. **Project planning skills** break down your project
2. **Sequential Thinking** for complex reasoning
3. **Domain skills** provide expertise
4. **Custom commands** automate your workflows

The combination creates a sophisticated development environment tailored to you.

## Next Steps

1. Try Sequential Thinking MCP for complex problem-solving
2. Search for domain skills matching your tech stack
3. As you get comfortable, explore building your own

The community has done incredible work. Take advantage of it.
