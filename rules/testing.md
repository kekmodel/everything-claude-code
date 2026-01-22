# Testing Guidelines

## Test-Driven Development

Recommended workflow:
1. Write test first (RED)
2. Run test - it should FAIL
3. Write minimal implementation (GREEN)
4. Run test - it should PASS
5. Refactor (IMPROVE)
6. Verify coverage

## Test Types

| Type | Purpose | When |
|------|---------|------|
| Unit | Individual functions | Always |
| Integration | Components together | API, database |
| E2E | User flows | Critical paths |

## Test Quality

Good tests are:
- **Fast**: Run in milliseconds
- **Isolated**: No shared state
- **Repeatable**: Same result every time
- **Self-validating**: Pass or fail, no interpretation
- **Timely**: Written with or before code

## Troubleshooting Test Failures

1. Read the error message fully
2. Check test isolation (shared state?)
3. Verify mocks are correct
4. Fix implementation, not tests (unless tests are wrong)
5. After 3 failures, apply self-correction process (Principle 3)

## Coverage Guidelines

- Aim for meaningful coverage, not 100%
- Cover critical paths thoroughly
- Edge cases and error paths matter
- Don't test framework code

## Test Commands by Language

```bash
# TypeScript/JavaScript
npm test
bun test

# Python
pytest
python -m pytest

# Go
go test ./...

# Rust
cargo test
```

## Supports Principle 2

Tests are evidence:
- All tests passing = implementation works
- Coverage report = extent of testing
- Test output included in completion report
