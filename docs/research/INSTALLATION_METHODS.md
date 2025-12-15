# Research: Beads Installation & Initialization Methods

This document catalogs all the different ways end users can install and initialize the beads (`bd`) issue tracker.

---

## Part 1: Installing the `bd` Binary

### 1.1 Quick Install Scripts

#### Unix/Linux/macOS - Curl Script
```bash
curl -fsSL https://raw.githubusercontent.com/steveyegge/beads/main/scripts/install.sh | bash
```
- Auto-detects platform (macOS/Linux, amd64/arm64)
- Uses `go install` if Go is available
- Falls back to building from source if needed
- Guides user through PATH setup

#### Windows - PowerShell Script
```powershell
irm https://raw.githubusercontent.com/steveyegge/beads/main/install.ps1 | iex
```
- Native Windows support (no MSYS/MinGW required)
- Requires Go 1.24+ and Git for Windows

---

### 1.2 Package Managers

#### Homebrew (macOS & Linux)
```bash
brew tap steveyegge/beads
brew install bd
```
**Advantages:**
- Simple one-command install
- Automatic updates via `brew upgrade`
- No need to install Go
- Handles PATH setup automatically

#### npm (Node.js environments)
```bash
npm install -g @beads/bd
```
**Advantages:**
- Works in environments where npm is pre-installed
- Downloads native binary during postinstall
- Best for Claude Code for Web environments

**Project-local npm install:**
```bash
npm install --save-dev @beads/bd
npx bd version
```

#### Arch Linux (AUR)
```bash
yay -S beads-git
# or
paru -S beads-git
```
Maintained by community contributor.

#### mise (polyglot runtime manager)
```bash
mise use -g ubi:steveyegge/beads[exe=bd]
```
**Advantages:**
- Single tool for managing development tools
- Version pinning per project via `mise.toml`
- Cross-platform (macOS, Linux, Windows)

#### pip/uv (Python environments - MCP server only)
```bash
# Using uv (recommended)
uv tool install beads-mcp

# Or using pip
pip install beads-mcp
```
Note: This installs the MCP server wrapper, not the core CLI.

---

### 1.3 Go Install

#### Standard Go Install
```bash
go install github.com/steveyegge/beads/cmd/bd@latest
```
Requires Go 1.24+ and `$GOPATH/bin` in PATH.

#### With CGO Enabled (for SQLite issues)
```bash
CGO_ENABLED=1 go install github.com/steveyegge/beads/cmd/bd@latest
```
Use if experiencing crashes on macOS.

---

### 1.4 Build From Source

#### Standard Build
```bash
git clone https://github.com/steveyegge/beads
cd beads
go build -o bd ./cmd/bd
sudo mv bd /usr/local/bin/
```

#### Windows Build
```powershell
git clone https://github.com/steveyegge/beads
cd beads
go build -o bd.exe ./cmd/bd
Move-Item bd.exe $env:USERPROFILE\AppData\Local\Microsoft\WindowsApps\
```

#### Build with CGO (macOS crash workaround)
```bash
git clone https://github.com/steveyegge/beads
cd beads
CGO_ENABLED=1 go build -o bd ./cmd/bd
sudo mv bd /usr/local/bin/
```

---

### 1.5 Environment-Specific Installation

#### Claude Code for Web (SessionStart Hook)

Create `.claude/hooks/session-start.sh`:
```bash
#!/bin/bash
# Try npm first, fall back to go install
if ! command -v bd &> /dev/null; then
    if npm install -g @beads/bd --quiet 2>/dev/null && command -v bd &> /dev/null; then
        echo "Installed via npm"
    elif command -v go &> /dev/null; then
        go install github.com/steveyegge/beads/cmd/bd@latest
        export PATH="$PATH:$HOME/go/bin"
    fi
fi
bd version
```

#### Devcontainers (GitHub Codespaces / VS Code Remote)
- Auto-configured via `.devcontainer/` in repo
- Builds from source during container creation
- Git hooks automatically installed
- No manual setup required

#### Claude Code Plugin
```bash
# In Claude Code
/plugin marketplace add steveyegge/beads
/plugin install beads
```
Adds slash commands and MCP tools.

---

## Part 2: Project Initialization

### 2.1 Standard Initialization

#### Basic Init
```bash
cd your-project
bd init
```
Creates `.beads/` directory with database, prompts for hooks and merge driver.

#### Non-Interactive Init (for agents)
```bash
bd init --quiet
```
Auto-installs git hooks and merge driver, no prompts.

---

### 2.2 Workflow-Specific Initialization

#### OSS Contributor (Fork Workflow)
```bash
bd init --contributor
```
For contributing to open source projects via forks.

#### Team Member (Branch Workflow)
```bash
bd init --team
```
For team collaboration using branches.

#### Protected Branch Support
```bash
bd init --branch beads-metadata
```
Commits issue updates to a separate branch when `main` is protected.

---

### 2.3 Stealth Mode (Isolated Usage)

