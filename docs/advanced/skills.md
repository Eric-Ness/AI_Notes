# Skills

Skills are Claude Code's most powerful customization feature. They give Claude persistent expertise, workflows, and behaviors that activate when relevant. This guide explains what Skills are, why they matter, and how to use them effectively.

## What Are Skills?

A Skill is a markdown file (SKILL.md) that teaches Claude how to handle specific types of tasks. Unlike slash commands (which you invoke manually), Skills activate automatically when Claude detects they're relevant.

Think of Skills as giving Claude specialized training:
- A React skill makes Claude an expert React developer
- A debugging skill gives Claude a systematic debugging methodology
- A planning skill helps Claude break down complex projects

## Why Skills Matter

### Without Skills

Every session, you might find yourself saying:
- "Remember to use TypeScript"
- "Follow our naming conventions"
- "Don't forget error handling"
- "Use our project's patterns"

Claude does what you ask, but you're constantly repeating context.

### With Skills

Claude automatically:
- Knows your conventions
- Applies best practices
- Follows consistent workflows
- Uses domain-appropriate patterns

You focus on WHAT you want. Skills handle HOW it gets done.

## How Skills Work

### Location

Skills live in:
- **Project**: `.claude/skills/` (project-specific)
- **User**: `~/.claude/skills/` (global, all projects)

### Structure

A basic skill is just a markdown file:

```
~/.claude/skills/
└── react-expert/
    └── SKILL.md
```

The folder name becomes the skill identifier.

### Activation

Skills activate automatically based on:
- File types you're working with
- Keywords in your requests
- Project context
- Explicit invocation

You don't have to remember to "turn on" a skill.

## Using Pre-Built Skills

The fastest way to get started is using skills others have created.

### Installing Skills

#### Via Plugin (Easiest)

Some skill collections are available as plugins:

```bash
# Check available plugins
claude plugins list

# Install a plugin
claude plugins install plugin-name
```

#### Manual Installation

Copy skill folders to your skills directory:

```bash
# Clone a skill repository
git clone https://github.com/user/skill-repo

# Copy to your skills folder
cp -r skill-repo/skills/* ~/.claude/skills/
```

### Popular Skill Collections

#### Matt Pocock's Skills For Real Engineers

The companion repo to Matt Pocock's *Software Fundamentals Matter More Than Ever* talk (in [videos.md](../videos.md#software-fundamentals-matter-more-than-ever)) — straight from his actual `.claude/` directory. ~43k stars and actively maintained. Built around five failure modes Matt sees over and over with AI coding agents, with the fixes drawn from *The Pragmatic Programmer*, *A Philosophy of Software Design*, and *Domain-Driven Design*.

The headline skills:

- **`/grill-me`** — interviews you relentlessly until you and the agent share a *design concept* for what you're building (Matt's most popular skill — the one he says you should run *every time* before making a change)
- **`/grill-with-docs`** — same as above but with extra context-gathering for code work
- **`/ubiquitous-language`** — scans the codebase, surfaces terminology, builds a shared `CONTEXT.md` so the agent stops using 20 words where one will do
- **`/improve-codebase-architecture`** — refactors toward Ousterhout's *deep modules* pattern (few large modules with simple interfaces)
- **`/write-prd`** — planning skill that's explicit about module changes and interfaces

One-line install:

```bash
npx skills@latest add mattpocock/skills
```

Then run `/setup-matt-pocock-skills` — it prompts for your issue tracker (GitHub/Linear/local files), label conventions, and where to save docs.

