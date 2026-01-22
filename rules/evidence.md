# Evidence-Based Completion

## Principle

**No evidence = Not complete**

Self-reported completion is worthless. Only verified results matter.

## Evidence Requirements

| Action | Required Evidence | How to Get |
|--------|-------------------|------------|
| Code change | No new errors | Run linter, type checker |
| Build | Success | Run build command, check exit code |
| Test | All pass | Run test suite, show results |
| Bug fix | Test proves fix | Write/run regression test |
| Feature | All above + works | Demonstrate functionality |

## What Counts as Evidence

### Valid Evidence

```markdown
Build: SUCCESS (exit code 0)
Tests: 47/47 passing
Lint: No errors
Type check: Clean
```

```markdown
$ npm run build
> project@1.0.0 build
> tsc && vite build
Done in 3.2s
```

### Invalid Evidence

```markdown
"I've completed the implementation"
"The code should work now"
"I think everything is correct"
```

## Verification Commands

### Universal

```bash
# Check what changed
git diff --name-only
git status
```

### By Language

**TypeScript/JavaScript:**
```bash
npm run build          # or: bun run build
npm test               # or: bun test
npx tsc --noEmit       # Type check only
npx eslint .           # Lint
```

**Python:**
```bash
python -m py_compile [file]   # Syntax check
pytest                        # Tests
mypy [files]                  # Type check
ruff check .                  # Lint
```

**Go:**
```bash
go build ./...         # Build
go test ./...          # Tests
golangci-lint run      # Lint
```

**Rust:**
```bash
cargo build            # Build
cargo test             # Tests
cargo clippy           # Lint
```

### With LSP (if enabled)

```
lsp_diagnostics [file]   # Real-time errors
```

## Completion Report Format

When marking work complete, provide:

```markdown
## Completion Report

### Changes Made
- [File 1]: [What changed]
- [File 2]: [What changed]

### Verification Results
- Build: SUCCESS
- Tests: X/Y passing
- Lint: No errors
- Type check: Clean

### Evidence
[Paste relevant command output]
```

## Partial Completion

If verification fails, report honestly:

```markdown
## Status: INCOMPLETE

### What works
- Build succeeds
- 45/47 tests pass

### What doesn't work
- 2 tests failing in auth module
- Error: [specific error]

### Next steps needed
- Fix authentication token refresh logic
- Update related tests

Would you like me to continue, or do you have guidance?
```

## Common Mistakes

### Mistake 1: Skipping Verification

```
Bad:  "I've added the function" (no build/test run)
Good: "Function added. Build passes, tests pass (12/12)."
```

### Mistake 2: Ignoring Warnings

```
Bad:  "Build succeeds" (with 15 warnings)
Good: "Build succeeds with 15 warnings. Should I address them?"
```

### Mistake 3: Selective Testing

```
Bad:  Run only the test you think is relevant
Good: Run the full test suite to catch regressions
```

### Mistake 4: Assuming Success

```
Bad:  "The fix should work" (no verification)
Good: "Fix applied and verified with [specific test]"
```

## Integration with Verify Agent

For thorough verification, delegate to Verify agent:

```
TASK: Verify implementation of [feature]
CONTEXT: Changed files: [list]
EXPECTED:
  - All tests pass
  - Build succeeds
  - No security issues
  - Evidence collected
```

Verify agent will:
1. Run all verification commands
2. Check code quality
3. Review security
4. Collect and report evidence
