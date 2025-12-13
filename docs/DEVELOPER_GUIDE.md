# Beads Developer Guide

**Audience:** Developers who want to contribute to the Beads project itself

This guide is for **developers** who want to contribute to the Beads repository. If you're looking to use Beads in your projects, see [USER_GUIDE.md](USER_GUIDE.md).

## Table of Contents

- [Project Overview](#project-overview)
- [Development Setup](#development-setup)
- [Project Structure](#project-structure)
- [Building and Testing](#building-and-testing)
- [Development Workflow](#development-workflow)
- [Adding Features](#adding-features)
- [Code Standards](#code-standards)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)
- [Release Process](#release-process)
- [Troubleshooting Development Issues](#troubleshooting-development-issues)

## Project Overview

Beads is a Git-backed issue tracker written in Go, designed for AI-supervised coding workflows.

**Tech Stack:**
- **Language:** Go 1.24+
- **Database:** SQLite (via `internal/storage/sqlite/`)
- **CLI Framework:** Cobra
- **Testing:** Go standard testing with table-driven tests
- **CI/CD:** GitHub Actions
- **Integrations:** Python MCP server, npm package, Claude plugin

**Key Design Principles:**
- Minimal dependencies
- Fast local operations
- Git-native storage (JSONL)
- AI-friendly API (JSON output)
- Dependency-aware issue tracking

## Development Setup

### Prerequisites

**Required:**
- Go 1.24 or later ([install Go](https://go.dev/doc/install))
- Git
- Make (usually pre-installed on Unix systems)

**Optional but recommended:**
- [golangci-lint](https://golangci-lint.run/usage/install/) - Code linting
- [delve](https://github.com/go-delve/delve) - Go debugger
- SQLite command-line tools - Database inspection

### Initial Setup

1. **Fork and clone the repository:**

   ```bash
   # Fork on GitHub first, then clone your fork
   git clone https://github.com/YOUR_USERNAME/beads
   cd beads
   ```

2. **Add upstream remote:**

   ```bash
   git remote add upstream https://github.com/steveyegge/beads
   ```

3. **Build the project:**

   ```bash
   # Using make (recommended)
   make build
   
   # Or directly with go
   go build -o bd ./cmd/bd
   ```

4. **Install locally:**

   ```bash
   # Install to $GOPATH/bin with version info
   make install
   
   # Verify installation
   bd version
   ```

5. **Initialize for dogfooding:**

   ```bash
   # Use beads to track your beads development work
   bd init --quiet
   ```

### IDE Setup

**VS Code:**
- Install Go extension
- Configure settings for go formatting and linting
- Install delve for debugging

**GoLand/IntelliJ:**
- Import as Go project
- Enable Go modules support
- Configure file watchers for gofmt

## Project Structure

```
beads/
├── cmd/bd/                      # CLI entry point
│   ├── main.go                  # Command root and setup
│   ├── create.go                # Create command
│   ├── list.go                  # List command
│   ├── update.go                # Update command
│   ├── close.go                 # Close command
│   ├── dep.go                   # Dependency commands
│   ├── ready.go                 # Ready work detection
│   └── ...                      # Other commands
│
├── internal/                    # Internal packages (not importable)
│   ├── types/                   # Core data structures
│   │   ├── types.go             # Issue, Dependency, etc.
│   │   └── types_test.go        # Type tests
│   │
│   └── storage/                 # Storage layer
│       ├── storage.go           # Storage interface
│       └── sqlite/              # SQLite implementation
│           ├── sqlite.go        # Main storage implementation
│           ├── schema.go        # Database schema
│           ├── migrations.go    # Schema migrations
│           └── sqlite_test.go   # Storage tests
│
├── integrations/                # External integrations
│   └── beads-mcp/               # MCP server (Python)
│       ├── pyproject.toml       # Python package config
│       └── src/beads_mcp/       # MCP server code
│
├── npm-package/                 # npm package for Node.js
│   ├── package.json             # npm package config
│   └── postinstall.js           # Binary download script
│
├── examples/                    # Usage examples
│   ├── python-agent/            # Python agent example
│   ├── bash-agent/              # Bash agent example
│   └── ...                      # Other examples
│
├── scripts/                     # Build and release scripts
│   ├── install.sh               # User installation script
│   ├── bump-version.sh          # Version management
│   ├── release.sh               # Release automation
│   └── update-homebrew.sh       # Homebrew formula update
│
├── docs/                        # Documentation
│   ├── USER_GUIDE.md            # End-user guide
│   ├── DEVELOPER_GUIDE.md       # This file
│   ├── INSTALLING.md            # Installation guide
│   ├── CLI_REFERENCE.md         # Complete CLI reference
│   └── ...                      # Specialized docs
│
├── .github/                     # GitHub-specific files
│   ├── workflows/               # CI/CD workflows
│   │   ├── ci.yml               # Main CI pipeline
│   │   ├── release.yml          # Release automation
│   │   └── ...                  # Other workflows
│   └── copilot-instructions.md  # GitHub Copilot instructions
│
├── Makefile                     # Build targets
├── .goreleaser.yml              # Release configuration
├── .golangci.yml                # Linter configuration
├── go.mod                       # Go module definition
├── go.sum                       # Go module checksums
│
├── README.md                    # Main project README
├── AGENTS.md                    # AI agent instructions
├── AGENT_INSTRUCTIONS.md        # Detailed agent dev procedures
├── CONTRIBUTING.md              # Contribution guidelines
├── CHANGELOG.md                 # Version history
├── LICENSE                      # MIT license
└── SECURITY.md                  # Security policy
```

### Key Files for Different Tasks

**Adding a new command:**
- `cmd/bd/mycommand.go` - Command implementation
- `cmd/bd/main.go` - Register command
- `docs/CLI_REFERENCE.md` - Document command

**Adding storage features:**
- `internal/storage/storage.go` - Update interface
- `internal/storage/sqlite/sqlite.go` - Implement in SQLite
- `internal/storage/sqlite/schema.go` - Update schema if needed
- `internal/storage/sqlite/migrations.go` - Add migration if needed

**Updating documentation:**
- `README.md` - Main user-facing documentation
- `docs/USER_GUIDE.md` - End-user guide
- `docs/CLI_REFERENCE.md` - Command reference
- Specialized docs in `docs/` as needed

## Building and Testing

### Building

```bash
# Build binary (output: ./bd)
make build
# or
go build -o bd ./cmd/bd

# Install to $GOPATH/bin with version info
make install

# Build for specific platform
GOOS=linux GOARCH=amd64 go build -o bd-linux-amd64 ./cmd/bd
```

### Testing

**Run tests:**
```bash
# Quick tests (recommended during development)
go test -short ./...

# Full test suite (before committing)
go test ./...

# With coverage
go test -coverprofile=coverage.out ./...
go tool cover -html=coverage.out

# With race detection
go test -race ./...

# Specific package
go test ./internal/storage/sqlite -v

# Specific test
go test ./internal/types -run TestIssueValidation -v
```

**Test categories:**
- **Fast tests (< 2s):** Unit tests, run with `-short`
- **Slow tests (2-20s):** Integration tests with git operations, skipped with `-short`

**IMPORTANT:** Never pollute the production database with test data!

```bash
# For manual testing, use BEADS_DB environment variable
BEADS_DB=/tmp/test.db bd init --quiet
BEADS_DB=/tmp/test.db bd create "Test issue" -p 1
```

### Linting

```bash
# Run linter
golangci-lint run ./...
```

**Note:** The linter reports ~100 baseline warnings (documented false positives and idiomatic Go patterns). See [docs/LINTING.md](LINTING.md). Focus on avoiding new issues.

### Continuous Integration

CI runs on every push and pull request:
- **Fast tests** (`go test -short ./...`) - ~2s
- **Linting** (`golangci-lint run ./...`)
- **Build verification** (all platforms)

Full tests run nightly due to git operation overhead (~14s).

## Development Workflow

### Standard Workflow

1. **Create a feature branch:**
   ```bash
   git checkout -b feature/my-feature
   ```

2. **Make changes and test locally:**
   ```bash
   # Make changes
   vim cmd/bd/myfeature.go
   
   # Build
   make build
   
   # Test manually
   ./bd mycommand --test
   
   # Run tests
   go test -short ./...
   ```

3. **Track your work in beads:**
   ```bash
   bd create "Implement feature X" --type feature --priority 1
   bd update bd-a1b2 --status in_progress
   ```

4. **Commit and push:**
   ```bash
   git add .
   git commit -m "Add feature X"
   git push origin feature/my-feature
   
   # Sync beads
   bd close bd-a1b2 --reason "Completed"
   bd sync
   ```

5. **Open a pull request:**
   - Go to GitHub and create PR
   - Fill in description with what changed and why
   - Link to related issues if applicable
   - Wait for CI to pass and review

### Using Beads to Track Beads Development

We dogfood Beads for tracking development work:

```bash
# Check what's ready to work on
bd ready

# Claim an issue
bd update bd-a1b2 --status in_progress

# During work: discover a bug? File it!
bd create "Found bug in export logic" \
  --description="Export fails when issue has null parent_id" \
  --type bug \
  --priority 0 \
  --deps discovered-from:bd-a1b2

# Complete your work
bd close bd-a1b2 --reason "Implemented and tested"

# End of session
bd sync
```

## Adding Features

### Adding a New Command

1. **Create command file:**
   ```bash
   # Create cmd/bd/mycommand.go
   ```

2. **Implement using Cobra:**
   ```go
   package main
   
   import (
       "fmt"
       "github.com/spf13/cobra"
   )
   
   var myCommandCmd = &cobra.Command{
       Use:   "mycommand [args]",
       Short: "Brief description",
       Long:  "Detailed description",
       RunE: func(cmd *cobra.Command, args []string) error {
           // Implementation
           return nil
       },
   }
   
   func init() {
       // Add flags
       myCommandCmd.Flags().StringP("option", "o", "", "Option description")
       myCommandCmd.Flags().Bool("json", false, "Output in JSON format")
   }
   ```

3. **Register in main.go:**
   ```go
   rootCmd.AddCommand(myCommandCmd)
   ```

4. **Add tests:**
   ```bash
   # Create cmd/bd/mycommand_test.go
   ```

5. **Document:**
   - Update `docs/CLI_REFERENCE.md`
   - Update README.md if user-facing
   - Add example usage

### Adding Storage Features

1. **Update interface:**
   ```go
   // internal/storage/storage.go
   type Store interface {
       // ... existing methods ...
       MyNewMethod(ctx context.Context, arg string) error
   }
   ```

2. **Implement in SQLite:**
   ```go
   // internal/storage/sqlite/sqlite.go
   func (s *Store) MyNewMethod(ctx context.Context, arg string) error {
       // Implementation
       return nil
   }
   ```

3. **Update schema if needed:**
   ```go
   // internal/storage/sqlite/schema.go
   const schemaVersion = 10  // Increment
   
   // Add to migrations.go
   func (s *Store) migrate9to10(ctx context.Context) error {
       // Migration logic
       return nil
   }
   ```

4. **Add tests:**
   ```go
   // internal/storage/sqlite/sqlite_test.go
   func TestMyNewMethod(t *testing.T) {
       // Test implementation
   }
   ```

### Adding Examples

1. **Create directory:**
   ```bash
   mkdir -p examples/my-example
   ```

2. **Add README:**
   ```bash
   # Create examples/my-example/README.md
   ```

3. **Add working code:**
   ```bash
   # Add example scripts/programs
   ```

4. **Link from main examples README:**
   ```bash
   # Update examples/README.md
   ```

## Code Standards

### Go Style

- Follow [Effective Go](https://go.dev/doc/effective_go)
- Use `gofmt` (automatic in most editors)
- Keep functions small and focused
- Use descriptive variable names
- Add comments for exported functions and types

### Patterns We Use

**Table-driven tests:**
```go
func TestValidation(t *testing.T) {
    tests := []struct {
        name    string
        input   string
        wantErr bool
    }{
        {"valid input", "test", false},
        {"empty input", "", true},
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            err := Validate(tt.input)
            if (err != nil) != tt.wantErr {
                t.Errorf("got err=%v, want err=%v", err, tt.wantErr)
            }
        })
    }
}
```

**Error handling:**
```go
// Wrap errors with context
if err := doSomething(); err != nil {
    return fmt.Errorf("failed to do something: %w", err)
}
```

**Defer for cleanup:**
```go
func processFile(path string) error {
    f, err := os.Open(path)
    if err != nil {
        return err
    }
    defer f.Close()  // Always close
    
    // Process file
    return nil
}
```

### Comments

**Package comments:**
```go
// Package types provides core data structures for beads.
package types
```

**Function comments:**
```go
// CreateIssue creates a new issue with the given parameters and
// returns the issue ID. Returns an error if validation fails.
func CreateIssue(ctx context.Context, title string) (string, error) {
```

**Inline comments (sparingly):**
```go
// Only when non-obvious
if x > 0 {
    // Edge case: negative values would break the hash function
    hash = computeHash(x)
}
```

## Testing Guidelines

### Test Structure

**Unit tests:**
- Test one function/method
- Use mocks/stubs for dependencies
- Fast (< 100ms per test)
- Run with `-short`

**Integration tests:**
- Test multiple components together
- May use real database/filesystem
- Slower (100ms - 2s)
- Skip with `if testing.Short() { t.Skip() }`

### Writing Tests

**Good test structure:**
```go
func TestCreateIssue(t *testing.T) {
    // Setup
    tmpDir := t.TempDir()
    dbPath := filepath.Join(tmpDir, ".beads", "beads.db")
    store := newTestStore(t, dbPath)
    
    // Test data
    tests := []struct {
        name    string
        title   string
        wantErr bool
    }{
        {"valid issue", "Test issue", false},
        {"empty title", "", true},
    }
    
    // Execute and verify
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            id, err := store.CreateIssue(context.Background(), tt.title)
            if (err != nil) != tt.wantErr {
                t.Errorf("CreateIssue() error = %v, wantErr %v", err, tt.wantErr)
            }
            if !tt.wantErr && id == "" {
                t.Error("CreateIssue() returned empty ID")
            }
        })
    }
}
```

**Test helpers:**
```go
// Create reusable test helpers
func newTestStore(t *testing.T, path string) *sqlite.Store {
    t.Helper()
    store, err := sqlite.Open(path)
    if err != nil {
        t.Fatalf("failed to open store: %v", err)
    }
    t.Cleanup(func() {
        store.Close()
    })
    return store
}
```

### Test Coverage

Aim for:
- **Core logic:** 80%+ coverage
- **Commands:** Test happy path and error cases
- **Storage layer:** High coverage (90%+)

Check coverage:
```bash
go test -coverprofile=coverage.out ./...
go tool cover -func=coverage.out | grep total
```

## Documentation

### When to Update Docs

**Always update for:**
- New commands or flags
- Breaking changes
- New features
- Configuration changes

**Update these files:**
- `README.md` - User-facing changes
- `docs/USER_GUIDE.md` - End-user workflows
- `docs/CLI_REFERENCE.md` - Command reference
- `CHANGELOG.md` - Version history
- Specialized docs as needed

### Documentation Style

**Be clear and concise:**
```markdown
## Good
Use `bd create` to create new issues. Add `--priority 1` for high priority.

## Bad
The creation of issues is performed by the create subcommand which accepts
various flags including the priority flag...
```

**Include examples:**
```markdown
## Creating Issues

```bash
# Basic issue
bd create "Fix bug" --type bug --priority 1

# With description
bd create "Add feature" \
  --description "Detailed explanation" \
  --type feature
```
```

**Cross-link related docs:**
```markdown
For more on labels, see [LABELS.md](LABELS.md).
```

## Release Process

### Version Numbering

We use [Semantic Versioning](https://semver.org/):
- **Major (X.0.0):** Breaking changes
- **Minor (0.X.0):** New features, backward compatible
- **Patch (0.0.X):** Bug fixes, backward compatible

### Bumping Version

```bash
# Preview changes
./scripts/bump-version.sh 0.21.0

# Commit version bump
./scripts/bump-version.sh 0.21.0 --commit
git push origin main
```

This updates:
- `cmd/bd/version.go`
- `.claude-plugin/plugin.json`
- `integrations/beads-mcp/pyproject.toml`
- Documentation

### Creating a Release

**Automated (recommended):**
```bash
./scripts/release.sh 0.21.0
```

This script:
1. Bumps version
2. Runs tests
3. Creates git tag
4. Waits for GitHub Actions to build artifacts
5. Updates Homebrew formula
6. Verifies installation

**Manual:**
1. Bump version: `./scripts/bump-version.sh 0.21.0 --commit`
2. Update CHANGELOG.md with release notes
3. Run tests: `go test ./...`
4. Push: `git push origin main`
5. Tag: `git tag v0.21.0 && git push origin v0.21.0`
6. Wait for GitHub Actions (~5 min)
7. Update Homebrew: `./scripts/update-homebrew.sh 0.21.0`
8. Verify: `brew update && brew upgrade bd && bd version`

See [docs/RELEASING.md](RELEASING.md) for complete details.

### Release Checklist

- [ ] Version bumped in all files
- [ ] CHANGELOG.md updated
- [ ] Tests pass (`go test ./...`)
- [ ] Linter passes (`golangci-lint run ./...`)
- [ ] Documentation updated
- [ ] Tag pushed to GitHub
- [ ] GitHub Actions completed successfully
- [ ] Homebrew formula updated
- [ ] Verified installation from Homebrew
- [ ] Announced release (if major)

## Troubleshooting Development Issues

### Build Failures

**Problem:** `go build` fails with module errors

**Solution:**
```bash
# Clean module cache
go clean -modcache

# Re-download dependencies
go mod download

# Verify go.mod
go mod verify
```

### Test Failures

**Problem:** Tests pass locally but fail in CI

**Solution:**
- Check if test assumes specific file paths (use `t.TempDir()`)
- Check for timezone dependencies (use UTC in tests)
- Check for race conditions (run `go test -race ./...`)

### Database Lock Errors

**Problem:** "database is locked" during tests

**Solution:**
```bash
# Ensure proper cleanup in tests
t.Cleanup(func() {
    store.Close()
})

# Use isolated databases
tmpDir := t.TempDir()
dbPath := filepath.Join(tmpDir, "test.db")
```

### Import Cycle Errors

**Problem:** "import cycle not allowed"

**Solution:**
- Move shared types to `internal/types`
- Avoid circular dependencies between packages
- Use interfaces to break cycles

### Version Info Not Showing

**Problem:** `bd version` doesn't show commit/branch

**Solution:**
```bash
# Use make install (not go install)
make install

# Or set ldflags manually
go install -ldflags="-X main.Commit=$(git rev-parse HEAD)" ./cmd/bd
```

## Getting Help

- **Check existing issues:** Browse [GitHub issues](https://github.com/steveyegge/beads/issues)
- **Ask in discussions:** Use [GitHub Discussions](https://github.com/steveyegge/beads/discussions)
- **Read the docs:** Check [docs/](.) directory
- **Look at examples:** See [examples/](../examples/) directory

## Contributing

Thank you for contributing to Beads! Your contributions make this project better for everyone.

**Quick tips:**
- Start with small, focused changes
- Write tests for new functionality
- Update documentation
- Follow the code style
- Be patient and respectful in reviews

See [CONTRIBUTING.md](../CONTRIBUTING.md) for complete contribution guidelines.

## Documentation Map

**For End-Users:**
- [USER_GUIDE.md](USER_GUIDE.md) - End-user guide
- [INSTALLING.md](INSTALLING.md) - Installation guide
- [QUICKSTART.md](QUICKSTART.md) - Quick start tutorial

**For Developers (You):**
- [DEVELOPER_GUIDE.md](DEVELOPER_GUIDE.md) - This document
- [CONTRIBUTING.md](../CONTRIBUTING.md) - Contribution guidelines
- [AGENT_INSTRUCTIONS.md](../AGENT_INSTRUCTIONS.md) - Detailed dev procedures
- [TESTING.md](TESTING.md) - Testing infrastructure
- [LINTING.md](LINTING.md) - Linter configuration

**For Advanced Topics:**
- [ARCHITECTURE.md](ARCHITECTURE.md) - System architecture
- [INTERNALS.md](INTERNALS.md) - Internal implementation details
- [EXTENDING.md](EXTENDING.md) - Extension guide

---

Happy coding! 🔗
