# Beads User Guide

**Audience:** Software developers who want to use `bd` for issue tracking in their projects

This guide is for **end-users** who want to use Beads (`bd`) as their issue tracker. If you're interested in contributing to the Beads project itself, see [DEVELOPER_GUIDE.md](DEVELOPER_GUIDE.md).

## Table of Contents

- [What is Beads?](#what-is-beads)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Basic Workflows](#basic-workflows)
- [Understanding Beads Concepts](#understanding-beads-concepts)
- [Common Use Cases](#common-use-cases)
- [Integration with AI Assistants](#integration-with-ai-assistants)
- [Troubleshooting](#troubleshooting)
- [Next Steps](#next-steps)

## What is Beads?

Beads (command: `bd`) is a Git-backed issue tracker designed for modern development workflows. Unlike traditional issue trackers that live in the cloud, Beads stores your issues as JSONL files in your Git repository, making them:

- **Version controlled** - Issues are tracked alongside your code
- **Distributed** - Every clone has the full issue database
- **Fast** - Local SQLite cache for instant queries
- **Dependency-aware** - Track blockers and relationships between issues
- **AI-friendly** - Designed to work seamlessly with AI coding assistants

**Key Features:**
- Zero setup - `bd init` and you're ready
- Dependency tracking - Four types of dependencies (blocks, related, parent-child, discovered-from)
- Ready work detection - Automatically finds unblocked issues
- Git-native - Stored in `.beads/issues.jsonl`, synced via git
- Hash-based IDs - Collision-resistant for multi-user workflows

## Installation

### Quick Install (Recommended)

**macOS/Linux:**
```bash
curl -fsSL https://raw.githubusercontent.com/steveyegge/beads/main/scripts/install.sh | bash
```

**Windows (PowerShell):**
```powershell
irm https://raw.githubusercontent.com/steveyegge/beads/main/install.ps1 | iex
```

### Package Manager Installation

**Homebrew (macOS/Linux):**
```bash
brew tap steveyegge/beads
brew install bd
```

**npm (Node.js environments):**
```bash
npm install -g @beads/bd
```

**mise (polyglot runtime manager):**
```bash
mise use -g ubi:steveyegge/beads[exe=bd]
```

For more installation options, see [docs/INSTALLING.md](INSTALLING.md).

### Verify Installation

```bash
bd version
```

You should see output like:
```
bd version 0.20.1 (dev: main@a1b2c3d)
```

## Quick Start

### 1. Initialize Beads in Your Project

Navigate to your project root and run:

```bash
bd init
```

This will:
- Create `.beads/` directory with a local database
- Import any existing issues from Git (if present)
- Prompt to install Git hooks (recommended - say yes)
- Prompt to configure Git merge driver (recommended - say yes)
- Start a background daemon for auto-sync

**For team workflows:**
```bash
bd init --team  # Interactive setup for team collaboration
```

**For protected branches (GitHub/GitLab):**
```bash
bd init --branch beads-metadata  # Commits to separate branch
```

### 2. Create Your First Issue

```bash
bd create "Set up project structure" \
  --description "Create initial directory layout and build configuration" \
  --type task \
  --priority 1
```

This creates an issue with:
- A hash-based ID (e.g., `bd-a1b2`)
- Title: "Set up project structure"
- Description with context
- Type: task
- Priority: 1 (high priority)

### 3. View Your Issues

```bash
# List all issues
bd list

# See ready work (no blockers)
bd ready

# Show details of a specific issue
bd show bd-a1b2
```

### 4. Work on an Issue

```bash
# Claim the issue
bd update bd-a1b2 --status in_progress

# ... do your work ...

# Mark as complete
bd close bd-a1b2 --reason "Completed initial structure"
```

### 5. Sync with Git

Beads automatically syncs with Git, but you can force an immediate sync:

```bash
bd sync  # Exports to JSONL, commits, pulls, imports, pushes
```

## Basic Workflows

### Creating Issues

**Basic issue:**
```bash
bd create "Fix login bug" \
  --description "Login fails with 500 error when password contains quotes" \
  --type bug \
  --priority 0
```

**With labels:**
```bash
bd create "Add OAuth support" \
  --description "Implement OAuth 2.0 authentication flow" \
  --type feature \
  --priority 2 \
  --labels auth,backend
```

**With assignee:**
```bash
bd create "Write API documentation" \
  --description "Document REST API endpoints" \
  --type task \
  --priority 2 \
  --assignee alice
```

**From template:**
```bash
bd create --from-template bug "Critical security issue"
bd create --from-template feature "User profile page"
bd create --from-template epic "Q4 Platform Improvements"
```

### Managing Dependencies

Dependencies help you organize work that has prerequisites:

```bash
# Create two issues
bd create "Design API schema" --type task --priority 1
# Returns: bd-abc1

bd create "Implement API endpoints" --type task --priority 1
# Returns: bd-def2

# Add dependency: implementation depends on design
bd dep add bd-def2 bd-abc1

# View dependency tree
bd dep tree bd-def2
```

Output:
```
🌲 Dependency tree for bd-def2:

→ bd-def2: Implement API endpoints [P1] (open)
  → bd-abc1: Design API schema [P1] (open)
```

Now `bd ready` won't show `bd-def2` until `bd-abc1` is closed.

### Finding Work

```bash
# Show all unblocked issues
bd ready

# Show unblocked issues by priority
bd ready --priority 1

# Show unblocked issues assigned to you
bd ready --assignee alice

# Sort by different criteria
bd ready --sort priority  # Strict priority order (P0, P1, P2...)
bd ready --sort oldest    # Oldest issues first
bd ready --sort hybrid    # Recent by priority, old by age (default)
```

### Searching and Filtering

```bash
# Filter by status
bd list --status open
bd list --status in_progress

# Filter by priority
bd list --priority 0  # Critical issues
bd list --priority-min 0 --priority-max 1  # P0 and P1 only

# Filter by type
bd list --type bug
bd list --type feature

# Filter by labels
bd list --label backend,urgent  # Must have ALL labels (AND)
bd list --label-any frontend,ui  # Must have AT LEAST ONE (OR)

# Search in text
bd list --title-contains "auth"
bd list --desc-contains "implement"

# Filter by date
bd list --created-after 2024-01-01
bd list --updated-after 2024-06-01

# Combine filters
bd list --status open --priority 1 --label-any urgent,critical
```

### Working with Labels

Labels provide flexible metadata for organizing issues:

```bash
# Add labels during creation
bd create "Fix auth bug" --type bug --priority 1 --labels auth,backend,urgent

# Add/remove labels
bd label add bd-a1b2 security
bd label remove bd-a1b2 urgent

# List labels on an issue
bd label list bd-a1b2

# List all labels with usage counts
bd label list-all

# Filter by labels
bd list --label backend,auth     # AND: must have ALL labels
bd list --label-any frontend,ui  # OR: must have AT LEAST ONE
```

For more on labels, see [docs/LABELS.md](LABELS.md).

## Understanding Beads Concepts

### Issue IDs (Hash-Based)

Beads uses short hash-based IDs instead of sequential numbers:

- **Format:** `bd-a1b2`, `bd-f14c`, `bd-3e7a`
- **Length:** 4-6 characters depending on database size
- **Collision-resistant:** Safe for multi-user/multi-branch workflows

**Why hashes?** When multiple developers or branches create issues concurrently, sequential IDs (bd-1, bd-2) collide. Hash IDs are generated from random UUIDs, making collisions extremely rare.

### Hierarchical Issues (Epics)

For large features, use hierarchical IDs with dot notation:

```bash
# Create parent epic
bd create "Auth System" --type epic --priority 1
# Returns: bd-a3f8e9

# Create child tasks (auto-numbered)
bd create "Design login UI" --priority 1
# Returns: bd-a3f8e9.1

bd create "Backend validation" --priority 1
# Returns: bd-a3f8e9.2

bd create "Integration tests" --priority 1
# Returns: bd-a3f8e9.3

# View hierarchy
bd dep tree bd-a3f8e9
```

Output:
```
🌲 Dependency tree for bd-a3f8e9:

→ bd-a3f8e9: Auth System [epic] [P1] (open)
  → bd-a3f8e9.1: Design login UI [P1] (open)
  → bd-a3f8e9.2: Backend validation [P1] (open)
  → bd-a3f8e9.3: Integration tests [P1] (open)
```

### Issue Types

- **bug** - Something broken that needs fixing
- **feature** - New functionality to implement
- **task** - Work item (tests, docs, refactoring)
- **epic** - Large feature composed of multiple issues
- **chore** - Maintenance work (dependencies, tooling)

### Priorities

- **0** - Critical (security, data loss, broken builds)
- **1** - High (major features, important bugs)
- **2** - Medium (default, nice-to-have features, minor bugs)
- **3** - Low (polish, optimization)
- **4** - Backlog (future ideas)

### Dependency Types

- **blocks** - Hard dependency (issue X blocks issue Y from starting)
- **related** - Soft relationship (issues are connected but not blocking)
- **parent-child** - Hierarchical relationship (epic → subtasks)
- **discovered-from** - Tracks work discovered during another task

Only `blocks` dependencies affect the ready work queue. Others are for context.

### Issue Status

- **open** - Not started yet (default)
- **in_progress** - Currently being worked on
- **closed** - Completed or resolved

## Common Use Cases

### Solo Development Workflow

```bash
# Morning: Check what's ready to work on
bd ready

# Start work on highest priority item
bd update bd-a1b2 --status in_progress

# During work: Discover a bug, file it immediately
bd create "Fix validation error in signup form" \
  --description "Email validation regex allows invalid addresses" \
  --type bug \
  --priority 1 \
  --deps discovered-from:bd-a1b2

# Complete your work
bd close bd-a1b2 --reason "Implemented and tested"

# End of day: Sync to Git
bd sync
git add .beads/issues.jsonl
git commit -m "Updated issue tracker"
git push
```

### Team Collaboration Workflow

```bash
# Team member A: Initialize with team workflow
bd init --team

# Team member A: Creates issues
bd create "Design database schema" --type task --priority 1
bd create "Implement API" --type task --priority 1 --deps blocks:bd-abc1

# Commit and push
bd sync

# Team member B: Pull and sync
git pull
bd sync  # Auto-imports latest issues

# Team member B: Check available work
bd ready

# Team member B: Claims an issue
bd update bd-abc1 --status in_progress --assignee bob

# Commit and push
bd sync

# Team member A: Pulls updates
git pull
bd sync
bd list --status in_progress  # Sees Bob's work
```

### Feature Planning Workflow

```bash
# Create epic for large feature
bd create "User Authentication System" --type epic --priority 1
# Returns: bd-x7y9

# Break down into phases with child issues
bd create "Phase 1: User registration" --priority 1
# Returns: bd-x7y9.1

bd create "Phase 2: Login/logout" --priority 1
# Returns: bd-x7y9.2

bd create "Phase 3: Password reset" --priority 2
# Returns: bd-x7y9.3

# Add dependencies between phases
bd dep add bd-x7y9.2 bd-x7y9.1  # Login depends on registration
bd dep add bd-x7y9.3 bd-x7y9.2  # Reset depends on login

# View the plan
bd dep tree bd-x7y9
```

### Bug Triage Workflow

```bash
# List all open bugs
bd list --type bug --status open

# Prioritize critical bugs
bd update bd-bug1 --priority 0
bd update bd-bug2 --priority 1

# Add labels for triage
bd label add bd-bug1 security,urgent
bd label add bd-bug2 ui,enhancement

# Assign to team members
bd update bd-bug1 --assignee alice
bd update bd-bug2 --assignee bob

# Check ready work by priority
bd ready --priority 0  # Critical bugs
```

### Sprint Planning Workflow

```bash
# Create sprint epic
bd create "Sprint 12 - Authentication" --type epic --priority 1
# Returns: bd-spr12

# Add sprint tasks as children
bd create "Implement OAuth provider" --priority 1
bd create "Add session management" --priority 1
bd create "Write auth middleware" --priority 1

# Assign to team
bd update bd-spr12.1 --assignee alice
bd update bd-spr12.2 --assignee bob
bd update bd-spr12.3 --assignee charlie

# During sprint: Check progress
bd list --status in_progress
bd show bd-spr12 --json  # Get JSON for dashboard

# End of sprint: Close completed work
bd close bd-spr12.1 bd-spr12.2 bd-spr12.3 --reason "Sprint 12 complete"
```

## Integration with AI Assistants

Beads is designed to work seamlessly with AI coding assistants like Claude, GitHub Copilot, and others.

### For Claude Code and Similar Tools

If you're using an AI assistant with shell access:

1. **Add to AGENTS.md or CLAUDE.md:**
   ```markdown
   ## Issue Tracking
   
   This project uses `bd` (Beads) for issue tracking. Before starting any work:
   - Check ready work: `bd ready --json`
   - Claim issues: `bd update <id> --status in_progress`
   - File discovered work: `bd create "Found bug" --description="..." --deps discovered-from:<parent-id>`
   - Complete work: `bd close <id> --reason "Done"`
   - End of session: `bd sync`
   ```

2. **Optional: Add session start hook:**
   ```bash
   bd hooks install  # Enables automatic context injection
   ```

### For Claude Desktop (MCP)

If you're using Claude Desktop without shell access:

1. **Install MCP server:**
   ```bash
   pip install beads-mcp
   ```

2. **Add to Claude Desktop config:**
   ```json
   {
     "beads": {
       "command": "beads-mcp",
       "args": []
     }
   }
   ```

See [integrations/beads-mcp/README.md](../integrations/beads-mcp/README.md) for details.

### Stealth Mode (Personal Use Only)

Want to use Beads in your local clone without other collaborators seeing it?

```bash
bd init --stealth
```

This configures:
- Global gitignore to exclude `.beads/` from all repos
- Local Claude settings for AI assistant integration
- No beads-related files committed to the shared repository

Perfect for:
- Personal experimentation
- Working on repos where not everyone uses Beads
- Contributing to open source while keeping your issue tracking private

## Troubleshooting

### "Database not found" Error

**Problem:** Running `bd` commands shows "database not found"

**Solution:** Initialize Beads in your project:
```bash
bd init
```

### Issues Not Syncing Between Machines

**Problem:** Issues created on one machine don't appear on another

**Solution:**
1. Make sure you committed and pushed the JSONL file:
   ```bash
   bd sync
   git status  # Should show .beads/issues.jsonl committed
   ```

2. On the other machine, pull and import:
   ```bash
   git pull
   bd sync
   ```

3. Install git hooks to automate this:
   ```bash
   bd hooks install
   ```

### Merge Conflicts in JSONL

**Problem:** Git merge conflicts in `.beads/issues.jsonl`

**Solution:**
1. Accept remote version:
   ```bash
   git checkout --theirs .beads/issues.jsonl
   ```

2. Re-import and export:
   ```bash
   bd import -i .beads/issues.jsonl
   bd sync
   ```

The intelligent merge driver (installed via `bd init`) usually prevents this.

### Daemon Not Running

**Problem:** Auto-sync not working, daemon shows as stopped

**Solution:**
```bash
# Restart daemon
bd daemons restart .

# Or restart all daemons
bd daemons killall
```

### Version Mismatch Warnings

**Problem:** `bd info` shows "daemon version mismatch"

**Solution:**
```bash
# After upgrading bd, restart daemons
bd daemons killall

# Update git hooks
bd hooks install
```

For more troubleshooting, see [docs/TROUBLESHOOTING.md](TROUBLESHOOTING.md).

## Next Steps

Now that you understand the basics:

- **Learn advanced features:** See [docs/ADVANCED.md](ADVANCED.md)
- **Configure integrations:** See [docs/CONFIG.md](CONFIG.md)
- **Multi-repo workflows:** See [docs/MULTI_REPO_MIGRATION.md](MULTI_REPO_MIGRATION.md)
- **Extend Beads:** See [docs/EXTENDING.md](EXTENDING.md)
- **Complete CLI reference:** See [docs/CLI_REFERENCE.md](CLI_REFERENCE.md)
- **FAQ:** See [docs/FAQ.md](FAQ.md)

### Documentation Map

**For End-Users (You):**
- [USER_GUIDE.md](USER_GUIDE.md) - This document
- [INSTALLING.md](INSTALLING.md) - Installation guide
- [QUICKSTART.md](QUICKSTART.md) - Quick start tutorial
- [FAQ.md](FAQ.md) - Frequently asked questions
- [TROUBLESHOOTING.md](TROUBLESHOOTING.md) - Common issues

**For AI Assistant Integration:**
- [AGENTS.md](../AGENTS.md) - AI agent instructions
- [beads-mcp README](../integrations/beads-mcp/README.md) - MCP server docs

**For Developers Contributing to Beads:**
- [DEVELOPER_GUIDE.md](DEVELOPER_GUIDE.md) - Development setup
- [CONTRIBUTING.md](../CONTRIBUTING.md) - Contribution guidelines
- [AGENT_INSTRUCTIONS.md](../AGENT_INSTRUCTIONS.md) - Detailed dev procedures

**For Advanced Use Cases:**
- [ADVANCED.md](ADVANCED.md) - Advanced features
- [CONFIG.md](CONFIG.md) - Configuration system
- [EXTENDING.md](EXTENDING.md) - Database extensions
- [MULTI_REPO_MIGRATION.md](MULTI_REPO_MIGRATION.md) - Multi-repo patterns

---

**Questions or feedback?** Open an issue: `bd create "Documentation feedback: ..." --type task`
