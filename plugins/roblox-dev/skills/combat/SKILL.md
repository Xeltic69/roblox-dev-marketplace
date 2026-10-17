---
name: combat
description: Build or fix Roblox combat, abilities and hit validation with a server-authoritative design. Use when the user mentions damage, weapons, abilities, cooldowns or PvP.
argument-hint: "<combat task>"
---

# /roblox-dev:combat

Task: $ARGUMENTS (if empty, ask what to build or fix, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/combat.md, ../roblox-dev/references/networking-security.md.

- Treat every client combat message as a request: validate shape, range, line of sight, cooldown and state on the server.
- Centralize shared checks (cooldowns, can-activate) in one parent system; abilities are sub-systems that ask it, so a change to the checks happens once.
- Verify one full hit-to-damage flow, including a rejected invalid request.
