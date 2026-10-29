# Transport, sessions, selected-wire readiness

Identify the exact failure or cost stage before proposing a transport change:
name resolution, TCP/proxy connect, TLS/WS/FIX/gRPC setup, authentication,
subscription/ACK, first data frame, steady-state receive, heartbeat, reconnect,
terminal write or order/user ACK reader. A cold-stage improvement is not
automatically H0 latency improvement.

## Transport correctness

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
