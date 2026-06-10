# Stop Prompting. Start Engineering.

A 7-slide lightning talk (~5–10 min) on the three-layer method for working with AI,
adapted from Austin Marchese's [*Stop Prompting Claude. Use Karpathy's Method
Instead.*](https://www.youtube.com/watch?v=7zZy1QTvokM) (see [videos.md](../videos.md#stop-prompting-claude-use-karpathys-method-instead)).

**Audience**: mixed / cross-functional (some technical, some not)
**Format**: lightning, ~7 slides, 6–9 min
**Through-line**: AI is brilliant at what's *measurable* and blind to what's *contextual*. The three layers are just how you hand it the context it can't see.

🎤 = a spot to drop your own example so it lands as *your* workflow, not a recap.

---

## Slide 1 — The Hook *(~60 sec)*

**One idea:** Almost everyone is using AI wrong — and a 50-meter car wash proves it.

- Ask the room: *"You're going to a car wash 50m away. Drive or walk?"*
- Every frontier model says **walk**. It misses the obvious: the car has to be *at* the wash.
- Punchline: **AI is genius at what can be measured, blind to context.** Everything today fixes that gap.

*Visual:* the car-wash question on screen, big.

## Slide 2 — What AI Actually Is *(~60 sec)*

**One idea:** Stop treating it like a person. Treat it like a **robot librarian.**

- It only answers from the books in its library. No book = it can't help.
- The danger: **it doesn't know when a book is missing**, so it confidently makes one up.
- So yelling, pleading, "just make it better" — useless. The only real lever is **how you set it up and check it.**

*Visual:* librarian icon. (This reframe is what makes the rest click for non-technical folks.)

## Slide 3 — Layer 1: The Spec *(the blueprint)* *(~90 sec)*

**One idea:** Tell it the **goal**, not just the task.

- "Write the monthly report" is a task. The *goal* is the **decision the report drives** — only you know that.
- Get it out of your head: *"Interview me to figure out the real goal."*
- Work in **small chunks, not one big dump** — check direction as you go (agile, not waterfall).

🎤 *[Your example: a time a vague ask drifted, vs. a tight spec that nailed it.]*

## Slide 4 — Layer 2: The Verifier *(the quality-check station)* *(~90 sec)*

**One idea:** Define what "good" looks like **before** it starts, and give it a way to check itself.

- Vague: "make this look good." Precise: "3 sections, each ends with a recommendation."
- Get a **second opinion** — a different model/library grading the first.
- Pull in **outside proof** — e.g. check the actual deployment, or hand it last month's report as the format to match.
- Stat to land it: **a feedback loop 2–3×'s the quality of the result.**

## Slide 5 — Layer 3: The Environment *(the workshop itself)* *(~90 sec)*

**One idea:** Don't start from an empty workshop every time. Build a world the AI lives in.

- A **`CLAUDE.md`** house-rules file it reads on every task ("always make a verification plan first").
- Your **own knowledge base** — feed it your data so it knows where to look. *"Your data is your moat."*
- **Reusable skills** for anything you do repeatedly; they get sharper the more you run them.
- **Guardrails** for the things that must never go wrong (a real lock, not a polite request).

*Visual:* workshop = blueprint on the wall (spec) + QC station by the door (verifier) + the room itself (environment).

## Slide 6 — The One Thing *(~45 sec)*

**One idea:** *"You can outsource your thinking, but you can't outsource your understanding."* — Karpathy

- All three layers are just structured ways of getting **your understanding** into the machine.
- The skill of the next decade isn't prompting — it's **understanding the problem well enough to direct the work.**

## Slide 7 — How I Use This / Your Takeaway *(~45 sec)*

**One idea:** Pick **one layer** to improve this week.

- Spec: next task, ask the AI to interview you first.
- Verifier: write your "what good looks like" before you start.
- Environment: start a `CLAUDE.md` (or a notes folder) you add to over time.

🎤 *[Close on how this maps to your own workflow + one line on the payoff you've seen.]*

---

## Design notes

- **Analogies do the heavy lifting** (librarian, workshop/blueprint/QC station) — they let a non-technical listener follow without knowing what a hook or a `CLAUDE.md` is. The technical folks still get the real terms underneath.
- **One prompt or one stat per layer**, not a menu — at lightning pace, more than that and you lose the room.
- **Two personal-example beats** (Slides 3 and 7) turn "a video I watched" into "how I work."
- The arc is a **tension-and-resolution loop**: Slide 1 opens the context gap; each layer closes part of it, so the audience always knows why the next slide exists.
- Slides 3–5 share a **parallel shape** (name → analogy → one concrete move) — a memory device that makes a fast talk feel coherent, not rushed.
