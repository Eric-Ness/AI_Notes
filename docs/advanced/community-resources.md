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

### TÂCHES Claude Code Resources

**What it is**: A comprehensive collection of commands, skills, and agents for Claude Code.

**GitHub**: https://github.com/glittercowboy/taches-cc-resources

**Why it's valuable**: This isn't just a random collection—it's a thoughtfully designed system for professional Claude Code usage. The philosophy: "When you use a tool like Claude Code, it's your responsibility to assume everything is possible."

#### What's Included

**Skills (7)**:
| Skill | Purpose |
|-------|---------|
| `create-plans` | Hierarchical project planning optimized for solo developers |
| `create-agent-skills` | Build new skills with expert guidance |
| `create-slash-commands` | Create custom commands |
| `create-subagents` | Configure specialized agents |
| `create-hooks` | Set up event automation |
| `create-meta-prompts` | Build Claude-to-Claude pipelines |
| `debug-like-expert` | Systematic debugging methodology |

**Commands (27)**:
- Meta-prompting tools (separate analysis from execution)
- Todo management (capture ideas without losing focus)
- Context handoff utilities
- 12 thinking frameworks (first-principles, Pareto, 5-whys, etc.)

**Agents (3)**:
- Skill auditor
- Slash command auditor
- Subagent auditor

#### Highlights

**create-plans**: This skill alone is worth the install. Instead of Claude diving straight into code, it:
1. Creates a project brief (vision and goals)
2. Builds a roadmap (phases and milestones)
3. Plans each phase in detail
4. Executes with clear verification criteria

For complex projects, this structure prevents the chaos of unplanned development.

**debug-like-expert**: Activates when troubleshooting and enforces proper debugging:
- Evidence gathering (not guessing)
- Hypothesis formation
- Systematic testing
- Verification before declaring "fixed"

**Thinking frameworks**: Commands like `/consider:first-principles`, `/consider:pareto`, and `/consider:5-whys` apply structured thinking to problems. Great for decisions and analysis.

#### Installation

Via plugin:
```bash
claude plugins install taches-cc-resources
```

Or manually clone and copy to your skills/commands directories.

---

### Get Shit Done (GSD)

**What it is**: A meta-prompting and context engineering system for Claude Code that automates project planning and execution.

**GitHub**: [get-shit-done](https://github.com/glittercowboy/get-shit-done)

**Why it's valuable**: Also from Tash (creator of TÂCHES), GSD addresses the core problem with "vibe coding" - inconsistent results that fall apart at scale. It provides structured context and methodical task breakdown.

#### GSD: The Problem It Solves

> "Vibecoding has a bad reputation. You describe what you want, AI generates code, and you get inconsistent garbage that falls apart at scale."

GSD prevents quality degradation by:

- Breaking work into atomic tasks
- Running each task in a fresh 200k-token context (no accumulated confusion)
- Maintaining persistent state tracking across sessions

#### GSD: How It Works

**Workflow Structure**:

1. **Project extraction** - Guided questioning creates PROJECT.md
2. **Ecosystem research** - Optional deep-dive for complex domains
3. **Roadmap creation** - Phase-based planning
4. **Atomic task execution** - Fresh subagent contexts per task
5. **Modular iteration** - Support for MVPs and feature additions

**Key Features**:

- XML-formatted prompts optimized for Claude
- Persistent state tracking (STATE.md)
- Clean Git history with documented summaries
- Deferred issue management
- 18+ commands for the complete development lifecycle

#### GSD: Installation

```bash
npx get-shit-done-cc
```

#### When to Use GSD vs TÂCHES

| Use Case | Recommendation |
|----------|----------------|
| Individual skills/commands | TÂCHES |
| Full project lifecycle automation | GSD |
| Learning how skills work | TÂCHES |
| Shipping complete projects | GSD |

Both are from the same creator and share the same philosophy - they complement each other.

---

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

**Claude Code**:

```bash
claude mcp add sequential-thinking -- npx -y @anthropic/mcp-server-sequential-thinking
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

**Docker**:

```bash
docker run -p 8080:8080 mcp/sequentialthinking
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
# Just the planning skill
cp -r resource-repo/skills/create-plans ~/.claude/skills/
```

## Best Practices

### Start with One Resource

Don't install everything at once. Start with one tool (like TÂCHES create-plans), use it for a week, then expand.

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

1. **TÂCHES planning** breaks down your project
2. **GSD** automates full project lifecycle
3. **Sequential Thinking** for complex reasoning
4. **Domain skills** provide expertise
5. **Custom commands** automate your workflows

The combination creates a sophisticated development environment tailored to you.

## Next Steps

1. Install TÂCHES resources - the planning and debugging skills are immediately useful
2. Try Sequential Thinking MCP for complex problem-solving
3. Search for domain skills matching your tech stack
4. As you get comfortable, explore building your own

The community has done incredible work. Take advantage of it.
