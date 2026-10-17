---
name: roblox-dev
description: General Roblox, Luau and Roblox Studio development help that no specific /roblox-dev command covers, plus the shared reference library (architecture, networking and security, persistence, economy, UI, world, performance, discovery and growth, release). Use for Roblox questions, design discussions and tasks that span several areas.
---

# Roblox Dev

Build the requested game or improvement and verify the behavior that matters. Any genre, project size, framework or visual style. Respond in the user's language. Follow [command rules](references/command-rules.md) (inspect first, minimal change, approval gates, one playtest, honest reports) for all work, whether or not a command was used.

## Commands

For common actions use the namespaced commands; they load the right references and apply gates.

| Command | Use |
| --- | --- |
| `/roblox-dev:new-game` | Plan and build a game from scratch |
| `/roblox-dev:add-feature` | Add a feature as a system or sub-system |
| `/roblox-dev:fix-bug` | Fix a bug; modes `diagnose` (no edits) and `playtest` (one short test) |
| `/roblox-dev:new-system` | Create a system with folders, API and layout |
| `/roblox-dev:refactor-system` | Bring one existing system to the conventions |
| `/roblox-dev:restructure` | Restructure a whole codebase (backup, audit, approved migration) |
| `/roblox-dev:cleanup` | Remove dead code, prints, unused assets (after approval) |
| `/roblox-dev:backup` | Export scripts before risky changes |
| `/roblox-dev:onboard` | Explain an unfamiliar project |
| `/roblox-dev:full-audit` | Read-only audit, complete or per area (rules, security, performance, persistence, economy, gameplay, ui, world, release, growth, analytics) |
| `/roblox-dev:release-check` | Read-only release readiness verdict with evidence |
| `/roblox-dev:save-data` | Persistence and migrations |
| `/roblox-dev:economy` | Currencies, inventory, shops, monetization code |
| `/roblox-dev:combat` | Combat, abilities, server-side hit validation |
| `/roblox-dev:gameplay` | NPCs, quests, rounds, checkpoints |
| `/roblox-dev:ui` | Build, restyle or review UI |
| `/roblox-dev:world` | Levels, terrain, physics, streaming |
| `/roblox-dev:performance` | Find and fix lag, leaks, load cost |
| `/roblox-dev:analytics` | Add or review analytics events and funnels |
| `/roblox-dev:growth` | Improve a stat with the hypothesis loop |
| `/roblox-dev:packaging` | Title, thumbnails, detail page, ads plan |
| `/roblox-dev:market-research` | Market, competitors, gaps |

## Principles

- Apply the [architecture conventions](references/architecture-conventions.md) to new systems and to scripts you substantially edit; in a project with another convention, follow it for existing code and mention the mismatch.
- Convert the request into observable outcomes. For a whole game define the loop, fantasy, progression, content, input targets and acceptance scenarios; work in integrated slices.
- Keep authority explicit: clients express intent; the server validates consequential state. Persistence and paid grants need durable recovery.
- For small, clear tasks act and report; for large, ambiguous or risky ones (restructures, migrations, pricing, deleting assets) state the plan and open questions first.
- Roblox facts in the references are labeled verified, unverified or creator opinion. Do not turn creator opinions or numbers into platform rules; re-check version-dependent facts in the official docs.

## Studio connection (MCP)

Detect what is available before relying on it; a listed tool is not proof of an active connection. Working pattern and safety rules are in [Studio MCP](references/studio-mcp.md).

1. **Official Roblox Studio MCP** connected: inspect the tree, read and edit scripts, run Luau, read the console, run one short playtest, using the tools the live connection exposes.
2. **Other Studio MCP servers**: use their equivalents; map tool names from the live schema, never from memory.
3. **Offline** (no Studio tools): produce usable source plus placement and initialization instructions; state which runtime checks remain.

Persist source changes in the intended edit-time or project source, not only a disposable play session.

## Load only the relevant route

Choose the primary row and add adjacent references only when the task crosses that boundary.

