# Game design building blocks (creator field notes)

Practitioner heuristics from one producer's videos (see [sources-attribution.md](sources-attribution.md); extends [game-design.md](game-design.md)). Game design (rules, systems, what the player does and how they win) is the most valuable skill; development is execution. These are observed patterns, not laws.

## Games as swappable building blocks

Popular trend games are mechanically similar under the hood and differ in a few areas that matter. Map the reference games in your niche in a table and decide where to innovate.

| Block | What it means | Examples |
| --- | --- | --- |
| Fantasy | The primary verb/role | Ride a pet, steal an egg, escape with valuables, kick, dig up treasure, save animals, raise a pet |
| Unique mechanic | What makes the loop different | Exploration with simulator progression; stock-refresh timer applied to the world (eggs restock every 5 min, from Grow a Garden seeds); pressure-valve level design; kick skill-check; cleaning mechanic; feeding |
| Core loop | Usually "leave base, get thing, return" | Nearly all |
| RNG placement | Spawn-table roll in the world vs. roll after acquisition (hatch at base) vs. pre-acquisition (kick the block) | Differs per game |
| Level design | Linear runway, open map, sky islands | Linear in escape/steal/kick games |
| Tension | Source of "just made it" moments | PvE chaser, tsunami, countdown timer on an egg, PvP on top of PvE (steal an egg) |
| Progression | Get faster, stronger, collect | |
| Collection | Pets, treasure, characters, sandwiches | |
| Audience | Who the fantasy attracts | The creator guesses a rescue-animals fantasy may attract a mostly female audience (check your own demographics) |

How to use it: Never reuse another creator's names, art, audio, UI, code or thumbnails; adapt mechanics and fantasy only. Pick a reference game and **change at least ~20%**, in areas that matter (fantasy, unique mechanic, level design, tension, audience). The creator's unvalidated estimate is that ~20% suffices for roughly 1-5K, maybe 10K CCU, and that larger games stack several meaningful innovations (a ride-a-pet-style game changed about 40%); "Pareto" here is a loose analogy, not a measurement. A "clone" with a meaningful twist to the core loop is acceptable; a reskin is not (see [discovery](platform-discovery-metrics.md)).

Pressure-valve level design: tension rises while running to get the thing, with safe troughs where the player can choose to continue; compare with constant tension until a safe zone.

## What makes a game sticky and viral (five factors from the viral-games videos)
1. **Clickable idea / strong core fantasy.** A scenario kids imagine ("animals run a hospital"). The player should be unable to resist clicking when they see the packaging.
2. **Great onboarding.** Explain *why* the action matters; emotional investment within about 90 s (cutscenes help bounce rate); one mechanic at a time ([onboarding](onboarding-retention-ux.md)).
3. **Socialization.** The game should be much more fun with friends so friends invite friends (word-of-mouth flywheel). Add a **social flex element** (leaderboards, visible progress, cosmetics, level design that shows other players' progress immediately, a fast player zooming past you). Allow co-op, free private servers, friends helping build. One top game reported a 42-minute average play time on a Sunday two weeks after launch and attributes it to PvP, co-op and free private servers (the creator's attribution, not proof).
4. **Simple mechanics with deep systems ("depth versus complexity").** One mechanic with many outcomes (voxel building, one RNG mechanic, role-play, base-building vs. stealers). Every session should feel different. PvP is replayable because other players create unsolved situations; PvE build-to-survive games, per the creator, tend to become a solved strategy within about 5 minutes. Simplify: *simple scales, fancy fails*; every feature needs a clear, immediate cause and effect; the creator estimates most players are around 9 years old (check Audience demographics).
5. **Clippable and community-driven.** Imagine a creator playing: funny moments (hitting a thief into the void, ragdolling), builds that others tutorial (F-22 builds), hiding spots. Watch which moments YouTubers keep and react to; that is free advertising. A strong community creates content for years.
Also: excellent mobile/console UX, social flex, replayability (curiosity hook for tomorrow), strong monetization, a tight fantasy. The creator's claim that all five guarantee a large audience is anecdotal.

## Evergreen genres and PvP stealing
- "Build to X" is an evergreen demand genre; a PvP version was a gap. A loop of roll rare pets → defend/build base → get stolen from → rebuild with new traps is a tight, unsolvable feedback loop. Combine two forces: an evergreen demand (building) and a proven mechanic (stealing).
- Do not copy mechanics blindly: an auto-roller suited an AFK game but broke a PvP game's economy (endgame content in 3 hours). Remove unsuitable convenience; remove roll-speed upgrades that destroy the economy.
- The creator staged the first roll to flash rare animals to build curiosity; that scripted tease can mislead about odds, so show the real outcome pool instead of staging near-misses. Pets cost in-game cash, and a luck upgrade the player cannot afford can offer a Robux purchase; the creator reports payer conversion rising from about 0.3% to about 0.75% blended across countries (about 2% for the U.S.). Robux-purchasable cash or luck used for rolls is a paid random item: show every outcome with its odds and do not stage rare near-misses ([reward design](reward-design-random-items.md)).
- Keep the map small and fast: a large map with boats slowed play. Use a center island/level design to add juking, vines, obbies, or rotating biomes (mushrooms every ~15 min) for variety.
- Mechanic examples that worked: base lock as the first tutorial step (signals PvP without text), buy 1/buy max on upgrade boards (copy from an incremental game), 24 h base lock as a consumable.

## Level design guidance
Use proven layouts that players already understand (Grow a Garden 2 plot spacing; Bedwars islands) and change ~20% (sky plots, bridges, void knockback). A world should make the threat visible within 5 seconds (tsunami waves at spawn). Use level design to show other players' progress without zooming out; a game whose plots have walls hid its social flex.

## Fantasy-fit trade-offs
Sometimes the best design choice conflicts with the fantasy (an indoor cafe hides other players' progress; an outdoor cafe would show it). Note such conflicts instead of ignoring them.

## Replayability and retention hooks
Collection and index completion, emotional attachment to pets, sunk cost (hours invested in a base, Robux-bought pets), rare items to flex, strong curiosity hook for tomorrow ("what new base can I build, what pet can I unlock"), events tied to the index, AFK-friendly collection where the genre fits. Verify that retention hooks do not come at the cost of fairness.

## Co-op, PvP, polish
Co-op play that is intentionally designed can carry a low-monetization game (a survival game stayed alive via very high intentional co-play versus benchmark). PvP needs anti-grief rules, free private servers for players who want to build in peace, and a base lock.

Note: the creator observes that one egg game stacked FOMO, urgency and scarcity on top of PvP. Use only real, disclosed scarcity and avoid pressure tactics aimed at young players ([reward design](reward-design-random-items.md)).
