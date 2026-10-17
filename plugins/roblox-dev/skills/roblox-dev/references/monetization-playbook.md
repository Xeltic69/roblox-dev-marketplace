# Monetization playbook (creator field notes)

Practitioner heuristics from one producer's monetization and post-mortem videos (see [sources-attribution.md](sources-attribution.md)). Technical contracts (receipts, grants, idempotency) remain in [monetization.md](monetization.md) and [economy-transactions.md](economy-transactions.md). This file covers *what to sell and where*. Pricing convention (optional, set by the project owner): some projects end every Robux price in 9; follow the project's convention if it has one. Do not use manipulative or predatory tactics; sell things that fix a real friction point and keep the economy intact.

## Process
1. Look at the data: Monetization → top dev products by sales. Extend the bestseller (a game with only "+10 speed" added +30 and +100 for whales; it became the new bestseller).
2. Observe player behavior live and read feedback. Players use the game differently than intended (AFK players being robbed).
3. Study competitors in the genre for mechanics that solve the same friction.
4. Add a product that **solves a pain point** (below), choose where it appears, and check side effects on play time, D1, D7 ([iteration loop](iteration-liveops-playtesting.md)).

## Consumables (dev products) beat passes for repeat spend
- Consumable dev products can be bought again and again, so they raise "7-day spend days per user" (unique days a user spends Robux over seven days). Examples: 24-hour base lock (became the top seller within two days), 2x offline earnings per collection, instant hatch, boosts.
- Do not default to a one-time game pass for a repeatable benefit just because it is valuable. The creator reasoned that a 2x offline earnings pass would lower spend days per user (it was the original design and never shipped); a consumable prompt (e.g. 19 Robux at the moment the player collects offline earnings) shipped instead and, per the creator, raised payer conversion.
- Compensate economy and long-term progression for multipliers so they do not wreck pacing.
- Avoid auto-collect or other "fix" passes that remove the loop and wreck the economy; fix the root friction instead (base lock instead of auto collect for AFK players).

## Best sellers solve a pain
> Caution: these are one creator's tactics and most players are children. Use only real, disclosed scarcity (true stock caps), no countdown pressure or shaming, keep offers dismissible and capped per session, and check current Roblox policy for minors before using any of them.

- Pain of effort: "+30 speed", "one bill money" (price carefully; a too-cheap mass cash product destabilized the economy).
- Pain of loss/fear: "lock my base for 24 hours so no one steals while I'm AFK".
- Status and cosmetic wants (keep it positive, no shaming): limited, numbered items (RGB antenna/server, only 100-150 in stock; a limited 1,000-Robux character with stock 1,000 became the #2 seller).
- Pain of missing out: 2x offline earnings prompt at the moment of seeing the reward.
- Products should feel like a must-have, not a nice-to-have.

## Purchase pathways and placement
- More purchase pathways raise sales: one cash product originally sold only via the HUD shop icon; adding a "+" button next to the currency and an offer after repeated "not enough cash" errors (shown on the 3rd attempt, limited to a few times per session) turned a near-zero seller into a seller. Do not open the shop on every insufficient-funds error (annoying, hurts play time).
- Place physical products at points of interest where foot traffic is highest (the base entrance), not in a side corner next to the free version.
- Show offers at the contextually right moment (offline earnings collection, failing to afford a luck upgrade). Fix mobile shop UX; a shop fix restored ARPDAU.
- Tutorial: introduce products only after the player is invested.

## Structure of offers
- Always have a cheap starter pack (the easiest quick win for payer conversion).
- Three tiers for packs/passes (starter, pro, OP like small/medium/large fries); keep an expensive option for whales for higher ARPPU.
- Entry-level stacking products (a very cheap tier 1 that sold in large volume, then tiers stepping up to about twelve; use your own prices and the project's price convention) cross the player→payer threshold (loss-leader logic).
- Launch with whale products and limiteds from day one (shipping them two weeks late was a regret); ARPDAU moved from about 0.9-1.0 to about 2.0 when whale sinks arrived.
- Scarcity for powerful consumables: make OP food scarce and pricier (it became the top food seller) to protect balance.
- Check demographics: if ~50% of players are female, ship cute limiteds too.
- Consider demographic and country mix: US share and 18+ share raise revenue per player; revenue estimates from the dashboard are conservative.

## Pitfalls
- Selling cash packs and handing out strong items too often during admin abuse destabilized one economy.
- Monetization before gameplay kills games (pay-to-win studios).
- Aggressive pop-ups can hurt D1 and play time.
- Revenue figures in the videos are the creators' own and not audited.

## Monetizing a roll mechanic
Remove auto-roll in PvP games, price rolls in cash, and offer Robux to skip the wait when the player cannot afford; tease high-rarity previews on the first roll. One game doubled payer conversion this way.

## Metrics to watch
Payer conversion rate, ARPPU, ARPDAU, 7-day spend days per user, best-selling products (28/7 days), plus side effects on engagement metrics. A product that increases Robux but destabilized play time or D1 fails.
