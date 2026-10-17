# Parties, teams, matchmaking and teleports

Define authoritative party membership, leader transfer, capacity, invitations, expiration and cancellation. Keep shared membership separate from client UI selection. Changing teams or joining after a round begins must respect the game's participation rules. Trade has a separate final-offer/transaction contract in [economy-transactions.md](economy-transactions.md).

Choose platform matchmaking/server scoring when it fits the desired party/mode/skill/capacity behavior; consult current [matchmaking guidance](https://create.roblox.com/docs/matchmaking). A custom distributed queue is optional, not a standard prerequisite. If needed, it requires deduplicated claims, short-lived reservations, a match identity and crash recovery. MemoryStore queue invisibility is temporary, not proof an entry is permanently processed.

## Server handoff

Create authoritative match membership/config and destination before sending players. Configure access appropriate to private subplaces. Short-lived matching metadata can use TTL storage; durable inventory/rewards remain in canonical profiles. Do not trust TeleportData as permission, ownership or currency.

Use server-side TeleportAsync with verified destination/options. A successful call initiates a transition; handle later TeleportInitFailed and partial party departure. Retry only retryable failure cases with bounded backoff and an active attempt ID. A new attempt must invalidate old retry work. Preserve/reacquire profile ownership correctly after failure, rather than leaving the player in a stranded released-profile state.

Destination validates membership and obtains authoritative data. Handle missing arrivals, expired admission, late arrival, cancellation and duplicate results. Rewards after match completion use a stable operation identity so repeated result delivery cannot grant twice. Public server-browser entries need heartbeats/TTL and removal of stale entries.

See [teleport documentation](https://create.roblox.com/docs/projects/teleport) and [MemoryStore](https://create.roblox.com/docs/cloud-services/memory-stores). End-to-end TeleportService behavior requires a published test experience/client; Studio can verify local adapters and transition state but cannot certify actual cross-place arrival.

## Verify

Party member leaves, leader leaves, capacity races, expired invite, simultaneous queue joins/cancel, lost claim, partial teleport, repeated init failure, duplicate completion and destination data load failure. Distinguish isolated deterministic transition tests from actual platform handoff evidence.

## Teams and permissions

For team games use the `Teams` service and keep team membership authoritative on the server. Gate admin or moderator features on the server by group role (the older `Player:GetRankInGroup` is deprecated; use the current group API from the docs, for example `GroupService`, on the server) or an allowlist of user IDs, never by a client flag. Team Create (collaboration) permissions are separate from in-game roles.
