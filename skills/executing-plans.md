# Executing Plans

Execute implementation plans with smart task grouping. Groups related tasks to share context, parallelizes across independent subsystems.

## 1. Setup

**Create a branch** for the work unless trivial.

**Clarify ambiguity upfront:** If the plan has unclear requirements, ask before starting.

## 2. Group Tasks by Subsystem

Group related tasks to share context. One pass per subsystem.

**Why grouping matters:**
```
Without: Task 1 (auth/login) → explore auth/
         Task 2 (auth/logout) → explore auth/ again

With:    Tasks 1-2 (auth/*) → explore once, execute both
```

| Signal | Group together |
|--------|----------------|
| Same directory prefix | `src/auth/*` tasks |
| Same domain/feature | Auth tasks, billing tasks |
| Plan sections | Tasks under same heading |

**Limits:** 3-4 tasks max per group.

**Parallel:** Groups touch different subsystems
**Sequential:** Groups have dependencies

## 3. Execute

Work through task groups in order. For each task:

1. Read the context files listed
2. Implement the steps
3. Run the verification command
4. Commit after each task completes

**Auto-recovery:**
1. Attempt to fix failures (you have context)
2. If can't fix, report failure with error output
3. Same error twice → stop and ask

## 4. Verify

All four checks must pass before marking complete:

1. **Code review:** Review all changes for quality, DX, and correctness
2. **Automated tests:** Run the full test suite. All tests must pass.
3. **Manual verification:** Actually exercise the changes:
   - API changes: curl endpoints with realistic payloads
   - CLI changes: run actual commands, verify output
   - Parser changes: feed real data, not just fixtures
4. **DX quality:** Watch for confusing error messages, noisy output, rough edges

## 5. Commit

After verification passes:

1. Run `git status` to see all changes
2. **Stage files by name, not with `git add -A`** - only stage files from this plan
3. **Leave unrelated changes alone**
4. Write a commit message summarizing what was implemented

## 6. Cleanup

After committing:
- Merge branch to main (if using branches)
- Mark plan file as COMPLETED
- Move to `./plans/done/` if applicable
