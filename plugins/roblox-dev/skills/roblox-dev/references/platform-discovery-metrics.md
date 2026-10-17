# Discovery, algorithm and metrics

Tags: **[Docs]** = stated in Roblox Creator Hub documentation (checked October 2026); **[DevForum]** = Roblox announcement posts; **[Creator]** = one practitioner's opinion or experience from public videos, unverified (see [sources-attribution.md](sources-attribution.md)). The dashboard and ranking change often: confirm in the [Discovery docs](https://create.roblox.com/docs/discovery) before relying on anything, and never promise players, ranking or revenue.

## The game is a funnel [Creator model, signals from Docs]

Every player is filtered at each stage. Find the biggest leak, hypothesize a fix, ship it, measure ([iteration loop](iteration-liveops-playtesting.md)).

| Stage | Metric | Usual cause of a leak | Fix direction |
| --- | --- | --- | --- |
| Impression → click | Play-through rate (PTR) | Packaging (thumbnail + title) | Test new thumbnails first; keep a good title ([packaging](packaging-thumbnails-ads.md)) |
| Detail page → play | User detail page CTR (Acquisition) | Empty or generic experience page | Best-performing thumbnails/ad creatives, each showing different gameplay |
| First 60 s / 61-180 s | First-play bounce rate (low is good; high lowers home recommendation exposure) | Mismatch between title/thumbnail promise and the first minute; clickbait | Deliver the promise in the first 30 s; cutscene or immediate signature action ([onboarding](onboarding-retention-ux.md)) |
| Session length | Play time per user | Weak core loop, no feedback | Sound, VFX, camera shake per action; random events; collection/index |
| Next day | D1 | Tutorial/first-time experience | Funnel every onboarding step; slice by device |
| Week | D2-7 | Not enough content or social flex; completing the game too fast (one game took ~2.5 h) | Weekly events, more content, deeper systems |
| Month | D8-28 | Shallow progression | Index/collection and mechanics with real depth, not just more models |
| Spend | Payer conversion, ARPPU, spend days per user | See [monetization playbook](monetization-playbook.md) | Consumables raise spend days per user |

## What the docs say [Docs]
- Most important ranking signals: play-through rate, first-play bounce rate, play days per user and playtime per user (play days and playtime are split into D1, D2-7 and D8-28 windows). Important but secondary: intentional co-play days per user, qualified play sessions per user, spend days per user, Robux spent per user. Retention is not named as a ranking metric; improving it helps indirectly.
- [DevForum] QPTR was replaced by play-through rate plus first-play bounce rate on 2026-06-15. Per the Discovery docs, playtime counts up to 60 minutes per user per day, and PTR and first-play bounce are measured on organic Home first-session users.
- Games whose metadata and place files closely resemble existing ones are no longer prioritized for recommendation and may rank lower in search; use original imagery and naming; thumbnails must accurately reflect the game. Clickbait and unmodified clones lose; add a meaningful twist.
- [Creator] Signals use a rolling window (the creator says 7 days; the Discovery page does not state this); the algorithm keeps testing games with new users. Data updates daily (some reports take days).
- The dashboard retention page reports D1, D7 and D30 cohorts; D7 and D30 charts are empty for recent dates until the window closes.
- [Experiments](https://create.roblox.com/docs/production/experiments) are config-value and matchmaking A/B tests: choose a rollout percentage, up to two variants plus a control, run 14-60 days, compare D1, D7, playtime, ARPU, ARPPU, payer conversion and session time; playtime, ARPU and conversion are watched for harm in the first 24 h. They do not cover thumbnail tests.
- Funnel and economy events: see [analytics events](analytics-events.md).
- Where to look: Analytics → Acquisition → Home recommendations (PTR, bounce, play days, play time, benchmarks vs similar experiences), Engagement (including new user first session retention), Funnels, Monetization, Audience → Feedback (votes and comments; the Creator Hub Assistant can summarize), Audience Reach (Kids/Select progress).

## Creator's mental model of the home algorithm [Creator, not Roblox documentation]
1. Traffic first: a new game has no data. Sources: sponsored ads, short-form clips, creators, friends (the creator has not researched free UGC as a source).
2. Initial data: ads bring cold traffic optimized for the cheapest player, so initial stats look worse than later home-algorithm players; idle bots in the lobby are common.
3. Ranking against the genre, then against experiences with similar players. The "market" is defined by similar loops, not strict genre labels. Early green stats can turn red once compared with similar players.
4. Farmers-market analogy: limited front slots go to the best retention and monetization stats; mostly winner-takes-all, which explains launch peaks followed by decline.
5. Ads and the home algorithm are separate markets: more ads on a dying game do not move it into the home market; improve stats with updates first, then re-run ads to feed fresh data about the improved version.
6. **Beta mode (unverified):** the creator says a beta-labeled experience is not shown in home recommendations, so studios optimize on ad traffic first (one claim: big studios spend about $10K in a day to feed data). No official page confirms this; the Discovery docs do not mention beta.
7. Work on the weakest stat first.
Traffic-source anecdotes (home 20%, friends 27%, search 31% D1; D7 about 4%) are single-game observations.

## Audience and device facts [Creator estimates]
Mobile is said to hold about 80% of players and console about 30% of one top game's audience; check your own Audience demographics in Creator Hub. Slice funnels by device and traffic source (one team's console tutorial completion was ~30% vs 77% overall; slicing is the creator's method, not confirmed on the funnel docs page). See [onboarding](onboarding-retention-ux.md) for the first-session retention curve.

## "Highly engaged players" gate for Roblox Kids and Select (2026)
Checked against DevForum announcements in October 2026; the discovery docs do not describe the gate. Re-check DevForum and Creator Hub **Audience Reach** before relying on a number.
- **[DevForum] Thresholds:** early-2026 community videos say 500. Roblox lowered the entry threshold from **500 to 250 on 2026-08-19** and set a separate maintenance bar of **25** (from 100, on 2026-07-16). On 2026-07-06 the definition of a highly engaged player was relaxed. See [Highly Engaged Player Threshold Drops to 250](https://devforum.roblox.com/t/highly-engaged-player-threshold-drops-to-250/4820164).
- **[DevForum] Other requirements:** ID verification, good account standing and a refundable publishing fee (reported as 1,000 Robux; other account requirements may apply), see [Alternate Publishing Requirements](https://devforum.roblox.com/t/alternate-publishing-requirements-for-roblox-kids-and-select/4630944/737). An expedited review path with a higher fee is mentioned; check the current terms.
- **[Docs] Ads Manager** has an **Engagement** objective for age-checked, highly engaged players whose sessions count toward the threshold; higher cost per play; it does not pause automatically at the threshold; the docs suggest reviewing onboarding if no progress after 3-5 days ([Ads Manager](https://create.roblox.com/docs/production/promotion/ads-manager)).
- **[Creator]** The purpose is child safety against bot-pumped predatory games (the creator's interpretation). A highly engaged player is, per an official statement the creator read in the video that was not found in the docs, someone with a minimum purchase anywhere on Roblox in the last 60 days, judged by account age, play history and platform spend. The game's target age does not matter. Anecdotes from the creator and others say progress toward the threshold is slow on ad traffic and speeds up once home recommendations begin, because algorithm traffic contains more engaged players. You can reach the algorithm before the gate. Heavy spending is not required (creator's view).
- Do not buy bots or fake engagement; the gate exists to catch it.

## Ads
Protocol and figures are in [packaging, thumbnails and ads](packaging-thumbnails-ads.md).
