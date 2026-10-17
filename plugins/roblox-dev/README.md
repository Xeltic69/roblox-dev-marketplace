# roblox-dev

Roblox game development for Claude Code, by Xeltic69.

One router skill (`roblox-dev`) loads a shared reference library on demand, and **22 namespaced commands** (`/roblox-dev:<name>`) cover the common jobs: understanding a project, building, fixing, tidying, shipping and growing a Roblox game. It works with the official Roblox Studio MCP server (or any other Studio MCP) and falls back to writing source plus placement instructions when Studio is not connected.

## Contents

- [Quick start](#quick-start)
- [How the commands work](#how-the-commands-work)
- [Which command should I use?](#which-command-should-i-use)
- [Command guide in depth](#command-guide-in-depth)
  - [Understand a project](#understand-a-project): `onboard`, `full-audit`, `release-check`, `market-research`
  - [Build](#build): `new-game`, `add-feature`, `new-system`, `gameplay`, `combat`, `ui`, `world`
  - [Fix and improve](#fix-and-improve): `fix-bug`, `performance`, `save-data`, `economy`, `analytics`
  - [Restructure and tidy](#restructure-and-tidy): `backup`, `cleanup`, `refactor-system`, `restructure`
  - [Grow the game](#grow-the-game): `growth`, `packaging`
- [Safety model](#safety-model)
- [Reference library](#reference-library)
- [Typical workflows](#typical-workflows)
- [Limits](#limits)
- [Status, license and credits](#status-license-and-credits)

## Quick start

```text
/plugin marketplace add Xeltic69/roblox-dev-marketplace
/plugin install roblox-dev@roblox-dev-marketplace
```

With a Roblox project open (and Studio MCP connected if you want live inspection), start with a read-only command:

```text
/roblox-dev:onboard
/roblox-dev:full-audit rules
```

Anything you type after the command name becomes the task, for example `/roblox-dev:fix-bug diagnose shop buttons do nothing on mobile`. If a command needs information you did not give, it asks one short question.

## How the commands work

Every command is a short, focused instruction file. Behind it sits the same machinery:

1. **Shared rules first.** Each command begins by reading `references/command-rules.md`: inspect the real project before changing anything, change only what the request needs, keep persisted names (DataStore keys, product and pass IDs, attribute names used by saved data) unchanged, one focused playtest per change, and the approval gates below.
2. **Studio access.** If a Studio MCP server is connected, commands inspect the real place (tree, script source, console), edit scripts and instances, and can run one short playtest. If nothing is connected, commands work offline: they deliver complete source with exact placement (container, script type, name, initialization order) and say plainly that nothing was run.
3. **Task-specific references.** After the shared rules, each command loads only the reference files for its area (for example `persistence.md` for `save-data`, `networking-security.md` for `combat`). Nothing else is loaded.
4. **Project conventions win.** The plugin's architecture conventions (feature folders, API modules, script layout, naming) apply to new systems and substantially edited scripts, unless your project already follows another convention. In that case existing code keeps its convention and the command mentions the mismatch.
5. **Honest reports.** Every command ends with what changed, where it lives, what was verified and how, what was not verified, and the sensible next command. A pass is never claimed without evidence.

Two kinds of commands are marked below:

- **read-only**: never edits your place. Audit-style commands may write one report file in the project folder and never overwrite an existing one (they use a dated name instead, or answer in chat if there is no folder).
- **user-invoked only**: Claude will not start these on its own because they move, delete, bulk-export or write report files. You type them.

## Which command should I use?

| I want to... | Use |
| --- | --- |
| understand a project I just opened | `onboard` |
| find everything that is wrong or risky | `full-audit` (or one area, e.g. `full-audit security`) |
| know if I can ship | `release-check` |
| validate an idea before building | `market-research` |
| start a game from nothing | `new-game` |
| add a mechanic or screen | `add-feature` |
| start a self-contained system | `new-system` |
| fix something broken | `fix-bug` |
| make it faster or lighter | `performance` |
| protect player data | `save-data` |
| work on shops, currencies, Robux products | `economy` |
| build NPCs, quests or rounds | `gameplay` |
| build combat or abilities | `combat` |
| build or restyle a screen | `ui` |
| fix a map, terrain or streaming issue | `world` |
| find out where players drop off | `analytics`, then `growth` |
| improve a weak stat | `growth` |
| improve title, thumbnails, ads | `packaging` |
| reorganize code safely | `backup`, then `refactor-system` or `restructure` |
| remove dead code and assets | `cleanup` |

## Command guide in depth

Each entry lists what it is for, how it works, what you get and the guardrails. Examples show typical wording; the text after the command is free-form.

### Understand a project

#### `onboard [focus]` (read-only)

**For:** the first hour with a project you did not write, or one you have forgotten.

**How it works:** reads the shared rules plus the architecture and Luau references, then maps the project without changing it: containers and their sizes, systems and which side (server, client, shared) each script runs on, remotes and the handlers behind them, persistence paths (what is saved, where, how), purchase paths, tags and attributes. It should say which parts it only sampled rather than read in full.

**You get:** a concise overview, the main data flows (client to server, server to client, saving, purchases), hot spots (very large scripts, oversized containers, backup clutter inside the place) and risks, followed by the most useful next command.

**Guardrails:** no edits, no playtest, no files written.

**Try:** `/roblox-dev:onboard`, or focus it: `/roblox-dev:onboard the purchase and data paths`.

#### `full-audit [area ...]` (read-only, user-invoked only)

**For:** a structured health check of the whole game or specific areas.

**Areas:**

| Area | What is checked |
| --- | --- |
| `rules` | feature folders, API naming and placement, cross-system access, dependency direction, script layout, naming, strict mode, leftovers |
| `security` | remote validation, rate limiting, client-trusted values, exploitable currency, damage and teleport paths |
| `performance` | hot loops, leaks, per-frame work, replication and memory cost |
| `persistence` | keys and schemas, session ownership, load and save failure, save on leave and shutdown, migrations |
| `economy` | atomic transactions, duplication, receipt handling, pass checks, paid random items showing every outcome and odds, price convention |
| `gameplay` | server authority, cooldowns, respawn and lifecycle, mobile and console input |
| `ui` | phone and desktop scaling, safe areas, states, UI hiding done in code |
| `world` | streaming assumptions, anchoring, collision, part count |
| `release` | the release checklist (or use `release-check` for just the verdict) |
| `growth` | funnels, packaging honesty versus the first minute, retention hooks, purchase pathways |
| `analytics` | economy and funnel events present, named stably, called from the server |

**How it works:** inspects the real project first (tree, script source, remotes, tags, attributes, DataStore and Marketplace usage), then audits each selected area against its reference. Findings are separated into rule violations and real bugs or risks; style opinions are not reported as defects; anything it cannot verify (dashboard-only data, for example) is marked "not verified".

**You get:** `FULL_AUDIT.md` with a verdict per area and findings sorted by severity. Each finding has severity, area, exact location (instance path or script and line), what is wrong and a concrete fix. It also gives a recommended fix order that names the command for each fix, and the top five findings in chat.

**Guardrails:** read-only; it does not start fixing unless you ask; at most one short playtest, and only when a finding cannot be judged without one.

**Try:** `/roblox-dev:full-audit` (everything), `/roblox-dev:full-audit security economy`.

#### `release-check [scope]` (read-only, user-invoked only)

**For:** a go or no-go before a release, a big update or starting ads.

**How it works:** walks the release checklist section by section with evidence from the real project (script source, console, Studio inspection): security and safety, data (session ownership, shutdown saves, migrations, rollback plan), monetization and economy (receipt handling, price convention, paid random item odds summing to 100 percent), player experience (first 90 seconds, respawn, late join, phone, console), performance and stability, discovery and analytics, and operations (test place, hotfix path, feedback channel). Each item is marked pass, fail or not verified.

**You get:** `RELEASE_CHECK.md` with a verdict (ready, ready with risks, not ready), a table of items with status and evidence, and an ordered fix list. The top blockers appear in chat.

**Guardrails:** read-only. It never publishes, spends Robux or changes live settings, and dashboard-only items stay "not verified" unless you provide the data.

**Try:** `/roblox-dev:release-check`.

#### `market-research <idea>` (read-only)

**For:** validating a game idea, comparing concepts or finding a gap before you build.

**How it works:** uses current sources (and cites them with dates), separates observation from inference, and applies the plugin's research method: demand signals on and off Roblox, the five checks for an idea, and the blue, red and purple ocean phases of a trend. It may read your project for context but does not edit it.

**You get:** the evidence, the gaps and differentiators, and a recommended core loop. It offers to save the findings as `MARKET_RESEARCH.md` so `new-game` can use them.

**Guardrails:** no project edits. Creator advice in the references is treated as hypotheses, never as proof, and ideas must adapt mechanics and fantasy only, never another game's names, art or code.

**Try:** `/roblox-dev:market-research a firefighter extraction game`.

### Build

#### `new-game <idea>`

**For:** starting a game from nothing, or a clean prototype.

**How it works:** first writes a short plan: fantasy and primary verb, core loop, unique mechanic, progression, the first 90 seconds, social or co-op hook, input targets (phone, desktop, console), content scope and acceptance scenarios. **It then waits for your yes before building.** After approval it builds in integrated, playable slices: each feature as its own system with an API, server-authoritative state, UI and persistence where needed. If the place already has content it runs the backup procedure first. It reads the networking, persistence and economy references when they apply, and the odds-policy reference when the game has eggs, rolls or crates.

**You get:** a plan to approve, then working slices, each small enough to verify, with a report of what each slice contains.

**Guardrails:** creator heuristics (such as "change about 20 percent of a proven reference") are hints, not rules; it never reuses another creator's names, art, UI, code or thumbnails; it does not publish.

**Try:** `/roblox-dev:new-game a cozy pet shop tycoon with co-op`.

#### `add-feature <feature>`

**For:** adding a mechanic, screen or system to a game that already exists.

**How it works:** states the observable outcome and decides who owns it: a new system, a sub-system or an extension of an existing one. Behavior is exposed through that system's API or events; other systems' internals are never touched directly. If the feature is meant to move a metric it names the stat and writes the hypothesis first. It keeps the server authoritative for anything consequential and implements end to end: logic, UI, assets and persistence if needed.

**You get:** the working feature, the integration points and one verification of the new flow.

**Guardrails:** minimal changes outside the owning system; persisted names unchanged.

**Try:** `/roblox-dev:add-feature daily login rewards with a streak`.

#### `new-system <Name and purpose>`

**For:** creating a self-contained feature area the right way from the start.

**How it works:** searches the Explorer so the name is unique and not generic, then creates the folders it needs (server, client, shared, assets, `Workspace.Scripted`), an API module with the correct suffix (`<Name>API` for server only, `<Name>ClientAPI`, `<Name>SharedAPI`), and starter scripts in the prescribed layout order. Other systems depend on it only through events and the API, so removing it needs no edits elsewhere.

**You get:** the folder tree and the API surface, ready to fill in.

**Try:** `/roblox-dev:new-system Inventory: item storage, equip and trading`.

#### `gameplay <task>`

**For:** NPC AI, quests, dialogue, rounds, checkpoints and match flow.

**How it works:** defines who owns state (who mutates round, quest or NPC state) before writing logic, makes cleanup scopes explicit (round, player, character), handles late join and respawn, and verifies one full loop from start to finish. It reads the gameplay, character and input references, and social and teleport for rounds and matchmaking.

**You get:** the implemented loop with its state ownership documented in the code and a report of the scenarios checked.

**Try:** `/roblox-dev:gameplay a round system with lobby, intermission and late join`.

#### `combat <task>`

**For:** weapons, abilities, cooldowns, damage and PvP.

**How it works:** treats every client combat message as a request and validates shape, range, line of sight, cooldown and state on the server. Shared checks (cooldowns, can-activate) live in one parent system and abilities are sub-systems that ask it, so a rule change happens once. It verifies one full hit-to-damage flow, including a rejected invalid request.

**You get:** a server-authoritative combat flow, with the validation rules listed.

**Try:** `/roblox-dev:combat melee swings with server-side hit checks and cooldowns`.

#### `ui <task>`

**For:** menus, HUDs, shop screens, screenshot-inspired interfaces and UI fixes.

**How it works:** follows the UI design references (components, patterns, platform, accessibility, verification). UI stays inside its system, tool UI is named `<toolName>Tool`, and ScreenGuis are shown and hidden explicitly in code instead of relying on `ResetOnSpawn`. It provides buy-one and buy-max style options where players repeat an action, places purchase offers where players already are, and never shows offers before the player is invested. It checks phone and desktop sizes, safe areas and gamepad focus. An installed UI-design skill can help with screenshot references but is not required.

**You get:** the screen or the fixes, with the states, sizes and inputs it checked.

**Try:** `/roblox-dev:ui a mobile-friendly shop screen with a clear price and odds panel`.

#### `world <task>`

**For:** maps, terrain, collisions, StreamingEnabled problems and layout.

**How it works:** places scripted objects under `Workspace.Scripted.<SystemName>` and tags them with CollectionService instead of fixed paths, accounts for streaming (instances may not exist on the client), and uses level design to show the threat or goal early and, when the game has a social element, to make other players' progress visible.

**You get:** the world change with notes on streaming behavior and tags used.

**Try:** `/roblox-dev:world fix floating parts when the map streams in`.

### Fix and improve

#### `fix-bug [diagnose or playtest] <bug>`

**For:** errors, broken behavior and console messages.

**Modes** (chosen if the first word is exactly `diagnose` or `playtest`):

- **diagnose:** reads the console and the involved scripts fully, forms a hypothesis from evidence, confirms it (one playtest allowed only to confirm), and reports cause and minimal fix. Edits nothing.
- **playtest:** runs exactly one short playtest of the described change or flow, reads console and state, and reports pass or fail with evidence.
- **default (fix):** reproduces the trigger, finds the observed root cause, fixes it with the smallest change in the owning system, and checks the original trigger. At most one playtest covers both reproduction and verification. It loads the matching area reference (for example persistence for save bugs, monetization for receipt bugs).

**Guardrails:** no speculative rewrites and no retry loops without new evidence.

**Try:** `/roblox-dev:fix-bug diagnose data not saving on leave`, `/roblox-dev:fix-bug playtest the new shop buttons on mobile`.

#### `performance [system or symptom]`

**For:** lag, low FPS, memory growth, network cost and slow loading.

**How it works:** collects evidence first (profiler notes, memory and ping observations, script activity), ranks causes by impact, fixes the clear ones with minimal changes (batching, throttling, pooling, disconnecting, streaming) and re-checks the original symptom. It reads the performance and world references.

**You get:** the ranked causes, the changes made and the before and after observation.

**Guardrails:** it does not claim device numbers it did not measure.

**Try:** `/roblox-dev:performance lag during egg hatching on phones`.

#### `save-data <task>`

**For:** player data: saving, loading, session ownership, retries, migrations and data loss.

**How it works:** reads the existing save code and lists every key and field in use. It covers session ownership, load-failure handling (never overwrite good data after a failed load), save on leave and in `BindToClose`, retries with backoff, and access to data only through the owning system's API.

**Guardrails:** **it asks before changing any existing key or schema.** Migrations are versioned and reversible, never run against live or published data, tested on a copy or a fresh key, and come with a rollback path.

**Try:** `/roblox-dev:save-data add a versioned profile migration for the new pets table`.

#### `economy <task>`

**For:** currencies, inventory, crafting, trading, shops and monetization code.

**How it works:** keeps transactions server-authoritative and atomic, balances change only through the owning system's API, and economy events are logged there. It models sources and sinks before adding paid convenience and checks side effects on play time and retention. Paid random items (eggs, rolls, crates, luck boosts, pity) must show every outcome with its odds.

**Guardrails:** **it asks before changing any price, product ID, pass ID or receipt handler, and never creates, publishes or buys products or spends Robux.** It hands back the exact values for you to enter in Creator Hub, and follows your price convention if you have one.

**Try:** `/roblox-dev:economy review the shop purchase flow and the odds display`.

#### `analytics <stat or feature>`

**For:** knowing where players drop off or how the economy flows.

**How it works:** adds events only where a stat needs diagnosis: economy events (sources and sinks per currency) and funnel steps (every micro-step of onboarding, shop and rounds). Calls come from the server in the owning system's API, names are stable and documented, volume respects the rate limit, and it tells you how to verify events in the Creator Hub after publishing a test build (events do not arrive from Studio).

**Guardrails:** it does not publish for you.

**Try:** `/roblox-dev:analytics funnel for the tutorial and the first purchase`.

### Restructure and tidy

All four are user-invoked only because they move, delete or export.

#### `backup [target folder]`

**For:** a safety copy before anything risky.

**How it works:** exports every Script, LocalScript and ModuleScript source with its path, plus a tree listing (with attributes and tags) of the other containers, into a timestamped folder `_backup/YYYYMMDD-HHMMSS` (valid on Windows). It never overwrites a backup, asks for a target folder if none is obvious (and for approval if it is outside the project), and prefers a commit or copy when the project is managed by Rojo or git.

**You get:** the backup location plus reminders: save a copy of the place file too (script exports cannot restore UI, models or terrain), add `_backup/` to `.gitignore`, and never publish the backup because scripts can contain secrets.

**Try:** `/roblox-dev:backup`.

#### `cleanup [scope]`

**For:** dead code, commented-out code, debug prints and unused assets.

**How it works:** finds candidates, confirms a backup exists, and verifies each candidate is unreferenced (names, tags, attributes, `require` strings, DataStore-related names). Anything that could be referenced dynamically (names built from strings, `FindFirstChild` with variables, attributes or tags read elsewhere) is "unverifiable" and never a candidate.

**Guardrails:** it lists every candidate with path and evidence and **asks for approval; it never deletes on its own.** Approved assets move to a `Trash` folder first; real deletion only on your explicit say-so. Genuine error warnings stay, and behavior does not change.

**Try:** `/roblox-dev:cleanup scripts only`.

#### `refactor-system <Name>`

**For:** bringing one existing system onto the architecture conventions without touching the rest.

**How it works:** runs the backup procedure (checking whether Rojo or git owns the sources), inventories the system's scripts, assets and outside consumers, shows the plan (moves, API, renames) and **waits for approval**. Then it moves files into system folders, adds the API with the right suffix, routes every outside consumer through it, applies the script layout and naming, and removes dead code and debug prints. Other systems change only where direct access is replaced by an API call.

**Guardrails:** persisted names unchanged, every broken `require` path fixed, one verification at the end.

**Try:** `/roblox-dev:refactor-system Pets`.

#### `restructure [notes]`

**For:** reorganizing a whole codebase into systems with APIs. Use it only when you explicitly want the entire project reorganized.

**How it works:**

1. Runs the backup procedure and **does not migrate until you confirm you also saved a copy of the place file.** It checks whether Rojo or git owns the sources.
2. Audits read-only and writes `RESTRUCTURE_AUDIT.md`: proposed systems and sub-systems, cross-system accesses and the API that replaces each, dependency-direction violations, dead assets and name collisions.
3. **Stops and presents the plan.** It migrates only after you approve, and asks separately before renaming persisted data, deleting or moving assets that may be in use, or renaming remotes.
4. Migrates one system at a time using the `refactor-system` procedure, keeps the game working after each, and runs one short sanity check per system.
5. Finishes with `cleanup` (with its approvals) and a report: what moved, which APIs exist and what it was unsure about.

**Try:** `/roblox-dev:restructure`.

### Grow the game

#### `growth <stat or goal>`

**For:** improving a weak stat with evidence instead of guesses.

**How it works:** the hypothesis loop.

1. Gets the current stats from you (play-through rate, bounce, play time, D1, D7, D28 or D30, conversion, ARPPU). It never invents dashboard numbers.
2. Picks the single weakest stat and gathers three kinds of evidence: player feedback, metrics and competitors (asking you, or using `market-research`).
3. Writes the hypothesis: if I add, remove or improve X, stat Y improves.
4. **States the hypothesis and waits for your yes before editing**, then implements it in the owning system, adding analytics only if the result could not otherwise be measured.
5. Tells you how and when to check results (the data window, side effects on other stats).

It reads the discovery, iteration, onboarding and analytics references, plus packaging for CTR problems and the monetization playbook (with its caution about minors) for conversion problems.

**Guardrails:** no pricing changes, publishing or live-setting edits without approval.

**Try:** `/roblox-dev:growth D1 retention is 8 percent, here are my funnel numbers: ...`.

#### `packaging <game and part>`

**For:** title, thumbnails, detail page and sponsored ads.

**How it works:** checks the core fantasy, the reading level of the title, the implied challenge, honesty compared with the first minute of play, and legibility on phones. It produces 5 to 10 thumbnail concepts and 5 title options with reasons, a detail-page plan, and an ads protocol (the budget is your decision). If an image-generation skill is installed it uses it only when you ask.

**You get:** a plan to hand to your artist or tool, plus a test plan for comparing creatives.

**Guardrails:** it never publishes or spends Robux, and packaging must truthfully reflect the game.

**Try:** `/roblox-dev:packaging title and thumbnails for my pet game`.

## Safety model

- **Approval gates.** Nothing is published, purchased, priced, deleted or migrated against live data without an explicit yes in the current conversation, and approval for one action does not carry over to the next. The shared rules are in `skills/roblox-dev/references/command-rules.md`.
- **User-invoked only:** `backup`, `cleanup`, `restructure`, `refactor-system`, `full-audit`, `release-check`.
- **Read-only commands** (`onboard`, `full-audit`, `release-check`, `market-research`) never edit your place. Report files are never overwritten.
- **Backups before big moves**, including a reminder to save a place-file copy, because script exports cannot restore UI, models or terrain.
- **Project conventions win** over the plugin's architecture style.
- **Honest reports:** what was verified, how, and what was not.

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

## Limits

- The plugin is guidance plus guardrails, not a game template or runtime library. It cannot see your Creator Hub dashboard: you provide the numbers.
- Without Studio MCP everything is offline: it produces source and instructions, and states which checks were not run.
- Roblox rules change (for example the Kids and Select engagement threshold). Facts carry "verify" notes; re-check version-dependent claims in the official docs.
- The commands have not been exercised end to end across many projects. Please open issues for anything that does not behave as described.

## Status, license and credits

Version 0.1.0. Manifests, frontmatter and internal links are checked by script. Roblox facts were checked against the Creator Hub in October 2026.

MIT License. See [LICENSE](LICENSE). Sources and credits: `skills/roblox-dev/references/sources-attribution.md`.

Roblox and other game names mentioned here are trademarks of their respective owners; this project is not affiliated with or endorsed by Roblox Corporation.
