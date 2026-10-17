---
name: economy
description: Work on Roblox currencies, inventory, crafting, trading, shops and monetization code. Use when the user mentions Robux, products, passes, prices, shops or game economy.
argument-hint: "<economy or shop task>"
---

# /roblox-dev:economy

Task: $ARGUMENTS (if empty, ask what to build or review, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/economy-transactions.md, ../roblox-dev/references/monetization.md, ../roblox-dev/references/monetization-playbook.md, ../roblox-dev/references/reward-design-random-items.md, ../roblox-dev/references/analytics-events.md.

- Keep transactions server-authoritative and atomic; access balances only through the owning system's API; log economy events at that API.
- **Ask before changing any price, product ID, pass ID or receipt handler. Never create, publish or buy products or spend Robux; hand back the exact values for the owner to enter in Creator Hub.** Follow the project's price convention if it has one.
- Paid random items (eggs, rolls, crates, luck boosts, pity) must show every outcome and its odds. Model sources and sinks before adding paid convenience; check side effects on play time and retention.
