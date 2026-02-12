# Workflow: Execute

Execute an implementation plan from the plans folder.

## Usage

> "Execute the plan in plans/2025-01-15-auth.md"
> "Execute the latest plan"

## Process

Follow the [executing-plans](../skills/executing-plans.md) skill:

1. **Find plans** (if no path given):
   ```bash
   find . -path "*/plans/*.md" -o -name "*-plan.md" -o -name "*-PLAN.md"
   ```
   Filter to incomplete plans (status: DRAFT, APPROVED, IN_PROGRESS).

2. **Review the plan** - show spec, success criteria, task breakdown

3. **Decide on branching:**
   - Large tasks (5+ tasks, 3+ subsystems) → create feature branch
   - Small tasks → work directly

4. **Execute tasks** in order:
   - Read context files
   - Implement steps
   - Run verification command
   - Commit after each task

5. **Verify** - code review, test suite, manual verification, DX quality

6. **Cleanup** - merge branch, mark plan COMPLETED, move to `plans/done/`
