# Documentation & CLI Information Architecture Audit

**Date:** 2024-12-13
**Purpose:** Analyze documentation structure, identify overlaps, gaps, and redundancies

---

## Table of Contents

1. [CLI Commands Inventory](#1-cli-commands-inventory)
2. [Documentation Files Inventory](#2-documentation-files-inventory)
3. [Target Audience Matrix](#3-target-audience-matrix)
4. [Command Coverage Analysis](#4-command-coverage-analysis)
5. [Documentation Cross-References](#5-documentation-cross-references)
6. [Overlaps & Redundancies](#6-overlaps--redundancies)
7. [Contradictions & Inconsistencies](#7-contradictions--inconsistencies)
8. [Recommendations](#8-recommendations)

---

## 1. CLI Commands Inventory

### All Commands (47 total)

| Command | Source File | Subcommands | Description |
|---------|-------------|-------------|-------------|
| `bd` | main.go | - | Root command |
| `blocked` | ready.go | - | Show blocked issues |
| `clean` | clean.go | - | Clean unused data |
| `cleanup` | cleanup.go | - | Bulk delete closed issues |
| `close` | show.go | - | Close issue(s) |
| `comment` | comments.go | - | Add comment (alias) |
| `comments` | comments.go | add | Manage comments |
| `compact` | compact.go | - | Memory decay/compaction |
| `config` | config.go | set, get, list, unset | Configuration management |
| `count` | count.go | - | Count issues with filters |
| `create` | create.go | - | Create new issue |
| `daemon` | daemon.go | - | Start daemon process |
| `daemons` | daemons.go | list, health, stop, restart, logs, killall | Multi-daemon management |
| `delete` | delete.go | - | Delete issue(s) |
| `deleted` | deleted.go | - | Show deletion history |
| `dep` | dep.go | add, remove, tree, cycles | Dependency management |
| `detect-pollution` | detect_pollution.go | - | Detect DB pollution |
| `doctor` | doctor.go | - | Health check |
| `duplicates` | duplicates.go | - | Find/merge duplicates |
| `edit` | show.go | - | Edit issue in $EDITOR |
| `epic` | epic.go | status, close-eligible | Epic management |
| `export` | export.go | - | Export to JSONL |
| `hooks` | hooks.go | install, uninstall, list | Git hooks management |
| `import` | import.go | - | Import from JSONL |
| `info` | info.go | - | Database/daemon info |
| `init` | init.go | - | Initialize beads |
| `label` | label.go | add, remove, list, list-all | Label management |
| `list` | list.go | - | List issues |
| `merge` | merge.go | - | Merge duplicate issues |
| `migrate` | migrate.go | - | Database migrations |
| `monitor` | monitor.go | - | Web UI server |
| `onboard` | onboard.go | - | Generate onboarding docs |
| `prime` | prime.go | - | Context injection for AI |
| `quickstart` | quickstart.go | - | Interactive tutorial |
| `ready` | ready.go | - | Show ready work |
| `rename-prefix` | rename_prefix.go | - | Rename issue prefix |
| `reopen` | reopen.go | - | Reopen closed issue |
| `repair-deps` | repair_deps.go | - | Repair broken dependencies |
| `repo` | repo.go | add, remove, list, sync | Multi-repo management |
| `reset` | reset.go | - | Reset database |
| `restore` | restore.go | - | Restore compacted issue |
| `search` | search.go | - | Search issues |
| `setup` | setup.go | claude, cursor, aider | Editor integration setup |
| `show` | show.go | - | Show issue details |
| `stale` | stale.go | - | Find stale issues |
| `stats` | stats.go | - | Project statistics |
| `status` | status.go | - | Status overview |
| `sync` | sync.go | - | Sync database with git |
| `template` | template.go | list, show, create | Template management |
| `update` | show.go | - | Update issue |
| `upgrade` | upgrade.go | status, review, ack | Version upgrade management |
| `validate` | validate.go | - | Validate database |
| `version` | version.go | - | Show version |
| `worktree` | worktree.go | - | Git worktree support |

---

## 2. Documentation Files Inventory

### By Location (90+ files)

| Location | Count | Purpose |
|----------|-------|---------|
| **Root (`/`)** | 8 | Core project docs |
| **`docs/`** | 35+ | Detailed guides & references |
| **`docs/dev-notes/`** | 4 | Internal development notes |
| **`docs/adr/`** | 1 | Architecture Decision Records |
| **`skills/beads/`** | 1 | Claude Skill definition |
| **`skills/beads/references/`** | 6 | Skill reference material |
| **`integrations/beads-mcp/`** | 5 | MCP server documentation |
| **`npm-package/`** | 7 | NPM package docs |
| **`examples/`** | 18+ | Example project READMEs |
| **`.beads/`** | 2 | Per-project guides |
| **`.github/`** | 1 | Copilot instructions |
| **`.claude/`** | 1 | Claude test strategy |
| **`scripts/`** | 2 | Script documentation |
| **`cmd/bd/`** | 1 | CLI docs |

### Key Documentation Files

| File | Lines | Primary Purpose |
|------|-------|-----------------|
| `README.md` | 878 | Main user documentation |
| `AGENTS.md` | 755 | AI agent workflow guide |
| `AGENT_INSTRUCTIONS.md` | 398 | Development procedures |
| `docs/CLI_REFERENCE.md` | 560 | Command reference |
| `skills/beads/SKILL.md` | 645 | Claude Skill definition |
| `docs/DAEMON.md` | 537 | Daemon management |
| `integrations/beads-mcp/README.md` | 299 | MCP server guide |
| `docs/QUICKSTART.md` | 264 | Getting started tutorial |

---

## 3. Target Audience Matrix

### Four Audience Categories

| Audience | Description | Primary Docs |
|----------|-------------|--------------|
| **AI Agents** | Claude, Copilot, other AI assistants using bd | AGENTS.md, skills/SKILL.md, CLI_REFERENCE.md |
| **Human End Users** | Developers using bd in their projects | README.md, QUICKSTART.md, docs/*.md |
| **Beads Developers** | Contributors to the beads codebase | AGENT_INSTRUCTIONS.md, CONTRIBUTING.md, docs/dev-notes/ |
| **Dual-Purpose** | Relevant to multiple audiences | TROUBLESHOOTING.md, DAEMON.md, CONFIG.md |

### Detailed Audience Classification

#### AI Agents Only
| Document | Notes |
|----------|-------|
| `AGENTS.md` | Primary AI workflow guide, comprehensive |
| `AGENT_INSTRUCTIONS.md` | Development procedures for AI agents |
| `.github/copilot-instructions.md` | Copilot-optimized, condensed |
| `skills/beads/SKILL.md` | Claude Skill definition |
| `skills/beads/references/*.md` | Detailed reference for skills |
| `docs/CLI_REFERENCE.md` | Agent-optimized command reference |
| `docs/AGENT_MAIL*.md` | Multi-agent coordination |
| `docs/MULTI_REPO_AGENTS.md` | Multi-repo patterns for agents |

#### Human End Users Only
| Document | Notes |
|----------|-------|
| `README.md` | Main entry point, installation, quick start |
| `docs/QUICKSTART.md` | Interactive tutorial |
| `docs/INSTALLING.md` | Platform-specific installation |
| `docs/FAQ.md` | Frequently asked questions |
| `docs/UNINSTALLING.md` | Removal instructions |
| `npm-package/README.md` | NPM installation |
| `npm-package/CLAUDE_CODE_WEB.md` | Web-specific setup |
| Most `examples/*/README.md` | Setup & usage instructions |

#### Beads Developers Only
| Document | Notes |
|----------|-------|
| `CONTRIBUTING.md` | Contribution guidelines |
| `RELEASING.md` / `docs/RELEASING.md` | Release process |
| `SECURITY.md` | Security policy |
| `build-docs.md` | Build documentation |
| `docs/TESTING.md` | Testing guide |
| `docs/README_TESTING.md` | Test documentation |
| `docs/PERFORMANCE_TESTING.md` | Performance benchmarks |
| `docs/LINTING.md` | Linter configuration |
| `docs/dev-notes/*.md` | Internal development notes |
| `docs/adr/*.md` | Architecture decisions |
| `docs/INTERNALS.md` | Internal architecture |
| `docs/ARCHITECTURE.md` | System architecture |
| `npm-package/PUBLISHING.md` | PyPI publishing |
| `scripts/README.md` | Development scripts |

#### Dual-Purpose (AI + Human End Users)
| Document | Notes |
|----------|-------|
| `CLAUDE.md` | Claude Code project guidance |
| `docs/CLAUDE.md` | Architecture for Claude |
| `docs/DAEMON.md` | Daemon management |
| `docs/CONFIG.md` | Configuration system |
| `docs/TROUBLESHOOTING.md` | Problem solving |
| `docs/GIT_INTEGRATION.md` | Git workflows |
| `docs/LABELS.md` | Label system |
| `docs/ADVANCED.md` | Advanced features |
| `docs/EXTENDING.md` | Database extensions |
| `docs/PROTECTED_BRANCHES.md` | Protected branch setup |

#### Dual-Purpose (Human End Users + Beads Developers)
| Document | Notes |
|----------|-------|
| `CHANGELOG.md` | Version history |
| `BENCHMARKS.md` | Performance data |
| `integrations/beads-mcp/README.md` | MCP server (use + development) |

---

## 4. Command Coverage Analysis

### Well-Documented Commands
Commands documented in 3+ locations with examples:

| Command | Documentation Locations |
|---------|------------------------|
| `create` | README, AGENTS, CLI_REFERENCE, QUICKSTART, skills/SKILL.md |
| `ready` | README, AGENTS, CLI_REFERENCE, QUICKSTART, skills/SKILL.md |
| `update` | README, AGENTS, CLI_REFERENCE, skills/SKILL.md |
| `close` | README, AGENTS, CLI_REFERENCE, skills/SKILL.md |
| `list` | README, AGENTS, CLI_REFERENCE, skills/SKILL.md |
| `show` | README, AGENTS, CLI_REFERENCE, skills/SKILL.md |
| `sync` | README, AGENTS, DAEMON, GIT_INTEGRATION |
| `dep` | README, AGENTS, CLI_REFERENCE, QUICKSTART |
| `init` | README, QUICKSTART, examples/* |
| `daemons` | README, DAEMON, CLI_REFERENCE |
| `import/export` | README, CLI_REFERENCE, ADVANCED |
| `migrate` | README, CLI_REFERENCE, QUICKSTART |
| `config` | README, CONFIG, CLI_REFERENCE |
| `compact` | README, CLI_REFERENCE, QUICKSTART |
| `label` | README, CLI_REFERENCE, LABELS |
| `hooks` | README, AGENTS, GIT_INTEGRATION |

### Moderately Documented Commands
Commands with 1-2 documentation locations:

| Command | Documentation |
|---------|---------------|
| `cleanup` | CLI_REFERENCE |
| `delete` | CLI_REFERENCE, DELETIONS |
| `deleted` | AGENTS (brief), DELETIONS |
| `duplicates` | AGENTS, CLI_REFERENCE |
| `merge` | CLI_REFERENCE |
| `stale` | CLI_REFERENCE |
| `info` | CLI_REFERENCE, DAEMON |
| `doctor` | README (brief) |
| `blocked` | CLI_REFERENCE, skills/SKILL.md |
| `stats` | skills/SKILL.md |
| `reopen` | CLI_REFERENCE |

### Under-Documented Commands
Commands with minimal or no dedicated documentation:

| Command | Status | Notes |
|---------|--------|-------|
| `clean` | Minimal | Brief mention only |
| `comment/comments` | Minimal | No dedicated section |
| `count` | Minimal | Mentioned in passing |
| `detect-pollution` | **None** | No documentation found |
| `edit` | Minimal | CLI_REFERENCE only, marked "HUMANS ONLY" |
| `epic` | Minimal | Only hierarchical ID examples |
| `monitor` | Minimal | README example only |
| `onboard` | Minimal | Brief mention in AGENTS |
| `prime` | Minimal | Mentioned but not detailed |
| `rename-prefix` | Minimal | CLI_REFERENCE only |
| `repair-deps` | **None** | No documentation found |
| `repo` | **None** | No dedicated documentation |
| `reset` | **None** | No documentation found |
| `restore` | Minimal | CLI_REFERENCE only |
| `search` | Minimal | Not documented |
| `setup` | Minimal | Brief mention |
| `status` | Minimal | Not documented |
| `template` | Minimal | README mention only |
| `upgrade` | **None** | No dedicated documentation |
| `validate` | **None** | No documentation found |
| `worktree` | Minimal | DAEMON only |

---

## 5. Documentation Cross-References

### Hub Documents (many outbound links)

| Document | Outbound Links | Role |
|----------|----------------|------|
| `README.md` | ~30+ | Main entry point for end users |
| `AGENTS.md` | ~15+ | Main entry point for AI agents |
| `docs/CLI_REFERENCE.md` | ~8 | Command reference hub |
| `skills/beads/SKILL.md` | 6 | Skill reference hub |
| `docs/DAEMON.md` | ~5 | Daemon topic hub |

### Spoke Documents (inbound links only)

| Document | Linked From |
|----------|-------------|
| `docs/COLLISION_MATH.md` | README only |
| `docs/ANTIVIRUS.md` | TROUBLESHOOTING only |
| `docs/EXCLUSIVE_LOCK.md` | DAEMON only |
| `docs/DELETIONS.md` | README only |
| `docs/ADAPTIVE_IDS.md` | Not linked |

### Orphan Documents (not linked from anywhere)

| Document | Notes |
|----------|-------|
| `docs/adr/002-agent-mail-integration.md` | ADR not referenced |
| `docs/dev-notes/*.md` | Internal notes, not linked |
| `docs/PERFORMANCE_TESTING.md` | Not referenced |
| `docs/ATTRIBUTION.md` | Not referenced |
| `docs/ROUTING.md` | Not referenced |
| `docs/INTERNALS.md` | Not referenced |
| `docs/ARCHITECTURE.md` | Minimal references |
| `docs/AGENT_MEMORY.md` | Not referenced |
| `docs/MULTI_REPO_HYDRATION.md` | Not referenced |

---

## 6. Overlaps & Redundancies

### Critical Duplications

#### 1. CLI Reference Files (Near-Identical)
| File | Lines | Issue |
|------|-------|-------|
| `docs/CLI_REFERENCE.md` | 560 | Original |
| `skills/beads/references/CLI_REFERENCE.md` | 560 | **Near-duplicate** |

**Recommendation:** Remove or symlink `skills/beads/references/CLI_REFERENCE.md`

#### 2. RELEASING.md Files (90% Identical)
| File | Lines | Issue |
|------|-------|-------|
| `RELEASING.md` (root) | 341 | Longer version |
| `docs/RELEASING.md` | ~300 | Shorter version |

**Recommendation:** Keep one canonical version, redirect/delete the other

#### 3. CLAUDE.md Files (Overlapping Purpose)
| File | Purpose | Issue |
|------|---------|-------|
| `CLAUDE.md` (root) | Project instructions for Claude | Refinery-specific |
| `docs/CLAUDE.md` | Architecture overview for Claude | General Claude guidance |

**Recommendation:** Clarify distinct purposes or consolidate

### Content Repeated Across Multiple Documents

#### Issue Types & Priorities
Exact definitions repeated in **6+ documents**:
- `README.md`
- `AGENTS.md`
- `docs/CLI_REFERENCE.md`
- `docs/QUICKSTART.md`
- `skills/beads/SKILL.md`
- `.github/copilot-instructions.md`

#### Workflow Instructions
"ready → update → close → sync" workflow in **6+ documents**:
- `AGENTS.md` (most detailed)
- `README.md`
- `docs/QUICKSTART.md`
- `docs/CLI_REFERENCE.md`
- `skills/beads/SKILL.md`
- `.github/copilot-instructions.md`

#### Dependency Types
Four dependency types explained in **5+ documents**:
- `README.md`
- `AGENTS.md`
- `docs/CLI_REFERENCE.md`
- `skills/beads/SKILL.md`
- `skills/beads/references/DEPENDENCIES.md`

---

## 7. Contradictions & Inconsistencies

### Factual Inconsistencies

| Issue | Location 1 | Location 2 | Resolution Needed |
|-------|------------|------------|-------------------|
| **Debounce timing** | README: "5 seconds" | AGENTS.md: "30-second" / "5-second" mixed | Clarify actual value |
| **Go version** | AGENTS.md: "Go 1.24+" | copilot-instructions: "Go 1.21+" | Update to current |
| **MCP recommendation** | README: "CLI + hooks recommended" | copilot: "MCP Server (Recommended)" | Clarify per-context |
| **Database location** | QUICKSTART: `~/.beads/default.db` | skills/SKILL: `.beads/*.db` | Both valid, clarify |

### Terminology Inconsistencies

| Term | Variations Found |
|------|------------------|
| JSONL filename | `issues.jsonl`, `beads.jsonl` (both mentioned) |
| Issue type casing | "bug", "Bug", "BUG" |
| Daemon socket | `bd.sock` vs `bd.pipe` (OS-dependent, not always noted) |

### Structural Inconsistencies

| Issue | Description |
|-------|-------------|
| Root vs docs/ | Some topics have files in both locations (RELEASING, CLAUDE) |
| Skills structure | `skills/beads/references/CLI_REFERENCE.md` duplicates `docs/CLI_REFERENCE.md` |
| Audience mixing | Some docs mix AI-specific and human-specific content |

---

## 8. Recommendations

### High Priority

#### 1. Deduplicate CLI Reference
- **Action:** Remove `skills/beads/references/CLI_REFERENCE.md`
- **Alternative:** Create symlink or use `<!-- include -->` directive
- **Impact:** Eliminates 560 lines of duplicate content

#### 2. Consolidate RELEASING.md
- **Action:** Keep `docs/RELEASING.md`, delete root `RELEASING.md`
- **Alternative:** Keep root version, add redirect in docs/
- **Impact:** Single source of truth for release process

#### 3. Clarify CLAUDE.md Files
- **Action:** Rename `docs/CLAUDE.md` to `docs/CLAUDE_ARCHITECTURE.md`
- **Alternative:** Merge into single comprehensive file
- **Impact:** Reduces confusion for Claude Code

#### 4. Fix Debounce Timing
- **Action:** Audit code, update all docs to match actual value
- **Impact:** Accurate documentation

### Medium Priority

#### 5. Document Missing Commands
Create documentation for:
- `repair-deps` - What it does, when to use
- `reset` - What it resets, safety warnings
- `validate` - What it validates, output format
- `detect-pollution` - Use case, interpretation
- `repo` - Multi-repo workflow
- `upgrade` - Version upgrade process
- `count` - Filtering options
- `search` - Search syntax

#### 6. Link Orphan Documents
Add references to hub documents for:
- `docs/ARCHITECTURE.md` → Link from README, CONTRIBUTING
- `docs/INTERNALS.md` → Link from CONTRIBUTING
- `docs/adr/` → Link from CONTRIBUTING
- `docs/AGENT_MEMORY.md` → Link from AGENTS

#### 7. Create Audience-Specific Entry Points
- Add "For AI Agents" section in README pointing to AGENTS.md
- Add "For Contributors" section pointing to CONTRIBUTING
- Consider separate "Getting Started" pages per audience

### Low Priority

#### 8. Standardize Repeated Content
- Create single canonical source for:
  - Issue types definitions
  - Priority level definitions
  - Dependency type definitions
  - Basic workflow pattern
- Reference via includes or links

#### 9. Standardize Terminology
- Pick one: `issues.jsonl` (current canonical name)
- Consistent casing: lowercase for types
- Note OS-specific paths consistently

#### 10. Create Command Index
- Single page listing all 47 commands
- Brief description for each
- Link to detailed documentation
- Indicate documentation status (full/partial/none)

---

## Appendix: Documentation Map

```
beads/
├── README.md                    [End Users] Main entry
├── AGENTS.md                    [AI Agents] Primary guide
├── AGENT_INSTRUCTIONS.md        [AI + Developers] Procedures
├── CLAUDE.md                    [AI] Project instructions
├── CONTRIBUTING.md              [Developers] Guidelines
├── RELEASING.md                 [Developers] Release process (DUPLICATE)
├── SECURITY.md                  [Developers] Security policy
├── CHANGELOG.md                 [All] Version history
├── BENCHMARKS.md                [Developers] Performance
├── build-docs.md                [Developers] Build docs
│
├── docs/
│   ├── CLI_REFERENCE.md         [AI + End Users] Commands
│   ├── QUICKSTART.md            [End Users] Tutorial
│   ├── INSTALLING.md            [End Users] Installation
│   ├── DAEMON.md                [All] Daemon guide
│   ├── CONFIG.md                [All] Configuration
│   ├── TROUBLESHOOTING.md       [All] Problems
│   ├── FAQ.md                   [End Users] Questions
│   ├── ADVANCED.md              [All] Advanced features
│   ├── LABELS.md                [All] Labels
│   ├── GIT_INTEGRATION.md       [All] Git workflows
│   ├── PROTECTED_BRANCHES.md    [End Users] Protected branches
│   ├── EXTENDING.md             [Developers] Extensions
│   ├── TESTING.md               [Developers] Testing
│   ├── RELEASING.md             [Developers] Release (DUPLICATE)
│   ├── CLAUDE.md                [AI] Architecture (OVERLAP)
│   ├── CLAUDE_INTEGRATION.md    [Developers] Design decisions
│   ├── AGENT_MAIL*.md           [AI] Multi-agent
│   ├── MULTI_REPO_*.md          [AI + End Users] Multi-repo
│   ├── DELETIONS.md             [All] Deletion tracking
│   ├── EXCLUSIVE_LOCK.md        [Developers] Lock protocol
│   ├── LINTING.md               [Developers] Linting
│   ├── ARCHITECTURE.md          [Developers] Architecture (ORPHAN)
│   ├── INTERNALS.md             [Developers] Internals (ORPHAN)
│   ├── dev-notes/               [Developers] Internal notes
│   └── adr/                     [Developers] ADRs (ORPHAN)
│
├── skills/beads/
│   ├── SKILL.md                 [AI] Skill definition
│   └── references/
│       ├── CLI_REFERENCE.md     [AI] Commands (DUPLICATE)
│       ├── WORKFLOWS.md         [AI] Workflows
│       ├── BOUNDARIES.md        [AI] bd vs TodoWrite
│       ├── DEPENDENCIES.md      [AI] Dependencies
│       ├── ISSUE_CREATION.md    [AI] Issue creation
│       └── STATIC_DATA.md       [AI] Static data usage
│
├── integrations/beads-mcp/
│   ├── README.md                [All] MCP server
│   ├── SETUP_DAEMON.md          [Developers] Daemon setup
│   ├── CONTEXT_MANAGEMENT.md    [Developers] Context
│   └── PYPI.md                  [Developers] Publishing
│
├── npm-package/
│   ├── README.md                [End Users] NPM package
│   ├── CLAUDE_CODE_WEB.md       [End Users] Web setup
│   ├── PUBLISHING.md            [Developers] Publishing
│   └── ...
│
├── examples/*/README.md         [End Users] Examples
│
└── .github/
    └── copilot-instructions.md  [AI] Copilot guide
```

Legend:
- `[AI]` = AI Agents
- `[End Users]` = Human End Users
- `[Developers]` = Beads Developers
- `[All]` = Multiple audiences
- `(DUPLICATE)` = Redundant content
- `(OVERLAP)` = Partially overlapping
- `(ORPHAN)` = Not linked from anywhere
