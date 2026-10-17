# Game loops, genre choices, and player comprehension

Use genre patterns as hypotheses, not mandatory feature lists. The player's actual fantasy and the requested game determine the system.

## Loop contract

Write the immediate action → readable result → meaningful decision → next goal. Explain what the player risks, gains, learns, and can vary. Separate second-to-second feedback, session goals, and long-term progression. Reward repetition only when the action remains interesting; more currencies and upgrade tiers do not automatically produce depth.

Onboarding should make the goal and its reason understandable, demonstrate one useful action at a time, and let players act soon. Observe confusion, first success, failures, and recovery. Tutorial completion alone can hide a player who complied with arrows without understanding the game. Check the same path with touch/gamepad and without prior genre knowledge. Cutscenes are optional, not a universal bounce-rate cure.

Create social or shareable moments through legible stakes, cooperation, surprises, or skill. A short clip should communicate what happened without misleading viewers about normal gameplay. Do not promise virality or engineer frustration solely to force invitations or purchases.

## Genre-specific decisions

| Pattern | Core decision | Design/implementation fault to test |
| --- | --- | --- |
| Obby/parkour | Route, timing, recovery | Checkpoint recognition, fair restart distance, camera/touch obstruction, skipped-stage validation |
| Simulator/collection | Collect, improve, unlock | Clear next upgrade, resource sinks/sources, runaway multipliers, tedious early progress |
| Tycoon/building | Placement and production choice | Plot ownership, placement collision, affordability, saved ownership, griefing boundaries |
| RPG/adventure | Exploration, quest, equipment choice | Quest dependencies, branch recovery, combat readability, level gates, content pacing |
| Horror/co-op | Anticipation, survival, cooperation | Visibility/accessibility, safe audio levels, fair threat cues, dead-player participation, content maturity |
| Round-based/PvP | Contest, resolve, replay | Joining mid-round, ties, disconnects, team imbalance, reward once, spectator lifecycle |
| Tower defense/strategy | Allocation, positioning, timing | Path reliability, target choice, predictable waves, cooperative roles, measured balance |
| Social/roleplay | Expression and interaction | Useful shared activities, moderation/filtering, personal space, opt-in interaction, server consistency |

Hybrid and novel genres are valid. Do not force an RPG into a simulator economy or an obby into paid progression.

## Balance and improvement

Expose tunable parameters with units and purpose. Test progression with representative starting/mid/late states, not only a developer's maximum-level account. Separate mathematical simulations from evidence of player enjoyment. Inspect distributions and friction points by cohort/input/version; averages can hide disadvantaged players.

Form a hypothesis for each substantial change: observed problem, proposed cause, intervention, desired player effect, metric, and guardrail. Use qualitative playtest observations alongside aggregate metrics. Retention, monetization, accessibility, and fun can trade off; do not optimize a single number by silently changing the user's game identity.

For visual identity and clarity, route to [ui/design.md](ui/design.md) and [presentation-assets.md](presentation-assets.md). For choosing concepts, use [market-research.md](market-research.md).
