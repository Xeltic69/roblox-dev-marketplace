---
name: onboard
description: Explain an unfamiliar Roblox project: structure, systems, data flow, risks and where to start. Use when the user opens a project they do not know or asks how a game is built.
argument-hint: "[focus]"
---

# /roblox-dev:onboard

Task: $ARGUMENTS (if empty, use the defaults described below).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/architecture-conventions.md, ../roblox-dev/references/luau-architecture.md.

Read-only. Map containers, systems, scripts by side, remotes and their handlers, persistence and purchase paths, tags and attributes. Report a concise overview, the main data flows, hot spots and risks, and suggest the most useful next command (`full-audit`, `refactor-system`, `fix-bug`).
