# Git Workflow

## Commit Message Format

```
<type>: <description>

<optional body>
```

Types: feat, fix, refactor, docs, test, chore, perf, ci

## Commit Guidelines

- Commit after each verified change (Principle 4)
- Small, atomic commits preferred
- Commit message describes "why", not "what"
- Never commit broken code

## Pull Request Workflow

When creating PRs:
1. Analyze full commit history (not just latest commit)
2. Use `git diff [base-branch]...HEAD` to see all changes
3. Draft comprehensive PR summary
4. Include test plan with TODOs
5. Push with `-u` flag if new branch

## Pre-Commit Checklist

Before any commit (supports Principle 2):
- [ ] Build succeeds
- [ ] Tests pass
- [ ] Lint clean
- [ ] No hardcoded secrets
- [ ] Changes are verified

## Branch Naming

```
feat/description
fix/issue-number-description
refactor/component-name
```

## Merge Strategy

- Prefer squash merges for feature branches
- Preserve history for long-running branches
- Always review the full diff before merge
