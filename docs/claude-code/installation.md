# Installation

Claude Code can run in your terminal (CLI) or integrated into your favorite IDE. This guide covers both approaches.

## Prerequisites

Before installing, you'll need:

1. **Anthropic Account** - Sign up at [anthropic.com](https://anthropic.com)
2. **Claude Pro or Max subscription** - Required for Claude Code access
3. **Node.js 18+** - For CLI installation

## Option 1: CLI Installation

The command-line interface works in any terminal and gives you full control.

### Install via npm

```bash
npm install -g @anthropic-ai/claude-code
```

### Verify Installation

```bash
claude --version
```

### First Run

```bash
claude
```

On first run, you'll be prompted to authenticate with your Anthropic account.

### Update

```bash
npm update -g @anthropic-ai/claude-code
```

## Option 2: VS Code Extension

The most popular way to use Claude Code - right in your editor.

### Install

1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X / Cmd+Shift+X)
3. Search for "Claude Code"
4. Click Install on the official Anthropic extension

Or install from command line:

```bash
code --install-extension anthropic.claude-code
```

### Setup

1. After installation, you'll see Claude Code in the sidebar
2. Click to open the Claude Code panel
3. Sign in with your Anthropic account
4. You're ready to go

### Usage

- **Open Panel**: Click the Claude icon in the sidebar
- **Quick Chat**: Ctrl+Shift+P → "Claude Code: Open"
- **Keyboard Shortcut**: Configure in VS Code settings

### Features

- Chat panel integrated in VS Code
- Sees your open files and workspace
- Can edit files directly
- Terminal access for commands
- Git integration

## Option 3: Visual Studio (Windows)

For .NET developers using full Visual Studio.

### Install

1. Open Visual Studio
2. Go to Extensions → Manage Extensions
3. Search for "Claude Code"
4. Download and install
5. Restart Visual Studio

### Setup

1. After restart, find Claude Code in View menu or toolbar
2. Sign in with your Anthropic account
3. The panel integrates with your solution

### Features

- Works with .NET, C#, C++, and other Visual Studio languages
- Solution-aware context
- Integrated debugging context

## Option 4: JetBrains IDEs

Works with IntelliJ IDEA, PyCharm, WebStorm, Rider, and other JetBrains products.

### Install

1. Open your JetBrains IDE
2. Go to Settings/Preferences → Plugins
3. Search Marketplace for "Claude Code"
4. Install and restart IDE

### Setup

1. After restart, find Claude Code in the tool windows
2. Sign in with your Anthropic account
3. Ready to use

### Supported IDEs

- IntelliJ IDEA (Java, Kotlin)
- PyCharm (Python)
- WebStorm (JavaScript, TypeScript)
- Rider (.NET)
- GoLand (Go)
- RubyMine (Ruby)
- PHPStorm (PHP)
- CLion (C/C++)

## CLI vs IDE: When to Use Which

| Situation | Recommendation |
|-----------|----------------|
| Quick question or task | IDE (already open) |
| Large refactoring | CLI (focused interface) |
| Learning/exploring | IDE (see context) |
| Automation/scripting | CLI (scriptable) |
| Pair programming feel | IDE (side by side) |
| Remote/SSH work | CLI (terminal-based) |

Many developers use both - IDE for daily work, CLI for specific tasks.

## Terminal Options for CLI

### Windows

- **Windows Terminal** (recommended) - Modern, supports colors
- **PowerShell** - Works well
- **Git Bash** - Good if you prefer bash
- **CMD** - Works but limited features

### macOS

- **Terminal.app** - Built-in, works fine
- **iTerm2** (recommended) - Better features
- **Warp** - Modern alternative

### Linux

- Most terminal emulators work well
- Ensure UTF-8 support for best experience

## Authentication

### First-Time Setup

When you first run Claude Code (CLI or IDE):

1. A browser window opens
2. Log in to your Anthropic account
3. Authorize Claude Code
4. Return to your terminal/IDE

### Token Storage

Your auth token is stored securely:
- **macOS**: Keychain
- **Windows**: Credential Manager
- **Linux**: Secret Service or file

### Re-authenticate

If you have auth issues:

```bash
claude auth logout
claude auth login
```

Or in IDE: Look for "Sign Out" in Claude Code settings.

## Verify Everything Works

### CLI Test

```bash
claude
# Then type: What files are in this directory?
```

Claude should list files in your current directory.

### IDE Test

1. Open a project
2. Open Claude Code panel
3. Ask: "What does this project do?"

Claude should analyze your project and respond.

## Troubleshooting

### "Command not found" (CLI)

Node.js bin directory isn't in your PATH. Try:

```bash
# Find where npm installs global packages
npm config get prefix

# Add that path + /bin to your PATH
```

### Extension Not Showing (VS Code)

1. Reload VS Code (Ctrl+Shift+P → "Reload Window")
2. Check extension is enabled
3. Look for Claude icon in sidebar

### Authentication Fails

1. Check you have Claude Pro or Max subscription
2. Try logging out and back in
3. Check your internet connection
4. Disable VPN if using one

### Slow or Unresponsive

- Large projects take longer to index
- Check your internet connection
- Try closing and reopening

## Next Steps

Once installed, learn [Basic Usage](basic-usage.md) to start working with Claude Code effectively.
