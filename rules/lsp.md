# LSP Integration

## Setup

Enable LSP for enhanced code intelligence:

```bash
# Add to ~/.bashrc or ~/.zshrc
export ENABLE_LSP_TOOL=1

# Or run once
ENABLE_LSP_TOOL=1 claude
```

## Supported Languages

Python, TypeScript, Go, Rust, Java, C/C++, C#, PHP, Kotlin, Ruby, HTML/CSS

## LSP Tools

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `lsp_diagnostics` | Get errors/warnings | After every edit |
| `go_to_definition` | Jump to definition | Understanding code |
| `find_references` | Find all usages | Before modifying/deleting |
| `hover` | Get type info | Understanding types |
| `rename` | Safe symbol rename | Refactoring |

## Performance

```
find_references with LSP:  ~50ms
find_references with grep: ~45 seconds

→ 900x faster
```

## Workflow Integration

### After Every Edit

```
Edit file
    ↓
lsp_diagnostics(file)
    ↓
Errors? → Fix → lsp_diagnostics again
    ↓
No errors → Continue
```

### Before Deleting Code

```
find_references(symbol)
    ↓
References found? → Don't delete, or update references first
    ↓
No references → Safe to delete
```

### When Refactoring

```
Understand: go_to_definition, hover
    ↓
Check impact: find_references
    ↓
Rename safely: rename (LSP)
    ↓
Verify: lsp_diagnostics
```

## LSP vs Text Search

| Task | LSP (Preferred) | Text Search (Fallback) |
|------|-----------------|------------------------|
| Find definition | go_to_definition | Grep + manual |
| Find usages | find_references | Grep (misses dynamic) |
| Check errors | lsp_diagnostics | Run linter manually |
| Rename | rename | Find/replace (risky) |
| Type info | hover | Read code manually |

## When LSP is Unavailable

If LSP is not enabled or doesn't support the language:

```bash
# Type check (language-specific)
npx tsc --noEmit          # TypeScript
mypy [files]              # Python
go build ./...            # Go
cargo check               # Rust

# Find references (text-based)
rg "functionName" --type ts
grep -r "functionName" --include="*.py"
```

## Checklist

Before completing any code task:
- [ ] Used LSP for navigation when available
- [ ] Ran lsp_diagnostics (or linter) after edits
- [ ] Checked find_references before deletions
- [ ] Fixed all reported errors
- [ ] No type errors remaining

## Supports Principle 2

LSP provides concrete evidence of code correctness (diagnostics, type checks).

**No evidence = Not complete**
