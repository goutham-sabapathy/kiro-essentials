# Workflow: Optimize

Find and fix performance issues in code.

## Usage

> "Optimize src/components/DataTable.tsx"
> "Find performance bottlenecks in the unstaged changes"

## Process

1. **Determine target:**
   - If a path is provided, use it directly
   - If empty, run `git diff` and focus on unstaged changes

2. **Measure baseline** (REQUIRED — never optimize without data):

   | Metric | How to Measure |
   |--------|----------------|
   | Time | `performance.now()`, profilers |
   | Re-renders | React DevTools Profiler |
   | Memory | DevTools Memory tab |
   | Network | Network tab, bundle analyzer |
   | Database | `EXPLAIN (ANALYZE, BUFFERS)` |

3. **Identify root cause:**

   | Issue | Indicators | Fix |
   |-------|------------|-----|
   | O(n²) complexity | Nested loops, `.includes()` in loop | Use Set/Map |
   | Unnecessary work | Re-computing same result | Cache/memoize |
   | I/O bottleneck | N+1 queries, sequential APIs | Batch, use joins |
   | Large datasets | Rendering 1000+ items | Virtualization |
   | Payload size | >500KB bundles | Tree-shake, lazy load |

4. **Evaluate cost vs benefit:**
   - Reduces complexity AND improves performance → always do it
   - Increases complexity → only if 10x faster OR fixes critical UX
   - Otherwise → don't do it

5. **Implement and re-measure** — verify the improvement with the same benchmark

## Output

- Specific file:line references for each issue
- Explanation of the performance impact
- Code examples showing the optimization
- Cost-benefit analysis for each proposed change

See [optimizing-performance](../skills/optimizing-performance.md) for win-win patterns and anti-patterns.
