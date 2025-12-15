# Research: Installation & Initialization Documentation Audit

Catalog of all installation and initialization methods documented in the codebase, with exact line references.

---

## Installation Methods

### Quick Install Scripts

| Method | Location |
|--------|----------|
| Unix/Linux/macOS curl script | [README.md#L37](https://github.com/steveyegge/beads/blob/main/README.md#L37), [README.md#L105](https://github.com/steveyegge/beads/blob/main/README.md#L105) |
| Unix/Linux/macOS curl script | [docs/INSTALLING.md#L35](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L35) |
| Windows PowerShell script | [README.md#L110](https://github.com/steveyegge/beads/blob/main/README.md#L110) |
| Windows PowerShell script | [docs/INSTALLING.md#L108](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L108) |

### Package Managers

| Method | Location |
|--------|----------|
| Homebrew | [README.md#L115-L116](https://github.com/steveyegge/beads/blob/main/README.md#L115-L116) |
| Homebrew | [docs/INSTALLING.md#L10-L11](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L10-L11), [#L50-L51](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L50-L51), [#L71-L72](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L71-L72), [#L142](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L142) |
| npm global | [README.md#L94](https://github.com/steveyegge/beads/blob/main/README.md#L94) |
| npm global | [npm-package/CLAUDE_CODE_WEB.md#L34](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L34), [#L55](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L55), [#L145](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L145) |
| npm project-local | [npm-package/CLAUDE_CODE_WEB.md#L64](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L64) |
| Arch Linux AUR | [docs/INSTALLING.md#L78-L80](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L78-L80) |
| mise | [README.md#L121](https://github.com/steveyegge/beads/blob/main/README.md#L121) |
| mise | [docs/INSTALLING.md#L23](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L23) |
| pip/uv (MCP server) | [docs/INSTALLING.md#L187-L190](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L187-L190) |

### Go Install

| Method | Location |
|--------|----------|
| `go install` | [README.md#L99](https://github.com/steveyegge/beads/blob/main/README.md#L99) |
| `go install` | [docs/INSTALLING.md#L56](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L56), [#L87](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L87), [#L113](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L113), [#L250](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L250), [#L316](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L316) |
| `go install` | [npm-package/CLAUDE_CODE_WEB.md#L168](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L168), [#L191](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L191) |
| `CGO_ENABLED=1 go install` | [docs/INSTALLING.md#L260](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L260) |
| `CGO_ENABLED=1 go install` | [docs/TROUBLESHOOTING.md#L71](https://github.com/steveyegge/beads/blob/main/docs/TROUBLESHOOTING.md#L71) |

### Build From Source

| Method | Location |
|--------|----------|
| Standard build (Unix) | [README.md#L85](https://github.com/steveyegge/beads/blob/main/README.md#L85), [#L857](https://github.com/steveyegge/beads/blob/main/README.md#L857) |
| Standard build (Unix) | [docs/INSTALLING.md#L63](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L63), [#L94](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L94) |
| Standard build (Unix) | [docs/QUICKSTART.md#L9](https://github.com/steveyegge/beads/blob/main/docs/QUICKSTART.md#L9) |
| Windows build | [docs/INSTALLING.md#L120](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L120) |
| CGO-enabled build | [docs/INSTALLING.md#L265](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L265) |
| CGO-enabled build | [docs/TROUBLESHOOTING.md#L76](https://github.com/steveyegge/beads/blob/main/docs/TROUBLESHOOTING.md#L76) |

### Environment-Specific

| Method | Location |
|--------|----------|
| Claude Code for Web SessionStart hook | [npm-package/CLAUDE_CODE_WEB.md#L26-L48](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L26-L48), [#L179-L202](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L179-L202), [#L249-L289](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L249-L289) |
| Devcontainers | [README.md#L199](https://github.com/steveyegge/beads/blob/main/README.md#L199) |
| Devcontainers | [.devcontainer/README.md#L12-L24](https://github.com/steveyegge/beads/blob/main/.devcontainer/README.md#L12-L24), [#L29-L34](https://github.com/steveyegge/beads/blob/main/.devcontainer/README.md#L29-L34) |
| Claude Code Plugin | [docs/INSTALLING.md#L170-L171](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L170-L171) |
| Claude Code Plugin | [docs/PLUGIN.md#L36-L37](https://github.com/steveyegge/beads/blob/main/docs/PLUGIN.md#L36-L37), [#L51-L54](https://github.com/steveyegge/beads/blob/main/docs/PLUGIN.md#L51-L54) |
| MCP Server (Claude Desktop) | [docs/INSTALLING.md#L200-L206](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L200-L206) |
| MCP Server (Sourcegraph Amp) | [docs/INSTALLING.md#L213-L218](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L213-L218) |

---

## Initialization Methods

### Basic Init

| Method | Location |
|--------|----------|
| `bd init` | [README.md#L137](https://github.com/steveyegge/beads/blob/main/README.md#L137), [#L169](https://github.com/steveyegge/beads/blob/main/README.md#L169), [#L171](https://github.com/steveyegge/beads/blob/main/README.md#L171), [#L178](https://github.com/steveyegge/beads/blob/main/README.md#L178), [#L180](https://github.com/steveyegge/beads/blob/main/README.md#L180) |
| `bd init` | [docs/INSTALLING.md#L255](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L255) |
| `bd init` | [docs/QUICKSTART.md#L19](https://github.com/steveyegge/beads/blob/main/docs/QUICKSTART.md#L19) |
| `bd init --quiet` | [README.md#L167](https://github.com/steveyegge/beads/blob/main/README.md#L167), [#L169](https://github.com/steveyegge/beads/blob/main/README.md#L169) |
| `bd init --quiet` | [npm-package/CLAUDE_CODE_WEB.md#L38](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L38), [#L56](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L56), [#L277](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L277), [#L323](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L323) |
| `bd init --quiet` | [docs/INSTALLING.md#L146](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L146) |

### Workflow Modes

| Method | Location |
|--------|----------|
| `bd init --contributor` | [README.md#L140](https://github.com/steveyegge/beads/blob/main/README.md#L140) |
| `bd init --contributor` | [docs/QUICKSTART.md#L22](https://github.com/steveyegge/beads/blob/main/docs/QUICKSTART.md#L22) |
| `bd init --team` | [README.md#L143](https://github.com/steveyegge/beads/blob/main/README.md#L143) |
| `bd init --team` | [docs/QUICKSTART.md#L25](https://github.com/steveyegge/beads/blob/main/docs/QUICKSTART.md#L25) |
| `bd init --branch <name>` | [README.md#L146](https://github.com/steveyegge/beads/blob/main/README.md#L146), [#L159](https://github.com/steveyegge/beads/blob/main/README.md#L159) |
| `bd init --branch <name>` | [docs/QUICKSTART.md#L28](https://github.com/steveyegge/beads/blob/main/docs/QUICKSTART.md#L28) |
| `bd init --stealth` | [README.md#L206-L225](https://github.com/steveyegge/beads/blob/main/README.md#L206-L225) |

### Post-Init Configuration

| Method | Location |
|--------|----------|
| `bd hooks install` | [README.md#L339](https://github.com/steveyegge/beads/blob/main/README.md#L339) |
| `bd hooks install` | [docs/INSTALLING.md#L149](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L149) |
| Manual merge driver config | [README.md#L173-L175](https://github.com/steveyegge/beads/blob/main/README.md#L173-L175) |
| Manual merge driver config | [docs/GIT_INTEGRATION.md#L131-L132](https://github.com/steveyegge/beads/blob/main/docs/GIT_INTEGRATION.md#L131-L132), [#L143-L144](https://github.com/steveyegge/beads/blob/main/docs/GIT_INTEGRATION.md#L143-L144) |

---

## Agent Onboarding

| Method | Location |
|--------|----------|
| `bd onboard` | [README.md#L156](https://github.com/steveyegge/beads/blob/main/README.md#L156), [#L162](https://github.com/steveyegge/beads/blob/main/README.md#L162), [#L211](https://github.com/steveyegge/beads/blob/main/README.md#L211) |
| AGENTS.md bootstrap instruction | [README.md#L156](https://github.com/steveyegge/beads/blob/main/README.md#L156) |
| AGENTS.md bootstrap instruction | [npm-package/CLAUDE_CODE_WEB.md#L109-L122](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L109-L122) |

---

## Verification Commands

| Command | Location |
|---------|----------|
| `bd version` | [docs/INSTALLING.md#L126](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L126), [#L232](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L232) |
| `bd version` | [npm-package/CLAUDE_CODE_WEB.md#L77](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L77), [#L174](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L174) |
| `bd help` | [docs/INSTALLING.md#L233](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md#L233) |
| `bd doctor` | [README.md#L466](https://github.com/steveyegge/beads/blob/main/README.md#L466) |
| `bd info` | [npm-package/CLAUDE_CODE_WEB.md#L80](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md#L80) |

---

## Files Reviewed

- [README.md](https://github.com/steveyegge/beads/blob/main/README.md)
- [docs/INSTALLING.md](https://github.com/steveyegge/beads/blob/main/docs/INSTALLING.md)
- [docs/QUICKSTART.md](https://github.com/steveyegge/beads/blob/main/docs/QUICKSTART.md)
- [docs/PLUGIN.md](https://github.com/steveyegge/beads/blob/main/docs/PLUGIN.md)
- [docs/TROUBLESHOOTING.md](https://github.com/steveyegge/beads/blob/main/docs/TROUBLESHOOTING.md)
- [docs/GIT_INTEGRATION.md](https://github.com/steveyegge/beads/blob/main/docs/GIT_INTEGRATION.md)
- [npm-package/CLAUDE_CODE_WEB.md](https://github.com/steveyegge/beads/blob/main/npm-package/CLAUDE_CODE_WEB.md)
- [.devcontainer/README.md](https://github.com/steveyegge/beads/blob/main/.devcontainer/README.md)
