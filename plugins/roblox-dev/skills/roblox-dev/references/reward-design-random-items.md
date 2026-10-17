# Reward design, random items and player psychology

Two layers: (1) **policy** that is verified against Roblox's documentation, (2) **design heuristics** from community skill collections and creator videos, which are not rules. Keep them separate when advising. Check the live pages before relying on wording.

## Policy: paid random items (verified)
Source: [Paid random items policy](https://create.roblox.com/docs/production/monetization/paid-random-items).
- Applies to any random item obtained with Robux or with an in-game currency that Robux can buy: capsule-style items (egg hatches, chests, prize wheels, gachas, rolls), enhancement and combination items, and probability modifiers such as **luck boosts and pity systems**.
- You must list **every possible outcome with its numerical odds** where the player can see it before buying; the odds are shown as percentages that **sum to exactly 100%**. An (i) icon without a descriptive word is not enough; use a clearly labeled "Info/Details" control or a clickable pop-up when the list is long. Many outcomes with identical odds may be grouped.
- If a modifier changes the odds, the displayed odds must update dynamically.
- Robux-purchasable cash or luck used for rolls counts as a paid random item, and so does any luck or pity modifier.
- Indirect purchases count: buying a seed or key with Robux and then opening it for a random item is covered.
- Regional rules may add requirements. When building egg, pet, roll, crate or gacha systems, treat odds display as part of the feature, not polish. Include it in `/roblox-dev:full-audit economy` and in release checks.

## Design heuristics (not rules)
- **Transparent randomness:** show rarity tiers, the pity counter if one exists, and what luck does. Hidden pity and unclear luck effects are both a policy risk and a trust problem.
- **First-minute engagement:** deliver one clear, positive reward quickly (a visible growth moment, a first upgrade). For rolls, show the real outcome pool; do not stage rare-looking near-misses that imply better odds than the disclosed ones.
- **Reward schedules:** mix predictable progress (guaranteed upgrades, index completion) with variable rewards (rolls, events). Avoid designs that depend on compulsion; players are largely children, so favor clarity over pressure. Do not use countdown pressure on purchases aimed at minors in ways that conflict with Roblox policy; check current rules.
- **Pity and bad-luck protection** reduces frustration; it also changes the odds displayed (see policy above).
- **Pricing psychology:** cheap entry tier, three-tier packs, scarce limited items for high spenders, and offers that fix a real friction point ([monetization playbook](monetization-playbook.md)). Prefer fair value over manufactured urgency.
- **Economy health first:** every source needs a sink; paid convenience (auto-roll, cash packs, speed boosts) can destroy pacing, especially in PvP games ([creator lessons](creator-lessons-simulator-launch.md)).
- **Community loops:** index/collection completion, trading or showing off, events tied to collections, and co-op or leaderboards give players reasons to return ([game design building blocks](game-design-building-blocks.md)).
- **Ethics check before shipping:** would a parent understand what was bought and what the odds were? Is anything misleading about rarity, stock or timers?
