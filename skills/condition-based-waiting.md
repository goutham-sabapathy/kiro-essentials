# Condition-Based Waiting

Fixes flaky tests by replacing arbitrary timeouts with condition polling. Use when tests fail intermittently, have setTimeout delays, or involve async operations that need proper wait conditions.

**Core principle:** Wait for the actual condition you care about, not a guess about how long it takes.

## When to Use

```
Test has arbitrary delay (setTimeout/sleep)?
    │
    ├─ Testing actual timing (debounce, throttle)?
    │   └─ Yes → Keep timeout, document WHY
    │
    └─ No → Replace with condition-based waiting
```

## Core Pattern

```typescript
// Bad: Guessing at timing
await new Promise((r) => setTimeout(r, 50));
const result = getResult();
expect(result).toBeDefined();

// Good: Waiting for condition
const result = await waitFor(() => getResult(), 'result to be available');
expect(result).toBeDefined();
```

## Implementation

**Prefer framework built-ins:**
- Testing Library: `findBy` queries, `waitFor`
- Playwright: auto-waiting, `expect(locator).toBeVisible()`
- pytest: `asyncio.wait_for`, tenacity

**Custom polling fallback:**

```typescript
async function waitFor<T>(
  condition: () => T | undefined | null | false,
  description: string,
  timeoutMs = 5000
): Promise<T> {
  const startTime = Date.now();
  while (true) {
    const result = condition();
    if (result) return result;
    if (Date.now() - startTime > timeoutMs) {
      throw new Error(`Timeout waiting for ${description} after ${timeoutMs}ms`);
    }
    await new Promise((r) => setTimeout(r, 50));
  }
}
```

## Python Patterns

```python
import asyncio

async def wait_for_condition(condition, description, timeout=5.0, interval=0.05):
    start = asyncio.get_event_loop().time()
    while True:
        result = condition()
        if result:
            return result
        if asyncio.get_event_loop().time() - start > timeout:
            raise TimeoutError(f"Timeout waiting for {description}")
        await asyncio.sleep(interval)
```

**With tenacity:**
```python
from tenacity import retry, stop_after_delay, wait_fixed

@retry(stop=stop_after_delay(5), wait=wait_fixed(0.05))
def wait_for_ready(service):
    assert service.is_ready()
```

## TypeScript Patterns

**Testing Library (preferred):**
```typescript
// Auto-waits for element
const button = await screen.findByRole('button', { name: /submit/i });

// Wait for assertion
await waitFor(() => expect(screen.getByText('Done')).toBeVisible());
```

**Playwright (auto-waits by default):**
```typescript
await expect(page.getByRole('button')).toBeVisible();
await page.getByRole('button').click(); // auto-waits
```

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Polling too fast | `setTimeout(check, 1)` wastes CPU | Poll every 50ms |
| No timeout | Loop forever if condition never met | Always include timeout |
| Stale data | Caching state before loop | Call getter inside loop |
| No description | "Timeout" with no context | Include what you waited for |

## When Arbitrary Timeout IS Correct

```typescript
// Tool ticks every 100ms - need 2 ticks to verify partial output
await waitForEvent(manager, "TOOL_STARTED");  // First: wait for condition
await new Promise((r) => setTimeout(r, 200)); // Then: wait for timed behavior
// 200ms = 2 ticks at 100ms intervals - documented and justified
```

Requirements: wait for triggering condition first, based on known timing, comment explaining WHY.
