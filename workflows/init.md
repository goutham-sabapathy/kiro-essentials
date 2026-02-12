# Workflow: Init

Bootstrap repository with development configuration.

## Usage

> "Initialize this repo with best practices"
> "Audit my project configuration"

## Process

### Step 1: Detect Stack

| File | Stack | Test Framework |
|------|-------|----------------|
| `pyproject.toml` / `requirements.txt` | Python | pytest |
| `package.json` | Node.js/TypeScript | vitest, jest |
| `Cargo.toml` | Rust | cargo test |
| `go.mod` | Go | go test |
| `pom.xml` / `build.gradle` | Java/Kotlin | JUnit |
| `Gemfile` | Ruby | RSpec |

Also check: `tsconfig.json` (TypeScript), React in dependencies, Next.js/Vite configs.

### Step 2: Read Project Metadata

Extract from manifest: name, description, scripts, dependencies.

### Step 3: Generate Configuration

Create project documentation and rules:

**Project README or context file:**
- Project name and description
- Architecture section (if complex)
- Quick commands from package scripts
- Prerequisites

**Development rules/guidelines:**
- Testing rules referencing [writing-tests](../skills/writing-tests.md)
- Error handling referencing [handling-errors](../skills/handling-errors.md)
- Debugging referencing [systematic-debugging](../skills/systematic-debugging.md)
- Verification referencing [verification-before-completion](../skills/verification-before-completion.md)
- Stack-specific patterns

### Step 4: Confirm and Write

Present the plan to the user, confirm before writing files.

## Audit Mode

For existing configurations:
1. Read existing docs and config
2. Check for missing skill references
3. Identify gaps in testing, error handling, debugging guidance
4. Suggest improvements
5. Apply fixes if confirmed
