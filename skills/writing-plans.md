# Writing Plans

Create implementation plans with tasks grouped by subsystem. Use when planning features, refactors, or multi-step work.

**Save to:** `**/plans/YYYY-MM-DD-<feature-name>.md`

## Plan Template

````markdown
# [Feature Name] Implementation Plan

> **Status:** DRAFT | APPROVED | IN_PROGRESS | COMPLETED

## Specification

**Goal:** [What we're building and why]

**Success Criteria:**
- [ ] Criterion 1
- [ ] Criterion 2

## Context Loading

_Run before starting:_
```bash
read src/relevant/file.ts
glob src/feature/**/*.ts
```

## Tasks

### Task 1: [Complete Feature Unit]

**Context:** `src/auth/`, `tests/auth/`

**Steps:**
1. [ ] Create `src/auth/login.ts` with authentication logic
2. [ ] Add tests in `tests/auth/login.test.ts`
3. [ ] Export from `src/auth/index.ts`

**Verify:** `npm test -- tests/auth/`

---

### Task 2: [Another Complete Unit]

**Context:** `src/billing/`

**Steps:**
1. [ ] ...

**Verify:** `npm test -- tests/billing/`
````

## Task Sizing

A task includes **everything** to complete one logical unit:
- Implementation + tests + types + exports
- All steps a single pass should do together

**Right-sized:** "Add user authentication" - model, service, tests, types
**Wrong:** Separate tasks for model, service, tests - these should be one task

**Bundle trivial items:** Group small related changes into one task.

## Parallelization & Grouping

Structure your plan to make grouping clear:

```markdown
## Authentication Tasks ← These run together

### Task 1: Add login
### Task 2: Add logout

## Billing Tasks ← These run in parallel with auth

### Task 3: Add billing API
### Task 4: Add webhooks

## Integration Tasks ← Sequential (depends on above)

### Task 5: Wire auth + billing
```

## Rules

1. **Explicit paths:** Say "create `src/utils/helpers.ts`" not "create a utility"
2. **Context per task:** List files to read first
3. **Verify every task:** End with a command that proves it works
4. **Clarify ambiguity upfront:** Ask before guessing

## Large Plans

For plans over ~500 lines, split into phases:

```
**/plans/YYYY-MM-DD-feature/
├── README.md           # Overview + phase tracking
├── phase-1-setup.md
└── phase-2-feature.md
```
