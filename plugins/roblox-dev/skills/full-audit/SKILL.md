---
name: full-audit
description: Read-only audit of a Roblox game, complete or limited to areas (rules, security, performance, persistence, economy, gameplay, ui, world, release, growth, analytics), with a prioritized report. Use when the user asks for an audit, review or health check.
argument-hint: "[area ...]"
disable-model-invocation: true
---

# /roblox-dev:full-audit

Task: $ARGUMENTS (if empty, use the defaults described below).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/sharp-edges.md, ../roblox-dev/references/release-checklist.md (area release), ../roblox-dev/references/platform-discovery-metrics.md (area growth), ../roblox-dev/references/analytics-events.md (area analytics).

Scope: the areas named in the task; if none, all of them. **Read-only.** Inspect the real project (full tree, every relevant script's source, remotes, tags, attributes, DataStore and MarketplaceService usage) before judging.

Areas and the references to audit against (all in `../roblox-dev/references/`):
1. **rules** - architecture-conventions.md, luau-architecture.md: system folders, API naming and placement, cross-system access, dependency direction, script layout, naming, strict mode, leftovers.
2. **security** - networking-security.md: validation, rate limiting, client-trusted values, exploitable currency, damage and teleport paths.
3. **performance** - performance.md: hot loops, leaks, per-frame work, replication and memory cost.
4. **persistence** - persistence.md: keys and schemas, session ownership, load/save failure, save on leave and shutdown, migrations.
5. **economy** - economy-transactions.md, monetization.md, reward-design-random-items.md: atomic transactions, duplication, receipts, pass checks, paid random items show every outcome and odds, project price convention.
6. **gameplay** - gameplay-systems.md, combat.md, characters-input.md: server authority, cooldowns, respawn and lifecycle, mobile/console input.
7. **ui** - ui/design.md, ui/verification.md: phone/desktop scaling, safe areas, states, UI hidden in code.
8. **world** - world-physics.md: streaming assumptions, anchoring, collision, part count.
9. **release** - release-checklist.md (or use `/roblox-dev:release-check` for the verdict-only version).
10. **growth** - platform-discovery-metrics.md, onboarding-retention-ux.md, monetization-playbook.md: funnels, packaging honesty versus first minute, retention hooks, purchase pathways. Dashboard-only items are "not verified" unless the owner provides data.
11. **analytics** - analytics-events.md: economy and funnel events present, named stably, called on the server.

For each finding: severity (critical/high/medium/low), area, exact location (instance path or script and line), what is wrong, concrete fix. Separate rule violations from real bugs and risks; style opinions are not defects; mark unverifiable items as unverified.

Output: write `FULL_AUDIT.md` (see shared rules for existing files) with a summary and verdict per area, findings by severity, and a recommended fix order naming the matching command (`fix-bug`, `refactor-system`, `restructure`, `cleanup`, `save-data`, `economy`, `combat`, `ui`, `world`, `performance`, `growth`, `packaging`, `analytics`). Give the top 5 findings in chat. Do not start fixing unless asked. No playtest unless a finding cannot be judged without one (then one short test).
