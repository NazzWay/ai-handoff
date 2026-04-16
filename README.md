# ai-handoff

Structured handoff documents for AI coding agents. Type `/handoff` and your AI generates a complete session summary — what was done, what failed, what's next — formatted for the next agent to pick up seamlessly.

## What it does

When you run `/handoff`, the AI reviews its own conversation context and generates a markdown doc with:

- **Completed** — what got done, with file paths and status
- **Incomplete / Failed** — blockers and exact errors
- **Next Steps** — prioritized actions for the next session
- **How It Works** — architecture context for continuity
- **Do Not Touch** — guardrails to prevent regressions
- **Attempted & Failed** — avoid repeating dead ends
- **Key Files** — quick reference to relevant paths

Output: `handoff_docs/handoff_YYYY-MM-DD_[short-task-name].md`

## Install

### Claude Code (plugin)

```bash
claude plugin add nazmoney/ai-handoff
```

Then use `/handoff` in any session.

### Manual (any AI tool)

Copy the skill file into your project:

```bash
mkdir -p .claude/skills
cp skills/handoff/SKILL.md .claude/skills/handoff.md
```

Add to your `CLAUDE.md` (or equivalent instructions file):

```markdown
## Handoff
- **handoff** (`.claude/skills/handoff.md`) - generate session handoff document. Trigger: `/handoff`
When the user says `/handoff`, read and follow `.claude/skills/handoff.md`.
```

### OpenCode

1. Copy the skill file as above
2. Make sure `CLAUDE.md` is in your `instructions` array in `~/.config/opencode/opencode.json`:

```json
{
  "instructions": ["CLAUDE.md"]
}
```

### Other AI tools (Cursor, Windsurf, Cline, etc.)

Copy `skills/handoff/SKILL.md` into your project's instruction/rules directory and reference it from your tool's config. The skill is plain markdown — any AI tool that reads instruction files can use it.

## Usage

```
/handoff
```

Or natural language:
- "make a handoff"
- "write a handoff doc"
- "generate handoff"

The AI analyzes the current conversation and writes a structured doc to `handoff_docs/`.

## Template

The handoff doc follows a fixed structure optimized for AI-to-AI continuity:

```
# HANDOFF DOC: [Project/Feature]
Date | Agent/Dev | Current Scope/Goal

## COMPLETED
## INCOMPLETE / FAILED
## NEXT STEPS & FUTURE PIPELINE
## HOW IT WORKS (Critical Context)
## DO NOT TOUCH
## ATTEMPTED & FAILED (Avoid Repeating)
## SUGGESTED FIXES / METHODS
## KEY FILES & REFERENCES
```

See [`skills/handoff/SKILL.md`](skills/handoff/SKILL.md) for the full template.

## Why

AI coding sessions are stateless. When context resets — new session, different model, token limit hit — all the nuance of what was tried, what failed, and why is lost. Handoff docs solve this by giving the next agent a structured briefing.

## License

MIT
