# Packaging: title, thumbnail, detail page and ads (creator field notes)

Practitioner heuristics from one producer's videos (see [sources-attribution.md](sources-attribution.md)). Packaging must honestly reflect the first minutes of play: misleading packaging raises bounce rate and is penalized ([metrics](platform-discovery-metrics.md)).

## Core fantasy first

A core fantasy is the emotional promise of the game: who you are, what you do and how it feels. It is the main reason a player clicks. Packaging = thumbnail + title; the title gives context to the thumbnail, the thumbnail registers first.

- Test it with the "fifth grader at lunch" pitch: *"a game where you hack McDonald's/Apple/Netflix"* beats *"a game where you collect data and sell it"*. A game renamed from an abstract "sell your data" title to a concrete "hack a business" title, with a new thumbnail, roughly doubled its ad CTR (about 1.5% to 3.2%) (title and thumbnail changed together; creator's account).
- Write titles at about a 3rd-4th grade reading level (check word reading levels; "data" and "corporation" were too advanced, "business" fit). Avoid abstract words.
- Templates for strong titles: `Verb a Noun` (Steal a Brain Rot, Grow a Garden), `Be a Noun` (nurse, firefighter, YouTuber), `Escape the Noun`, `Don't X the Noun`. The title should convey the **emotional state** (what the player will feel) and an **implied challenge** ("99 Nights in the Forest", "Escape the Zoo", "Hide from the Villain").
- Keyword research: search a candidate verb/noun in Creator Exchange (filter all games, sort by visits). Several games with large visits for the keyword (e.g. "hack": 11M, 5M, 20M visits) validate the fantasy; a lone result or only role-play results means weak or unserved demand ([ideation](ideation-market-validation.md)). Study the common objects/themes in their thumbnails (mask, green code).
- The most important thumbnail principle in the creator's view: communicate what the player will **feel** (power, tension, outplaying someone). A core-loop tease also works ("buy and sell cars"). A thumbnail can also tease the **unique mechanic** by text when the game is a sequel or second entry ("steal at night", "cure the survivors").

## Thumbnail principles (patterns seen in top performers)
- One or two characters (sometimes three), simple background, high color contrast, one clear action.
- Facial emotion clearly readable (menacing smile, panic); the scene communicates the fantasy and implies the feeling (power, tension, outplaying someone).
- Concept variants to test: before/after (noob vs pro, "level 1 / level 999"), first-person for "Be a ..." games, one character + a clear action, two-character scene.
- Proven characters help (bacon/noob, acorn hair). Do not copy another game's thumbnail wholesale: the [Discovery docs](https://create.roblox.com/docs/discovery) say games with metadata and place files closely resembling existing games are no longer prioritized for recommendation and may rank lower in search, and that thumbnails must accurately reflect the game. In one case a thumbnail inspired by a hit lost to a fully original one.
- **Check mobile and console.** Most designers check only desktop; text and logos become unreadable on phones. A free third-party tool (qptr.io; free and unsponsored when the creator recorded) simulates home, search, charts and icon placement per device. Make logos/text large, remove visual noise (e.g. clouds, brown clutter), keep text off the main object.
- Expect PTR to fall as impressions rise: rotate creative (aim for 2-3 new thumbnails a week; one team reported testing 50 thumbnails across two campaigns). Volume beats taste; no hired artist beat the team's own tested CTR/PTR.

## AI thumbnail workflow (creator process)
1. Study 5-10 top thumbnails in your genre and note patterns.
2. Make a rough mockup in an editor (Canva) from screenshots of your real assets.
3. Give an image-generation tool the concept with *very specific* instructions (e.g. split screen, big buildings with logos, "the Apple Store, not the fruit"); add references.
4. Iterate: fix color contrast, remove noise, enlarge key elements, adjust text so it does not cover the subject. If the tool keeps repeating a mistake, **start a new chat** with the best reference image and a cleaned prompt.
5. Check on mobile; spend 10-15 minutes per thumbnail; ship many; keep winners.
(The `gpt-image-bridge` skill can generate images when available.)

## Experience detail page
Roblox's docs call it the Game Details Page; it supports Experience events (up to 5 thumbnails per the docs summary; check the current limit) and highlights similar games ([Discovery](https://create.roblox.com/docs/discovery)). Users who click a thumbnail still decide on the detail page (metric: user detail page CTR). Fill it with best-performing thumbnails/ad creatives that vary and show gameplay and the unique mechanic, with an honest description.

## Running sponsored ads (simple protocol)
1. Do fantasy/title/thumbnail work *before* ads.
2. Prepare many creatives (the creator launched at least 10, ideally 20 or more). The [Ads Manager docs](https://create.roblox.com/docs/production/promotion/ads-manager) allow up to **10** thumbnails per campaign (spread evenly; toggle individual ones after launch); the creator reported 25 per campaign, so check the current limit and use several campaigns if needed.
3. Choose the experience, the objective (Plays, Earnings, or Engagement for the Kids/Select threshold), recommended targeting, a **daily** budget (the creator used about $16/day; the docs name no minimum), no manual advanced targeting unless needed. Pay with Robux converted to ad credits (the creator says this is cheaper than USD; per the Ads Manager docs the conversion is permanent and the preview before confirming shows the rate; name, budget amount, schedule and creatives of a published campaign can be edited, while goal, audience, budget type and payment method are fixed).
4. Run at least 3 days, ideally a week. The creator reports that first home-recommendation impressions usually take about a week of ads, that Roblox data is slow, and that nobody has enough data yet to understand the engaged-player gate fully; do not panic in the first days.
5. As soon as stats arrive, ship updates targeting the worst stat; watch live players, feedback, funnels.
6. Keep running until home-recommendation impressions exceed sponsored impressions; then stop. Re-run ads after a *meaningful* update to re-feed data.
7. If you cannot afford ads: commissions, short-form content, free UGC; ask for budget rather than waiting (the creator has not researched free UGC as a traffic source).
Do not conclude from small samples; none of this is guaranteed. Platform ad rules and prices change.

## Market phases
See [ideation and market validation](ideation-market-validation.md) for blue/red/purple ocean phases; the packaging consequence is that a generic title and thumbnail for a crowded fantasy gets poor CTR, so mutate both.
