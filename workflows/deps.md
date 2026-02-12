# Workflow: Deps

Audit and upgrade project dependencies.

## Usage

> "Audit my dependencies"
> "Check for outdated packages"
> "Upgrade dependencies"

## Process

1. **Detect the package manager:**
   - `package.json` → npm/yarn/pnpm
   - `requirements.txt` or `pyproject.toml` → pip/poetry
   - `Cargo.toml` → cargo
   - `go.mod` → go
   - `Gemfile` → bundler

2. **Execute based on action:**

### Audit (default)
- Run security audit (`npm audit`, `pip-audit`, `cargo audit`, etc.)
- Identify vulnerabilities by severity
- Report affected packages and recommended fixes
- Check for deprecated packages

### Outdated
- List packages with available updates
- Show current vs latest versions
- Highlight major version bumps with breaking changes

### Upgrade
- Separate safe updates (patch/minor) from risky ones (major)
- Suggest running tests after upgrades
- Check changelogs for breaking changes

## Output Format

```markdown
## Security Vulnerabilities
[List by severity with affected packages]

## Outdated Packages
| Package | Current | Latest | Update Type |
|---------|---------|--------|-------------|

## Recommendations
[Prioritized list of actions]
```
