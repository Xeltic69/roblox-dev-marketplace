---
name: fix-bug
description: Diagnose, fix and verify a Roblox bug at its root cause with a minimal change. Use when the user reports an error, broken behavior or a console message. Modes: diagnose (no edits) and playtest (one short test).
argument-hint: "[diagnose|playtest] <bug or change>"
---

# /roblox-dev:fix-bug

Task: $ARGUMENTS (if empty, ask for the symptom, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/studio-testing.md.

Mode: if the first word of the task is exactly `diagnose` or `playtest`, remove it and use that mode; otherwise fix.
- **diagnose:** read the console and the involved scripts fully, form a hypothesis from evidence, confirm it (one playtest is allowed only to confirm the hypothesis), report cause and minimal fix. Edit nothing.
- **playtest:** run exactly one short playtest of the described change or flow, read console and affected state, report pass or fail with evidence, then stop.
- **fix (default):** reproduce the trigger, read console and relevant scripts fully, identify the observed cause, fix it with the smallest change in the owning system, then check the original trigger. At most one playtest may cover both reproduction and verification. Load the area reference from the router table in ../roblox-dev/SKILL.md (for example persistence.md for save bugs, monetization.md for receipt bugs). No speculative rewrites, no retry loops without new evidence.
