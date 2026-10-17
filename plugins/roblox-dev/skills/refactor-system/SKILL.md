---
name: refactor-system
description: Bring one existing Roblox system onto the architecture conventions without touching the rest of the project. Use when the user names a system to clean up.
argument-hint: "<SystemName>"
disable-model-invocation: true
---

# /roblox-dev:refactor-system

Task: $ARGUMENTS (if empty, ask for the system name, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/architecture-conventions.md, ../roblox-dev/references/luau-architecture.md.

1. Follow the procedure in ../backup/SKILL.md for the affected scripts first (or confirm a recent backup exists). Check whether Rojo or git owns the sources; if so, edit the filesystem sources, not only the Studio copy.
2. Inventory the system's scripts and assets; list outside consumers.
3. Show the plan (moves, API, renames) and wait for approval.
4. Move into system folders, add the API (correct suffix), route every outside consumer through it, apply script layout and naming, remove dead code and debug prints. Touch other systems only to replace direct access with API calls.
5. Keep persisted names unchanged. Fix every broken `require` path. Verify once.
