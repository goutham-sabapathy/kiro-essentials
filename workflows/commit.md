# Workflow: Commit

Create a well-formatted git commit for current changes.

## Usage

> "Commit my changes"
> "Commit with context: added OAuth support"

## Process

1. **Check what changed:**
   ```bash
   git diff --cached --name-only  # staged
   git diff --name-only           # unstaged
   ```

2. **Analyze the changes:**
   ```bash
   git log -n 10 --oneline  # learn project conventions
   git diff --cached         # read the actual changes
   ```

3. **Draft the message** following Conventional Commits (see [writer](../skills/writer.md), Contributor persona):
   - Format: `<type>(<scope>): <subject>`
   - Header: 50 chars max, imperative mood, lowercase, no period
   - Types: `feat`, `fix`, `docs`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`
   - Body: 72 char wrap, focus on WHY not WHAT

4. **Execute:**
   ```bash
   git commit -m "header" -m "body"
   ```

5. **Handle failure:** If pre-commit hooks fail, report the error. Don't auto-fix.

## Examples

```
feat(auth): add password reset flow

Users couldn't recover accounts without contacting support.
This adds email-based reset with 24h expiry tokens.

Closes #234
```

```
fix(api): prevent race condition in session refresh

Concurrent requests could both try to refresh the token,
causing one to fail with 401. Now uses mutex lock.
```

**Important:** No Claude/AI attribution footers.
