# Inventory, equipment, crafting, trade and economy

## Canonical ownership

Separate item catalog definitions from owned instances, equipped slots and rendered Tools/previews. Use unique IDs for distinct possessions and integer quantities for homogeneous stacks. Resolve costs/rarity/capacity/compatibility from the server catalog. Define conservation invariants: a transfer removes what it credits; consumption happens once; balances/counts stay finite and nonnegative.

Equip validates actual ownership, legal slot, current action/alive state and already-equipped behavior. Reconstruct visuals after respawn from canonical equipped ownership. A visual object arriving late does not invalidate an accepted equip; reconcile rather than duplicating it.

Craft request: recipe ID, bounded integer amount and operation ID. Validate unlock, required location, ingredients, capacity and catalog version. Consume and produce through one owned mutation path, with no yielding race between local checks and changes. Persist using the actual transaction boundary; client dismissal does not cancel an already committed craft. Show pending/rejected/unknown outcomes honestly.

## Trade protocol

Establish trade ID, participants, permissions, expiry and an offer revision. Both parties explicitly accept the same final revision. Every offer edit invalidates acceptance. Reject duplicate item IDs. Reserve offered value across sell/drop/equip/consume/craft/other trades, not just inside the trade panel. Revalidate session ownership, final offers and capacity immediately before committing.

Two profile keys are not one atomic DataStore transaction. A same-server lock or two successful writes cannot guarantee crash-safe cross-profile exchange. Valuable durable trades need an authoritative recovery protocol: stable transaction identity, prepared/committed/applied states, idempotent debit/credit legs, reservations honored by all writers and reconciliation after restart. This is a design contract to implement and fault-test, not supplied middleware. See [persistence](persistence.md).

Failure after an ambiguous write must reconcile before rollback; blind compensation can duplicate value. Disconnect/teleport should enter an explicit cancel or recovery state. If the project cannot support the required durability, explain the missing implementation and avoid advertising the feature as crash-safe.

## Balance

Describe sources, sinks, reward probabilities, frequency, prices and intended progression bands. Independently check expected-value arithmetic and affordability at early/mid/late states. Economies need not balance every minute or acquire more currencies by default. Changes to event rewards can affect both supply and demand. Consult [economy balance](https://create.roblox.com/docs/production/game-design/balance-virtual-economies); documentation examples can contain arithmetic typos and must still be checked.

Use telemetry for successful committed changes with actual ending balance; rejected requests belong to separate failure events. Avoid manipulative purchase pressure or sacrificing the game's stated audience/fairness solely to raise revenue. Paid currency routes also use [monetization](monetization.md).

## Verify

Duplicate offered IDs, changed offers after acceptance, simultaneous consume/trade, repeated confirm, disconnect, lost ownership lease, crash before/between commit legs and repeated recovery should preserve conservation and converge after restart. For small non-durable craft/equip behavior, test the relevant local authority path without pretending it proves a distributed exchange.
