# Analytics events: economy, funnel and custom events

Source: Creator Hub [economy events](https://create.roblox.com/docs/production/analytics/economy-events) and [funnel events](https://create.roblox.com/docs/production/analytics/funnel-events) (checked October 2026). Use these to give the iteration loop real data ([iteration, LiveOps and playtesting](iteration-liveops-playtesting.md), [discovery and metrics](platform-discovery-metrics.md)). Analytics is optional instrumentation: add it when a stat needs diagnosis, not as an unrequested rewrite.

## Rules that apply to all `AnalyticsService` events
- Log from the **server**. Economy events cannot be sent from the client or from Studio, and the game must be published.
- Events are rate limited together (Economy, Funnel and Custom). The funnel-events page lists `120 + 20 x CCU` requests per minute (verify the live figure). Never log per frame; log decisions and milestones, which is why "every micro-step" means every decision in a flow, not every tick.
- Use a stable, documented naming scheme (see taxonomy). Renaming a step later breaks historical comparison.
- Do not log personal data. Use gameplay identifiers only.

## Economy events (resource flow)
- `AnalyticsService:LogEconomyEvent` takes, in order: player, flow type, currency name, amount, balance after the transaction, transaction type. `itemSKU` is optional and custom fields use the optional arguments described in the Creator Hub custom-fields guide; read the live signature before writing the call.
- `flowType` is Source (gained) or Sink (spent) from `Enum.AnalyticsEconomyFlowType`. Pass **positive** amounts for both; the dashboard shows sinks as negative.
- Default transaction types (`Enum.AnalyticsEconomyTransactionType`): IAP (source), TimedReward (source), Onboarding (source), Shop (source or sink), Gameplay (source or sink), ContextualPurchase (sink). Custom names are allowed.
- `itemSKU` is optional; set it for shop items so the dashboard can attribute sources and sinks to items (a missing SKU appears as unattributed in the creator-reported dashboard).
- Custom fields (quest name, store location) let you segment charts; up to three can be used as filters.
- The dashboard tracks **up to five currencies** (the event-types page lists a limit of 10 resource types; check the live docs): pick the ones that matter. Charts: sources and sinks by category, average wallet balance for users/payers/non-payers, top sources and sinks.
- Wire the call into the single server function that changes a balance (the owning system's API), so every grant and spend is logged once and the balance-after value is correct.

## Funnel events (progress through steps)
- One-time funnels (onboarding): `LogOnboardingFunnelStepEvent(player, stepNumber, stepName)`.
- Recurring funnels (shop, rounds): `LogFunnelStepEvent(player, funnelName, funnelSessionId, stepNumber, stepName)`; generate `funnelSessionId` with `HttpService:GenerateGUID()` per attempt so repeated runs by the same player stay separate.
- The Funnel page unlocks once events arrive; up to ten funnels per dashboard. Use "View Events" and the error report to check instrumentation.
- Log **every micro-step** (open shop, select item, confirm, close) rather than one "bought item" step. Slice by device and source in the dashboard where available.

## Suggested event taxonomy
| Area | Funnel / event | Why |
| --- | --- | --- |
| Onboarding | join → first action → first reward → core loop done → first upgrade | D1, bounce, tutorial drop-off |
| Progression | first/second/Nth core upgrade, zone reached, plot upgrade | balancing walls |
| Monetization | shop opened → product selected → prompt shown → purchase result | conversion pathways |
| Economy | every source and sink with SKU | inflation and sink checks |
| Social | friend join, trade, gift, private server | virality |

## Checklist for adding analytics to a feature
1. Which stat or decision does this event serve?
2. Is the call on the server in the owning system's API?
3. Are names and steps stable and documented in the system's folder?
4. Is volume safe under the rate limit at peak CCU?
5. Did you verify events appear in the dashboard's "View Events" after publishing a test build (not in Studio)?
