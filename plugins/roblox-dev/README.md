# roblox-dev

Roblox game development for Claude Code, by Xeltic69.

One router skill (`roblox-dev`) loads a shared reference library on demand, and **22 namespaced commands** (`/roblox-dev:<name>`) cover the common jobs: building, fixing, auditing, shipping and growing a Roblox game. It works with the official Roblox Studio MCP server (or any other Studio MCP) and falls back to writing source plus placement instructions when Studio is not connected.

## Contents

- [Quick start](#quick-start)
- [Command reference](#command-reference)
- [Safety model](#safety-model)
- [Reference library](#reference-library)
- [Typical workflows](#typical-workflows)
- [Status, license and credits](#status-license-and-credits)

## Quick start

```text
/plugin marketplace add Xeltic69/roblox-dev-marketplace
/plugin install roblox-dev@roblox-dev-marketplace
```

Then, with a Roblox project open (and Studio MCP connected if you want live inspection), try a read-only command first:

```text
/roblox-dev:onboard
/roblox-dev:full-audit rules
```

Commands accept free text after the name. Anything you type becomes the task, for example `/roblox-dev:fix-bug diagnose shop buttons do nothing on mobile`.

## Command reference

Legend: **read-only** = never edits your place (audits may write one report file, never overwriting an existing one). **user-invoked** = Claude will not start it on its own; you type it.

### Understand a project

| Command | What it does | Example |
| --- | --- | --- |
| `onboard [focus]` | **Read-only.** Maps an unfamiliar project: containers, systems, scripts by side, remotes and handlers, persistence and purchase paths, tags and attributes. Reports data flows, hot spots, risks and which command to run next. | `/roblox-dev:onboard` |
| `full-audit [area ...]` | **Read-only, user-invoked.** Audits the whole game or chosen areas: `rules`, `security`, `performance`, `persistence`, `economy`, `gameplay`, `ui`, `world`, `release`, `growth`, `analytics`. Each finding has severity, exact location, why it is wrong and a concrete fix. Writes `FULL_AUDIT.md` and lists the top 5 findings in chat. | `/roblox-dev:full-audit security economy` |
| `release-check [scope]` | **Read-only, user-invoked.** Release readiness review with evidence per item (security, data, monetization including paid random item odds, player experience, performance, discovery, operations). Verdict: ready, ready with risks or not ready. Writes `RELEASE_CHECK.md`. | `/roblox-dev:release-check` |
| `market-research <idea>` | **Read-only.** Demand signals, competitors, gaps and trend phase for a game idea, with sources and dates, ending in differentiators and a recommended loop. | `/roblox-dev:market-research a firefighter extraction game` |

### Build

| Command | What it does | Example |
| --- | --- | --- |
| `new-game <idea>` | Plans first (fantasy, core loop, unique mechanic, progression, first 90 seconds, social hook, phone/desktop/console), waits for your yes, then builds in playable slices with a server-authoritative design. | `/roblox-dev:new-game a cozy pet shop tycoon` |
| `add-feature <feature>` | Adds a feature as a new system, sub-system or extension of the owning system, exposed through an API. States the metric and hypothesis when the feature is meant to move a stat. | `/roblox-dev:add-feature daily login rewards` |
| `new-system <Name and purpose>` | Creates a self-contained system: folders, API module with the right suffix, starter scripts in a fixed layout, wired through events so nothing else must change to remove it. | `/roblox-dev:new-system Inventory: item storage and equip` |
| `gameplay <task>` | NPC AI, quests, dialogue, rounds and checkpoints. Defines state ownership and cleanup scopes, handles late join and respawn, verifies one full loop. | `/roblox-dev:gameplay a round system with intermission` |
| `combat <task>` | Combat, abilities and hit validation. Every client message is a request validated on the server (range, cooldown, state). Shared checks live in one parent system. | `/roblox-dev:combat melee with server-side hit checks` |
| `ui <task>` | Builds, restyles or reviews UI (menus, HUDs, shop screens, screenshot-inspired layouts). Keeps UI inside its system, checks phone/desktop sizes, safe areas and gamepad focus. | `/roblox-dev:ui a mobile-friendly shop screen` |
| `world <task>` | Levels, terrain, physics and streaming. Uses tagged objects instead of fixed paths and accounts for StreamingEnabled. | `/roblox-dev:world fix floating parts when streaming in` |

### Fix and improve

| Command | What it does | Example |
| --- | --- | --- |
| `fix-bug [diagnose or playtest] <bug>` | Finds the root cause and fixes it with the smallest change. `diagnose` explains the cause and edits nothing; `playtest` runs one short test and reports pass or fail with evidence. | `/roblox-dev:fix-bug diagnose data not saving on leave` |
| `performance [system or symptom]` | Collects evidence first (profiler, memory, activity), ranks causes by impact, fixes the clear ones with minimal changes and re-checks the symptom. | `/roblox-dev:performance lag during egg hatching` |
| `save-data <task>` | Player data persistence: session ownership, retries, load-failure handling, save on leave and shutdown, versioned migrations. Asks before changing any existing key or schema and never migrates live data on its own. | `/roblox-dev:save-data add a versioned profile migration` |
| `economy <task>` | Currencies, inventory, shops, monetization code. Server-authoritative and atomic transactions, one receipt handler, paid random items show every outcome with odds. Never changes prices, products or receipts without approval. | `/roblox-dev:economy review the shop purchase flow` |
| `analytics <stat or feature>` | Adds or reviews economy and funnel events so a stat can be diagnosed. Server-side, stable names, rate-limit aware, plus how to verify events after a published test build. | `/roblox-dev:analytics funnel for the tutorial` |

### Restructure and tidy (user-invoked)

| Command | What it does | Example |
| --- | --- | --- |
| `backup [target folder]` | Exports every script (path preserved) and a tree listing to a timestamped `_backup` folder, never overwriting one, and reminds you to save a copy of the place file too. | `/roblox-dev:backup` |
| `cleanup [scope]` | Finds dead code, commented-out code, debug prints and unused assets. Verifies references, lists candidates with evidence, deletes nothing without your approval and moves approved assets to a Trash folder first. | `/roblox-dev:cleanup scripts only` |
| `refactor-system <Name>` | Brings one existing system onto the architecture conventions: backup, plan, approval, then moves, API, consumer updates and naming. Persisted names stay unchanged. | `/roblox-dev:refactor-system Pets` |
| `restructure [notes]` | Whole-codebase reorganization: backup, read-only audit (`RESTRUCTURE_AUDIT.md`), your approval, then one system at a time with a sanity check after each. Requires a saved place-file copy before migrating. | `/roblox-dev:restructure` |

### Grow the game

| Command | What it does | Example |
| --- | --- | --- |
| `growth <stat or goal>` | The hypothesis loop: take your dashboard numbers, pick the weakest stat, gather feedback, metric and competitor evidence, propose one focused change and wait for your yes before editing. | `/roblox-dev:growth D1 retention is low` |
| `packaging <game and part>` | Title, thumbnail concepts, detail page and a sponsored-ads protocol. Checks core fantasy, reading level, honesty versus the first minute and mobile legibility. Plans only; never spends Robux. | `/roblox-dev:packaging title and thumbnails for my pet game` |

## Safety model

- **Approval gates.** Nothing is published, purchased, priced, deleted or migrated against live data without an explicit yes in the conversation, and approval for one action does not carry over to the next. The rules every command shares are in `skills/roblox-dev/references/command-rules.md`.
- **User-invoked only:** `backup`, `cleanup`, `restructure`, `refactor-system`, `full-audit`, `release-check`.
- **Read-only commands** (`onboard`, `full-audit`, `release-check`, `market-research`) never edit your place. Report files are never overwritten; a dated name is used instead.
- **Project conventions win.** The architecture conventions apply to new systems and substantially edited scripts unless your project already uses another convention.
- **Honest reports.** Every report says what was verified, how, and what was not.

## Reference library

Loaded on demand through the `roblox-dev` router:

- **Engineering:** architecture conventions, Luau and architecture, networking and security, persistence, economy and transactions, monetization, combat, gameplay systems, characters and input, world and physics, presentation and assets, performance, social and teleport, UI (design, components, patterns, platform, accessibility, verification), tooling and Open Cloud, analytics events, release checklist, sharp edges.
- **Studio:** working with Studio MCP, studio testing.
- **Growth (labeled by evidence level):** discovery and metrics, packaging and ads, ideation and market validation, game design building blocks, onboarding and retention, iteration and LiveOps, monetization playbook, reward design and random items (including the paid-random-items odds policy), team and production notes.

Statements are tagged **[Docs]**, **[DevForum]** or **[Creator]** where it matters. Creator material is paraphrased practitioner experience, not Roblox rules.

## Typical workflows

- **New to a project:** `onboard`, then `full-audit`, then pick findings, then `fix-bug` or `refactor-system`.
- **Tidy a messy codebase:** `backup`, then `restructure` (audit, approval, per-system migration), then `cleanup`.
- **Before launch:** `release-check`, then `economy` and `save-data` fixes, then `analytics`, then `packaging`.
- **After launch:** `growth` on your weakest stat, implement the approved change, check the results window, repeat.
- **New idea:** `market-research`, then `new-game`, then `add-feature`, then `ui`.

## Status, license and credits

Version 0.1.0. Manifests, frontmatter and internal links are checked by script. Roblox facts were checked against the Creator Hub in October 2026 and carry "verify" notes where they may change. Commands have not been exercised end to end across many projects; please open issues for anything that does not behave as described.

MIT License. See [LICENSE](LICENSE). Sources and credits: `skills/roblox-dev/references/sources-attribution.md`.

Roblox and other game names mentioned here are trademarks of their respective owners; this project is not affiliated with or endorsed by Roblox Corporation.
