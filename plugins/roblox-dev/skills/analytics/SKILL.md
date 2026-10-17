---
name: analytics
description: Add or review Roblox analytics events (economy, funnel, custom) so a stat can be diagnosed. Use when the user wants funnels, event tracking or to know where players drop off.
argument-hint: "<stat or feature to instrument>"
---

# /roblox-dev:analytics

Task: $ARGUMENTS (if empty, ask which stat or flow to instrument, if missing).

First read ../roblox-dev/references/command-rules.md and follow it. Then read: ../roblox-dev/references/analytics-events.md, ../roblox-dev/references/platform-discovery-metrics.md.

Add events only where a stat needs diagnosis. Call from the server in the owning system's API, keep names stable, respect the rate limit, log every micro-step of the funnel, and tell the owner how to verify events in the Creator Hub after publishing a test build (events do not arrive from Studio). Do not publish for them.
