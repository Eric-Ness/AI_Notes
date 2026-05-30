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

### [Every Level of Claude Code Memory Systems](https://www.youtube.com/watch?v=UHVFcUzAGlM)

**Length**: ~30 min

A field guide through the six layers of memory architecture available to Claude Code — from the built-in `CLAUDE.md` / `memory.md` files all the way to a cross-tool Postgres "second brain" any AI app can read from. Same level-by-level framing (and likely same creator) as the *Every Level of Claude Code Skills* video below.

The framing question every memory system answers: *when you give Claude a task, how does it pull the right context at the right time?* Two variables: **where the memory lives** (markdown? vectors? SQLite? Postgres?) and **how Claude retrieves it** (always-loaded, hook-injected, MCP-queried, semantically searched).

The six levels:

1. **Native — `CLAUDE.md` + auto-memory** — already running on your machine. `CLAUDE.md` is always loaded; `memory.md` is the silent index Claude builds in the background. Cardinal rule: **keep `CLAUDE.md` under 200 lines** to dodge context rot. Stuff brand voice or full client lists into separate referenced files instead.
2. **Hook-injected structured memory** (John Connelly / Pavel Hurin) — adds a `SessionStart` hook that auto-injects a `~/.claude/memory/` index split into `general.md`, `domain/<topic>.md`, and `tools/<tool>.md`. Includes a `reorganize memory` command that prunes empties, consolidates duplicates, and adds cross-references. Shareable across teammates via synced domain files.
3. **Semantic search with mem-search** (Zilliz plugin) — ports OpenClaude's memory architecture into Claude Code as a 2-line install. Markdown-first, but chunks everything into vectors and uses a `UserPromptSubmit` hook to auto-inject the top-3 semantic matches into every prompt. *Compared to the alternative `claude-mem`*: mem-search keeps everything in readable markdown and auto-injects locally; claude-mem is MCP-based with a dashboard but Claude has to actively call its search tool.
4. **Verbatim recall with me-palace** — a proper local RAG system using SQLite (entities + relationships) plus Chroma DB (verbatim chunks). Indexes information into a "memory palace" structure (wing → room → closet → drawer) using a dense symbolic dialect the model can scan in a single pass. Claims the highest published memory-system benchmark and ~42 ms retrieval. Use when you need *exact words* from a decision made weeks ago, not summaries.
5. **Knowledge graphs — Karpathy's LLM Wiki / Recall / LightRAG** — a different problem entirely: building an interconnected knowledge base from articles, podcasts, transcripts. `raw/` folder holds sources Claude reads but never writes; `wiki/` folder Claude owns completely. Recall is the hosted, no-setup version; LightRAG is the enterprise-grade overkill version. **Skip this level unless you actually do deep research on connected topics** — it's not operational memory.
6. **Cross-tool memory — Open Brain (Nate Jones) / Mem0** — a Supabase-hosted Postgres `thoughts` table fronted by Edge Functions, queryable from ChatGPT, Claude Desktop, Cursor, Claude Code, anything via MCP. ~$0.10–0.30/month on Supabase free tier. Tradeoff: you give up local-only privacy and add network latency, but every tool sees the same brain. Mem0 is the production-ready hosted alternative, used by 100k+ devs but stores your data on their servers permanently.

**Which level should you actually pick?**

- **Just starting?** Stop at Level 1. Use `CLAUDE.md` properly, let auto-memory do its thing.
- **Used Claude Code for a month+?** Level 2. Install the hook, walk away. *The speaker's own recommendation is most people should stop here.*
- **Months of context, losing decisions?** Level 3 (mem-search) for semantic recall, or Level 4 (me-palace) for word-for-word.
- **Doing real cross-source research?** Level 5 — but only for that.
- **Switching between Claude Code, ChatGPT, Cursor, etc. constantly?** Level 6.

Levels 1, 2, and 3 stack cleanly together (similar folder structures). The speaker personally runs L1+L2+L3 inside their Aentic OS.

