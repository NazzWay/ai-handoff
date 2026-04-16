Generate a structured handoff document from the current session's conversation context.

## Trigger

`/handoff` or "make a handoff", "write a handoff", "handoff doc"

## Process

1. **Review your conversation context.** Identify: goal, completed work, failures, current state, decisions made, and what's next.
2. **Determine metadata:**
   - Date: today's date (YYYY-MM-DD)
   - Agent/Dev: your model name (e.g., "Claude Opus 4.6", "GPT-5.4", "Gemini 3.1 Pro")
   - Branch: current git branch (run `git branch --show-current` if available)
   - Status: In Progress / Blocked / Complete
   - Short task name: 3-5 word slug using hyphens (e.g., `arena-model-extraction-fix`)
3. **Populate the template below** with precise, actionable details from the session.
4. **Write the file** to `handoff_docs/handoff_YYYY-MM-DD_[short_task_name].md` in the project root. Create `handoff_docs/` if it doesn't exist.
5. **Confirm** to the user with the file path and a 1-line summary.

## Rules

- Use ONLY the template structure below. Do not add or remove sections.
- **Omit section content** (write "N/A" under the header) if nothing applies — do not fabricate.
- Use **exact file paths** (absolute when possible).
- Include **exact error messages** and line numbers in failure sections.
- Bullet points only. No prose paragraphs.
- Prioritize clarity for an AI agent continuing the work.
- No fluff. Every line must be actionable or informational.
- Mark completed items with `[x]`, incomplete with `[ ]`.
- Code Context section: include only signatures, API shapes, or snippets critical for continuity — not full files.

## Template

```markdown
# HANDOFF: [Task Title]

**Date:** [YYYY-MM-DD] | **Agent:** [ID] | **Branch:** [branch] | **Status:** [In Progress/Blocked/Complete]
**Goal:** [1-2 sentences strictly defining what this session was attempting to achieve]

---

## COMPLETED

- [x] **[Task/Module]** -> `[Path]` | [Stable/Tested/Implemented]

## INCOMPLETE

- [ ] **[Task/Module]** -> `[Path]` | Issue: [Exact error/blocker]

## CURRENT STATE

- **Working:** [What functions correctly right now]
- **Broken:** [What's failing + exact error at file:line]

## FAILED APPROACHES (Don't Repeat)

- **[Approach]** -> Failed: [Error/Reason] -> Use `[Alternative]` instead

## KEY DECISIONS

| Decision | Rationale |
|----------|-----------|
| [Choice made] | [Why — constraint, tradeoff, or evidence] |

## RESUME INSTRUCTIONS

Step-by-step for the next agent to continue:

1. **[Action]** -> `[Path]` | Expected: [Outcome]
2. **[Action]** -> `[Path]` | Expected: [Outcome]

**Future (once unblocked):**

- [ ] **[Task]** -> [Brief description]

Verification: `[command to confirm things work, e.g., npm test, curl localhost:8000/api/health]`

## HOW IT WORKS

- **Flow:** [1-line architecture/data flow diagram]
- **State/Storage:** [DB, cache, files, where data lives]

## SETUP REQUIRED

- [Env vars, dependencies, test data, or config needed before resuming]

## CODE CONTEXT

Key signatures, API shapes, or snippets the next agent needs:

[Include only what's essential — function signatures, response shapes, hook interfaces]

## WARNINGS

- `[Path/Thing]` -> [Why not to touch / what breaks / time-sensitive constraints]

## KEY FILES

- `[Path]` -> [Purpose]
```

## Boundaries

- Only generates handoff docs. Does not commit, push, or modify other files.
- Output is a single markdown file in `handoff_docs/`.
- One-shot skill — not a persistent mode.
