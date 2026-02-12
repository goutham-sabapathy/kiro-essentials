# Workflow: Refactor

Improve code quality following best practices.

## Usage

> "Refactor src/utils/auth.ts"
> "Refactor the unstaged changes"

## Process

Follow the [refactoring-code](../skills/refactoring-code.md) skill:

1. **Determine target:**
   - If path provided, use it directly
   - If empty, check unstaged changes: `git diff --name-only`
   - If no unstaged changes: `git diff --name-only main...HEAD`

2. **Understand current behavior** - read code, find call sites
3. **Verify test coverage** - behavior-driven tests must exist
4. **Identify issues** - complexity, duplication, naming, types
5. **Plan incremental steps** - high impact + low risk first
6. **Execute with continuous verification** - one change at a time, test after each
