# Workflow

=== THIS DEFINES HOW TO ORCHESTRATE AGENTS AND TOOLS ===

## Request Classification (First Step)

Classify every request before acting.

| Type | Signal | Action |
|------|--------|--------|
| **Trivial** | Single file, obvious fix, typo | Execute directly → Verify |
| **Explicit** | Specific file/line given | Execute directly → Verify |
| **Exploratory** | "How does X work?" | Explore → Answer |
| **Research** | "What is best practice for X?" | research → Answer |
| **Design** | New feature, refactoring | EnterPlanMode → Plan approval → Implement |
| **Ambiguous** | Unclear scope or intent | AskUserQuestion |

## Agent Selection

| Situation | Agent | Trigger |
|-----------|-------|---------|
| Need to explore/navigate codebase | **Explore** | Finding files, understanding structure |
| Need deep code analysis (LSP/AST) | **analyze** | References, definitions, call hierarchy |
| Need external documentation | **research** | Unfamiliar API, library, pattern |
| Need structural decisions | **architect** | New feature, multi-component change |
| Need implementation steps | **Plan** | Multi-step implementation |
| Need to validate changes | **verify** | After implementation, before complete |
| Need post-implementation cleanup | **refine** | After feature complete, code feels messy |

### When to Skip Agents (Use Tools Directly)

| Condition | Action |
|-----------|--------|
| Specific file path given | Read directly (skip Explore) |
| Specific class/function name known | Glob/Grep directly (skip Explore) |
| Single definition/reference lookup | LSP directly (skip analyze agent) |
| Simple 2-3 file scope | Read files directly |

## Workflow Sequence

```
[Request]
    │
    ▼
[Classify Request] ─── Trivial/Explicit? ──→ Execute → Verify → Done
    │
    │ Open-ended/Design
    ▼
[Explore] ─── Understand codebase structure
    │
    ▼
[analyze] ─── Deep code analysis (LSP/AST) if needed
    │
    ▼
[research] ─── External docs if needed (optional)
    │
    ▼
[architect] ─── Design if structural (optional)
    │
    ▼
[EnterPlanMode] ─── Get user approval for plan
    │
    ▼
┌─────────────────────────┐
│   Implementation Loop   │
│                         │
│   Small change          │
│       ↓                 │
│   Verify incrementally  │
│       ↓                 │
│   Repeat...             │
└─────────────────────────┘
    │
    ▼
[refine] ─── Cleanup if needed
    │
    ▼
[verify] ─── Final verification
    │
    ▼
[Complete] ─── With evidence
```

## Codebase State Recognition

Use **Explore** agent to assess codebase, then adapt behavior:

| State | Signals | Behavior |
|-------|---------|----------|
| **Disciplined** | Consistent patterns, configs present | Follow existing style strictly |
| **Transitional** | Mixed patterns | Ask: "Which pattern to follow?" |
| **Chaotic** | No consistency | Propose: "I suggest convention X. OK?" |
| **Greenfield** | Empty/new project | Apply modern best practices |

## Verification Checkpoints

| After | Verification |
|-------|--------------|
| Each small change | Build + affected tests |
| Feature complete | Full test suite + lint |
| Before PR | verify agent (full report) |
| Auth/payment/security changes | + Security review |

## Tool Selection

| Task | Tool | NOT |
|------|------|-----|
| Find files by pattern | Glob | `find` in Bash |
| Search file contents | Grep | `grep` in Bash |
| Read specific file | Read | `cat` in Bash |
| Edit existing file | Edit | `sed` in Bash |
| Create new file | Write | `echo >` in Bash |
| Run shell commands | Bash | File operations above |
| Explore codebase structure | Explore agent | Multiple manual searches |
| Deep code analysis | analyze agent (LSP/AST) | Text-only Grep |
| Find references/definitions | analyze agent (LSP) | Manual Grep |
| Search web | WebSearch | - |
| Fetch web page content | WebFetch | - |
| Spawn specialized agent | Task | - |
| Ask user for clarification | AskUserQuestion | - |
| Get plan approval before implementation | EnterPlanMode | - |
| Find definition/references directly | LSP | - |

## Failure Protocol

```
Failure 1 → Investigate → Fix → Retry
Failure 2 → Investigate → Fix → Retry
Failure 3 →
    STOP
    ↓
    REVERT to last working state
    ↓
    DOCUMENT what was attempted
    ↓
    ASK user for guidance
```

REMEMBER: Classify first. Use the right agent for each phase. Verify after every change.
