# Performance Guidelines

## Model Selection

| Model | Use Case |
|-------|----------|
| **Haiku** | Quick searches, simple tasks, worker agents |
| **Sonnet** | Main development, orchestration |
| **Opus** | Complex architecture, deep research, analysis |

## Context Window Management

Reserve context for:
- Large-scale refactoring
- Multi-file feature implementation
- Complex debugging

Lower context sensitivity:
- Single-file edits
- Simple bug fixes
- Documentation updates

## Agent Efficiency

- Use Explore agent for codebase search
- Parallelize independent agent tasks
- Delegate complex subtasks to appropriate agents

## Code Performance

General principles (language-agnostic):
- Avoid premature optimization
- Profile before optimizing
- Optimize hot paths, not everything
- Consider algorithmic complexity

## Build Performance

- Use incremental builds when available
- Cache dependencies
- Parallelize where possible
- Clean build artifacts periodically

## Supports Principle 4

Small changes enable:
- Faster feedback loops
- Easier performance profiling
- Incremental optimization
