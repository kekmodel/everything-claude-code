# Everything Claude Code

Principles-first workflow system for Claude Code.

## Installation

### For Humans

Copy and paste this to Claude Code:

```
Install everything-claude-code by following:
https://raw.githubusercontent.com/kekmodel/everything-claude-code/master/README.md
```

### For LLM Agents

```bash
git clone https://github.com/kekmodel/everything-claude-code.git /tmp/ecc
mkdir -p ~/.claude/agents ~/.claude/rules
cp /tmp/ecc/agents/*.md ~/.claude/agents/
cp /tmp/ecc/rules/*.md ~/.claude/rules/
rm -rf /tmp/ecc
```

## What's Included

**Rules**
- `principles.md` - 7 core principles
- `workflow.md` - Agent/tool orchestration

**Agents**
- `research.md` - External docs lookup
- `architect.md` - System design
- `verify.md` - Validation
- `refine.md` - Cleanup

## License

MIT