GitHub: [mattpocock/skills](https://github.com/mattpocock/skills) — "Skills for Real Engineers. Straight from my .claude directory."

> 💡 **Read the README before bulk-installing.** The repo is opinionated against process-heavy frameworks (BMAD, Spec-Kit) and aims for small, composable skills. If you're already running a meta-framework, these skills may overlap or conflict with it — pick the individual ones you need rather than installing everything.

#### AGENTS Book Rules

Rule sets distilled from classic software engineering books, ready to drop into Claude Code, Codex, or Cursor. Covers *A Philosophy of Software Design*, *Clean Architecture*, *Clean Code*, *Code Complete*, *Designing Data-Intensive Applications*, *Domain-Driven Design* (three variants), *Patterns of Enterprise Application Architecture*, *Refactoring*, *Release It!*, *The Pragmatic Programmer*, and *Working Effectively with Legacy Code* — 13 books in total.

> ⚠️ **Don't install all 13 at once.** Active skills sit in context, and stacking the full versions of every book will burn through your context window before Claude has read your code. Pick the one or two that match the work you're actually doing. The repo itself acknowledges this — every rule set ships in three sizes:
>
> - **`mini`** — recommended for most real task use (~30-40 lines, ~2KB)
> - **`nano`** — compact fallback for tight context budgets (~30 lines, ~1KB)
> - **`full`** — canonical complete reference (often 250-1000 lines)
>
> Default to `mini`. Reach for `full` only when you're doing focused work where the extra detail earns its keep (e.g. refactoring legacy code with the Feathers book actively pinned).

How to choose between overlapping books:

| If you're doing... | Pick |
| --- | --- |
| Everyday coding, code review | *Clean Code* OR *The Pragmatic Programmer* (don't stack both — they overlap) |
| API / module design, fighting complexity | *A Philosophy of Software Design* |
| New service architecture, tech-churn resistance | *Clean Architecture* |
| Refactoring an existing codebase | *Refactoring* |
| Modernising legacy code without tests | *Working Effectively with Legacy Code* |
| Distributed systems, data consistency | *Designing Data-Intensive Applications* |
| Domain modelling for a complex business | *Domain-Driven Design Distilled* (lightest entry point) |
| Choosing patterns in enterprise apps | *Patterns of Enterprise Application Architecture* |
| Production reliability, failure modes | *Release It!* |

GitHub: [ciembor/agent-rules-books](https://github.com/ciembor/agent-rules-books) — see `USAGE.md` in the repo for editor-specific (Claude Code / Codex / Cursor) install instructions.

**Pairs well with**: Matt Pocock's *Software Fundamentals Matter More Than Ever* talk (in [videos.md](../videos.md#software-fundamentals-matter-more-than-ever)) — that talk argues these exact books matter more in the AI era; this repo is the operationalised version of that argument.

#### Domain Expertise Skills

Community-built expertise for specific tech stacks:
- React/Next.js development
- Python backend development
- Database design
- API development

Search GitHub for "claude-code skills" to find more.

## Skill Anatomy

Understanding skill structure helps you use them better and eventually create your own.

### Basic SKILL.md

```markdown
# React Expert

You are an expert React developer. When working on React code:

## Principles
- Use functional components with hooks
- Prefer composition over inheritance
- Keep components small and focused

## Patterns
- Custom hooks for shared logic
- Context for global state
- Error boundaries for resilience

## Code Style
- TypeScript for all components
- Named exports (not default)
- Props interfaces defined above component
```

### Advanced SKILL.md

More sophisticated skills include:
- Triggers (when to activate)
- References (supporting documents)
- Examples (code samples)
- Workflows (step-by-step processes)

```markdown
---
triggers:
  - "*.tsx"
  - "*.jsx"
  - "react"
  - "component"
---

# React Expert

[Core content...]

## Workflows

### New Component
1. Create component file
2. Define props interface
3. Implement component
4. Add tests
5. Export from index

## References
@references/react-patterns.md
@references/testing-guide.md
```

## Key Skills to Know

### Planning Skills

**What they do**: Break down complex projects into manageable phases.

**Why they matter**: Without planning, Claude jumps straight into coding. With a planning skill, Claude first creates a roadmap, identifies dependencies, and sequences work properly.

**Example**: A good planning skill produces hierarchical plans (Brief → Roadmap → Phase Plans) that Claude can then execute systematically.

### Debugging Skills

**What they do**: Provide a systematic methodology for finding bugs.

**Why they matter**: Without guidance, Claude might guess at fixes. A debugging skill enforces evidence gathering, hypothesis testing, and verification.

**Example**: The `debug-like-expert` skill activates when you're troubleshooting and guides Claude through proper root cause analysis.

### Domain Expertise Skills

**What they do**: Give Claude deep knowledge of specific technologies.

**Why they matter**: Generic advice vs. framework-specific best practices. A Next.js skill knows about App Router, Server Components, and the patterns that actually work.

**Example**: A `nextjs-expert` skill might include routing patterns, data fetching strategies, and deployment considerations specific to Next.js.

### Meta-Prompt Skills

**What they do**: Help Claude create prompts that other Claude instances will execute.

**Why they matter**: Complex workflows sometimes benefit from Claude preparing work for a fresh context. Meta-prompts are prompts designed for Claude-to-Claude communication.

**Example**: The `create-meta-prompts` skill helps build research → plan → implement pipelines.

## Getting the Most from Skills

### Let Skills Activate Naturally

You don't need to say "use the React skill." Just work on React code and relevant skills activate.

### Combine Multiple Skills

Skills stack. You might have:
- A React skill (domain expertise)
- A testing skill (quality practices)
- A planning skill (workflow management)

All active simultaneously, each contributing their expertise.

### Override When Needed

Skills are defaults, not mandates. You can always say:
- "Don't follow the usual pattern here because..."
- "Skip the planning phase, this is a quick fix"
- "Use a different approach this time"

### Review What's Active

Ask Claude:
```
What skills are currently active?
```

This helps you understand why Claude is behaving certain ways.

## Organizing Your Skills

### Project vs Global

| Location | Use Case |
|----------|----------|
| `.claude/skills/` | Project-specific conventions |
| `~/.claude/skills/` | Personal preferences, general expertise |

### Naming Conventions

```
~/.claude/skills/
├── react-expert/           # Domain expertise
├── python-backend/         # Domain expertise
├── debugging/              # Methodology
├── planning/               # Workflow
└── my-conventions/         # Personal style
```

### Keep Skills Focused

One skill = one area of expertise. Don't create a mega-skill that covers everything. Smaller, focused skills are:
- Easier to maintain
- More reliably activated
- Simpler to override

## Creating Your Own Skills

Once you're comfortable using skills, you can create your own.

### Start Simple

```markdown
# My Python Conventions

When writing Python code:

- Use type hints for all functions
- Docstrings for public functions (Google style)
- pytest for testing
- Black for formatting
- Sort imports with isort
```

Save as `~/.claude/skills/python-conventions/SKILL.md`

### Add Specificity Over Time

As you notice patterns:
- "I keep telling Claude to handle errors this way" → Add to skill
- "I always want tests structured like this" → Add to skill
- "Our API patterns are specific" → Add to skill

### Use Skills to Create Skills

A skill-creation skill (such as Anthropic's `skill-creator`) helps you build new skills:

```
I want to create a skill for our Django project conventions
```

Claude will guide you through creating a well-structured skill.

## Troubleshooting Skills

### Skill Not Activating

1. Check file location (`.claude/skills/` or `~/.claude/skills/`)
2. Verify folder contains `SKILL.md`
3. Check for syntax errors in frontmatter
4. Try explicit reference: "Use the [skill-name] skill"

### Skill Conflicting with Intent

Skills are suggestions. Override when needed:
```
I know the skill says X, but for this case do Y because...
```

### Too Many Skills Active

If Claude seems confused or inconsistent:
- Review active skills
- Disable conflicting ones
- Be explicit about which approach to use

## Next Steps

- Browse [Community Resources](community-resources.md) for ready-to-use skills
- Start simple: Install one skill, use it for a week, then expand

Skills are the difference between Claude as a generic assistant and Claude as your personalized development partner. Invest time here—it pays dividends on every future session.
