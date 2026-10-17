# Purchases and durable paid benefits

Separate owned entitlements such as passes from repeatable developer products. UI requests a platform prompt; fulfillment is an authoritative server/data operation. Display current relevant product information and do not invent prices or misrepresent regional/personalized pricing. Cancellation, pending, granting, saved, failed and already-owned are distinct states. Consult [developer products](https://create.roblox.com/docs/production/monetization/developer-products).

## Receipt contract

Use the existing reliable handler architecture. Current [MarketplaceService](https://create.roblox.com/docs/reference/engine/classes/MarketplaceService) documents ProcessReceipt and newer receipt-handler APIs; verify the chosen API and its matching decision enums. Do not mix enums or add a parallel handler that overrides existing products.

For ProcessReceipt, unresolved callbacks are not scheduled on a simple guaranteed retry timer; pending deliveries can recur on later relevant platform activity. Receipts can be delivered concurrently across servers and in an unexpected order. A client prompt result is not proof of durable product granting.

Under the canonical profile/session owner, validate the genuine receipt and product mapping. Commit the saved benefit and its completion marker in the same authoritative durable transaction, prove persistence, then acknowledge. If the receipt was already durably fulfilled, acknowledge without adding value again. Unknown product, inactive/unloaded profile or uncertain write requires safe deferral/reconciliation, not invented success.

An in-memory marker after a failed save is insufficient. Recording a marker before an unrelated grant can lose the benefit; granting before an unrelated marker can duplicate it. Effects inside a retried UpdateAsync transform can repeat. Review even official examples against the [single-key transaction semantics](persistence.md).

A saved revision proves fulfillment only when it identifies a committed record containing this receipt's marker and benefit, or the data layer exposes equivalent operation-specific proof. A generic recent save timestamp/revision does not establish that the relevant pending mutation was included.

With an established ProfileStore data layer, inspect its current [developer-product recipe](https://madstudioroblox.github.io/ProfileStore/devproducts/) for saved-state proof. A bounded recent-ID cache has a finite retention guarantee, not unconditional forever deduplication. Never trim pending/unconfirmed markers to fit a cache. Permanent-value designs need an explicit retention, size and reconciliation policy.

## Failure and lifecycle

Assign correlation for diagnostics without revealing secrets. A closing screen or UI timeout does not undo a committed transaction, and cannot justify asking the player to purchase twice. Reconcile unknown outcome from canonical ownership/balance. Handle player leaving, rejoining and losing profile ownership during fulfillment. Gracefully expose unavailable product/asset metadata.

Do not use test purchases against live player data. Choose isolated data and current documented testing flows. Verify repeated genuine receipt, concurrent handling, saved benefit after rejoin, crash windows, failed save, marker retention and unknown product. A passing pure fixture is not proof of real MarketplaceService behavior.

## Cash-out

Developer Exchange rates and eligibility (including a higher rate for some purchases by age-verified U.S. adults, and different rates for older balances) change over time and third-party calculators are often outdated. Read the live [Developer Exchange page](https://create.roblox.com/docs/production/monetization/developer-exchange) before planning a cash-out, and never present an income projection as a promise.

## Concrete receipt and pass details (verify in the docs)

- `MarketplaceService.ProcessReceipt` has **one** callback per server; assign it exactly once. It receives a `ReceiptInfo` table (including `PlayerId`, `PurchaseId`, `ProductId`). Return `Enum.ProductPurchaseDecision.PurchaseGranted` only after the grant and the `PurchaseId` marker are durably recorded, and `NotProcessedYet` when anything failed or the player data is not ready so Roblox retries.
- Handle the same `PurchaseId` arriving again (retry, rejoin) without granting twice.
- A prompt-finished event is not proof of a grant. For game passes, confirm ownership on the server (and cache it for the session) before granting benefits.
- Plan refund handling: decide whether the benefit is revoked and how the economy recovers, and use a webhook or a periodic check where appropriate ([Open Cloud](tooling.md)).
- For paid random items, check the player's policy flags (for example `PolicyService:GetPolicyInfoForPlayerAsync`, which returns a dictionary whose `ArePaidRandomItemsRestricted` field applies to paid random item generators) and disable those purchases for restricted players.
