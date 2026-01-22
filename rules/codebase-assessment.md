# Codebase Assessment

## Purpose

Before modifying code, understand the codebase's state. Different states require different approaches.

## When to Assess

- Starting work on unfamiliar codebase
- Open-ended requests ("add feature", "improve")
- Before major changes
- When patterns seem inconsistent

## Assessment Process

### Step 1: Quick Scan

```bash
# Check for config files
ls -la
ls .github/ .vscode/ .idea/

# Check for linter/formatter configs
ls .eslintrc* .prettierrc* pyproject.toml setup.cfg

# Check for documentation
ls README* CONTRIBUTING* docs/
```

### Step 2: Pattern Analysis

```bash
# Sample file structure
find src -type f -name "*.ts" | head -20

# Check naming conventions
ls src/components/ src/utils/ src/services/

# Look at import patterns
head -30 src/**/*.ts | grep "import"
```

### Step 3: Classify State

## Codebase States

### Disciplined

**Signals:**
- Consistent naming (all camelCase or all snake_case)
- Config files present (.eslintrc, .prettierrc, etc.)
- Clear directory structure
- Consistent patterns across files
- Tests exist and follow conventions

**Behavior:**
```
Follow existing patterns STRICTLY
Do not introduce new conventions
Match the existing style exactly
```

**Example response:**
```
"I see you use Repository pattern for data access.
I'll follow that for the new feature."
```

### Transitional

**Signals:**
- Mixed naming conventions
- Some areas well-organized, others not
- Partial test coverage
- Multiple patterns for same problem
- Migration in progress

**Behavior:**
```
ASK before choosing a pattern
"I see both X and Y patterns used. Which should I follow?"
```

**Example response:**
```
"The codebase has both class-based and functional components.
For this new feature, which pattern should I follow?"
```

### Chaotic

**Signals:**
- No consistent conventions
- No linter/formatter config
- No clear structure
- Duplicate code everywhere
- No tests

**Behavior:**
```
PROPOSE a convention before proceeding
"I suggest using X convention. Is that okay?"
Don't just pick one silently
```

**Example response:**
```
"This area doesn't have consistent patterns.
I suggest we establish:
- camelCase for functions
- PascalCase for classes
- Barrel exports for modules
Should I proceed with these conventions?"
```

### Greenfield

**Signals:**
- New project or empty directory
- No existing code to follow
- Setting up from scratch

**Behavior:**
```
Apply modern best practices
Set up proper tooling
Establish conventions from start
```

**Example response:**
```
"Starting fresh, I'll set up:
- TypeScript with strict mode
- ESLint + Prettier
- Standard directory structure
- Test framework
Any preferences before I begin?"
```

## Quick Reference

| State | Signal | Action |
|-------|--------|--------|
| **Disciplined** | Consistent patterns | Follow exactly |
| **Transitional** | Mixed patterns | Ask which to follow |
| **Chaotic** | No patterns | Propose conventions |
| **Greenfield** | Empty/new | Apply best practices |

## Assessment Output

When assessing a codebase, document:

```markdown
## Codebase Assessment

### State: [Disciplined/Transitional/Chaotic/Greenfield]

### Evidence
- Naming: [consistent camelCase / mixed / inconsistent]
- Config: [eslint, prettier present / partial / none]
- Structure: [clear / partially organized / unclear]
- Tests: [comprehensive / partial / none]

### Patterns Observed
- [Pattern 1]: used in [locations]
- [Pattern 2]: used in [locations]

### Recommendation
[How I'll approach this work based on the assessment]
```

## Common Mistakes

### Mistake 1: Assuming Disciplined

```
Bad:  Jump in and start coding
Good: Verify patterns before writing
```

### Mistake 2: Ignoring Mixed Signals

```
Bad:  "I'll use my preferred pattern"
Good: "I see two patterns, let me ask"
```

### Mistake 3: Imposing Style

```
Bad:  "This should be refactored to..."
Good: "Following existing patterns..."
```

## Integration with Principle 7

This assessment supports **Principle 7: Respect Existing Patterns**.

Your code is a guest in the codebase. Assess before you act.
