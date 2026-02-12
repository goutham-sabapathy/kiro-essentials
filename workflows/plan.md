# Workflow: Plan

Create a detailed implementation plan for a feature or task.

## Usage

> "Plan the implementation of real-time notifications"
> "Create a plan for migrating to PostgreSQL"

## Process

1. **Clarify ambiguity** — Ask questions before guessing. Present options with tradeoffs if there are meaningful choices.

2. **Analyze the codebase** — Read relevant files, understand current architecture, identify where changes need to happen.

3. **Write the plan** and save to `**/plans/YYYY-MM-DD-<feature-name>.md`:

```markdown
# [Feature Name] Implementation Plan

> **Status:** DRAFT

## Specification

**Goal:** [What we're building and why]

**Success Criteria:**
- [ ] Criterion 1
- [ ] Criterion 2

## Tasks

### Task 1: [Complete Feature Unit]
**Context:** `src/auth/`, `tests/auth/`
**Steps:**
1. [ ] Create `src/auth/login.ts` with authentication logic
2. [ ] Add tests in `tests/auth/login.test.ts`
3. [ ] Export from `src/auth/index.ts`
**Verify:** `npm test -- tests/auth/`
```

4. **Task sizing rules:**
   - Each task = everything to complete one logical unit (implementation + tests + types)
   - Group tasks by subsystem (auth tasks together, billing tasks together)
   - End every task with a verification command
   - Use explicit file paths, not vague descriptions

5. **For large plans** (>500 lines), split into phases in a folder:
   ```
   plans/2025-01-15-feature/
   ├── README.md
   ├── phase-1-setup.md
   └── phase-2-feature.md
   ```

See [writing-plans](../skills/writing-plans.md) for the full template and grouping patterns.
