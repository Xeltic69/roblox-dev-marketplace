# Shared rules for every /roblox-dev command

Each command reads this file first. Command-specific steps and gates add to these rules, never replace them.

## Before acting
1. **Inspect the real project** (Studio via MCP, or the source files) before changing anything. See [Studio MCP](studio-mcp.md). If nothing is connected, work offline and say so.
2. **Architecture conventions** ([architecture conventions](architecture-conventions.md)) apply to all code you write or substantially edit, **unless the project already uses another convention**. In that case follow the project for existing code, use the conventions only for new systems if the owner wants them, and mention the mismatch.
3. Skim the [sharp-edges checklist](sharp-edges.md) for the area you touch.

## While working
- Change only what the request needs. No behavior change beyond the request; keep persisted names (DataStore keys, product and pass IDs, attribute names used by saved data) unchanged unless the owner agrees.
- Smallest appropriate implementation. No new framework, dependency or service because it is fashionable.
- Where a reference labels a Roblox claim as verified, unverified, beta or creator opinion, respect the label. Do not turn creator heuristics into rules, and re-check version-dependent facts in the official docs.
- One focused playtest per change; no repeated verification of the same thing. If the task names multi-client, lifecycle or failure scenarios (late join, respawn, two players), run exactly those scenarios, no more.

## Approval gates (ask first, wait for a clear yes)
Never do these without explicit approval in the current conversation: publish a place or update, spend Robux or ad budget, change prices, products, passes or receipt handlers, delete or overwrite assets and data, run a migration against live or published data, send external messages, change settings unrelated to the task, or write outside the project folder.
Approval for one action does not extend to the next.

## Reports and files
- Read-only commands (audits, checks, research) change nothing in the place. Any command that writes a report or audit file must never overwrite an existing file: use `<NAME>-<date>.md`, or return the report in chat if there is no project folder.
- Finish with a short report: what changed, where it lives, what was verified (and how), what was not verified, and the sensible next command.
- Distinguish source inspection, fixture results, Studio play mode, device checks and live behavior. Never claim a pass without evidence.
