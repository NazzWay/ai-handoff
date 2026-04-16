Generate a structured handoff document from the current session's conversation context.

## Trigger

`/handoff` or "make a handoff", "write a handoff", "handoff doc"

## Process

1. **Review your conversation context.** Identify: what was the goal, what got done, what failed, what's next.
2. **Determine metadata:**
   - Date: today's date (YYYY-MM-DD)
   - Agent/Dev: your model name (e.g., "Claude Opus 4.6", "GPT-5.4", "Gemini 3.1 Pro")
   - Short task name: 3-5 word slug using hyphens (e.g., `arena-model-extraction-fix`)
3. **Populate the template below** with precise, actionable details from the session.
4. **Write the file** to `handoff_docs/handoff_YYYY-MM-DD_[short_task_name].md` in the project root. Create `handoff_docs/` if it doesn't exist.
5. **Confirm** to the user with the file path and a 1-line summary.

## Rules

- Use ONLY the template structure below. Do not add or remove sections.
- **Omit section content** (leave the header + "N/A") if nothing applies — do not fabricate.
- Use **exact file paths** (absolute when possible).
- Include **exact error messages** in INCOMPLETE/FAILED and ATTEMPTED & FAILED sections.
- Bullet points only. No prose paragraphs.
- Prioritize clarity for an AI agent continuing the work.
- No fluff. Every line must be actionable or informational.
- Mark completed items with `[x]`, incomplete with `[ ]`.

## Template

```markdown
# HANDOFF DOC: [Project/Feature]

**Date:** [YYYY-MM-DD] | **Agent/Dev:** [ID]
**Current Scope/Goal:** [1-2 sentences strictly defining what this session was attempting to achieve]

---

## COMPLETED

- [x] **[Task/Module]** -> `[Path]` | Status: [Stable/Tested/Implemented]

## INCOMPLETE / FAILED

- [ ] **[Task/Module]** -> `[Path]` | Issue: [Exact error/blocker]

## NEXT STEPS & FUTURE PIPELINE

**Immediate Priorities (To Unblock/Finish Current Scope):**

1. **[Action]** -> `[Path]` | Expected: [Outcome]
2. **[Action]** -> `[Path]` | Expected: [Outcome]

**Subsequent Tasks (To Execute Once Unblocked):**

- [ ] **[Future Task]** -> [Brief description of what to build next]
- [ ] **[Future Task]** -> [Brief description of what to build next]

- Verification Command: `[e.g., npm run test, python script.py, curl http://localhost...]`

## HOW IT WORKS (Critical Context)

- **Flow:** [1-line architecture/data flow]
- **Key Configs/Env:** [Vars, APIs, deps]
- **State/Storage:** [DB, cache, files]

## DO NOT TOUCH

- `[Path]` -> Reason: [Stable/core/breaks X]

## ATTEMPTED & FAILED (Avoid Repeating)

- **[Approach]** -> Failed: [Error/Reason] -> Use `[Alternative]` instead

## SUGGESTED FIXES / METHODS

- For `[Issue]`: Try `[Method]` -> Ref: `[Doc/Pattern]`

## KEY FILES & REFERENCES

- `[Path]` -> [Purpose]
```

## Boundaries

- Only generates handoff docs. Does not commit, push, or modify other files.
- Output is a single markdown file in `handoff_docs/`.
- "stop handoff" or "normal mode": no effect (this is a one-shot skill, not a persistent mode).
