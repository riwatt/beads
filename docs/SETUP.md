# Setup Guide for bd (beads)

This guide explains the complete setup workflow for bd, clarifying the three main commands: `init`, `onboard`, and `setup`.

## Quick Summary

```bash
# Step 1: Initialize the project (REQUIRED - humans or AI)
bd init                    # Interactive (for humans)
bd init --quiet            # Non-interactive (for AI agents)

# Step 2: Generate AI documentation (RECOMMENDED - for AI agents)
bd onboard                 # Outputs instructions for integrating into AGENTS.md

# Step 3: Setup editor integration (OPTIONAL - for enhanced UX)
bd setup claude            # For Claude Code
bd setup cursor            # For Cursor IDE
bd setup aider             # For Aider
```

## The Three Commands Explained

### 1. `bd init` - Project Initialization

**Purpose:** Creates the `.beads/` directory and database in your project.

**Who runs this:** Either humans (interactively) OR AI agents (with `--quiet`)

**When:** This is the FIRST STEP. Must be run before using any other bd commands.

**Usage:**

```bash
# For humans (interactive prompts)
bd init

# For AI agents (non-interactive, auto-installs hooks)
bd init --quiet

# For OSS contributors (fork workflow)
bd init --contributor

# For team members (branch workflow)
bd init --team

# For protected branches
bd init --branch beads-metadata

# For stealth mode (personal use, invisible to repo)
bd init --stealth
```

**What it does:**
- Creates `.beads/` directory
- Creates `beads.db` SQLite database
- Imports existing issues from git (if any)
- Prompts to install git hooks (or auto-installs with `--quiet`)
- Prompts to configure git merge driver (or auto-configures with `--quiet`)
- Starts daemon for auto-sync

### 2. `bd onboard` - AI Agent Documentation

**Purpose:** Generates instructions for integrating bd workflow into project documentation.

**Who runs this:** AI agents (or humans setting up for AI agents)

**When:** AFTER running `bd init`, to integrate bd into your project's AI documentation.

**Usage:**

```bash
# Output instructions for AI agent to follow
bd onboard

# Generate canonical BD_GUIDE.md file
bd onboard --output .beads/BD_GUIDE.md
```

**What it does:**
- Outputs instructions for updating `AGENTS.md` with bd workflow
- Provides content for `.github/copilot-instructions.md` (GitHub Copilot)
- Suggests updating `CLAUDE.md` if present
- Can generate version-stamped `BD_GUIDE.md` file

**When to regenerate:**
- After upgrading bd to a new version
- When bd workflow changes significantly

### 3. `bd setup` - AI Editor Integration

**Purpose:** Installs editor-specific integration files for automatic context injection.

**Who runs this:** Humans or AI agents (optional enhancement)

**When:** AFTER running `bd init` and `bd onboard`, to enable automatic context injection in your AI editor.

**This is OPTIONAL** - bd works perfectly fine without editor-specific setup.

**Available subcommands:**

#### Claude Code Integration

```bash
# Install hooks globally (recommended)
bd setup claude

# Install for this project only
bd setup claude --project

# Check if installed
bd setup claude --check

# Remove hooks
bd setup claude --remove
```

**What it does:**
- Installs SessionStart and PreCompact hooks
- Hooks call `bd prime` to inject workflow context
- Prevents context loss after compaction

#### Cursor IDE Integration

```bash
# Install Cursor rules
bd setup cursor

# Check if installed
bd setup cursor --check

# Remove rules
bd setup cursor --remove
```

**What it does:**
- Creates `.cursor/rules/beads.mdc` with workflow context
- Cursor automatically loads these rules for AI assistance

#### Aider Integration

```bash
# Install Aider configuration
bd setup aider

# Check if installed
bd setup aider --check

# Remove configuration
bd setup aider --remove
```

**What it does:**
- Creates `.aider.conf.yml` with bd workflow instructions
- Aider AI suggests bd commands via `/run`

## Complete Setup Workflows

### For Humans Setting Up a New Project

```bash
# 1. Initialize (interactive)
cd your-project
bd init

# Follow prompts to:
#   - Install git hooks (recommended)
#   - Configure merge driver (recommended)

# 2. Have your AI agent integrate documentation
# Tell your AI: "Run 'bd onboard' and follow the instructions"

# 3. (Optional) Setup editor integration
bd setup claude    # If using Claude Code
# or
bd setup cursor    # If using Cursor
# or
bd setup aider     # If using Aider
```

