# Systematic Debugging

Four-phase debugging framework that finds root causes before proposing fixes. Use when investigating bugs, errors, unexpected behavior, failed tests, or when previous fixes haven't worked.

**Core principle:** Find root cause before attempting fixes. Symptom fixes are failure.

## The Four Phases

Complete each phase before proceeding to the next.

```
Debugging Progress:
- [ ] Phase 1: Root Cause Investigation
- [ ] Phase 2: Pattern Analysis
- [ ] Phase 3: Hypothesis Testing
- [ ] Phase 4: Implementation
```

### Phase 1: Root Cause Investigation

**Before attempting ANY fix:**

1. **Read error messages carefully** - Stack traces often contain the solution
2. **Reproduce consistently** - If not reproducible, gather more data
3. **Check recent changes** - Git diff, new dependencies, config changes
4. **Trace data flow backward** - Find where invalid data originates

**For multi-component systems:** Add diagnostic logging at each component boundary before proposing fixes.

**For log-heavy investigations:** See [reading-logs.md](reading-logs.md) for efficient analysis.

### Phase 2: Pattern Analysis

1. Find working examples of similar code in the codebase
2. Compare working vs broken - list every difference
3. Read reference implementations completely, not just skimming

### Phase 3: Hypothesis Testing

1. Form single hypothesis: "X is the root cause because Y"
2. Make the SMALLEST possible change to test it
3. Verify before continuing - if wrong, form NEW hypothesis

### Phase 4: Implementation

1. **Create failing test case first**
2. **Implement single fix at root cause**
3. **Apply defense-in-depth** - Validate at multiple layers
4. **Verify fix and run tests**

**If 3+ fixes have failed:** Stop fixing symptoms. Question the architecture.

## Red Flags

Stop and return to Phase 1 if you catch yourself:

- Proposing fixes without completing investigation
- "Just try changing X and see if it works"
- Adding multiple changes at once
- "It's probably X, let me fix that" (without evidence)
- Each fix reveals new problems in different places

## Tactical Techniques

### Binary Search / Git Bisect
```bash
git bisect start
git bisect bad HEAD
git bisect good v1.2.0
# Git walks you to the breaking commit
```

### Minimal Reproduction
Strip away everything unrelated until you have the smallest case that reproduces the bug.

### Strategic Logging
Add temporary logging at component boundaries:
```
[Component A] Input: X → Output: Y
[Component B] Input: Y → Output: Z (expected: W)
```

### Differential Analysis
Compare working vs broken environments:
- Same code, different config?
- Same config, different data?
- Same data, different timing?

### Backward Tracing
Start from the error and trace backward through the call chain until you find where correct data becomes incorrect.

## Reporting Format

```markdown
## Root Cause
[1-3 sentences explaining underlying issue]
Located in: `file.ts:123`

## What Was Wrong
[Specific problem - mutation, race condition, missing validation, etc.]

## The Fix
[Changes made and why they address root cause]

## Verification
- [x] Bug reproduced and confirmed fixed
- [x] Existing tests pass
- [x] Added regression test
```
