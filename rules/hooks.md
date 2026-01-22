# Hooks System

## Hook Types

- **PreToolUse**: Before tool execution (validation, parameter modification)
- **PostToolUse**: After tool execution (auto-format, checks)
- **Stop**: When session ends (final verification)

## Configuration Location

Hooks are configured in `~/.claude/settings.json`.

## Useful Hook Examples

### PreToolUse

- Long-running command reminder (suggest tmux for npm, cargo, etc.)
- Review before push (open editor for review)
- Block unnecessary file creation

### PostToolUse

- Auto-format after edit (prettier, black, gofmt)
- Type check after editing (tsc, mypy, cargo check)
- Lint warning check

### Stop

- Audit for debug statements (console.log, print, etc.)
- Verify all tests still pass

## Hook Best Practices

1. Keep hooks fast (< 5 seconds)
2. Make hooks language-aware (check file extension)
3. Provide clear feedback on blocked actions
4. Don't duplicate CI checks locally

## Auto-Accept Permissions

Use with caution:
- Enable for trusted, well-defined plans
- Disable for exploratory work
- Configure `allowedTools` in `~/.claude.json` instead

## Supports Principle 2

Hooks can automate evidence collection:
- Auto-run linter after edit
- Auto-run type checker after edit
- Enforce verification before commit
