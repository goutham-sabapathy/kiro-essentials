# Fixing Flaky Tests

Diagnose and fix tests that pass in isolation but fail when run concurrently. Covers shared state isolation and resource conflicts.

**Target symptom:** Tests pass when run alone, fail when run with other tests.

## Diagnose First

```
Test passes alone, fails with others?
    │
    ├─ Same error every time → Shared state
    │   └─ Database, globals, files, singletons
    │
    ├─ Random/timing failures → Race condition
    │   └─ See condition-based-waiting.md
    │
    └─ Resource errors (port, file lock) → Resource conflict
        └─ Need unique resources per test/worker
```

**Quick diagnosis:**
1. Run failing test 10x alone - does it always pass?
2. Run failing test 10x with the suite - same error or different?
3. Check error message - mentions port/file/connection?

## Shared State (Deterministic Failures)

| State Type | Isolation Pattern |
|------------|-------------------|
| **Database** | Transaction rollback, savepoints, worker-specific DBs |
| **Global variables** | Reset in `beforeEach`/`afterEach` |
| **Singletons** | Provide fresh instance per test |
| **Module state** | `jest.resetModules()` or equivalent |
| **Files** | Unique paths per test, temp directories |
| **Environment vars** | Save/restore in setup/teardown |

**Database isolation (most common):**

```python
# Python: Savepoint rollback
@pytest.fixture
async def db_session(db_engine):
    async with db_engine.connect() as conn:
        await conn.begin()
        await conn.begin_nested()  # Savepoint
        # ... yield session ...
        await conn.rollback()  # All changes vanish
```

```typescript
// Jest: Reset mocks between tests
beforeEach(() => {
  jest.clearAllMocks()
  jest.resetModules()
})
afterEach(() => {
  jest.restoreAllMocks()
})
```

## Resource Conflicts (Port/File Errors)

**Worker-specific resources:**

```python
# pytest-xdist: unique DB per worker
@pytest.fixture(scope="session")
def database_url(worker_id):
    if worker_id == "master":
        return "postgresql://localhost/test"
    return f"postgresql://localhost/test_{worker_id}"
```

```typescript
// Dynamic port allocation
const server = app.listen(0)  // OS assigns available port
const port = server.address().port
```

**File conflicts:**
```python
import tempfile

@pytest.fixture
def temp_dir():
    with tempfile.TemporaryDirectory() as d:
        yield d
```

## Playwright E2E Patterns

- Use `test.describe.configure({ mode: 'serial' })` only when tests truly depend on each other
- Use `page.waitForSelector()` instead of arbitrary timeouts
- Isolate test data per test (unique user accounts, unique IDs)
- Use `test.beforeEach` to navigate to clean state

## Verification

After fixing, verify the fix worked:

```bash
# Run the specific test many times
pytest tests/test_flaky.py -x --count=20

# Run with parallelism
pytest -n auto

# Jest equivalent
jest --runInBand  # First verify serial works
jest              # Then verify parallel works
```
