# Release, analytics, LiveOps and player-created content

## Release readiness

Record universe/place/build, affected assets, schema and configuration. Verify changed surfaces: player flow, permissions, input targets, lifecycle, failure recovery, service isolation and performance where relevant. Resolve material unknowns; a green percentage cannot cancel an unverified purchase or data-loss path.

Prepare a concrete reviewable result before any required publication approval. This skill does not itself authorize publishing, paying fees, exposing credentials or migrating live player data. Check current [publishing requirements](https://create.roblox.com/docs/production/publishing/publish-games-and-places) and audience/maturity declarations when release is requested; they can change and should not be frozen into offline eligibility rules.

[Version history](https://create.roblox.com/docs/projects/version-history) concerns place/code versions; restoring one does not automatically publish it or roll back player data. Plan code, config and schema recovery separately. A migration may need forward-compatible recovery rather than returning to an old build.

## Analytics

See [analytics events](analytics-events.md) for economy and funnel events and the dashboard metrics to watch; compare time windows and cohorts with advertising and seasonality in mind and do not infer causality from a coincident spike.

## LiveOps

Separate urgent fixes, permanent QoL/content and temporary events. Choose a sustainable cadence from player needs and production capacity, not a mandatory weekly rule. Events define schedule/time basis, eligibility, claim idempotency, end state and economic impact. A feature/config flag is not a transaction lock.

Use safe defaults and refresh at an appropriate transition. Inspect current [configs](https://create.roblox.com/docs/cloud/guides/configs), [LiveOps planning](https://create.roblox.com/docs/production/game-design/liveops-planning) and [essentials](https://create.roblox.com/docs/production/game-design/liveops-essentials). Compare time windows/cohorts with advertising, seasonality and competitor changes in mind. Do not infer causal retention gains from a coincident event spike.

Discovery changes over time. Check current [Discovery](https://create.roblox.com/docs/discovery) and [FAQ](https://create.roblox.com/docs/discovery-faq); avoid frozen ranking formulas or guarantees from spending/engagement tactics. Packaging should honestly communicate the actual fantasy/play. Use [market research](market-research.md) for the user's gap checklist and public observations.

## Player-authored content

Choose the actual moderation/filtering path for chat, saved names/signs, drawings, builds and other shared creations. [Safety](https://create.roblox.com/docs/safety) and [text filtering](https://create.roblox.com/docs/ui/text-filtering) are current primary references. Filtering failure must not fall back to broadcasting raw content; handle persisted/rebroadcast data as well as initial submission. Rich-text escaping is separate from moderation.

In-game generative AI introduces its own current [guidance](https://create.roblox.com/docs/generative-AI); distinguish AI-assisted development from exposing model outputs to players. Avatar marketplace UGC has separate requirements and needs focused research if requested. Apply feature-relevant controls, not an unsolicited compliance audit for every small game fix.
