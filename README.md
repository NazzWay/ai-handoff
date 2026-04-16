# 📄 AI-Handoff

> Type `/handoff` — your AI generates a complete session summary for the next agent to pick up seamlessly.

What was done. What failed. What's next. One command.

---

## 🤖 Supported Tools

<table>
<tr>
<td align="center"><img src="https://cdn.simpleicons.org/anthropic/181818" width="28" alt="Claude"><br><b>Claude Code</b></td>
<td align="center"><img src="https://cdn.simpleicons.org/openai/181818" width="28" alt="OpenAI"><br><b>Codex</b></td>
<td align="center"><img src="assets/logos/gemini.png" width="28" alt="Gemini"><br><b>Gemini CLI</b></td>
<td align="center"><img src="https://cdn.simpleicons.org/cursor/181818" width="28" alt="Cursor"><br><b>Cursor</b></td>
<td align="center"><img src="assets/logos/windsurf.png" width="28" alt="Windsurf"><br><b>Windsurf</b></td>
<td align="center"><img src="https://cdn.simpleicons.org/cline/181818" width="28" alt="Cline"><br><b>Cline</b></td>
</tr>
<tr>
<td align="center"><img src="assets/logos/amazon-q.png" width="28" alt="Amazon Q"><br><b>Amazon Q</b></td>
<td align="center"><img src="assets/logos/mistral.png" width="28" alt="Mistral"><br><b>Vibe</b></td>
<td align="center"><img src="https://cdn.simpleicons.org/openaigym/181818" width="28" alt="OpenCode"><br><b>OpenCode</b></td>
<td align="center">📝<br><b>Any AI CLI</b></td>
</tr>
</table>

Works with any AI tool that reads markdown instructions.

---

## ✨ What it does

When you run `/handoff`, the AI reviews its own conversation and generates a structured doc:

| Section | What it captures |
|---------|-----------------|
| ✅ **Completed** | What got done, file paths, status |
| ❌ **Incomplete** | Blockers and exact errors |
| 🔄 **Current State** | What's working vs what's broken |
| 🚫 **Failed Approaches** | Dead ends — so the next agent doesn't repeat them |
| ⚖️ **Key Decisions** | Choices made and why |
| ▶️ **Resume Instructions** | Step-by-step to continue |
| 🏗️ **How It Works** | Architecture context |
| ⚙️ **Setup Required** | Env vars, deps, test data |
| 💻 **Code Context** | Key signatures and API shapes |
| ⚠️ **Warnings** | What not to touch and why |
| 📁 **Key Files** | Quick reference to relevant paths |

**Output:** `handoff_docs/handoff_YYYY-MM-DD_[short-task-name].md`

---

## 📦 Install

### <img src="https://cdn.simpleicons.org/anthropic/181818" width="16"> Claude Code (plugin)

```bash
claude plugin marketplace add NazzWay/ai-handoff
claude plugin install ai-handoff@NazzWay-ai-handoff
```

Then restart Claude Code and use `/handoff` in any session.

### <img src="https://cdn.simpleicons.org/openaigym/181818" width="16"> OpenCode

Copy the repo into your project, then add to `~/.config/opencode/opencode.json`:

```json
{
  "instructions": ["CLAUDE.md"]
}
```

### <img src="assets/logos/gemini.png" width="16"> Gemini CLI

```bash
cp GEMINI.md /path/to/your/project/
cp -r skills/ /path/to/your/project/skills/
```

Gemini CLI auto-reads `GEMINI.md`.

### <img src="https://cdn.simpleicons.org/openai/181818" width="16"> Codex

```bash
cp AGENTS.md /path/to/your/project/
cp -r skills/ /path/to/your/project/skills/
```

Codex auto-reads `AGENTS.md`.

### <img src="https://cdn.simpleicons.org/cursor/181818" width="16"> Cursor

```bash
cp -r .cursor/ /path/to/your/project/.cursor/
cp -r skills/ /path/to/your/project/skills/
```

Activates when you mention "handoff".

### <img src="assets/logos/windsurf.png" width="16"> Windsurf

```bash
cp -r .windsurf/ /path/to/your/project/.windsurf/
cp -r skills/ /path/to/your/project/skills/
```

### <img src="https://cdn.simpleicons.org/cline/181818" width="16"> Cline

```bash
cp -r .clinerules/ /path/to/your/project/.clinerules/
cp -r skills/ /path/to/your/project/skills/
```

### <img src="assets/logos/amazon-q.png" width="16"> Amazon Q

```
/load skills/handoff/SKILL.md
```

### <img src="assets/logos/mistral.png" width="16"> Mistral Vibe

```bash
cp skills/handoff/SKILL.md ~/.vibe/prompts/handoff.md
```

### 📝 Any other AI tool

Copy `skills/handoff/SKILL.md` into your tool's instructions directory. If it reads markdown, it runs handoff.

---

## 🚀 Usage

```
/handoff
```

Or just say:
- *"make a handoff"*
- *"write a handoff doc"*
- *"generate handoff"*

---

## 📐 Template

```
# HANDOFF: [Task Title]
Date | Agent | Branch | Status
Goal

## COMPLETED
## INCOMPLETE
## CURRENT STATE
## FAILED APPROACHES (Don't Repeat)
## KEY DECISIONS
## RESUME INSTRUCTIONS
## HOW IT WORKS
## SETUP REQUIRED
## CODE CONTEXT
## WARNINGS
## KEY FILES
```

See [`skills/handoff/SKILL.md`](skills/handoff/SKILL.md) for the full template with placeholders.

---

## 🗂️ Repo Structure

```
ai-handoff/
├── .claude-plugin/plugin.json       ← Claude Code plugin
├── .cursor/rules/handoff.mdc        ← Cursor rule
├── .windsurf/rules/handoff.md       ← Windsurf rule
├── .clinerules/handoff.md           ← Cline rule
├── AGENTS.md                        ← Codex
├── CLAUDE.md                        ← Claude Code / OpenCode
├── GEMINI.md                        ← Gemini CLI
├── LICENSE                          ← MIT
├── README.md
└── skills/
    └── handoff/
        └── SKILL.md                 ← Core skill (one file, every tool)
```

---

## 💡 Why

AI sessions are stateless. Context resets — new session, different model, token limit — and everything learned is lost. Handoff docs give the next agent a structured briefing so work continues, not restarts.

---

## 📄 License

MIT
