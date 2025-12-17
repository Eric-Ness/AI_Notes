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

### Emergent Learning Framework (ELF)

**What it is**: A system that enables Claude Code to learn from experience across sessions.

**GitHub**: https://github.com/Spacehunterz/Emergent-Learning-Framework_ELF

**Why it's valuable**: ELF solves the "Claude forgets everything" problem. It creates persistent memory that survives between sessions.

#### The Problem It Solves

Every Claude Code session starts fresh. Yesterday's lessons, patterns, and context are gone. You end up:
- Re-explaining project conventions
- Repeating what didn't work
- Losing institutional knowledge

ELF changes this by recording outcomes and building knowledge over time.

#### How It Works

**Persistent Learning**:
- Records successes and failures to local SQLite database
- Patterns strengthen through repeated validation
- Confidence scores (0.0 to 1.0) track reliability

**Knowledge Progression**:
```
Observations → Heuristics → Golden Rules
(raw data)    (tested)     (high confidence)
```

**Hotspot Analysis**:
- Tracks which files you touch most (pheromone trails)
- Visualizes development focus areas
- Helps understand project evolution

**Dashboard**:
- Local web interface (localhost:3001)
- Session history and analytics
- Knowledge graphs
- Natural language search across previous work

#### Multi-Agent Coordination

On Pro/Max plans, ELF supports coordinated agent swarms:
- **Researcher**: Gathers information
- **Architect**: Designs solutions
- **Skeptic**: Challenges assumptions
- **Creative**: Explores alternatives

These agents work together, with learnings shared across the system.

#### Getting Started

```
check in
```

This triggers auto-setup. No API keys needed beyond Claude Code itself.

The value compounds over time—weeks of use builds significant institutional knowledge.

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
2. **ELF** learns from each session
3. **Domain skills** provide expertise
4. **Custom commands** automate your workflows

The combination creates a sophisticated development environment tailored to you.

## Next Steps

1. Install TÂCHES resources - the planning and debugging skills are immediately useful
2. Try ELF if session persistence appeals to you
3. Search for domain skills matching your tech stack
4. As you get comfortable, explore building your own

The community has done incredible work. Take advantage of it.
