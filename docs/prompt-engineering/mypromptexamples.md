# My Prompt Examples / Quick Guide

## Summary

The only three things you really need to know is that specificity and structure matter, and that talking through a problem is crucial.

1. Being detailed is required for complex tasks
2. Having a structured prompt makes for better output
3. Having a discussion about the task and answering questions is highly beneficial

## Mark Down

ChatGPT, Claude, Gemini, etc. all understand the Mark Down language very well. It will help you with structuring your prompts. Give them sections.

### Headings with `#`

Use `#` symbols to create a hierarchy in your prompts. More `#` symbols = deeper nesting.

```
# Main Title (Top Level)
## Section (Second Level)
### Subsection (Third Level)
#### Detail (Fourth Level)
```

**Why this matters for prompts:**

1. **Creates visual structure** - AI can "see" how your prompt is organized
2. **Signals importance** - `#` headings are treated as major sections
3. **Easier to reference** - "See the Context section" is clear when it's a heading
4. **Better responses** - AI often mirrors your structure in its output

**Example - Unstructured vs Structured:**

Unstructured:

```
I need help with my login function. It's not working.
Here's my code. I'm using Python. The error says
invalid credentials but the credentials are correct.
```

Structured:

```
# Problem
Login function returns "invalid credentials" even with correct credentials.

## Code
def login(user, pwd):
    ...

## Error Message
"Invalid credentials for user: admin"

## What I've Tried
- Verified password in database
- Checked for whitespace
```

The structured version is easier for both you and the AI to parse.


## Prompt Examples

### Basic Detailed Prompt

```
# Problem

Two to ten sentences about the problem you have. Be as detailed as you can. Voice your concerns and point out tricky scenarios. 

## Supporting Information / Documents

### Code

I have added the relevant code from GitHub for context

### Database Scheme / Table Structure

-- YOUR SQL CODE HERE

#### Data Sample

| Col 1 | Col 2 | Col 3|
------------------------
| 1 | 2 | 3 |
| 4 | 5 | 6 |


### Code

YOUR CODE HERE

## Steps To Complete

I need the following items:

1. Review this document
2. Restate the problem as you understand it
3. Ask any questions you may have
4. Add this task to our todo list and GitHub
5. Execute plan
```

### More Detailed Plan

```
# Role

You are an experienced full-stack .NET + SQL developer and python dev.
Your job is to understand the problem, design a solution, and produce implementation-ready code plus a clear explanation.

# Goal

**Primary goal:** STATE GOAL

# Problem

STATE THE PROBLEM

# Context & Supporting Assets

## GitHub Repository / Code Files

-- See the current project files

## Database (MS SQL)

### Schema / Tables


### Sample Data


# Constraints & Preferences

- Tech stack: python & SQL Server 2019


# Tasks

1. Restate Understanding  
2. Ask Clarifying Questions (if needed)  
3. Propose a Plan  
4. Implement the Solution  
5. Explain the Changes  
6. Verification & Edge Cases  
7. Final Summary

# Output Format (Required)

Use these headings:

## Understanding  
## Questions (if any)  
## Plan  
## Implementation  
## Explanation  
## Verification & Edge Cases  
## Final Summary

```

### Exampl Prompt Where You Provide A Template For Output

```
Give me a detailed report on the following data. Imagine you are the lead scientist of a large multi national company. Please follow, the following template.

# [TITLE]

*Company:* [Company Name]
*Regulation:* [Regulation Name]
*Locations:* [Location list] (Locations Total: [total])
*Indicators:* [Indicators List] (Indicators Total: [total])
*Time Frame:* [Data time frame]
*Date Prepared:* [Date]

### [Abstract]

-- Highlight results

## [Intro]

## [Data Stats/Results]

-- Start with a descriptive summary of the data.
-- Feel free to include a summary table. But do not include complete raw data. If there are a lot of locations do not include all data but perhaps do averages. 
-- And perhaps add a chart if there is something interesting to show. But, make sure the chart makes sense. For example if there are 12 locations plot all locations, etc. 
 

## [Discussion]

## [Concerns]

## [Conclusion]


As this is an environmental report it is EXTREMELY IMPORTANT that you double check your work and figures.
```

