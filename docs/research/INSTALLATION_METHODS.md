# Research: Installation & Initialization Documentation Audit

Catalog of all installation and initialization methods documented in the codebase, with exact line references.

---

## Installation Methods

### Quick Install Scripts

| Method | File | Lines |
|--------|------|-------|
| Unix/Linux/macOS curl script | README.md | 37, 105 |
| Unix/Linux/macOS curl script | docs/INSTALLING.md | 35 |
| Windows PowerShell script | README.md | 110 |
| Windows PowerShell script | docs/INSTALLING.md | 108 |

### Package Managers

| Method | File | Lines |
|--------|------|-------|
| Homebrew | README.md | 115-116 |
| Homebrew | docs/INSTALLING.md | 10-11, 50-51, 71-72, 142 |
| npm global | README.md | 94 |
| npm global | npm-package/CLAUDE_CODE_WEB.md | 34, 55, 145 |
| npm project-local | npm-package/CLAUDE_CODE_WEB.md | 64 |
| Arch Linux AUR | docs/INSTALLING.md | 78, 80 |
| mise | README.md | 121 |
| mise | docs/INSTALLING.md | 23 |
| pip/uv (MCP server) | docs/INSTALLING.md | 187, 190 |

### Go Install

| Method | File | Lines |
|--------|------|-------|
| `go install` | README.md | 99 |
| `go install` | docs/INSTALLING.md | 56, 87, 113, 250, 316 |
| `go install` | npm-package/CLAUDE_CODE_WEB.md | 168, 191 |
| `CGO_ENABLED=1 go install` | docs/INSTALLING.md | 260 |
| `CGO_ENABLED=1 go install` | docs/TROUBLESHOOTING.md | 71 |

### Build From Source

| Method | File | Lines |
|--------|------|-------|
| Standard build (Unix) | README.md | 85, 857 |
| Standard build (Unix) | docs/INSTALLING.md | 63, 94 |
| Standard build (Unix) | docs/QUICKSTART.md | 9 |
| Windows build | docs/INSTALLING.md | 120 |
| CGO-enabled build | docs/INSTALLING.md | 265 |
| CGO-enabled build | docs/TROUBLESHOOTING.md | 76 |

### Environment-Specific

| Method | File | Lines |
|--------|------|-------|
| Claude Code for Web SessionStart hook | npm-package/CLAUDE_CODE_WEB.md | 26-48, 179-202, 249-289 |
| Devcontainers | README.md | 199 |
| Devcontainers | .devcontainer/README.md | 12-24, 29-34 |
| Claude Code Plugin | docs/INSTALLING.md | 170-171 |
| Claude Code Plugin | docs/PLUGIN.md | 36-37, 51-54 |
| MCP Server (Claude Desktop) | docs/INSTALLING.md | 200-206 |
| MCP Server (Sourcegraph Amp) | docs/INSTALLING.md | 213-218 |

---

## Initialization Methods

### Basic Init

| Method | File | Lines |
|--------|------|-------|
| `bd init` | README.md | 137, 169, 171, 178, 180 |
| `bd init` | docs/INSTALLING.md | 255 |
| `bd init` | docs/QUICKSTART.md | 19 |
| `bd init --quiet` | README.md | 167, 169 |
| `bd init --quiet` | npm-package/CLAUDE_CODE_WEB.md | 38, 56, 277, 323 |
| `bd init --quiet` | docs/INSTALLING.md | 146 |

### Workflow Modes

| Method | File | Lines |
|--------|------|-------|
| `bd init --contributor` | README.md | 140 |
| `bd init --contributor` | docs/QUICKSTART.md | 22 |
| `bd init --team` | README.md | 143 |
| `bd init --team` | docs/QUICKSTART.md | 25 |
| `bd init --branch <name>` | README.md | 146, 159 |
| `bd init --branch <name>` | docs/QUICKSTART.md | 28 |
| `bd init --stealth` | README.md | 206-225 |

### Post-Init Configuration

| Method | File | Lines |
|--------|------|-------|
| `bd hooks install` | README.md | 339 |
| `bd hooks install` | docs/INSTALLING.md | 149 |
| Manual merge driver config | README.md | 173-175 |
| Manual merge driver config | docs/GIT_INTEGRATION.md | 131-132, 143-144 |

---

## Agent Onboarding

| Method | File | Lines |
|--------|------|-------|
| `bd onboard` | README.md | 156, 162, 211 |
| AGENTS.md bootstrap instruction | README.md | 156 |
| AGENTS.md bootstrap instruction | npm-package/CLAUDE_CODE_WEB.md | 109-122 |

---

## Verification Commands

| Command | File | Lines |
|---------|------|-------|
| `bd version` | docs/INSTALLING.md | 126, 232 |
| `bd version` | npm-package/CLAUDE_CODE_WEB.md | 77, 174 |
| `bd help` | docs/INSTALLING.md | 233 |
| `bd doctor` | README.md | 466 |
| `bd info` | npm-package/CLAUDE_CODE_WEB.md | 80 |

---

## Files Reviewed

- README.md
- docs/INSTALLING.md
- docs/QUICKSTART.md
- docs/PLUGIN.md
- docs/TROUBLESHOOTING.md
- docs/GIT_INTEGRATION.md
- npm-package/CLAUDE_CODE_WEB.md
- .devcontainer/README.md
