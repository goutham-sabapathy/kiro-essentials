# Writing Tests

Writes behavior-focused tests using Testing Trophy model with real dependencies. Use when writing tests, choosing test types, or avoiding anti-patterns like testing mocks.

**Core principle:** Test user-observable behavior with real dependencies. Tests should survive refactoring.

> "The more your tests resemble the way your software is used, the more confidence they can give you." — Kent C. Dodds

## Testing Trophy Model

| Priority | Type | When |
|----------|------|------|
| 1st | Integration | Default - multiple units with real dependencies |
| 2nd | E2E | Complete user workflows |
| 3rd | Unit | Pure functions only (no dependencies) |

## Mocking Guidelines

**Default: Don't mock. Use real dependencies.**

**Only mock:**
- External HTTP/API calls
- Time/randomness
- Third-party services (payments, email)

**Never mock:**
- Internal modules
- Database queries (use test DB)
- Business logic
- Your own code calling your own code

## Test Type Decision

```
Complete user workflow? → E2E test
Pure function (no side effects)? → Unit test
Everything else → Integration test
```

## Assertion Strategy

| Context | Assert On | Avoid |
|---------|-----------|-------|
| UI | Visible text, roles | CSS classes, internal state |
| API | Response body, status | Internal DB state |
| Library | Return values | Private methods |

## Anti-Patterns

| Pattern | Fix |
|---------|-----|
| Testing mock calls | Test actual outcome |
| Test-only methods in production | Move to test utilities |
| `sleep(500)` | Use condition-based waiting |
| Asserting on internal state | Assert on observable output |
| Incomplete mocks | Mirror real API completely |

## Quality Checklist

- [ ] Happy path covered
- [ ] Error conditions handled
- [ ] Real dependencies used (minimal mocking)
- [ ] Tests survive refactoring
- [ ] Test names describe behavior

---

## TypeScript/React Patterns

Use Testing Library idioms:

```typescript
import { render, screen } from '@testing-library/react'
import { http, HttpResponse } from 'msw'

// ✅ Behavior-driven
test('displays error when API returns 404', async () => {
  server.use(http.get('/api/users', () => new HttpResponse(null, { status: 404 })));
  render(<UserList />);
  expect(await screen.findByText(/not found/i)).toBeInTheDocument();
});

// ❌ Implementation-detail
test('sets error state', () => {
  wrapper.instance().handleError(new Error('404'));
  expect(wrapper.state('error')).toBe('404');
});
```

**HTTP mocking with MSW:**
```typescript
import { http, HttpResponse } from 'msw'
export const handlers = [
  http.get('/api/user', () => HttpResponse.json({ name: 'Test User' }))
]
```

**Async waiting:**
```typescript
await waitFor(() => expect(element).toBeVisible())
// NOT: await sleep(500)
```

## Python Patterns

```python
import respx
from httpx import Response

@respx.mock
@pytest.mark.asyncio
async def test_api_call():
    respx.get("https://api.example.com/data").mock(
        return_value=Response(200, json={"key": "value"})
    )
```

**Use `respx` for HTTP mocking** - integrates with httpx and handles async properly. `requests-mock` doesn't work with async code.

## Go Patterns

```go
func TestUserService_Create(t *testing.T) {
    db := setupTestDB(t)
    svc := NewUserService(db)

    user, err := svc.Create(context.Background(), "test@example.com")
    require.NoError(t, err)
    assert.Equal(t, "test@example.com", user.Email)

    // Verify via real DB query
    found, err := svc.GetByEmail(context.Background(), "test@example.com")
    require.NoError(t, err)
    assert.Equal(t, user.ID, found.ID)
}
```

**Use real test databases.** Table-driven tests for pure functions. `httptest.NewServer` for HTTP testing.

---

**Remember:** Behavior over implementation. Real over mocked. Outputs over internals.

For flaky tests with timing issues, see [condition-based-waiting.md](condition-based-waiting.md).
