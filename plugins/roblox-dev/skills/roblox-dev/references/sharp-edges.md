# Sharp edges: always-on checklist

Frequent, high-impact mistakes. Check these on every task that touches the area; details live in the linked references. Ranked by damage.

| # | Severity | Mistake | Do instead |
| --- | --- | --- | --- |
| 1 | Critical | Player data lost: raw overwrites, no session ownership, saving over a failed load | Own the session, update atomically, never save when the load failed ([persistence](persistence.md)) |
| 2 | Critical | Client decides currency, damage, inventory or position | Client sends intent; the server validates and mutates ([networking and security](networking-security.md)) |
| 3 | Critical | Purchase handled non-durably: duplicate grants, lost grants, refund abuse | Persist the grant with the receipt id before confirming; make receipt handling idempotent ([monetization](monetization.md)) |
| 4 | Critical | Paid random items without visible odds | Show every outcome and its odds (sum 100%) before purchase ([reward design](reward-design-random-items.md)) |
| 5 | High | Remote flooding or unbounded payloads | Per-player rate limits, type/size checks, reject early |
| 6 | High | Leaked connections, threads and instances after respawn, leave or screen close | One cleanup scope per lifetime (game, player, character, round, screen); idempotent cleanup ([Luau and architecture](luau-architecture.md)) |
| 7 | High | Work after a yield acts on stale state (player left, character died, view closed) | Re-check generation/prerequisites after every yield |
| 8 | High | Data not saved at shutdown or leave; long shutdown work | Save on leave and in `BindToClose` with parallel, bounded work ([persistence](persistence.md)) |
| 9 | High | Trusting `Instance` paths that may not stream in or replicate yet | Bounded waits with an explicit unavailable state for runtime-created or replicated instances; handle StreamingEnabled ([world and physics](world-physics.md)) |
| 10 | Medium | UI that works on desktop only | Test phone, console focus, safe areas ([onboarding and UX](onboarding-retention-ux.md)) |
| 11 | Medium | Economy sources without sinks; paid convenience that breaks pacing | Model sources/sinks, log economy events ([analytics events](analytics-events.md)) |
| 12 | Medium | Debug prints, commented-out code, dead assets left behind | Clean before finishing ([architecture conventions](architecture-conventions.md)) |
| 13 | Medium | Testing only in Studio or on a progressed account | Focused playtest on a live or test place with a fresh account |
| 14 | Medium | Secrets in replicated containers or client-readable scripts | Keep keys server-side or external ([Open Cloud](tooling.md)) |
