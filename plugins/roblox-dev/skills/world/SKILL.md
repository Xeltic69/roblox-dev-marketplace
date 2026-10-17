---
name: world
description: Build or fix Roblox levels, terrain, physics and streaming behavior. Use when the user mentions maps, terrain, collisions, StreamingEnabled or world layout.
argument-hint: "<level or environment task>"
---

# /roblox-dev:world

Task: $ARGUMENTS (if empty, ask what to build or fix, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/world-physics.md, ../roblox-dev/references/game-design-building-blocks.md (level design).

Place scripted objects under `Workspace.Scripted.<SystemName>` and tag them with CollectionService instead of direct path access. Account for StreamingEnabled (instances may not exist on the client). Use level design to show the threat or goal early and to make other players' progress visible when the game has a social-flex element.
