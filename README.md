# AI-Handoff

Structured handoff documents for AI coding agents. Type `/handoff` and your AI generates a complete session summary — what was done, what failed, what's next — formatted for the next agent to pick up seamlessly.

Works with: **Claude Code** | **OpenCode** | **Gemini CLI** | **Codex** | **Cursor** | **Windsurf** | **Cline** | **Aider** | **Amp** | **Amazon Q** | **Mistral Vibe** | and any AI tool that reads markdown instructions.

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

### Claude Code (plugin — recommended)

```bash
claude plugin add NazzWay/ai-handoff
```

Then use `/handoff` in any session.

### OpenCode

Clone or copy the repo into your project, then add `CLAUDE.md` to your instructions array in `~/.config/opencode/opencode.json`:

```json
{
  "instructions": ["CLAUDE.md"]
}
```

### Gemini CLI

Copy `GEMINI.md` and the `skills/` directory into your project root. Gemini CLI auto-reads `GEMINI.md`.

```bash
cp GEMINI.md /path/to/your/project/
cp -r skills/ /path/to/your/project/skills/
```

### OpenAI Codex

Copy `AGENTS.md` and the `skills/` directory into your project root. Codex auto-reads `AGENTS.md`.

```bash
cp AGENTS.md /path/to/your/project/
cp -r skills/ /path/to/your/project/skills/
```

### Cursor

Copy the `.cursor/` directory and `skills/` into your project root:

```bash
cp -r .cursor/ /path/to/your/project/.cursor/
cp -r skills/ /path/to/your/project/skills/
```

The `.cursor/rules/handoff.mdc` rule activates when you mention "handoff".

### Windsurf

Copy the `.windsurf/` directory and `skills/` into your project root:

```bash
cp -r .windsurf/ /path/to/your/project/.windsurf/
cp -r skills/ /path/to/your/project/skills/
```

### Cline

Copy the `.clinerules/` directory and `skills/` into your project root:

```bash
cp -r .clinerules/ /path/to/your/project/.clinerules/
cp -r skills/ /path/to/your/project/skills/
```

### Aider

Load the skill file as read-only context:

```bash
aider --read skills/handoff/SKILL.md
```

Or add to `.aider.conf.yml`:

```yaml
read:
  - skills/handoff/SKILL.md
```

### Amp (Sourcegraph)

Copy `AGENT.md` and the `skills/` directory into your project root. Amp auto-reads `AGENT.md`.

```bash
cp AGENT.md /path/to/your/project/
cp -r skills/ /path/to/your/project/skills/
```

### Amazon Q CLI

Load the skill manually per session:

```
/load skills/handoff/SKILL.md
```

### Mistral Vibe

Copy the skill to your Vibe prompts directory:

```bash
cp skills/handoff/SKILL.md ~/.vibe/prompts/handoff.md
```

### Any other AI tool

The skill is plain markdown. Copy `skills/handoff/SKILL.md` into whatever instructions/rules directory your tool reads. If it can read a markdown file, it can run handoff.

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

## Repo structure

```
ai-handoff/
├── .claude-plugin/plugin.json    ← Claude Code plugin manifest
├── .cursor/rules/handoff.mdc     ← Cursor rule (activates on "handoff")
├── .windsurf/rules/handoff.md    ← Windsurf rule (manual trigger)
├── .clinerules/handoff.md        ← Cline rule
├── AGENT.md                      ← Amp (Sourcegraph) instructions
├── AGENTS.md                     ← Codex instructions
├── CLAUDE.md                     ← Claude Code / OpenCode instructions
├── GEMINI.md                     ← Gemini CLI instructions
├── LICENSE                       ← MIT
├── README.md
└── skills/
    └── handoff/
        └── SKILL.md              ← Core skill (the actual template + logic)
```

## Why

AI coding sessions are stateless. When context resets — new session, different model, token limit hit — all the nuance of what was tried, what failed, and why is lost. Handoff docs solve this by giving the next agent a structured briefing.

## License

MIT
