# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

Production-ready Claude Code configurations (agents, skills, hooks, commands, rules, contexts, MCP configs) from an Anthropic hackathon winner. Battle-tested over 10+ months of daily use.

## Architecture

This is a **configuration repository**, not a code project. It contains markdown files, JSON configs, and shell scripts that users copy to `~/.claude/` to customize Claude Code behavior.

### Component Types

| Directory | Purpose | Format |
|-----------|---------|--------|
| `agents/` | Subagents for delegated tasks | Markdown with YAML frontmatter |
| `skills/` | Workflow definitions, domain knowledge | Markdown or directory with SKILL.md |
| `commands/` | Slash commands (`/tdd`, `/plan`) | Markdown with description frontmatter |
| `rules/` | Always-follow guidelines | Markdown, one domain per file |
| `hooks/` | Tool event automations | JSON config + shell scripts |
| `contexts/` | Dynamic system prompt injection | Markdown |
| `mcp-configs/` | MCP server configurations | JSON |
| `examples/` | Sample CLAUDE.md configs and session logs | Markdown/JSON |

### File Formats

**Agents** require frontmatter:
```markdown
---
name: agent-name
description: What it does
tools: Read, Grep, Glob, Bash
model: opus|sonnet|haiku
---
```

**Commands** require description:
```markdown
---
description: Brief description
---
```

**Hooks** in `hooks/hooks.json`:
```json
{
  "matcher": "tool == \"Edit\" && tool_input.file_path matches \"...\""",
  "hooks": [{"type": "command", "command": "..."}],
  "description": "What this hook does"
}
```

## Context Window Management

**Critical:** Don't enable all MCPs at once. Your 200k context window can shrink to 70k with too many tools enabled.

- Keep under 10 MCPs enabled per project, under 80 tools active
- Use `disabledMcpServers` in project config to disable unused ones

## Key Design Principles

1. **Agent-first** - Delegate complex tasks to specialized subagents
2. **Parallel execution** - Launch independent agents simultaneously
3. **Plan before execute** - Use planner agent for complex features
4. **Modular rules** - One domain per rule file, not monolithic configs

## Model Selection for Agents

- **opus** - Complex reasoning: planning, architecture, security review
- **sonnet** - General tasks: code review, documentation, refactoring
- **haiku** - Quick tasks: formatting, simple lookups, build error resolution

## Conventions

- Filenames: lowercase with hyphens (`code-reviewer.md`, `tdd-workflow.md`)
- No emojis in any files
- Agent/skill name should match filename
- API keys use `YOUR_*_HERE` placeholders in examples

## Available Commands

| Command | Purpose |
|---------|---------|
| `/tdd` | Test-driven development workflow |
| `/plan` | Create implementation plan |
| `/code-review` | Quality and security review |
| `/build-fix` | Fix build errors |
| `/e2e` | E2E test generation |
| `/refactor-clean` | Dead code removal |
| `/learn` | Extract patterns mid-session |
| `/test-coverage` | Analyze test coverage |
| `/update-docs` | Sync documentation |
| `/update-codemaps` | Update code structure maps |

## Hook Event Types

- `PreToolUse` - Before tool execution (validation, blocking)
- `PostToolUse` - After tool execution (formatting, warnings)
- `PreCompact` - Before context compaction (save state)
- `SessionStart` - New session initialization
- `Stop` - Session end processing

## When Contributing

1. Place files in the correct directory
2. Follow the format for that component type
3. Test with Claude Code before submitting
4. Use conventional commits: `feat:`, `fix:`, `docs:`
