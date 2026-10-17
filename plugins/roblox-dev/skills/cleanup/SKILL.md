---
name: cleanup
description: Find dead code, commented-out code, debug prints and unused assets in a Roblox project and remove them after approval. Use when the user asks to tidy or clean up.
argument-hint: "[scope]"
disable-model-invocation: true
---

# /roblox-dev:cleanup

Task: $ARGUMENTS (if empty, use the defaults described below).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/architecture-conventions.md.

1. Find candidates: commented-out code, leftover `print`/`warn` debugging, unused scripts and assets.
2. Confirm a backup exists (follow ../backup/SKILL.md if not). Verify each candidate is unreferenced (search by name, tags, attributes, `require` strings, DataStore-related names). Anything that could be referenced dynamically (names built from strings, `FindFirstChild` with variables, attributes or tags read elsewhere) is "unverifiable" and is never a candidate.
3. **List every candidate with path and evidence and ask for approval. Never delete on your own.** Move approved assets to a `Trash` folder (for example under ServerStorage) instead of deleting; delete only if the owner explicitly says so.
4. Keep genuine error warnings. Do not change behavior.
