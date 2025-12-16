# GitHub CLI Setup

The GitHub CLI (`gh`) is what allows Claude Code to interact with GitHub on your behalf - creating commits, pull requests, issues, and more. This guide walks you through setting it up.

## Why You Need This

Without the GitHub CLI:
- Claude can write code but can't save it to GitHub
- You have to manually create commits, PRs, and issues
- No integration between your AI workflow and version control

With the GitHub CLI:
- Claude can commit changes directly
- Claude can create and manage pull requests
- Claude can create issues from your todo lists
- Seamless workflow from idea to shipped code

## Installation

### Windows

Using winget (recommended):

```powershell
winget install GitHub.cli
```

Or download from: https://cli.github.com/

### macOS

Using Homebrew:

```bash
brew install gh
```

### Linux (Debian/Ubuntu)

```bash
sudo apt install gh
```

### Verify Installation

```bash
gh --version
```

You should see something like `gh version 2.x.x`

## Authentication

This is the important part - connecting `gh` to your GitHub account.

### Step 1: Start Login

```bash
gh auth login
```

### Step 2: Answer the Prompts

```
? What account do you want to log into? GitHub.com
? What is your preferred protocol for Git operations? HTTPS
? Authenticate Git with your GitHub credentials? Yes
? How would you like to authenticate GitHub CLI? Login with a web browser
```

### Step 3: Complete Browser Authentication

1. Copy the one-time code shown in terminal
2. Press Enter to open your browser
3. Paste the code on the GitHub page
4. Authorize the CLI

### Step 4: Verify It Worked

```bash
gh auth status
```

You should see:

```
github.com
  ✓ Logged in to github.com as YourUsername
  ✓ Git operations for github.com configured to use https protocol
  ✓ Token: gho_****
```

## Test the Connection

Try a simple command:

```bash
gh repo list
```

This should show your repositories. If it works, you're connected.

## What Claude Code Can Do Now

With `gh` authenticated, Claude Code can:

### Create Commits

```
"Commit these changes with message 'Add login validation'"
```

### Create Pull Requests

```
"Create a PR for this feature branch"
```

### Manage Issues

```
"Create an issue for this bug we found"
"Add this to GitHub issues"
```

### Check PR Status

```
"What's the status of my open PRs?"
```

## Troubleshooting

### "gh: command not found"

The CLI isn't in your PATH. Try:
- Restart your terminal
- On Windows, restart your computer
- Verify installation location is in PATH

### "authentication required"

Run `gh auth login` again. Your token may have expired.

### "permission denied"

Make sure you authorized the correct scopes during login. Run:

```bash
gh auth refresh -s repo,read:org
```

### Check Current Auth Status

```bash
gh auth status
```

This shows what account you're logged into and what permissions you have.

## Repository Setup

For each project you want Claude to manage:

### New Repository

```bash
# Create repo on GitHub and clone locally
gh repo create my-project --public --clone
```

### Existing Local Project

```bash
# Initialize git if needed
git init

# Create GitHub repo and connect it
gh repo create my-project --source=. --public --push
```

### Clone Existing Repo

```bash
gh repo clone username/repo-name
```

## Best Practices

### 1. Use HTTPS (Not SSH)

When `gh` asks about protocol, choose HTTPS. It's simpler and works better with the CLI authentication.

### 2. Keep Token Secure

Your auth token is stored locally. Don't share it or commit it to repos.

### 3. Re-authenticate If Issues Arise

When in doubt:

```bash
gh auth logout
gh auth login
```

Fresh authentication fixes most problems.

## Next Steps

Now that you're connected, learn how to use [Issues & Todos](issues-and-todos.md) for task management with Claude Code.
