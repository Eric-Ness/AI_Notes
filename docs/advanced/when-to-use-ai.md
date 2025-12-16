# When to Use AI

AI-assisted development is powerful, but it's not always the right tool. Knowing when to use Claude Code—and when not to—makes you more effective overall.

## Where AI Excels

### Boilerplate and Repetitive Code

AI is great at generating code you've written a hundred times:
- CRUD operations
- Form validation
- API endpoint scaffolding
- Test setup and basic cases
- Configuration files

**Example**: "Create a REST endpoint for user registration with validation"

Claude generates in seconds what would take you 15 minutes of typing.

### Explaining and Understanding Code

Reading unfamiliar code is slow. AI accelerates understanding:
- "Explain what this function does"
- "Trace the flow when a user logs in"
- "What's the purpose of this module?"

**Best for**: Onboarding to new codebases, understanding legacy code, reviewing PRs.

### Refactoring and Transformation

Mechanical transformations are tedious by hand:
- Converting class components to hooks
- Adding TypeScript types to JavaScript
- Updating deprecated API usage
- Applying consistent formatting changes

**Example**: "Convert all these callbacks to async/await"

### Documentation

Writing docs is often neglected because it's tedious:
- Docstrings and comments
- README files
- API documentation
- Code explanations

AI makes documentation cheap enough to actually do.

### Debugging Assistance

AI helps with:
- Explaining error messages
- Suggesting causes for bugs
- Reviewing code for common issues
- Proposing debugging strategies

**Note**: AI suggests, you verify. Don't blindly trust bug fixes.

### Learning and Exploration

When you're learning:
- "How does this pattern work?"
- "What's the idiomatic way to do X in Python?"
- "Show me an example of dependency injection"

AI provides personalized explanations with relevant examples.

### Cross-Referencing and Search

Finding things in large codebases:
- "Where is the database connection configured?"
- "What components use this hook?"
- "Find all places where we validate email"

Faster than grep for complex queries.

## Where AI Struggles

### Novel Architecture Decisions

AI can discuss trade-offs, but YOU must decide:
- Which database to use
- Microservices vs monolith
- Build vs buy decisions
- Technology choices

**Use AI for**: Gathering information, listing pros/cons
**Don't use AI for**: Making the final call

### Domain-Specific Logic

AI doesn't understand your business:
- Pricing calculations specific to your model
- Compliance requirements for your industry
- Business rules unique to your company
- Customer-specific edge cases

**You must**: Specify exact requirements. Don't assume AI knows your domain.

### Security-Critical Code

AI can have blind spots:
- Authentication flows
- Payment processing
- Data encryption
- Access control

**Always**: Review security-related AI code carefully. Consider security review by a human.

### Performance-Critical Optimization

AI generates working code, not necessarily optimal code:
- High-frequency trading algorithms
- Real-time system constraints
- Memory-constrained environments
- Latency-sensitive operations

**Use AI for**: First draft. Then profile and optimize.

### Highly Contextual Decisions

AI doesn't know:
- Your team's preferences
- Political dynamics of your organization
- Historical context of past decisions
- Implicit requirements not in the code

**You know things AI doesn't**.

## The Right Mindset

### AI as Collaborator, Not Oracle

Think of Claude as a knowledgeable colleague:
- Gets you 80% of the way fast
- Needs your guidance for the last 20%
- Makes mistakes you should catch
- Has knowledge gaps you fill

### Verify, Don't Trust

Always:
- Test generated code
- Review changes before committing
- Question suggestions that seem off
- Verify facts in documentation

### Speed vs Quality Trade-off

| Situation | Approach |
|-----------|----------|
| Prototype | Let AI generate fast, refine later |
| Production | Generate, then carefully review |
| Security-critical | Generate as starting point, thorough manual review |
| Learning | Let AI explain, then verify understanding |

### Know When to Stop

Sometimes you're fighting the AI:
- Multiple attempts, still wrong
- Constantly correcting misunderstandings
- Would have been faster to do manually

It's okay to say "I'll do this myself."

## Effective Patterns

### AI First Draft, Human Polish

1. AI generates initial version
2. You review and refine
3. AI incorporates feedback
4. You verify final result

### Human Design, AI Implementation

1. You design the approach
2. You specify requirements clearly
3. AI implements to your spec
4. You review and adjust

### AI Research, Human Decision

1. AI gathers information
2. AI presents options with trade-offs
3. You make the decision
4. AI implements your choice

## Anti-Patterns to Avoid

### Blind Trust

Never commit AI-generated code without reviewing it.

### Prompt Thrashing

If you've tried 5 different ways to explain something and AI still doesn't get it, step back. Maybe:
- The task isn't well-suited for AI
- You need to break it down differently
- You should do it manually

### Over-Delegation

Some things require human judgment. Don't try to outsource:
- Ethical decisions
- User experience judgment
- Architectural vision
- Team dynamics

### Under-Utilization

Conversely, don't do tedious work manually when AI could help:
- Writing boilerplate
- Generating test cases
- Documentation
- Repetitive refactoring

## Decision Framework

When deciding whether to use AI:

### Use AI When:
- Task is well-defined
- Outcome is verifiable
- Speed matters
- Task is tedious but straightforward
- You need exploration or explanation

### Be Cautious When:
- Task involves security
- Domain knowledge is crucial
- Outcome is hard to verify
- Novel problem-solving required
- High stakes if wrong

### Skip AI When:
- Faster to do manually (small tasks)
- Requires human judgment
- Context is too complex to explain
- You're fighting to make it work

## Getting Value Over Time

### Track What Works

Notice when AI saves you time:
- "That took 2 minutes instead of 30"
- "Would never have found that bug myself"
- "Explained the code perfectly"

And when it doesn't:
- "Spent 20 minutes fighting the AI"
- "Had to rewrite everything anyway"
- "Kept making the same mistake"

### Build Skills in Both

AI makes you more productive at AI-friendly tasks. But also develop:
- Deep debugging skills (AI can't always help)
- Architecture intuition (AI can't decide for you)
- Domain expertise (AI doesn't know your business)

### Evolve Your Usage

As you get better with AI:
- You'll know when to use it
- You'll write better prompts
- You'll catch AI mistakes faster
- You'll trust appropriately

## Summary

**AI is a tool, not a replacement for thinking.**

Use it to:
- Accelerate tedious work
- Explore and learn
- Generate first drafts
- Find and understand code

Don't use it to:
- Make decisions for you
- Replace careful review
- Handle things you don't understand
- Shortcut security or quality

The goal isn't to use AI for everything. It's to use AI where it genuinely helps—and human skills where they're needed.