**Sneak peek**: when the Claude Code source briefly leaked, references surfaced to an unreleased Anthropic-internal system codenamed **Chyros** — an always-on daemon that watches the project, decides what's worth remembering, and consolidates notes overnight. Native memory is going to keep getting better.

### [Every Level of Claude Code Skills in 27 mins](https://www.youtube.com/watch?v=-u_igSQHAIo)

**Length**: ~27 min

A practical, layered tour through Claude Code Skills — from "what is a skill" all the way to self-improving skill systems that coordinate as an AI workforce. The framing as seven progressive levels makes it easy to find your current rung and the next one.

The seven levels:

1. **Understand what a skill actually is** — a folder of knowledge with one required file (`SKILL.md`), plus optional `scripts/`, `references/`, and `assets/` folders. Anthropic's *progressive disclosure* model is the key: YAML frontmatter is always loaded, the SKILL.md body loads only when triggered, references load only when needed.
2. **Build skills that don't bloat context** — keep `SKILL.md` under 200 lines. Treat it as a table of contents, not a manual. Write the description with a clear trigger / non-trigger / outcome triplet (skill activation rates from marketplace skills are reportedly ~20% — better descriptions fix that).
3. **Refactor marketplace skills** — most public skills are 400-1000 line walls of text. Use Anthropic's `skill-creator` skill to slim them down and push detail into `references/`.
4. **Personalize with business context** — generic skills produce generic output. Wire each skill to a shared brand-context folder (voice profile, ICP, positioning) via a "context needs" section in the SKILL.md.
5. **Measure with evals** — `skill-creator` now ships built-in evaluation/benchmarking. Define 3-5 assertion criteria per run, A/B test whether a reference file actually improves output, and stop guessing about quality.
6. **Self-improving skills** — feed observations back into a `learnings.md` (or rules section) inside each skill via a wrap-up routine at session end. Prune weekly so it doesn't bloat.
7. **Composing skills** — skills calling other skills (e.g. a copywriting skill that pipes through a humanizer-gate skill) turns isolated tools into a workflow.

**Practical takeaway**: the 200-line ceiling on SKILL.md is the most actionable rule here — it forces progressive disclosure whether you planned for it or not.

## Prompt Engineering

*Learn how to communicate effectively with AI*

### [Build an MCP Server in 5 Prompts](https://www.youtube.com/watch?v=FRogt98OF80)

**Creator**: Matt Pocock (AI Hero) | **Length**: ~15 min | **Best for**: the prompt-structure framework, not the example

> ⚠️ **Note**: The MCP server example and some of the LLM failure modes shown are from an earlier era of Claude. Modern Claude Code is much better at codebase exploration on its own. **Watch for the prompt structure, not the specific debugging story** — that part is what's still relevant in 2026.

The lasting takeaway: Matt's three-section prompt template, which is still one of the cleanest patterns for non-trivial work:

1. **Problem** — what are we trying to solve?
2. **Supporting Information** — everything the LLM needs in context (tools, file structures, examples)
3. **Steps to Complete** — explicit, ordered instructions

Why this template still matters even though Claude is smarter now:

- **The framework forces *you* to think first** — the value isn't getting Claude to follow steps; it's that drafting a prompt this way exposes gaps in your own thinking before you spend tokens
- **Context curation is still the bottleneck** — better models haven't fixed this; they've just raised the ceiling on what good context delivers
- **"Look at existing implementations first"** generalises beyond the dated `createTool` example — it's the same principle behind every modern claim that your codebase architecture matters more than your prompts (see *Software Fundamentals* below)

**Key insight**: *"Was that our fault or the LLM's fault? I put this down to me not thinking ahead, not understanding what the LLM's context was supposed to be."*

