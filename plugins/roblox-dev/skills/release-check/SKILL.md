---
name: release-check
description: Read-only release readiness review of a Roblox game with a verdict and evidence per item. Use before a release, a big update or starting ads; for a full multi-area audit use full-audit.
argument-hint: "[scope]"
disable-model-invocation: true
---

# /roblox-dev:release-check

Task: $ARGUMENTS (if empty, use the defaults described below).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/release-checklist.md, ../roblox-dev/references/reward-design-random-items.md, ../roblox-dev/references/analytics-events.md.

Work through every section of the checklist with evidence from the real project (script source, console, Studio inspection). Mark each item pass / fail / not verified; dashboard-only items stay "not verified" unless the owner provides data. Write `RELEASE_CHECK.md` (see shared rules for existing files), give the verdict and top blockers in chat, and do not start fixing. Never publish, spend Robux or change live settings.