```bash
bd init --stealth
```
**What it does:**
- Configures global gitignore (`~/.config/git/ignore`) to ignore `.beads/`
- Keeps beads files invisible to other collaborators
- Perfect for personal experimentation or contributing to repos that don't use beads

**Use cases:**
- Personal experimentation
- Repos where not everyone uses beads
- Private issue tracking while contributing to open source

---

### 2.4 Post-Init Configuration

#### Install Git Hooks
```bash
bd hooks install
```
Adds:
- `pre-commit` - Immediate flush before commit
- `post-merge` - Guaranteed import after pull/merge

#### Configure Merge Driver (manual)
```bash
git config merge.beads.driver "bd merge %A %O %A %B"
git config merge.beads.name "bd JSONL merge driver"
echo ".beads/beads.jsonl merge=beads" >> .gitattributes
```

---

### 2.5 Importing Existing Issues

#### On Clone (automatic)
```bash
bd init  # Imports existing issues from .beads/issues.jsonl
```

#### Manual Import
```bash
bd import -i issues.jsonl
```

#### Orphan Handling Options
```bash
bd import -i issues.jsonl --orphan-handling allow      # Default, most permissive
bd import -i issues.jsonl --orphan-handling resurrect  # Recreate deleted parents
bd import -i issues.jsonl --orphan-handling skip       # Skip orphans
bd import -i issues.jsonl --orphan-handling strict     # Fail on missing parent
```

---

## Part 3: IDE/Editor Integrations

### 3.1 CLI + Hooks (Recommended)
Works with any editor with shell access.
```bash
brew install bd
cd your-project && bd init --quiet
bd hooks install
```

### 3.2 Claude Code Plugin
```bash
/plugin marketplace add steveyegge/beads
/plugin install beads
```
Adds slash commands: `/beads:ready`, `/beads:create`, `/beads:show`, etc.

### 3.3 MCP Server (for MCP-only environments)

**Claude Desktop (macOS):**
Add to `~/Library/Application Support/Claude/claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "beads": {
      "command": "beads-mcp"
    }
  }
}
```

**Sourcegraph Amp:**
```json
{
  "beads": {
    "command": "beads-mcp",
    "args": []
  }
}
```

### 3.4 VS Code Extension
Third-party: [vscode-beads](https://marketplace.visualstudio.com/items?itemName=planet57.vscode-beads)

---

## Part 4: Agent Onboarding

### 4.1 Tell Agent to Use Beads
Add to `AGENTS.md`:
```markdown
BEFORE ANYTHING ELSE: run 'bd onboard' and follow the instructions
```

### 4.2 Agent Self-Onboarding
When agent runs `bd onboard`, it will:
1. Receive integration instructions
2. Add bd workflow documentation to AGENTS.md
3. Update CLAUDE.md with a note (if present)
4. Remove the bootstrap instruction

---

## Part 5: Database Migration

### 5.1 Schema Migration
```bash
bd migrate --dry-run  # Preview
bd migrate            # Migrate
bd migrate --cleanup --yes  # Migrate and clean old files
```

### 5.2 AI-Supervised Migration
```bash
bd migrate --inspect --json  # Analysis for AI agents
bd info --schema --json      # Check schema state
```

---

## Part 6: Verification & Health Check

```bash
bd version   # Check version
bd help      # Show commands
bd doctor    # Validate installation and setup
bd info      # Show database path and daemon status
```

---

## Part 7: System Requirements

### Linux
- **Requires glibc 2.32+** (Ubuntu 22.04+, Debian 11+, RHEL 9+)
- Not supported: Ubuntu 20.04, Debian 10, CentOS 7, RHEL 8
- Workaround for older systems: Build from source

### macOS
- No special requirements

### Windows
- Go 1.24+ required
- Git for Windows required
- No MSYS/MinGW needed (native support)

---

## Summary Table

| Method | Platform | Complexity | Best For |
|--------|----------|------------|----------|
| `brew install bd` | macOS/Linux | Low | Most users |
| `npm install -g @beads/bd` | Any | Low | Node.js environments, Claude Code Web |
| `go install` | Any | Medium | Go developers |
| Install script | Unix/Windows | Low | Quick setup |
| From source | Any | High | Contributors, old systems |
| mise | Any | Low | Polyglot developers |
| AUR | Arch Linux | Low | Arch users |
| Devcontainer | Any | None | Codespaces/VSCode Remote |
| Plugin | Claude Code | Low | Claude Code users |

---

## Initialization Modes Summary

| Mode | Command | Use Case |
|------|---------|----------|
| Basic | `bd init` | Standard setup with prompts |
| Quiet | `bd init --quiet` | Agent/CI setup, no prompts |
| Contributor | `bd init --contributor` | OSS fork workflows |
| Team | `bd init --team` | Team branch collaboration |
| Protected | `bd init --branch <name>` | Protected main branches |
| Stealth | `bd init --stealth` | Private/invisible usage |