### Iterative Feature Development Workflow

Use this prompt when starting a new feature to ensure proper tracking and a clean PR-based workflow. It also will help provide a history that you can refer back to.

```markdown
I have the following feature that I want to implement:

DESCRIBE FEATURE

Before starting:
1. Ask any clarifying questions
2. Review relevant existing code to understand the current state

Then:
1. Add to todo list and roadmap
2. Create a GitHub issue with acceptance criteria
3. Create a feature branch and open a draft PR
4. Start implementation

Additional considerations:
- Is this a single PR or should it be broken into smaller pieces?
- What does "done" look like for this feature?
```

**Why this works:**

- **Questions first** - Prevents Claude from diving in with wrong assumptions
- **Context gathering** - Reviews existing code before making changes
- **Full tracking** - Todo list, roadmap, and GitHub issue create visibility
- **PR-first approach** - Changes are on a branch, reviewable, not directly on main
- **Scope check** - Catches features that should be multiple PRs
- **Acceptance criteria** - Defines when to stop

### GitHub Issue Template (Detailed Version)

A comprehensive GitHub Issue template designed for team collaboration. Your business partner fills this out when creating an issue, and Claude has full context when you say "work on issue #742".

**Setup:** Save this as `.github/ISSUE_TEMPLATE/feature-bug.md` in your repository.

```markdown
---
name: Feature / Bug Request
about: Template for new features or bug fixes (optimized for Claude Code)
title: ''
labels: ''
assignees: ''
---

## Type
- [ ] Feature
- [ ] Bug

## Summary
<!-- One or two sentences describing what needs to be done -->


## Detailed Description
<!-- Full context. What problem does this solve? Why is it needed? -->


## Reference Code/Pages
<!-- Help Claude understand existing patterns to follow -->

- **Similar page to reference:** <!-- URL or file path of existing page that works like this should -->
- **Database tables involved:** <!-- Table names that will be read from or written to -->
- **Views/Controllers to look at:** <!-- File paths if known, otherwise leave blank -->

## Database Changes Required
<!-- Note: LINQ to SQL updates will be handled manually by Eric -->

- **Tables affected:**
- **New columns needed:**
- **Column details:** <!-- Data types, nullable, defaults if known -->

## UI/Behavior Description
<!-- Describe what the user should see and do. If attaching images, also describe them in words here since Claude cannot see images directly -->


## Acceptance Criteria
<!-- How do we know it's done? Simple checklist -->

- [ ] User can...
- [ ] Data saves to...
- [ ] Page displays...

## Screenshots/Mockups (optional)
<!-- Attach images here. Remember to describe what they show in the UI/Behavior section above -->


---

## For Claude

**Tech Stack:** .NET MVC + SQL Server (LINQ to SQL)

**Before starting:**
1. Review the reference page/code mentioned above
2. Ask clarifying questions if anything is unclear
3. Check if this should be one PR or multiple smaller ones

**Then:**
1. Create a feature branch and open a draft PR
2. Add to todo list for tracking
3. Start implementation

**Important:**
- Do NOT modify LINQ to SQL database files - flag any DB schema changes for manual update
- Follow patterns from the reference code
- Keep changes focused on what's described in this issue
```

**Why this works:**

- **Complete context** - Claude gets everything needed without back-and-forth questions
- **Reference code** - Points to existing patterns to follow
- **Database awareness** - Captures schema changes while keeping LINQ to SQL manual
- **Image workaround** - Reminds authors to describe images in words (Claude can't see attached images directly)
- **Clear handoff** - "For Claude" section sets expectations for the workflow
