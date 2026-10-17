# Sources, credits and limits

The references in this plugin are independently written syntheses. External runtime modules, templates, icon registries, videos, images and third-party skill bodies are not bundled, and text recipes are not certified implementations. Roblox technical claims were checked against the Creator Hub documentation in October 2026; version-dependent facts carry "verify" notes and can go stale.

## Skill collections compared for coverage

Other public Roblox skill collections were read to find missing topics. Only ideas and topic coverage were used; no text was copied.

| Collection | License seen |
| --- | --- |
| [EL4CTEO/roblox-skills](https://github.com/EL4CTEO/roblox-skills) | MIT |
| [afrxo/roblox-agent-skills](https://github.com/afrxo/roblox-agent-skills) | MIT |
| [luumenlabs/luau-skills](https://github.com/luumenlabs/luau-skills) | MIT |
| [MSayib/roblox-dev-skill](https://github.com/MSayib/roblox-dev-skill) | MIT |
| [AshExplained/roblox-skills](https://github.com/AshExplained/roblox-skills) | MIT |
| [TabooHarmony/roblox-brain](https://github.com/TabooHarmony/roblox-brain) | MIT |
| [nonlooped/roblox-suite](https://github.com/nonlooped/roblox-suite) | MIT |
| [rib3ye/roblox-opsec](https://github.com/rib3ye/roblox-opsec) | README claims MIT, license file not seen |
| [Anthropic frontend-design](https://github.com/anthropics/skills/tree/main/skills/frontend-design) | Apache-2.0 (concepts only) |
| [UI UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | MIT (concepts only) |
| [Check-UI](https://github.com/TemporaryLooker22/Check-UI-Clean-Roblox) | README claims MIT; no code or assets used |

If a future revision copies substantial licensed prose or code, preserve the relevant license and copyright notices. These licenses do not cover Roblox assets or creator videos.

## Primary documentation

Roblox Creator Hub pages and Roblox-owned API references ground the technical contracts; Luau's own documentation grounds language semantics. Libraries such as ProfileStore, Fusion, Vide, React Lua, Jest Lua, Rojo and Wally are documentation references and optional project dependencies, not installed components.

## Architecture conventions

`architecture-conventions.md` is written for this plugin in original wording. Organizing a codebase into feature folders with API modules is common practice in the Roblox community, and an early draft was informed by community discussion of that pattern; no text from those discussions remains.

## Creator material

Several references (discovery and metrics, packaging, ideation, game design building blocks, onboarding, iteration, monetization playbook, team and production) summarize practitioner experience from a series of public videos by one Roblox producer. They are paraphrased, not quoted, and include self-reported results and opinions that were not audited. The creator's name, channel, own game titles and revenue figures were left out; a few single-game anecdotes remain, labeled as anecdotes, and well-known public games are named only as examples. Treat them as hypotheses to test in your own game, not as platform rules. Roblox-specific statements from those videos were re-checked against the Creator Hub where possible and are labeled [Docs], [DevForum] or [Creator] in the text.

Third-party tools named in the notes (for example RoTrends, qptr.io, Creator Exchange, QA Central, Canva, Trello, Loom) were not tested and may change.

## Verification status (October 2026)

- **Confirmed in the Creator Hub docs:** ranking signals (play-through rate, first-play bounce rate, play days and playtime with D1, D2-7 and D8-28 windows), the penalty for closely resembling metadata, thumbnail accuracy, the Game Details Page, Experiments (config-value and matchmaking tests), funnel and economy events, paid random items odds disclosure, Open Cloud authentication options.
- **Corrected:** the highly-engaged-player entry threshold for Roblox Kids and Select is 250 (since 2026-08-19, per a DevForum announcement), not 500; Ads Manager allows 10 thumbnails per campaign and offers an Engagement objective; the Feedback page shows votes and comments, with no confirmed AI summary there; Experiments do not cover thumbnail tests.
- **Unverified:** beta mode excluding home recommendations, a $16/day minimum ad budget, the exact length of the rolling window for ranking signals, several beta input and camera APIs.
- No game code, purchase, service mutation or device test was executed while writing these references.
