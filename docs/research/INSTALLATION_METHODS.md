# Research: Installation & Initialization Documentation Audit

Catalog of all installation and initialization methods documented in the codebase, with exact line references.

Permalinks reference commit `f83a8f5` on upstream main.

---

## Installation Methods

### Quick Install Scripts

| Method | Location |
|--------|----------|
| Unix/Linux/macOS curl script | [README.md#L35](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L35), [#L104](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L104) |
| Unix/Linux/macOS curl script | [docs/INSTALLING.md#L23](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L23) |
| Windows PowerShell script | [README.md#L109](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L109) |
| Windows PowerShell script | [docs/INSTALLING.md#L96](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L96) |

### Package Managers

| Method | Location |
|--------|----------|
| Homebrew | [README.md#L114-L115](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L114-L115) |
| Homebrew | [docs/INSTALLING.md#L10-L11](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L10-L11), [#L38-L39](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L38-L39), [#L59-L60](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L59-L60), [#L130](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L130) |
| npm global | [README.md#L93](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L93) |
| npm global | [npm-package/CLAUDE_CODE_WEB.md#L34](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L34), [#L55](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L55), [#L145](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L145) |
| npm project-local | [npm-package/CLAUDE_CODE_WEB.md#L64](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L64) |
| Arch Linux AUR | [docs/INSTALLING.md#L66-L68](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L66-L68) |
| pip/uv (MCP server) | [docs/INSTALLING.md#L175](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L175), [#L178](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L178) |

### Go Install

| Method | Location |
|--------|----------|
| `go install` | [README.md#L98](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L98) |
| `go install` | [docs/INSTALLING.md#L44](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L44), [#L75](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L75), [#L101](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L101), [#L238](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L238), [#L304](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L304) |
| `go install` | [npm-package/CLAUDE_CODE_WEB.md#L168](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L168), [#L191](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L191) |
| `CGO_ENABLED=1 go install` | [docs/INSTALLING.md#L248](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L248) |
| `CGO_ENABLED=1 go install` | [docs/TROUBLESHOOTING.md#L71](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/TROUBLESHOOTING.md?plain=1#L71) |

### Build From Source

| Method | Location |
|--------|----------|
| Standard build (Unix) | [README.md#L84](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L84), [#L851](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L851) |
| Standard build (Unix) | [docs/INSTALLING.md#L51](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L51), [#L82](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L82) |
| Standard build (Unix) | [docs/QUICKSTART.md#L9](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/QUICKSTART.md?plain=1#L9) |
| Windows build | [docs/INSTALLING.md#L108](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L108) |
| CGO-enabled build | [docs/INSTALLING.md#L253](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L253) |
| CGO-enabled build | [docs/TROUBLESHOOTING.md#L76](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/TROUBLESHOOTING.md?plain=1#L76) |

### Environment-Specific

| Method | Location |
|--------|----------|
| Claude Code for Web SessionStart hook | [npm-package/CLAUDE_CODE_WEB.md#L26-L48](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L26-L48), [#L179-L202](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L179-L202), [#L249-L289](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L249-L289) |
| Devcontainers | [README.md#L193](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L193) |
| Devcontainers | [.devcontainer/README.md#L12-L17](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/.devcontainer/README.md?plain=1#L12-L17), [#L19-L24](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/.devcontainer/README.md?plain=1#L19-L24) |
| Claude Code Plugin | [docs/INSTALLING.md#L158-L159](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L158-L159) |
| Claude Code Plugin | [docs/PLUGIN.md#L36-L37](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/PLUGIN.md?plain=1#L36-L37), [#L48-L51](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/PLUGIN.md?plain=1#L48-L51) |
| MCP Server (Claude Desktop) | [docs/INSTALLING.md#L187-L194](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L187-L194) |
| MCP Server (Sourcegraph Amp) | [docs/INSTALLING.md#L201-L206](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L201-L206) |

---

## Initialization Methods

### Basic Init

| Method | Location |
|--------|----------|
| `bd init` | [README.md#L131](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L131), [#L163](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L163), [#L165](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L165), [#L172](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L172) |
| `bd init` | [docs/QUICKSTART.md#L19](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/QUICKSTART.md?plain=1#L19) |
| `bd init --quiet` | [README.md#L161](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L161), [#L163](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L163) |
| `bd init --quiet` | [npm-package/CLAUDE_CODE_WEB.md#L38](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L38), [#L56](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L56), [#L277](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L277), [#L323](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L323) |
| `bd init --quiet` | [docs/INSTALLING.md#L134](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L134) |
| `bd init --quiet` | [.devcontainer/README.md#L32](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/.devcontainer/README.md?plain=1#L32) |

### Workflow Modes

| Method | Location |
|--------|----------|
| `bd init --contributor` | [README.md#L134](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L134) |
| `bd init --contributor` | [docs/QUICKSTART.md#L22](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/QUICKSTART.md?plain=1#L22) |
| `bd init --team` | [README.md#L137](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L137) |
| `bd init --team` | [docs/QUICKSTART.md#L25](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/QUICKSTART.md?plain=1#L25) |
| `bd init --branch <name>` | [README.md#L140](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L140), [#L153](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L153) |
| `bd init --branch <name>` | [docs/QUICKSTART.md#L28](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/QUICKSTART.md?plain=1#L28) |
| `bd init --stealth` | [README.md#L200-L219](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L200-L219) |

### Post-Init Configuration

| Method | Location |
|--------|----------|
| `bd hooks install` | [docs/INSTALLING.md#L137](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L137) |
| Manual merge driver config | [README.md#L167-L168](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L167-L168) |
| Manual merge driver config | [docs/GIT_INTEGRATION.md#L169-L170](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/GIT_INTEGRATION.md?plain=1#L169-L170), [#L181-L182](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/GIT_INTEGRATION.md?plain=1#L181-L182) |

---

## Agent Onboarding

| Method | Location |
|--------|----------|
| `bd onboard` | [README.md#L150](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L150), [#L156](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L156), [#L205](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L205) |
| AGENTS.md bootstrap instruction | [README.md#L150](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L150) |
| AGENTS.md bootstrap instruction | [npm-package/CLAUDE_CODE_WEB.md#L107-L122](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L107-L122) |

---

## Verification Commands

| Command | Location |
|---------|----------|
| `bd version` | [docs/INSTALLING.md#L114](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L114), [#L220](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L220) |
| `bd version` | [npm-package/CLAUDE_CODE_WEB.md#L77](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L77), [#L174](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L174) |
| `bd help` | [docs/INSTALLING.md#L221](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md?plain=1#L221) |
| `bd doctor` | [README.md#L460](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md?plain=1#L460) |
| `bd info` | [npm-package/CLAUDE_CODE_WEB.md#L80](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md?plain=1#L80) |

---

## Files Reviewed

- [README.md](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/README.md)
- [docs/INSTALLING.md](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/INSTALLING.md)
- [docs/QUICKSTART.md](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/QUICKSTART.md)
- [docs/PLUGIN.md](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/PLUGIN.md)
- [docs/TROUBLESHOOTING.md](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/TROUBLESHOOTING.md)
- [docs/GIT_INTEGRATION.md](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/docs/GIT_INTEGRATION.md)
- [npm-package/CLAUDE_CODE_WEB.md](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/npm-package/CLAUDE_CODE_WEB.md)
- [.devcontainer/README.md](https://github.com/steveyegge/beads/blob/f83a8f5a3897d1fa95a9e1e59ddce3144445bbdf/.devcontainer/README.md)
