---
name: restructure
description: Restructure a whole Roblox codebase into systems with APIs: backup, audit, approved plan, per-system migration. Use only when the user explicitly asks to reorganize the entire project.
argument-hint: "[scope or notes]"
disable-model-invocation: true
---

# /roblox-dev:restructure

Task: $ARGUMENTS (if empty, use the defaults described below).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/architecture-conventions.md, ../roblox-dev/references/luau-architecture.md.

1. Follow the procedure in ../backup/SKILL.md and confirm where the backup is. **Do not migrate until the owner confirms they also saved a copy of the place file** (File > Save As), because script exports cannot restore UI, models or terrain. Check whether Rojo or git owns the sources (see tooling.md) before moving anything in Studio.
2. Audit read-only and write `RESTRUCTURE_AUDIT.md` (never overwrite an existing file; use a dated name): proposed systems and sub-systems, cross-system accesses and their replacement APIs, dependency-direction violations, dead assets, name collisions.
3. **Stop and present the plan. Migrate only after the owner approves.** Ask separately before renaming persisted data, deleting or moving assets that may be in use, or renaming remotes.
4. Migrate one system at a time following ../refactor-system/SKILL.md; keep the game working after each system; one short sanity check per system.
5. Final cleanup following ../cleanup/SKILL.md (with its approvals), then a report of what moved, which APIs exist and what you were unsure about.
