---
name: add-feature
description: Add a feature to an existing Roblox game as a new system, a sub-system or an extension of the owning system. Use when the user asks for a new mechanic, screen or system.
argument-hint: "<feature>"
---

# /roblox-dev:add-feature

Task: $ARGUMENTS (if empty, ask for the feature, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/game-design-building-blocks.md, ../roblox-dev/references/onboarding-retention-ux.md.

1. State the observable outcome and which system owns it (new system, sub-system, or extension). Expose behavior through that system's API or events; never reach into another system's internals.
2. If the feature is meant to move a metric, name the stat and write the hypothesis ([iteration loop](../roblox-dev/references/iteration-liveops-playtesting.md)). Skip this for plain content or fixes.
3. Keep the server authoritative for consequential state. Implement end to end: logic, UI, assets, persistence if needed.
4. Verify the new flow once and report integration points.
