# Transport, sessions, selected-wire readiness

Identify the exact failure or cost stage before proposing a transport change:
name resolution, TCP/proxy connect, TLS/WS/FIX/gRPC setup, authentication,
subscription/ACK, first data frame, steady-state receive, heartbeat, reconnect,
terminal write or order/user ACK reader. A cold-stage improvement is not
automatically H0 latency improvement.

## Network latency

Trace receive and transmit separately: DNS, TCP/proxy connect, TLS/SSL,
WS/REST/FIX/gRPC protocol work, socket I/O, kernel queues and NIC, then the
application drain/publication or terminal-write boundary. Distinguish setup,
steady state, exchange response and local processing costs; include tails,
jitter, burst drain, backlog and backpressure rather than RTT alone.

The network latency specialist examines syscall/wakeup behavior, socket buffers,
partial-drain fairness, packet aggregation, offloads, IRQ/NAPI, RSS/RPS/XPS,
queue/core affinity and CPU/NUMA locality when relevant evidence is available.
Transport correctness remains a separate review of trust, framing, partial I/O,
deadlines and session recovery. Placement expertise establishes endpoint or
location claims; it does not substitute for socket/kernel/NIC analysis. Use the
[critical review matrix](delegation-and-review.md#critical-review-matrix): actual
network H0/H1 changes require the independent trio; pure C/D work selects
expertise by concrete risk after the matrix's bounded inspection establishes
no hot RX/TX effect. Investigate uncertainty before claiming the cold exemption.

Apply the [minimum-checks rule](architecture-and-contracts.md#minimum-necessary-checks-and-repeated-work)
through the affected RX/TX, handoff, send and recovery chain. Trust established
owner guarantees across modules; remove repeated validation, reads, copies and
preparation. Qualify immutable conditions at setup/bind and use owner events for
mutable state where semantics allow. Retain checks for concrete changes across
partial I/O, queues or reconnect, preserving wire/TLS, lifetime, capacity and
current-session/action authority at sufficient owners. Explain significant
retained/added checks without a per-if register or new proof wrappers.

## Linux system context and passive observations

The root coordinates relevant passive observations once per context and passes
their sources and provenance to reviewers; reviewers independently interpret
the evidence and inspect source. This skill grants no universal permission to
inspect an OS, write a cache or use SSH. Follow the active task/user/project
policy; absent authority, report unavailable system evidence and continue static
analysis. Observation is separate from tuning or workload execution.

- Identify the actual selected host and observation time. A local, WSL or VM
  environment is not evidence for a selected remote target. Record relevant
  host/boot/kernel, network namespace, NIC/driver and scope identity, plus
  virtualization/container boundaries where they affect conclusions.
- Collect only relevant current configuration: CPU topology/affinity and NUMA,
  NIC queues/IRQ placement, NAPI/RSS/RPS/XPS, offloads/coalescing, socket/kernel
  limits and routes/MTU as needed. Do not infer target configuration from
  defaults, another host or an old result. Distinguish config from observations
  of current load, drops, pressure, scheduling or queue occupancy.
- Reuse an authorized cache only for its actual host, boot, kernel, network
  namespace, NIC and selected scope. Check current configuration before calling
  cached values current; unvalidated cached facts are historical. Volatile
  load/pressure claims require fresh observations. Invalidate affected facts
  when identity or configuration changes. Store sources/provenance, never
  credentials or reusable user consent. Plan/no-write work never writes cache.
- When an explicitly chosen housekeeping/SYSTEM CPU is configured for the
  collector, constrain collector affinity to it. Do not guess workload placement
  or move application/IRQ work to make observation convenient. If the configured
  collection constraint cannot be met, report the limitation.
- No automatic tuning, package installation, traffic generation, packet capture,
  performance tracing or eBPF. Such actions require their own applicable task
  authority. SSH requires separately explicit user/project authorization for
  the host and operation; preserve host-key and credential trust, bound timeouts
  and failure attempts, and never weaken validation or retry indefinitely.

## Transport correctness

- Preserve required peer, framing, memory, session and unknown-outcome guarantees
  at their sufficient owning boundaries; downstream code trusts established
  guarantees unless an intervening change requires a current check. Removing a
  duplicate check does not weaken the underlying protocol or trust requirement.
- Trace the actual caller from configured route and session owner to the
  selected socket/client and framing/parser boundary. A compiled helper or
  syntactically valid config is not proof that live dispatch selects it.
- Enforce appropriate certificate authority loading, server name indication,
  hostname verification and protocol authentication. Never lower TLS or peer
  validation requirements to improve timing.
- Check nonblocking semantics, deadlines and bounded timeouts; handle partial
  reads/writes, interruption, EOF, handshake WANT_READ/WANT_WRITE-equivalents,
  short sends, backpressure and retry ownership explicitly.
- Check frame type, control frames, fragmentation, masking where applicable,
  compression/decompression bounds, maximum message size and buffer compaction.
  Treat malformed/truncated frames and decompression exhaustion as explicit
  observable states rather than unsafe continuation.
- Establish buffer/view lifetime across receive, decode, normalized publish,
  queue handoff, reconnect and session retirement. No borrowed view may outlive
  the producing bytes or silently straddle generations.
- Keep reconnect, backoff, authentication and configuration in the correct
  control owner. No unbounded retry, sleep or reconnect storm in critical
  compute/event loops; no silent alternate-protocol fallback to hide failures.
- Track readiness by exact account/product, **selected native route** and
  session/transport generation, not a single timeless connected flag. On
  disconnect/reconnect, invalidate stale bindings and reconcile in-flight
  commands/feedback according to their owner; do not treat a re-established
  socket as proof that account metadata, subscriptions, order feedback and risk
  admission are ready.
- Keep a compatible configuration reload separate from reconnect, an explicit
  Stop and resource retirement. Do not dispose of unchanged live subscriptions,
  active-order correlation or strategy state as a side effect of unrelated
  configuration. Unsupported structural changes require a declared restart
  rather than an unplanned fallback route.
- Inspect locks, atomics, queues, copies, syscalls and clock captures before a
  terminal order write. Necessary actual I/O stays; avoidable pre-send work
  needs a contract or measured reason.

## Capability/readiness proof

Trace the complete relevant closure, not a boolean configuration field:

1. Registered exchange/product/venue and operation.
2. Selected public/private/order wire, endpoint, route and subscribe grammar.
3. Actual runtime callback/parser and typed normalized payload.
4. Source/session/auth/metadata/capacity gates, where applicable.
5. Producer publication and direct consumer readiness.
6. For orders, exact authorized account/product/session generations, unique
   identifier availability, bounded command/feedback capacity, authorized
   risk admission and canonical pre-submit intent/correlation reservation,
   then prepared terminal send and distinct local/venue outcomes.

Distinguish public market-data support, private user events, account
reconciliation, terminal order capability and full trader readiness. One
available section does not prove another. Refuse unsupported selected wires,
missing parser coverage, absent native session proof, or generation mismatch
without manufacturing readiness through a compatibility route.

## Network-placement evidence

Endpoint IP, DNS, a ping result or a cloud region label does not prove the
matching-engine location or an availability zone. Keep region/edge/AZ/engine
claims at their actual evidence levels. Compare transport-specific connect,
TLS, first-frame and exchange ACK observations with tail latency, jitter,
failure behavior and route stability rather than average ICMP alone. Read
[specialized-surfaces.md](specialized-surfaces.md) when placement is in scope.
