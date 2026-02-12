# Workflow: Test

Run tests and analyze failures.

## Usage

> "Run my tests and analyze any failures"

## Steps

1. **Detect the test command** (if not specified):
   - `package.json` → `yarn test` or `npm test`
   - `pytest.ini` or `pyproject.toml` → `pytest`
   - `Cargo.toml` → `cargo test`
   - `Makefile` with test target → `make test`
   - `go.mod` → `go test ./...`

2. **Run the tests**

3. **Analyze failures** (if any):
   - Parse failure messages
   - Identify root causes
   - Reference specific file:line locations
   - Suggest fixes

4. **Report results**:
   - Total tests run
   - Passed/failed/skipped counts
   - For failures: clear, actionable feedback

## Related Skills

- [writing-tests](../skills/writing-tests.md)
- [fixing-flaky-tests](../skills/fixing-flaky-tests.md)
- [systematic-debugging](../skills/systematic-debugging.md)
