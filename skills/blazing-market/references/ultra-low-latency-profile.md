# Ultra-low-latency profile: strict H0 contract

This profile preserves the existing strict low-level engineering restrictions.
Apply it to hot operations when the project or user explicitly identifies the
market/trading system as LOW LATENCY, or explicitly selects the strict profile.
No HFT label is needed. H0, market data or “fast” alone is insufficient; ask
when intent is unclear. Explicit project policy controls the corresponding
rules and scope; preserve an already active stricter contract.

H0 follows the bans below. H1 follows them for operations actually on the
critical path or covered by an explicitly selected strict compute contract;
remaining H1 retains its boundedness, lifetime and ownership class contract.

## H0 computation and live event loop

- Apply the [minimum-checks rule](architecture-and-contracts.md#minimum-necessary-checks-and-repeated-work)
  across the affected chain, including module boundaries, send and recovery.
  Trust established owner guarantees; move immutable qualification to preparation
  and maintain mutable state by owner events where semantics allow. Remove
  redundant checks and work while retaining checks for concrete unproved facts
  or intervening changes and preserving necessary correctness guarantees.
- No per-event heap allocation or dynamic container growth. Preallocate
  fixed-capacity buffers, state and work slots in cold control code.
- No exceptions, RTTI, virtual dispatch, uncontrolled recursion, blocking
  waits, mutex locks, sleeps, formatting, file/console I/O or deep logging in
  the critical compute/cycle. Use bounded deterministic work and explicit
  error/refusal outcomes.
- No floating-point price/quantity/money conversion or decision arithmetic
  in the strict trading/financial core. Use declared integer-scaled or
  fixed-point arithmetic with checked overflow and rounding. Keep diagnostic
  floating-point or independent oracles outside that core.
- No unnecessary syscalls, copies, clock captures, scheduler interactions or
  per-message diagnostics before a required terminal socket/TLS write. The
  actual nonblocking receive/write I/O remains necessary; this profile does
  not prohibit performing the required send or receive.
- Use borrowed spans/views and direct cursors only with proved owner and
  lifetime. Bound frames, parser cursors, strings, queues, decompression,
  order payload patches, output capacity and stack frames.
- Prefer direct normalized publication and inline consumer work where the
  project contract establishes that route. Do not wait to fill a batch before
  delivering available market events; bound drain for fairness.
- Keep reconnect, DNS, auth, metadata, retry/backoff, configuration and
  presentation in cold/control. Keep deep probes, logs and dashboards in
  diagnostics. H1 handoffs and readiness state remain bounded and coherent.
- Check memory ordering, false sharing, state size/alignment and cache-line
  placement. Branch hints, SIMD and custom primitives require actual
  correctness and measured selection/bias; do not add them decoratively.

## Parser and dependency policy

- Strict-hot parsers use prepared storage and bounded wire-native scanning or
  cursors for the selected JSON, binary, FIX/SBE or protobuf representation.
  Avoid heap-first DOM traversal, padded-text preparation, generic fallback
  routes and compatibility structures masquerading as a real normalized
  strategy-fed stream.
- A project's prohibition of particular libraries or preference for its own
  string/memory primitives must be preserved **when that project declares it**.
  Such bans are implementation policies, not universal claims that a named
  third-party library cannot be performant or safe elsewhere.
- Keep exchange-specific fields, endpoint/control grammar and parser quirks
  with the venue owner. Do not put schema parsing into generic network framing.

## Offline computation under the same strict contract

Offline solvers, backtests and finance require an explicit additional project
or user requirement to apply the same no-allocation, no-float, bounded-work,
no-lock and no-diagnostic restrictions; the live system's selection alone
does not extend them to offline work.
Check scenario/state/stack bounds, integer arithmetic, overflow/refusal and
event application without pretending that offline linkage proves H0 live
latency or trading readiness. Diagnostics and independent oracles stay outside
the strict computational core.

## Strict veto and proof

For an actual change covered by the selected strict scope, block concrete allocation,
blocking, floating-point, unbounded parse/work, hidden compatibility fallback,
silent stale/gap recovery, wrong-order publication, or data-lifetime violations.
For existing heap, floating-point or virtual-dispatch violations, report the
exact divergence and its impact on the task. Do not silently expand the task
into arithmetic, API or architecture changes to repair pre-existing violations;
route material scope decisions through root under the existing rules.
Select independent reviewers from the
[critical review matrix](delegation-and-review.md#critical-review-matrix),
including the network trio where applicable.
Missing unrequested benchmarks limit performance claims; they are not by
themselves a functional veto or permission to run measurements.