### For AI Agents Setting Up a New Project

```bash
# 1. Initialize (non-interactive)
bd init --quiet

# 2. Follow onboarding instructions
bd onboard
# Then integrate the output into AGENTS.md and .github/copilot-instructions.md

# 3. (Optional) Setup editor integration if using Claude Code
bd setup claude
```

### For Cloning an Existing Project with bd

```bash
# 1. Clone the repository
git clone <repo-url>
cd <repo-name>

# 2. bd automatically discovers the .beads/ directory
# No initialization needed!

# 3. (Optional) Install git hooks if not already installed
bd hooks install

# 4. (Optional) Setup editor integration
bd setup claude    # If using Claude Code
```

## Understanding the Workflow

The three commands serve different purposes in the setup lifecycle:

```
┌─────────────────────────────────────────────────────────────┐
│ bd init                                                       │
│ ─────────────────────────────────────────────────────────── │
│ • Creates .beads/ directory and database                     │
│ • Required for any bd usage                                  │
│ • Run once per project                                       │
│ • Run by humans (interactive) or AI (--quiet)                │
└─────────────────────────────────────────────────────────────┘
                             ↓
┌─────────────────────────────────────────────────────────────┐
│ bd onboard                                                    │
│ ─────────────────────────────────────────────────────────── │
│ • Generates AI documentation integration instructions        │
│ • Updates AGENTS.md, copilot-instructions.md, CLAUDE.md      │
│ • Run after init to document bd workflow                     │
│ • Regenerate after bd version upgrades                       │
└─────────────────────────────────────────────────────────────┘
                             ↓
┌─────────────────────────────────────────────────────────────┐
│ bd setup                                                      │
│ ─────────────────────────────────────────────────────────── │
│ • Installs editor-specific integration files                 │
│ • Optional enhancement for automatic context injection       │
│ • Subcommands: claude, cursor, aider                         │
│ • Can be skipped if not using these editors                  │
└─────────────────────────────────────────────────────────────┘
```

## Common Questions

### "Which command should I run first?"

**`bd init`** - This is always the first step. It creates the database.

### "Do I need to run all three commands?"

- **`bd init`** - YES, required
- **`bd onboard`** - RECOMMENDED if using AI agents
- **`bd setup`** - OPTIONAL, for editor-specific enhancements

### "I'm an AI agent. What should I do?"

1. If `.beads/` directory doesn't exist: Run `bd init --quiet`
2. If you see instructions about running `bd onboard`: Run it and follow the output
3. If using Claude Code and want automatic context: Run `bd setup claude`

### "I'm a human. What should I do?"

1. Run `bd init` (interactive)
2. Tell your AI agent: "Run 'bd onboard' and follow the instructions"
3. (Optional) Run `bd setup <editor>` for your preferred AI editor

### "What's the difference between `bd onboard` and `bd setup`?"

- **`bd onboard`** = Generates **documentation** for AI agents (updates AGENTS.md, etc.)
- **`bd setup`** = Installs **editor configuration** for automatic context injection (optional)

### "When should I run `bd onboard` again?"

- After upgrading bd to a new version
- When you want to regenerate BD_GUIDE.md with latest workflow instructions
- If you deleted or corrupted AGENTS.md

### "Can I use bd without running `bd onboard` or `bd setup`?"

**YES!** After `bd init`, you can use all bd commands directly. The other commands just make the AI agent experience better:
- `bd onboard` documents the workflow for AI agents
- `bd setup` adds automatic context injection for your editor

## See Also

- [QUICKSTART.md](QUICKSTART.md) - Quick start guide for using bd
- [INSTALLING.md](INSTALLING.md) - Installation instructions
- [CLI_REFERENCE.md](CLI_REFERENCE.md) - Complete command reference
- [AGENTS.md](../AGENTS.md) - AI agent instructions
- [CLAUDE_INTEGRATION.md](CLAUDE_INTEGRATION.md) - Claude-specific integration details
- [AIDER_INTEGRATION.md](AIDER_INTEGRATION.md) - Aider-specific integration details
