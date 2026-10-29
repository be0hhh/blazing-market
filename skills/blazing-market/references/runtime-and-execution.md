# Runtime, strategy, execution and financial semantics

Apply execution-specific rules only when the project has an actual trading,
order, risk or finance component. For market-data-only consumers, inspect the
relevant bounded runtime and ownership sections without inventing an order path.

## Runtime ownership and lifecycle

- Locate the authoritative producer, runtime, session/account owner, mutable
  state owner and consumer. Producer storage must outlive borrowed clients and
  views; define thread/epoch ownership and publication ordering.
- Distinguish current generation/session state from older, external, foreign
  or replayed state. Do not adopt external orders, partial events or old
  snapshots as current-run truth without an explicit contract.
- H0 computations should use prepared state and bounded operations according
  to their selected latency profile. Keep connection lifecycle, UI, metrics,
  backoff and operational control out of the critical calculation.
- Queues and fan-in/out require explicit capacity, memory order, consumer
  pressure and terminal overflow behavior. A slow diagnostic/viewer consumer
  must not silently stall the live data producer.
- Distinguish **ordinary configuration reload**, supported structural reload,
  session reconnect, steady-state `SessionNotReady`, explicit operator/application
  Stop and resource retirement. These are different events with different
  authorization and order-state effects; none should silently inherit the
  behavior of another.
- On ordinary compatible reload, preserve unchanged active instruments/shards,
  strategy state, authoritative current-run orders and pending correlation.
  Do not cancel all orders or tear down healthy sessions merely because an
  unrelated setting changed. Reject unsupported structural changes with a
  clear restart requirement instead of silently rebuilding live ownership.
- Reconnect invalidates or advances the affected session generation and
  coherently updates pending commands, readiness and feedback attribution.
  `SessionNotReady` is a surfaced readiness/admission result, not a reason to
  sleep, reconnect or retry inside the per-event strategy loop. Retrying,
  authentication and backoff belong to the cold session owner.

## Strategy and signal contracts

- Keep deterministic strategy decisions and declared stream requirements with
  the strategy owner, not hidden in parser/transport or UI adapters.
- Check no-lookahead causality, event availability, freshness, primary/optional
  inputs and reload semantics. Preserve trading decisions across replay/live
  under explicitly equivalent inputs; a backtest result is not live proof.
- When relevant, include fees, funding, spread, slippage, tick/lot/size, order
  type, position, inventory, liquidation and exact risk/admission constraints.
  Avoid hiding risk policy in an offline simulator or transport adapter.
- Declare parameter precedence, structural versus non-structural reload,
  unknown-key rejection and numerical parsing at the responsible owner.

## Order and financial lifecycle

- Separate strategy intent, admission/reservation, local acceptance, terminal
  submission, venue ACK, reject, partial fill, complete fill and cancel.
  A send or local acceptance is never equivalent to an exchange fill.
- Enforce this **pre-submit ordering** at the actual selected runtime/venue
  boundary, without merging the separate owners:
  1. Produce a deterministic, bounded order/cancel intent.
  2. Check exact account and product, source/session generations, native
     capability and readiness, unique ID availability, bounded command and
     feedback capacity, and the owning risk/quota/admission decision.
  3. Install canonical current-run intent and reserve correlation/obligations
     **before the first submission**; do not create a second authority for
     pending IDs or economic state in the session/transport layer.
  4. Validate the selected native session, identity, route and remaining
     capacity at its producer/transport owner, then patch the prepared bounded
     payload and perform the actual terminal write.
  5. Track local acceptance, transport/terminal disposition, exchange ACK or
     reject, fills, cancellation and reconciliation as distinct facts.
- Preserve client/exchange order IDs, idempotency/correlation and source epochs
  across ACK/fill/cancel races, duplicates and reconnect. Unknown, partially
  written or timed-out outcomes do **not** grant automatic resend, ID reuse,
  duplicate intent creation or release of outstanding obligations.
- Preserve one authority for current-run orders and one store per financial
  fact. Keep cash, collateral, obligations, margin and reservations distinct
  where the accounting model requires them.
- Unknown terminal outcome does not itself authorize an automatic resend or
  release obligations. Explicitly handle incomplete/partial/cancelled outcomes
  and the owner's reconciliation policy.
- Stale/incomplete data, exhausted work/memory budgets and arithmetic overflow
  must not silently permit new risk. Applying already observed authoritative
  financial facts must remain possible without losing obligations.
- Use declared units, scaled arithmetic, valid ranges and conservative rounding
  where financial correctness requires it. If rational oracle and fixed-point
  implementation differ, state their domains and independently check relevant
  outcomes; no equivalence claim from shared code paths alone.
- For offline optimization/DP/scenario calculation, verify causality, bounds,
  states, recurrence, pruning, terminal conditions and conditional completeness
  against an independent small oracle where appropriate. An offline solution
  is not automatically a production-hot or live-execution capability.

## Stop, cancellation and recovery

Define who is authorized to stop, cancel or close positions, which exact account
and inventory the action covers, when authority expires, and what happens to
unknown outcomes. Explicit Stop must first quiesce the appropriate execution
owners, follow the user's/account owner's certified native cancellation and
position policy, and preserve a truthful degraded/control-only state when
identity, authority or outcome is uncertain. An ordinary reload, reconnect,
session retirement or worker disposal is **not** Stop and confers no permission
to place, cancel or flatten orders. Do not invent a blanket cancel-all,
foreign-position takeover or flatten policy; follow only the explicit product
contract. Changes to these semantics require a material user/domain decision
and independent relevant review.
