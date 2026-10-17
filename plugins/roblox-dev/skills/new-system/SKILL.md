---
name: new-system
description: Create a new Roblox system with the right folders, API module, script layout and naming. Use when the user wants a new self-contained feature area.
argument-hint: "<SystemName and purpose>"
---

# /roblox-dev:new-system

Task: $ARGUMENTS (if empty, ask for the system name and responsibility, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/architecture-conventions.md, ../roblox-dev/references/luau-architecture.md.

1. Search the Explorer first so the name is unique and not generic.
2. Create the container folders as needed (server, client, shared modules, assets, `Workspace.Scripted`), the API module with the correct Client/Shared/none suffix, and starter scripts in the prescribed layout order.
3. Make other systems depend on this one only through events and its API, so removing it needs no edits elsewhere.
4. Report the folder tree and the API surface.
