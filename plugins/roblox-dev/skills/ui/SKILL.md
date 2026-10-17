---
name: ui
description: Build, restyle or review Roblox UI. Use when the user asks for a menu, HUD, shop screen, screenshot-inspired interface or UI fixes.
argument-hint: "<screen or style task>"
---

# /roblox-dev:ui

Task: $ARGUMENTS (if empty, ask which screen and what style, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/ui/design.md, ../roblox-dev/references/onboarding-retention-ux.md, ../roblox-dev/references/monetization-playbook.md (shop screens).

- If the inspiration-ui skill is installed it can help with screenshot references; otherwise follow ui/design.md.
- Keep UI inside its system; name tool UI `<toolName>Tool`; hide ScreenGuis explicitly in code instead of relying on `ResetOnSpawn`.
- Provide buy-one / buy-max style options where players repeat an action; place purchase offers where players already are; do not show offers before the player is invested.
- Check phone and desktop sizes, safe areas and gamepad focus.
