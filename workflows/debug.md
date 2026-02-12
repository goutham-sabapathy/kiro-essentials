# Workflow: Debug

Start systematic debugging session for a bug.

## Usage

> "Debug this error: TypeError: Cannot read property 'id' of undefined"
> "Debug why the login flow is failing"

## Process

1. **Understand the bug** — Get the error message, reproduction steps, and when it started
2. **Reproduce consistently** — If not reproducible, gather more data before proceeding
3. **Check recent changes** — `git log --oneline -10`, `git diff`, new dependencies
4. **Read error messages carefully** — Stack traces often contain the solution
5. **Trace data flow backward** — Find where invalid data originates
6. **Form a hypothesis** — "X is the root cause because Y"
7. **Make the smallest possible change** to test it — if wrong, form a new hypothesis
8. **If logs are involved**, filter first then read:
   ```bash
   grep -Ei "error|warn" app.log | head -20
   grep -C 5 "the-error-text" app.log
   ```
9. **Implement fix at root cause** — create a failing test first, then fix
10. **Verify** — run tests, confirm the bug is gone, check for regressions

**If 3+ fixes have failed:** Stop fixing symptoms. Question the architecture.

**Red flags** — stop and re-investigate if you catch yourself:
- "Just try changing X and see if it works"
- Adding multiple changes at once
- Each fix reveals new problems in different places

See [systematic-debugging](../skills/systematic-debugging.md) for the full four-phase framework and [reading-logs](../skills/reading-logs.md) for log analysis techniques.
