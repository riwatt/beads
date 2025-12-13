---
description: Setup integration with AI editors
arguments:
  claude: Setup Claude Code integration (hooks)
  cursor: Setup Cursor IDE integration (rules)
  aider: Setup Aider integration (config)
---

# bd setup

Setup integration files for AI editors like Claude Code, Cursor, and Aider.

## Synopsis

```bash
bd setup claude [--project] [--stealth] [--check] [--remove]
bd setup cursor [--check] [--remove]
bd setup aider [--check] [--remove]
```

## Description

The `bd setup` command configures your AI editor to automatically use bd for issue tracking. Each editor has a different integration mechanism:

- **Claude Code**: Installs SessionStart hooks that call `bd prime` to inject workflow context
- **Cursor**: Creates `.cursor/rules/beads.mdc` with bd workflow rules
- **Aider**: Creates `.aider.conf.yml` with bd instructions

## Subcommands

### bd setup claude

Install Claude Code hooks that auto-inject bd workflow context.

**Options:**
- `--project` - Install for this project only (not globally)
- `--stealth` - Use `bd prime --stealth` (flush only, no git operations)
- `--check` - Check if Claude integration is installed
- `--remove` - Remove bd hooks from Claude settings

**Default behavior**: Installs hooks globally to `~/.claude/settings.json`

**Example:**
```bash
# Install globally (recommended)
bd setup claude

# Install for this project only
bd setup claude --project

# Check installation status
bd setup claude --check

# Remove hooks
bd setup claude --remove
```

### bd setup cursor

Install Beads workflow rules for Cursor IDE.

**Options:**
- `--check` - Check if Cursor integration is installed
- `--remove` - Remove bd rules from Cursor

Creates `.cursor/rules/beads.mdc` with bd workflow context. Uses BEGIN/END markers for safe idempotent updates.

**Example:**
```bash
bd setup cursor
bd setup cursor --check
bd setup cursor --remove
```

### bd setup aider

Install Beads workflow configuration for Aider.

**Options:**
- `--check` - Check if Aider integration is installed
- `--remove` - Remove bd config from Aider

Creates `.aider.conf.yml` with bd workflow instructions. Note that Aider requires explicit command execution - the AI will suggest bd commands which you must confirm using Aider's `/run` command.

**Example:**
```bash
bd setup aider
bd setup aider --check
bd setup aider --remove
```

## Typical Workflow

After installing bd and initializing your project:

```bash
# 1. Initialize beads in your project
bd init

# 2. Setup your AI editor integration
bd setup claude     # or cursor, aider

# 3. Your AI agent now automatically uses bd!
```

## See Also

- [QUICKSTART.md](../docs/QUICKSTART.md) - Getting started guide
- [INSTALLING.md](../docs/INSTALLING.md) - Installation options
- `bd prime` - The command that gets called by hooks to inject context
- `bd hooks` - Git hooks for auto-sync (different from editor hooks)
