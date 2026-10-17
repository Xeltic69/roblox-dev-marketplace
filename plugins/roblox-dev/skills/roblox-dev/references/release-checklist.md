# Release checklist (read-only readiness review)

Use before a public release, a big update, or a switch to ads. This is a review, not an authorization: publishing, paying fees, changing live settings and migrating live data need the owner's explicit approval ([release and LiveOps](release-liveops.md)). Mark each item **pass / fail / not verified** with evidence (script path, console line, dashboard screenshot, device). Dashboard-only items stay "not verified" unless the owner provides them.

## 1. Safety and security
- [ ] Every remote validates type, range, ownership, cooldown and state on the server ([networking and security](networking-security.md)); no client-trusted currency, damage or position.
- [ ] No secrets, API keys or admin tools in replicated containers; admin features gated server-side.
- [ ] Text players enter or see goes through filtering; a reporting/moderation path exists for player-authored content.
- [ ] Anti-exploit and logging for high-value actions (trades, purchases, teleports).

## 2. Data
- [ ] Session ownership, retry/backoff, save on leave and on shutdown, and a load-failure path that does not overwrite good data ([persistence](persistence.md)).
- [ ] Schema version and migration tested against an old-format profile.
- [ ] Backup/rollback plan for code *and* data (restoring a place version does not roll back player data).

## 3. Monetization and economy
- [ ] Receipt handling is durable and idempotent; every product and pass is granted and re-granted correctly after rejoin ([monetization](monetization.md)).
- [ ] Paid random items (eggs, rolls, crates, luck boosts, pity) show every outcome and its odds, summing to 100% ([reward design](reward-design-random-items.md)).
- [ ] Price convention followed (project-specific); no cash packs or boosts that break the economy; sources and sinks balanced; starter offer and whale tier exist if intended ([monetization playbook](monetization-playbook.md)).
- [ ] Economy events logged for each currency ([analytics events](analytics-events.md)).

## 4. Player experience
- [ ] First 90 seconds tested on a fresh account on phone, desktop and console; no dead ends; the title/thumbnail promise is delivered in the first 30 s ([onboarding](onboarding-retention-ux.md)).
- [ ] Respawn, rejoin, late join, leaving mid-action, private server and teleport paths behave.
- [ ] UI readable at small phone sizes, safe areas respected, gamepad focus works, no UI relies on `ResetOnSpawn` to hide; accessibility checklist reviewed ([accessibility](ui/accessibility.md)).
- [ ] Settings, sound controls and accessibility basics exist where the game needs them.

## 5. Performance and stability
- [ ] No unbounded loops, leaked connections or instances; heavy work is throttled ([performance](performance.md)).
- [ ] StreamingEnabled assumptions handled; no yielding on instances that may never stream in.
- [ ] Load and memory checked on a low-end mobile profile or with equivalent evidence.

## 6. Discovery and analytics
- [ ] Title, thumbnails and detail page are honest and legible on mobile ([packaging](packaging-thumbnails-ads.md)).
- [ ] Funnels for onboarding and the shop log every step; dashboards verified from a published test build ([analytics events](analytics-events.md)).
- [ ] Content-maturity questionnaire and audience requirements checked in Creator Hub; Kids/Select engagement-gate status noted ([discovery and metrics](platform-discovery-metrics.md)).
- [ ] Ads plan and budget approved by the owner, if used.

## 7. Operations
- [ ] Test place on live Roblox with testers; a hotfix path for exploits that does not wait for the weekly update ([iteration and LiveOps](iteration-liveops-playtesting.md)).
- [ ] Feedback channel (Discord, in-game prompt) and a bug-triage owner.
- [ ] Update notes and a config/kill switch for risky features.

## Output
Write `RELEASE_CHECK.md`: verdict (ready / ready with risks / not ready), a table of items with status and evidence, and an ordered fix list naming the matching command (`/roblox-dev:fix-bug`, `save-data`, `economy`, `ui`, `full-audit`). Never mark an item pass without evidence.
