# Required Watching

Curated video resources that are worth your time. These aren't random YouTube recommendations—they're videos that genuinely help you understand and use AI tools more effectively.

## Getting Started

*Videos for those new to AI-assisted development*

### [The Skill That Will Define The Next Decade of Work](https://www.youtube.com/watch?v=wv779vmyPVY)

**Speaker**: Jeremy Utley (Stanford) | **Length**: ~15 min

Jeremy Utley, adjunct professor of creativity and AI at Stanford, explains the fundamental mindset shift needed to get real value from AI. The key insight: **treat AI like a teammate, not a tool**.

Research showed that people who treat AI as a tool get mediocre results (and sometimes become *less* creative), while those who treat it as a teammate—coaching it, giving feedback, and getting it to ask *them* questions—dramatically outperform.

Highlights:

- The "realization gap": AI makes people 25% faster and 40% better quality, but less than 10% of professionals are seeing meaningful gains
- A National Park Service ranger built a tool in 45 minutes that saves 7,000 days of labor per year
- "Inspiration is a discipline" - what you bring to the model determines your output
- Creativity is "doing more than the first thing you think of"

**Quote**: "The only correct answer to the question 'how do you use AI' is: I don't use AI—I work with it."

## Claude Code

*Tutorials and deep dives on Claude Code specifically*

### [Claude Code Skills: Create Skills That Create Skills](https://www.youtube.com/watch?v=LJI7FafIDg4)

**Creator**: Tash (TÂCHES) | **Length**: ~25 min

A hands-on tutorial on Claude Code Skills - the feature that lets you package complex workflows into reusable, auto-invoked capabilities. Tash walks through building a skill from scratch using his meta `create-agent-skills` skill (a skill that creates skills).

What makes this valuable:

- **Live demonstration**: Watch a complete skill get built, break, and get fixed in real-time
- **The heal-skill workflow**: When a skill fails, capture what actually worked and update the skill automatically
- **XML over Markdown**: Why Tash uses pure XML structure for all skills/commands (Claude parses it better)
- **Slash command wrappers**: How to guarantee 100% skill invocation (no more "Claude only uses my skill 20% of the time")

Key concepts demonstrated:

- Skills auto-load their frontmatter (name + description) at session start (~50-100 tokens)
- Reference files only load when Claude actually needs them
- The ask-user-question workflow for gathering context before building
- Progressive disclosure: skill → references → API research → implementation

**Philosophy**: "With AI, it's your responsibility to assume that everything is possible. Dream bigger than what everybody else is telling you is possible."

The `create-agent-skills` and `heal-skill` tools shown are available in the [TÂCHES resources](https://github.com/glittercowboy/taches-cc-resources).

## Prompt Engineering

*Learn how to communicate effectively with AI*

### [Build an MCP Server in 5 Prompts](https://www.youtube.com/watch?v=FRogt98OF80)

**Creator**: Matt Pocock (AI Hero) | **Length**: ~15 min

A masterclass in structured prompting for real development. Matt builds a complete MCP server from scratch using just 5 carefully crafted prompts, demonstrating the difference between "vibe coding" and serious AI-assisted development.

The key framework - every prompt has three sections:

1. **Problem**: What are we trying to solve?
2. **Supporting Information**: Everything the LLM needs (tools, file structures, examples)
3. **Steps to Complete**: Explicit step-by-step instructions

Why this matters:

- **Planning and documentation are crucial** - "the boring stuff" is what makes AI-assisted dev actually work
- **File structure affects LLM understanding** - confusing structure = confused output
- **Context window is everything** - when the LLM hallucinates, it's usually because it didn't have the right files in context
- **Explicit beats implicit** - tell the LLM to "look at existing implementations first" rather than assuming it will

Real debugging shown:

- LLM invented a `createTool` function that didn't exist
- Fix: Add "look at existing implementations" to steps
- Lesson: The LLM had no idea what to copy because those files weren't in context

**Key insight**: "Was that our fault or the LLM's fault? I put this down to me not thinking ahead, not understanding what the LLM's context was supposed to be."

Great complement to the prompt engineering guides in this repo - shows these principles in action.

## Advanced Techniques

*For those ready to go deeper*

<!-- Add videos here -->

## Talks & Presentations

*Conference talks, interviews, and thought leadership*

<!-- Add videos here -->

---

## Contributing

Found a great video? This list is always growing. Videos should be:
- **Practical** - Actually teaches something useful
- **Current** - AI moves fast; outdated content can mislead
- **Quality** - Well-produced, clear explanations
- **Focused** - Not just hype or speculation

---

*Last updated: December 2024*
