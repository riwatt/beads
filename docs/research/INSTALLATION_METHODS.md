# Research: Installation & Initialization Documentation Audit

Catalog of all installation and initialization methods documented in the codebase.

---

## Installation Methods

### Quick Install Scripts

| Method | Documented In |
|--------|---------------|
| Unix/Linux/macOS curl script | README.md, docs/INSTALLING.md |
| Windows PowerShell script | README.md, docs/INSTALLING.md |

### Package Managers

| Method | Documented In |
|--------|---------------|
| Homebrew (`brew install bd`) | README.md, docs/INSTALLING.md |
| npm (`npm install -g @beads/bd`) | README.md, docs/INSTALLING.md, npm-package/CLAUDE_CODE_WEB.md |
| npm project-local (`npm install --save-dev @beads/bd`) | npm-package/CLAUDE_CODE_WEB.md |
| Arch Linux AUR (`yay -S beads-git`) | docs/INSTALLING.md |
| mise | README.md, docs/INSTALLING.md |
| pip/uv (`beads-mcp`) | docs/INSTALLING.md |

### Go Install

| Method | Documented In |
|--------|---------------|
| `go install` | README.md, docs/INSTALLING.md, npm-package/CLAUDE_CODE_WEB.md |
| `CGO_ENABLED=1 go install` | README.md, docs/INSTALLING.md |

### Build From Source

| Method | Documented In |
|--------|---------------|
| Standard build (Unix) | README.md, docs/INSTALLING.md, docs/QUICKSTART.md |
| Windows build | docs/INSTALLING.md |
| CGO-enabled build | docs/INSTALLING.md |

### Environment-Specific

| Method | Documented In |
|--------|---------------|
| Claude Code for Web (SessionStart hook) | npm-package/CLAUDE_CODE_WEB.md |
| Devcontainers (Codespaces/VS Code Remote) | README.md, .devcontainer/README.md |
| Claude Code Plugin | README.md, docs/INSTALLING.md, docs/PLUGIN.md |
| MCP Server (Claude Desktop) | docs/INSTALLING.md |
| MCP Server (Sourcegraph Amp) | docs/INSTALLING.md |

---

## Initialization Methods

### Basic Init

| Method | Documented In |
|--------|---------------|
| `bd init` | README.md, docs/INSTALLING.md, docs/QUICKSTART.md |
| `bd init --quiet` | README.md, npm-package/CLAUDE_CODE_WEB.md |

### Workflow Modes

| Method | Documented In |
|--------|---------------|
| `bd init --contributor` | README.md, docs/QUICKSTART.md |
| `bd init --team` | README.md, docs/QUICKSTART.md |
| `bd init --branch <name>` | README.md, docs/QUICKSTART.md |
| `bd init --stealth` | README.md |

### Post-Init Configuration

| Method | Documented In |
|--------|---------------|
| `bd hooks install` | README.md, docs/INSTALLING.md |
| Manual merge driver config | README.md |

---

## Agent Onboarding

| Method | Documented In |
|--------|---------------|
| `bd onboard` | README.md |
| AGENTS.md bootstrap instruction | README.md, npm-package/CLAUDE_CODE_WEB.md |

---

## Verification Commands

| Command | Documented In |
|---------|---------------|
| `bd version` | docs/INSTALLING.md, npm-package/CLAUDE_CODE_WEB.md |
| `bd help` | docs/INSTALLING.md |
| `bd doctor` | README.md |
| `bd info` | npm-package/CLAUDE_CODE_WEB.md |

---

## System Requirements

| Requirement | Documented In |
|-------------|---------------|
| Linux glibc 2.32+ | README.md |
| Windows Go 1.24+ | docs/INSTALLING.md |
| Windows Git for Windows | docs/INSTALLING.md |

---

## Files Reviewed

- README.md
- docs/INSTALLING.md
- docs/QUICKSTART.md
- docs/PLUGIN.md
- docs/CLAUDE_INTEGRATION.md
- npm-package/CLAUDE_CODE_WEB.md
- .devcontainer/README.md