**Pairs well with**: [Software Fundamentals Matter More Than Ever](#software-fundamentals-matter-more-than-ever) — same speaker, more recent. That talk is the *philosophical* case for why fundamentals (modular design, shared design concepts, ubiquitous language) matter; this one is the *practical* drill on how to actually structure a single prompt. Watch *Software Fundamentals* first, then come here for the hands-on technique.

**Matt's skills repo**: [`mattpocock/skills`](https://github.com/mattpocock/skills) — the prompting discipline shown here is operationalised across his actual `.claude/` skills (`grill-me`, `grill-with-docs`, `write-prd`, etc.). See the [skills doc](advanced/skills.md#matt-pococks-skills-for-real-engineers) for the full breakdown.

## Advanced Techniques

*For those ready to go deeper*

<!-- Add videos here -->

## Talks & Presentations

*Conference talks, interviews, and thought leadership*

### [Software Fundamentals Matter More Than Ever](https://www.youtube.com/watch?v=v4F1gFy-hqg)

**Speaker**: Matt Pocock (AI Hero) | **Length**: ~20 min | **Format**: Conference keynote

A direct rebuttal to the "code is cheap" / specs-to-code movement. Matt's thesis: AI doesn't make software fundamentals obsolete — it makes them more valuable, because **AI does dramatically better work in a well-designed codebase**. A good codebase is one that's easy to change; a bad codebase is one where every AI iteration produces *worse* code than the last (software entropy in fast-forward).

The talk is structured as five failure modes with skill-based fixes:

1. **"The AI didn't do what I wanted"** → Build a *shared design concept* before writing code. Matt's `grill-me` skill ("interview me relentlessly until we reach a shared understanding") asks 40-100 questions and reportedly outperforms Claude Code's default plan mode, which is too eager to commit to an asset.
2. **"The AI is way too verbose"** → Borrow *ubiquitous language* from Domain-Driven Design. A markdown file of shared terminology keeps planning, code, and conversations aligned. Improves both planning *and* the LLM's reasoning traces.
3. **"The AI built the right thing but it doesn't work"** → TDD. Feedback loops are the speed limit; the LLM's natural tendency is to "outrun its headlights" by writing huge batches before checking anything.
4. **"Testing is hard in this codebase"** → Refactor toward Ousterhout's *deep modules*: few large modules with simple interfaces, instead of many shallow modules with complex ones. Deep modules are testable at the boundary, and AI navigates them more reliably.
5. **"My brain can't keep up"** → Design interfaces yourself, delegate implementation to AI, treat each deep module as a gray box. This is how senior engineers stay sane while shipping AI-assisted code at scale.

Books cited (and worth owning):

- *A Philosophy of Software Design* — John Ousterhout (deep vs. shallow modules, "complexity is what makes a system hard to change")
- *The Pragmatic Programmer* — Hunt & Thomas (software entropy, requirements gathering, "rate of feedback is your speed limit")
- *The Design of Design* — Frederick P. Brooks (the *design concept* — the invisible shared model between collaborators)
- Domain-Driven Design — Evans (ubiquitous language)
- Kent Beck on continuous design: *"Invest in the design of the system every day."*

**Quote**: *"Code is not cheap. Bad code is the most expensive it's ever been."*

**Pairs well with**: [Build an MCP Server in 5 Prompts](#build-an-mcp-server-in-5-prompts) (also Matt Pocock) — that talk shows the prompting discipline; this one shows the architectural discipline that makes the prompting actually pay off.

**Matt's skills repo**: [`mattpocock/skills`](https://github.com/mattpocock/skills) — every skill referenced in the talk (`grill-me`, `ubiquitous-language`, `improve-codebase-architecture`, `write-prd`) ships from his actual `.claude/` directory. ~43k stars, install via `npx skills@latest add mattpocock/skills`. The talk is the *why*, the repo is the *what*. See the [skills doc](advanced/skills.md#matt-pococks-skills-for-real-engineers) for the full breakdown including which ones to start with.

---

## Contributing

Found a great video? This list is always growing. Videos should be:
- **Practical** - Actually teaches something useful
- **Current** - AI moves fast; outdated content can mislead
- **Quality** - Well-produced, clear explanations
- **Focused** - Not just hype or speculation

---

*Last updated: April 2026*
