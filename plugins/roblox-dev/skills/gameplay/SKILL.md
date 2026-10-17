---
name: gameplay
description: Build or fix Roblox gameplay systems such as NPC AI, quests, dialogue, rounds and checkpoints. Use when the user mentions NPCs, enemies, quests or match flow.
argument-hint: "<NPC, quest or round task>"
---

# /roblox-dev:gameplay

Task: $ARGUMENTS (if empty, ask what to build or fix, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/gameplay-systems.md, ../roblox-dev/references/characters-input.md, ../roblox-dev/references/social-teleport.md (rounds, matchmaking).

Define state and ownership first (who mutates round, quest or NPC state), make cleanup scopes explicit (round, player, character), handle late join and respawn, and verify one full loop from start to finish.
