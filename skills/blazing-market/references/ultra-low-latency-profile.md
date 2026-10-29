# Ultra-low-latency profile: strict H0 contract

This profile preserves the strong low-level engineering restrictions used by
the originating system. It is **opt-in**: apply its vetoes when the project or
user explicitly selects an ultra-low-latency/H0 contract, not automatically
to every language, runtime, target or latency budget. Do not weaken a project's
already active stricter policy merely because Blazing Market is portable.

## H0 computation and live event loop

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

A project may explicitly apply the same no-allocation, no-float, bounded-work,
no-lock and no-diagnostic restrictions to an offline finance/planning solver.
Check scenario/state/stack bounds, integer arithmetic, overflow/refusal and
event application without pretending that offline linkage proves H0 live
latency or trading readiness. Diagnostics and independent oracles stay outside
the strict computational core.

## Strict veto and proof

For an actual selected strict H0/H1 change, block concrete allocation,
blocking, floating-point, unbounded parse/work, hidden compatibility fallback,
silent stale/gap recovery, wrong-order publication, or data-lifetime violations.
Require the latency + relevant domain independent review pair if available.
Missing unrequested benchmarks limit performance claims; they are not by
themselves a functional veto or permission to run measurements.
