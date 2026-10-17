# Onboarding, retention and UX (creator field notes)

Practitioner heuristics from one producer's videos (see [sources-attribution.md](sources-attribution.md)). Extends [creator-lessons-simulator-launch.md](creator-lessons-simulator-launch.md) (frictionless first 90 s, contextual tutorials, progression testing) with details from the other videos. Validate against your own funnels; none of this is a rule of the platform.

## Goals of the first minutes
- Within 30 s deliver the promise of the title (a game whose title promises building starts with building in the first 10 s; a farm game leads with planting). Lead with the **most engaging mechanic**. Delivery of the title promise lowers bounce rate ([metrics](platform-discovery-metrics.md)).
- Within 60-120 s make the goal obvious, show how to progress and open a **curiosity loop** (what will other buildings look like, how big can it get).
- Emotionally invest the player in about 90 s: show *why* they should care ("survivors are sick; cure them"), not only what to click. A cutscene can set stakes (a pet is stolen, then the player must protect it) and measurably lowered bounce rate (one game: about 22% → 15-16%). Dedicated cutscene artists exist; one top game uses a ~15 s intro.
- Introduce **one mechanic at a time**; let the player feel it before adding another; avoid context-switching too fast.
- Prefer showing over telling: let the player see cause and effect (plant a seed → a carrot grows). Text tutorials are poorly read by kids. Signal the genre through actions (first step "lock your base" tells a player it is PvP; end the tutorial on "buy a bat").
- Use level design to guide: the threat is visible at spawn (tsunami waves coming) so the player understands the game before any text.
- Top-tier onboarding example: no UI during the tutorial, one mechanic at a time, fast progression, no packs/offers spammed at the start; introduce the HUD and products only after the player cares.
- Do not show monetization before engagement: spam of starter packs and "2x money" offers right at the beginning hurts.
- Add **contextual tutorials** later, fired by server-side triggers (first full plot, first low funds, out of consumables).
- Sunk-cost retention: build modes and private spaces let new players who cannot afford a private server invest in a base safely before returning to public servers.
- Do not let completion be the only goal. A high tutorial completion rate can hide low emotional investment; also watch **new-user first session retention** curve.

## Diagnose onboarding
1. Engagement → new user first session retention (30 s / 60 s / 5 min checkpoints; the creator reports cases with only 20-30% retained that traced to onboarding; one game kept 95% at 30 s, 87% at 1 min and 65% at 5 min).
2. Funnels: track every micro-step (open shop, buy bat, close shop as three steps, not one "bought gear"). Slice by **device** (console!), and traffic source. 77% overall completion with ~30% on console exposed a console bug.
3. Replay the problematic time offset yourself on a fresh account with a timer.
4. Watch real players, especially young ones on iPads; videos with 10-15 views sorted by "posted today" show where they get stuck.
5. Run many tutorial versions: one team shipped about 9 tutorial iterations (nearly one per day in week one). Funnel-driven daily changes.

## Mobile, console and friction
- The creator estimates about 80% of Roblox players are on phones (check your Audience demographics); console players (around 30% in one top game) play often and long. Test on both. Many devs never played their own game on a phone.
- "Death by a thousand cuts": every small friction (spamming "buy 1", unclear tap targets, clunky proximity prompts, UI that is not polished) adds up to a chore. Add "buy 1 / buy 100 / max" options like incremental games.
- Block-building needs a snap-to-grid *and* few taps on mobile; an otherwise great building mechanic limited a game's ceiling because of tap count.
- Use the **little-cousin test**: hand them the phone, do not explain, watch.
- Console improvements raised one game's D1 after research.

## Retention by horizon
- **D1**: first-time experience, tutorial, early progression wall (see testing in [iteration and liveops](iteration-liveops-playtesting.md)).
- **D7**: enough content and mechanics, social flex, events; speed of completion (a game finished in ~2.5 h needed a content update).
- **D28**: deeper progression: index, collection systems, interactions that give meaning to content instead of just more models.
- Return reasons: curiosity ("what ingredient do I unlock"), social flex, collection, investment in a base, events, limited items, new zones/biomes.

## Satisfying core loop
Every action needs feedback: sound, VFX, small camera shake (pickaxe hitting a rock). Low play time usually means the core loop is not satisfying.

## Accessibility and comprehension
Majority of the audience is very young. Use simple vocabulary, clear icons, immediate cause and effect. Avoid many complicated systems whose benefits players do not feel. Cutscenes can be skipped or short; test clarity with new players, not teammates.
