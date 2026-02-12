# Workflow: Optimize

Find and fix performance issues in code.

## Usage

> "Optimize src/components/DataTable.tsx"
> "Find performance bottlenecks in the unstaged changes"

## Process

Follow the [optimizing-performance](../skills/optimizing-performance.md) skill:

1. If no target specified, run `git diff` and focus on unstaged changes
2. Measure baseline performance
3. Identify root causes (algorithm, I/O, payload)
4. Evaluate cost vs benefit for each optimization
5. Implement and verify improvements

## Output

- Specific file:line references for each issue
- Explanation of the performance impact
- Code examples showing the optimization
- Cost-benefit analysis for each proposed change
