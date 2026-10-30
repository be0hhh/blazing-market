# Critical-path tracing and H0/H1/C/D separation

Classify by the work actually executed in the selected product, not by path
name, subsystem label, or an isolated function benchmark.

| Class | Meaning | Typical work |
| --- | --- | --- |
| H0 | Critical steady-state event-to-consumer or event-to-action path | Poll/receive, framing, hot decode, normalization, publication, inline calculation, prepared terminal send when applicable |
| H1 | Hot-adjacent correctness/state consumed by H0 | ACK/user reader, pending correlation, bounded handoff, readiness and operational counters |
| C | Cold/control and lifecycle | Resolve/connect/auth/subscribe, configuration, metadata refresh, registration, reconnect/backoff, reload, preallocation |
| D | Deep diagnostics | Logs, trace collection, probes, dashboards, reports, status rendering and viewers |

## Prove the selected chain

1. Start at the actual product startup, connector/route registration and
   selected wire/protocol. Inspect current build graph, loaded symbols,
   dispatch/registration and relevant runtime configuration.
2. Follow the active receive or source path through framing, parse callback,
   normalized payload, event/book state and direct consumer. If in scope,
   continue through strategy/risk/admission, prepared order payload,
   correlation and terminal transport write.
3. Exclude or separately label mock, compatibility, recorder, backtest,
   benchmark, test and offline implementations unless they are the target.
   Distinguish the evidence for an offline computational core with H0-like
   restrictions from live H0 reachability.
4. If production compile/load information is absent or profile-mismatched,
   report `surface unavailable` and limit findings to source analysis. Do not
   infer a fallback path or select another build merely to obtain a green trace.

## Cost and resource checks

Computation/memory latency and network latency are separate review capabilities.
Use [transport-and-readiness.md](transport-and-readiness.md) for RX/TX and Linux
system context, and the [critical review matrix](delegation-and-review.md#critical-review-matrix)
for required independent reviewers: the trio applies to actual network H0/H1
changes; pure C/D expertise follows concrete risk and bounded hot-impact inspection.

- On the proven path inspect dynamic allocation/growth, exception/error paths,
  virtual/indirect dispatch, locks, syscalls, sleeps, I/O, logging/formatting,
  timestamp capture, copies, temporary payloads, buffer lifetime and
  decompression work. Determine whether each is necessary or measured rather
  than issuing a blanket language-independent ban.
- Inspect queues and rings: producer/consumer ownership, capacity, pressure,
  memory ordering, false sharing, fairness, backlog, drop/overflow signal and
  bounded drain. On a hot low-latency path, publish available market data
  immediately without waiting to fill a batch; limits may guard fairness.
  Outside that path, batching requires explicitly agreed size, time and
  overload bounds.
- Inspect state size and locality (`sizeof`/alignment, cache lines, stack,
  prefetch/SIMD if relevant), branch-prediction hints and atomic contention.
  Hints and micro-optimizations are candidates until actual bias and cost are
  measured. Avoid decorating branches without evidence.
- Keep control-plane work and deep diagnostics out of the critical loop unless
  explicit production-hot overhead evidence supports them. Operational
  timestamps, deadlines, gap/risk guards and indispensable terminal writes
  must not be removed as if they were merely diagnostics.
- Fix the root cause: slow drain, parser cost, queue pressure, scheduling,
  memory/CPU placement, clock-domain error, or overbroad serialization.
  Avoid extra abstraction, copy, lock, queue, syscall or clock on a send path
  without an actual contract or measurable need.

## Latency claims

- A faster DNS lookup, startup handshake or reconnect is a cold/control
  improvement, not automatically lower steady-state tick-to-consumer latency.
- Do not confuse an isolated function benchmark with full-route improvement.
  State what portion of the active chain was actually exercised.
- Apply [ultra-low-latency-profile.md](ultra-low-latency-profile.md) to hot
  operations when user/project explicitly identifies the market/trading system
  as LOW LATENCY, or explicitly selects that profile. H0, market data or “fast”
  alone is insufficient; clarify unclear intent and preserve project scope.