| Task | Read |
| --- | --- |
| New game or broad improvement | [workflow](references/workflow.md), [game design](references/game-design.md), then relevant routes |
| System layout, APIs, script layout, naming, restructuring | [architecture conventions](references/architecture-conventions.md), [Luau and architecture](references/luau-architecture.md) |
| Multiplayer, remotes, abuse resistance | [networking and security](references/networking-security.md) |
| Saves, session ownership, migrations, leaderboards | [persistence](references/persistence.md) |
| Inventory, crafting, trading, currencies | [economy and transactions](references/economy-transactions.md) |
| Gamepasses, dev products, what to sell and where, cash-out | [monetization](references/monetization.md), [monetization playbook](references/monetization-playbook.md) |
| Eggs, rolls, crates, luck, pity, odds display, reward psychology | [reward design and random items](references/reward-design-random-items.md) |
| Movement, camera, input, respawn | [characters and input](references/characters-input.md) |
| Combat, abilities, hit validation | [combat](references/combat.md), [networking](references/networking-security.md) |
| NPC AI, quests, dialogue, rounds, checkpoints | [gameplay systems](references/gameplay-systems.md) |
| Teams, matchmaking, teleports | [social and teleport](references/social-teleport.md) |
| UI creation, restyle, review, screenshot inspiration | [UI design](references/ui/design.md) and its feature links |
| Level, terrain, physics, streaming | [world and physics](references/world-physics.md) |
| Animation, lighting, VFX, audio, models | [presentation and assets](references/presentation-assets.md) |
| Slow frames, leaks, memory and network cost | [performance](references/performance.md) |
| Debug or verify in Studio or offline | [Studio and testing](references/studio-testing.md), [Studio MCP](references/studio-mcp.md) |
| Rojo, packages, linters, CI, Open Cloud | [tooling](references/tooling.md) |
| Release, LiveOps, player-authored content | [release and LiveOps](references/release-liveops.md), [release checklist](references/release-checklist.md) |
| Analytics events, funnels, economy tracking | [analytics events](references/analytics-events.md) |
| Algorithm, ranking, PTR/bounce/retention, Kids/Select gate | [discovery and metrics](references/platform-discovery-metrics.md) |
| Title, thumbnail, detail page, sponsored ads | [packaging, thumbnails and ads](references/packaging-thumbnails-ads.md) |
| Finding ideas, demand signals, trend phases | [ideation and market validation](references/ideation-market-validation.md), [market research](references/market-research.md) |
| Fantasy, unique mechanic, depth, social flex, level design | [game design building blocks](references/game-design-building-blocks.md) |
| Tutorial, first minutes, retention, mobile and console friction | [onboarding, retention and UX](references/onboarding-retention-ux.md) |
| Improving a stat, patches vs updates, playtesters, balancing | [iteration, LiveOps and playtesting](references/iteration-liveops-playtesting.md) |
| Hiring, contracts, scope, production phases | [team, production and mindset](references/team-production-mindset.md) |
| Simulator launch lessons | [creator lessons](references/creator-lessons-simulator-launch.md) |
| Frequent high-impact mistakes | [sharp edges](references/sharp-edges.md) |
| Provenance, licenses, limits | [sources and attribution](references/sources-attribution.md) |

## Execution loop

1. **Inspect:** the correct project, source of truth, baseline and owners of the relevant code and data.
2. **Specify:** behavior, constraints and a proportionate verification path; ask only for material missing information.
3. **Implement:** edit relevant files and instances; keep migrations and integration boundaries explicit.
4. **Verify:** reproduce the trigger or complete the new flow; check state and output; test relevant lifecycle, failure and input cases.
5. **Repair:** fix observed causes and rerun affected checks. Missing tools or dependencies need an honest gap, not a fabricated pass.
6. **Deliver:** behavior changed, where it lives, actual checks, gaps and limits. Do not claim a complete game from a disconnected set of scripts.

## Boundaries

Reviews and design-only requests do not authorize implementation. Whole-game instructions authorize the required local implementation, but publication, spending, live data migration, external messages and unrelated configuration changes need their own approval ([approval gates](references/command-rules.md)). Preserve the user's Studio session and debugger state.
