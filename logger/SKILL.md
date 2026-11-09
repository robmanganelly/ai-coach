---
name: logger
description: "Manages persistent session checkpoints for the tutor skill. Creates and updates session state files in the designated coaching repository so progress can be resumed. Use when starting or ending a tutoring session, or when the user asks to save/resume state. Not for one-off questions."
type: workflow
lifecycle: active
---

# Logger

Persist and resume tutor session state using a designated GitHub repository (default: the ai-coach repository itself).

## Repository structure

- Path: `sessions/[discipline]/[topic]/` (e.g. `sessions/math/linear-algebra/`)
- Files in each topic folder:
  - `latest.md` — current session state (the compact block from the tutor “save state”)
  - `checkpoint.md` — previous version of `latest.md`

## At the start of every tutoring session

1. Identify the discipline and topic from the user's request (e.g. linear algebra → math/linear-algebra).
2. Check the repository for the file `sessions/[discipline]/[topic]/latest.md`.
3. If it exists and has content, use it to resume via the tutor “resume from:” mechanism before any diagnostic or teaching.
4. If it does not exist, start a fresh session as usual with the tutor skill.

## When saving state (user says “save state” or at natural session end)

1. Obtain the compact state block from the tutor skill.
2. Determine the path `sessions/[discipline]/[topic]/latest.md`.
3. Before writing:
   - If `latest.md` already exists and has content, copy its current content to `checkpoint.md` (create the file or overwrite it if it already exists).
   - Then write the new state block to `latest.md`.
4. Confirm the write succeeded.

## Notes

- Always use the connected GitHub tools to read from and write to the designated repository.
- Keep the skill focused on persistence only; the actual tutoring logic remains in the tutor skill.
- Create the sessions/discipline/topic folder structure as needed when writing the first file.
- Default repository is ai-coach; override if the user specifies another.
