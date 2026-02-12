# Verification Before Completion

Run verification commands before claiming work is complete or fixed. Use before asserting any task is done, bug is fixed, tests pass, or feature works.

**Core Principle:** No completion claims without fresh verification evidence.

## The Verification Gate

BEFORE any claim of success, completion, or satisfaction:

```
Verification Checklist:
- [ ] IDENTIFY: What command proves this claim?
- [ ] RUN: Execute the verification command (fresh, complete)
- [ ] READ: Check full output, exit code, failure counts
- [ ] VERIFY: Does output confirm the claim?
  - If NO → State actual status with evidence
  - If YES → State claim WITH evidence
```

Skip any step = invalid claim.

## When This Applies

ALWAYS before:

- Claiming "tests pass", "build succeeds", "linter clean", "bug fixed"
- Expressing satisfaction ("Great!", "Done!", "Perfect!")
- Using qualifiers ("should work", "probably fixed", "seems to")
- Committing, creating PRs, marking tasks complete
- Moving to next task
- ANY statement implying success or completion

## Common Verification Requirements

| Claim | Required Evidence | Not Sufficient |
|-------|-------------------|----------------|
| Tests pass | `yarn test` output: 0 failures | Previous run, "looks correct" |
| Build succeeds | Build command: exit 0 | Linter clean, "should work" |
| Bug fixed | Test reproducing bug: now passes | Code changed, assumed fix |
| Linter clean | Linter output: 0 errors | Partial check, spot test |
| Regression test works | Red→Green cycle verified | Test passes once |

## Red Flags

Stop and verify if you're about to:

- Use hedging language ("should", "probably", "seems to")
- Express satisfaction before running verification
- Rely on partial checks or previous runs
- Think "just this once" or "I'm confident it works"

## Key Examples

**Regression test (TDD Red-Green):**
```
✅ Write test → Run (fail) → Fix code → Run (pass) → Revert fix → Run (MUST fail) → Restore → Run (pass)
❌ "I've written a regression test" (without verifying red-green cycle)
```

**Build vs Linter:**
```
✅ Run `npm run build` → See "exit 0" → Claim "build passes"
❌ Run linter → Claim "build will pass" (linter ≠ compiler)
```

## No Exceptions

Run the command. Read the output. THEN claim the result.

Evidence before assertions, always.
