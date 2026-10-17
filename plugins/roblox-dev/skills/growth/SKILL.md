---
name: growth
description: Improve a Roblox game stat with the hypothesis loop: pick the weakest stat, cross-reference player feedback, metrics and competitors, propose and (after approval) implement one focused change, check results. Use when the user asks how to improve retention, play time, conversion or CTR.
argument-hint: "<stat or goal>"
---

# /roblox-dev:growth

Task: $ARGUMENTS (if empty, ask for the current stats or which stat to improve).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/platform-discovery-metrics.md, ../roblox-dev/references/iteration-liveops-playtesting.md, ../roblox-dev/references/onboarding-retention-ux.md, ../roblox-dev/references/analytics-events.md, ../roblox-dev/references/packaging-thumbnails-ads.md (CTR or PTR), ../roblox-dev/references/monetization-playbook.md (conversion or ARPPU; mind the caution about minors).

1. Get the current stats (PTR, bounce, play time, D1, D7, D28/D30, conversion, ARPPU). Dashboard data comes from the owner; do not invent numbers.
2. Choose the single weakest stat. Gather qualitative, quantitative and competitor evidence; ask the owner for player feedback and competitor facts or use ../market-research/SKILL.md, and never invent them.
3. Write the hypothesis: if I add / remove / improve X, stat Y improves.
4. State the hypothesis and wait for the owner's yes before editing. Then implement it in the owning system; add analytics only if the result cannot otherwise be measured.
5. State how and when to check results (moving data window, side effects on other stats). Do not change pricing, publish or edit live settings without approval.
