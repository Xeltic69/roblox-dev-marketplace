# NPCs, quests, dialogue, rounds and checkpoints

## NPC decision and navigation

Separate perception, decision, path computation, movement and visual feedback. Begin with a small state machine; a behavior tree is optional when actual complexity warrants it. Define target eligibility, aggro/leash thresholds, lost-target, unreachable-goal and death behavior. Validate targets again after yielding work.

Follow current [pathfinding guidance](https://create.roblox.com/docs/characters/pathfinding). Check computation failures and success, use agent dimensions that fit level geometry, and process waypoint actions. A Blocked notification only matters to the remaining route; an obstacle behind the agent should not trigger endless recomputation. Do not share one mutable path across simultaneous computations without serialization. Own route connections and discard results from an obsolete target/state generation.

Stagger thinking and navigation based on measurements; do not recompute every frame for every agent. Direct movement needs terrain/traversal awareness as well as line of sight. Selective server physics ownership may protect important NPC outcomes but adds load/responsiveness tradeoffs. Test simultaneous agents, dynamic doors, narrow paths, jumps, unreachable goals, target respawn and despawn.

## Quests, dialogue, and interactions

Separate versioned quest definitions from per-player progress and claim state. Use stable objective/choice IDs and authoritative events. Give repeated objective events and reward claims an idempotency policy. Reconnect reconstructs progress/markers from accepted state, not merely a series of past client events.

Dialogue is a graph of text keys, conditions and choice IDs. Client handles reveal, skip and focus; server verifies the current conversation, legal choice, prerequisites and relevant proximity before consequential outcomes. Conversation identity prevents delayed input from an earlier session. Define interruption on death, combat, leaving, timeout and target disappearance.

ProximityPrompt, ClickDetector and drag interactions are affordances, not complete authorization systems. Validate context/rate/ownership for outcomes rather than assuming all events enforce distance. See [security boundary](https://create.roblox.com/docs/scripting/security/client-server-boundary). Filter player-authored text before displaying to others and escape rich-text markup separately; see [release-liveops.md](release-liveops.md).

## Rounds and spawning

A round has ID, phase, deadline, participants, eligibility and accepted outcome. Use a controlled dispatcher/state machine instead of recursively entering the next phase forever. Delayed callbacks capture the round ID. Define late join, respawn participation, disconnect, no players, ties, aborted map loading, spectators and reward delivery.

Late joiners receive a snapshot/revision; presentation countdowns derive from a shared authoritative deadline. Validate map/spawn availability before moving players. Reward once per accepted round/participant; cleanup handlers, loot and effects before starting the next round. Team-aware spawning is a separate design choice from round participation; inspect [SpawnLocation](https://create.roblox.com/docs/reference/engine/classes/SpawnLocation).

For checkpoints, treat touch as candidate evidence. Verify active route, next allowed checkpoint, character and plausible proximity under game rules, then record a stable checkpoint ID and safe respawn placement. Touch can repeat; duplicated activation must not double-grant or skip sequence.

If two touch callbacks both wait for feedback before incrementing progress, commit the explicit accepted checkpoint first through the sole state owner without yielding. Feedback has no authority to change progress. Illustrative transition after synchronous eligibility/character/route checks:

```luau
if nextCheckpointStage ~= currentStage + 1 then
    return -- duplicate or out-of-order candidate
end
currentStage = nextCheckpointStage -- explicit accepted stage before async feedback
-- Schedule cosmetic feedback separately; recheck character/round generation there.
```

This excerpt is a local transition pattern, not a complete touch validator or persistence adapter. Test both completion orders of delayed feedback and verify that errors/respawn cannot advance a second time.

## Check

Run two full round cycles, late join, leave during rewards, death in each phase, stale callbacks, map failure, NPC target destruction, repeated quest claims, interrupted dialogue and long translated choices. Use representative populations; one agent on an empty baseplate is not scale verification.
