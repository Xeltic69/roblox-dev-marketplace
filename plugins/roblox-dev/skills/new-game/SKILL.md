---
name: new-game
description: Plan and build a new Roblox game from scratch: fantasy, core loop, systems, onboarding and first content. Use when the user wants to start a new game or prototype.
argument-hint: "<game idea>"
---

# /roblox-dev:new-game

Task: $ARGUMENTS (if empty, ask what the game is, if the idea is missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/workflow.md, ../roblox-dev/references/game-design.md, ../roblox-dev/references/game-design-building-blocks.md, ../roblox-dev/references/onboarding-retention-ux.md, ../roblox-dev/references/networking-security.md, ../roblox-dev/references/persistence.md (if player data is saved), ../roblox-dev/references/economy-transactions.md (if there is an economy), ../roblox-dev/references/reward-design-random-items.md (only if the game has eggs, rolls or crates).

1. Write a short plan: fantasy and primary verb, core loop, unique mechanic, progression, first-90-seconds onboarding, social/co-op hook, input targets (phone, desktop, console), content scope and acceptance scenarios. Treat creator heuristics (for example "change about 20% of a proven reference") as hints, not rules, and never reuse another creator's names, art, UI, code or thumbnails.
2. Present the plan and wait for the owner's yes before building. If the place already has content, follow the procedure in ../backup/SKILL.md first.
3. After approval, build in integrated, playable slices: each feature as its own system with an API ([architecture](../roblox-dev/references/architecture-conventions.md)), server-authoritative state, UI and persistence where needed.
4. If the owner pasted market findings, use them; otherwise suggest `/roblox-dev:market-research` before building.
5. Do not reduce the requested end state to a hollow prototype, but keep each slice small enough to verify.
