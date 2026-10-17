# Iteration, LiveOps and playtesting (creator field notes)

Practitioner heuristics from one producer's videos (see [sources-attribution.md](sources-attribution.md)); complements [release-liveops.md](release-liveops.md) and [studio-testing.md](studio-testing.md). The user decides cadence and scope; do not impose a weekly rule.

## The iterative hypothesis loop

Every update is an educated guess (hypothesis): *If I add / remove / improve X, then stat Y improves.*

1. **Research** three data sources and cross-reference them (each source gives the hypothesis legs):
   - **Qualitative** (weight by source: a game's Discord core is expert but sweaty, while the group forum skews young and complaining): voice of the player: Discord bug reports/suggestions, community forum, the Creator Hub Audience → Feedback page (votes and comments; the AI summary the creator mentions is unconfirmed there, the Creator Hub Assistant can summarize player feedback), in-game feedback mailbox, surveys, watching players live (the most overlooked), YouTube videos of small players.
   - **Quantitative**: funnels, new user first session retention curve, D1/D7/D28, play time, conversion, ARPPU.
   - **Competitors**: top games in the genre/for the same audience. Does the feature exist there? Also use players' server tags and "what else do you play" answers.
2. **Form the hypothesis** in writing, naming the stat.
3. **Ship** the update. Optionally A/B test config-driven changes with Experiments (14-60 days, up to two variants plus control).
4. **Check results** after the data window (about 24 h to several days; rolling window; the creator says 7 days, the docs do not state it). Also check side effects: did a new product hurt play time, D1, D7, session time, first-time experience?
5. **Keep or revert.** If it did not help, revert and form a new hypothesis. Repeat.
Example: players asked to collect from several servers at once → competitor has it → 2:30 drop in the first-session curve → hypothesis: allow collecting from all servers, play time improves → shipped.

## Pick one stat and focus
Pick the worst stat and work only on it until it improves. One game cut bounce rate from 21% to about 15%; the creator credits that change for a clear rise in concurrent players (his attribution, other factors unknown). Update daily or even twice a day in the first weeks; keep patches separate from larger updates.

Fix directions per stat:
- Average play time low → core loop not satisfying (action/response, sound, VFX, camera shake), add random events/collection.
- D1 low → onboarding; measure funnels, device-slice.
- D7 low → events (admin abuse/weekly events), content depth, social flex.
- D28 → deeper systems (index).
- Payer conversion low → cheap starter pack, consumable dev products.
- ARPPU low → expensive passes for whales, three tiers (small/medium/large).
- PTR low → packaging. Bounce high → expectation mismatch, cutscene.

## Patches versus updates
- **Patches**: bug, glitch, exploit fixes, small nerf/buff, monetization tweaks. Daily, same day for game-breaking issues or exploits (anti-cheat hotfix cannot wait for Saturday).
- **Updates**: weekly, later biweekly, targeted at metrics, based on player feedback, intentionally extending content. Useless updates (one skin) that do not create engagement are wasteful.
- Example weekly cadence (producer's): Saturday event/update → plan next update that day → Sunday assign work, sign off, hand to freelancers → Mon-Wed build and review → Thursday ready → Friday internal playtest, then playtest with core players → Saturday launch. Not ideal; some studios plan months ahead.

## Do and don't (LiveOps)
Do: listen to the audience and talk with them in Discord (players love an active dev); test updates before launch; watch YouTubers/small players for friction; hire a team incentivized to do good work; focus updates that extend content (D28); use polls; keep improving; internal live ops team may beat a big studio that treats the game as a number.
Don't: prioritize monetization over gameplay (pay-to-win kills games); ship at the last minute; implement every suggestion (granting the rarest pet to everyone fries the economy; players are right about problems, not always about solutions); push updates with no engagement effect; abandon the game when it earns.
Core community: keep a dedicated group (8-10 testers), plan updates with them, give them early access; use their server tags to find reference games.

## Playtesting
- Keep a **published test place** and test on live Roblox, not only Studio (some bugs appear only live); separate from the live game.
- Hire QA testers (e.g. QA Central Discord) or reuse a loyal group; pay in Robux. Testers find economy-breaking exploits (a tester farmed a quadrillion cash).
- Test on a **fresh alt account** to feel the first minutes.
- Be on top of your own game's play time leaderboard.
- Launch earlier than you think once the core loop is solid; real data beats months of guessing. Avoid building for months in isolation: "the real work begins when you get data". An edge case: a polished game flopped, a competitor copy with a slightly different map hit 10K; you can be one update away.

## Progression balancing (data-first, no spreadsheet math required)
Combine: your own timeline on a fresh account, funnels on each progression milestone (first/second/Nth upgrade purchase, zone reached, plot upgrade rate), paid tester logs (3-hour grind with item, cost, time, stuck points), and the reference game's curve. Feed these to an AI model as a brainstorming aid. A balancing wall in the first 5-10 minutes depressed D1 to 6-8% until fixed. See details in [creator lessons](creator-lessons-simulator-launch.md).

## Production cycle for a new game (creator process)
Market research → game design document → scope into a task board (Trello columns per discipline) → build models/builds/UI for the core loop first → programmer brings the loop to life (MVP) → playtest → launch (start ads, read feedback) or prototype tweaks in a copy with AI before returning to the programmer ([team and production](team-production-mindset.md)).

After launch expect to nerf the economy several times (creator's experience). Many contractors on Roblox are minors; see [team and production](team-production-mindset.md) for safe handling.
