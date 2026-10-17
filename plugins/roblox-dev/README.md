# roblox-dev

Roblox game development for Claude Code. One router skill (`roblox-dev`) loads a shared reference library on demand, and namespaced commands (`/roblox-dev:<name>`) cover common actions. It works with the official Roblox Studio MCP server (or any other Studio MCP) and falls back to offline source delivery when Studio is not connected.

## Commands

| Group | Commands |
| --- | --- |
| Build and change | `new-game`, `add-feature`, `new-system`, `refactor-system`, `restructure`, `cleanup`, `backup`, `onboard` |
| Fix and verify | `fix-bug` (modes `diagnose`, `playtest`), `full-audit` (all areas or one, e.g. `security`), `release-check`, `performance` |
| Systems | `save-data`, `economy`, `combat`, `gameplay`, `ui`, `world`, `analytics` |
| Growth | `growth`, `packaging`, `market-research` |

Example: `/roblox-dev:full-audit security economy`, `/roblox-dev:fix-bug diagnose shop buttons do nothing on mobile`.

## Safety model

- Commands that move, delete, bulk-export or write report files (`backup`, `cleanup`, `restructure`, `refactor-system`, `full-audit`, `release-check`) are user-invoked only; other commands edit the project only within the scope of your request.
- Nothing is published, purchased, priced, deleted or migrated against live data without an explicit yes in the conversation. See `skills/roblox-dev/references/command-rules.md`.
- Audit commands write one report file and never overwrite an existing one.
- Project conventions win: the architecture conventions apply to new systems and substantially edited scripts unless the project already uses another convention.

## What is inside

- Architecture conventions, networking and security, persistence, economy and monetization, combat, gameplay, UI, world, performance, tooling and Open Cloud, release checklist, analytics events.
- Creator-derived notes on discovery, packaging, ideation, onboarding, iteration and monetization. These are paraphrased practitioner heuristics, labeled by evidence level ([Docs], [DevForum], [Creator]); they are not Roblox rules.
- Roblox facts were checked against the Creator Hub in October 2026 and carry "verify" notes where they may change.

## Status

Version 0.1.0. Manifests, frontmatter and internal links are checked by script. Commands have not been exercised end to end across many projects; report problems in the repository issues once the repository is published.

## License

MIT. See [LICENSE](LICENSE). Sources and credits: `skills/roblox-dev/references/sources-attribution.md`.

Roblox and other game names mentioned here are trademarks of their respective owners; this project is not affiliated with or endorsed by Roblox Corporation.
