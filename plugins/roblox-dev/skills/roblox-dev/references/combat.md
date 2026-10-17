# Combat and abilities

Define action IDs, legal states, startup/active/recovery windows, cost, equipment, targets, cancellation and replay policy. The client may predict cosmetics; authoritative health, resources, cooldowns, eligibility and rewards come from accepted server actions.

## Validate before expensive work

Treat a remote action as a request. Check shape and cardinality, finite numeric/vector values, bounded distance, current character generation/alive state, equipped/owned weapon, ammo/resources, legal timing, cooldown, target rules and line of sight. Reject NaN, infinity, zero direction and oversized payloads before normalization or spatial queries. Do not accept a client-supplied damage amount or arbitrary target list. See [client/server security](https://create.roblox.com/docs/scripting/security/client-server-boundary).

Rate limits protect processing, while a serialized/guarded mutation path protects state during concurrent actions. These are different controls. Deduplicate accepted attacks/reward events by a scoped identity when replay could double-grant. Avoid automatically punishing lagging players from a single uncertain observation.

## Choose detection

| Attack | Useful starting approach | Edge case |
| --- | --- | --- |
| Hitscan | Server validation and ray query | Occlusion, finite range, aim origin plausibility |
| Fast projectile | Swept query or authoritative simulation | Tunneling, spawn overlap, lifetime and cancellation |
| Melee/area | Spatial overlap or sweep over accepted window | Multiple limbs, repeated frames, team eligibility |
| Persistent zone | Bounded membership checks and tick policy | Re-entry, owner leaving, effect stacking |

Ray direction includes its magnitude; client queries can miss streamed geometry. An authoritative query still depends on plausible attacker/target positions when movement is client-owned. Consult [raycasting](https://create.roblox.com/docs/workspace/raycasting) and [WorldRoot spatial queries](https://create.roblox.com/docs/reference/engine/classes/WorldRoot). Deduplicate character identities rather than awarding once per hit part.

## Latency and simulation

Choose the game's hit policy explicitly. Competitive compensation may need bounded server-observed history, a limited rewind window and carefully constrained client timestamps. Re-querying current positions alone is not full lag compensation. Read current [server-authority guidance](https://create.roblox.com/docs/projects/server-authority) before adopting rollback simulation; feature availability and API requirements must be checked. Keep cosmetic side effects out of resimulated logic.

Status effects specify identity, source, stacking/refresh rule, expiry, generation and cleanup. Derive final speed/damage from modifiers so ending one effect does not reset others. Death/respawn invalidates old effects. Animation track markers can time cosmetics; they are not sufficient authority for damage.

## Verification

Test walls, friendly fire, duplicate hit parts, out-of-range requests, zero/NaN/infinite vectors, repeated actions, death during attack, cancel/re-equip, high latency and two distinct client views. Inspect hit/miss/block cues and resource reconciliation. See [Studio testing](studio-testing.md); do not call a server-side print a validated combat flow.
