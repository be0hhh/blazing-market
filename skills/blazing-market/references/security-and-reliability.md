# Security, bounded reliability and fault containment

## Resource and failure contracts

- Every dynamic resource needs an owner, fixed bound or bounded allocation
  phase, and a terminal overflow/refusal policy. Measure worst-case work,
  queue capacity, stack, decode depth and retry amplification.
- Keep lost, stale, partial, disconnected, unknown, overloaded and capacity-
  exceeded states distinguishable. Do not report fabricated continuity,
  readiness or recovery when source evidence is missing.
- Producers must have explicit slow-consumer/backpressure behavior; a
  diagnostic or UI consumer should not block a live data producer unless the
  product deliberately defines that dependency.
- Retries/reconnects are bounded and do not reuse stale generations, duplicate
  financial events or turn failure into a storm. Preserve exact failure stage.
- Handle malformed input, truncated files, partial I/O, disk failure, process
  restart and recovery without silently erasing authoritative facts. Where
  persistence is involved, check atomic replacement, durable ownership and
  reader compatibility before claiming crash safety.
- Test capacity and adverse conditions with fixtures/replay, and do not
  describe those as evidence of a live exchange/session.

## Trust and capability boundaries

- Credentials and native authentication remain with the designated session
  owner. Do not expose them through public market packets, logs, status,
  traces, browser views, generated reports or agent handoffs.
- Authenticate IPC peers where trust boundaries require it; validate message
  size, schema/layout, identity, epoch/generation and owner before consuming
  a request or issuing a privileged operation.
- Keep read-only views physically and transitively separate from mutation,
  account, session and order-control capabilities. A UI, viewer, recorder or
  monitoring agent must not become another owner of trading authority.
- Check the entire dependency/capability closure, not only a direct import.
  A helper can accidentally introduce the forbidden capability transitively.
- Use appropriate file/socket permissions and clear provenance for snapshots,
  metadata, logs and exported artifacts. Missing authority does not permit
  silent downgrade, fake readiness or insecure fallback.

## Safety versus performance

Latency is part of the behavior contract, but never trade away event ordering,
boundedness, TLS identity, numeric meaning, permission, or financial integrity
to remove an instruction or short circuit a check. Move unnecessary work out
of H0 when possible; preserve operational deadlines, actual I/O, gap handling
and risk protection required by the live system.

When two causal hypotheses remain, choose the smallest authorized
counterexample that predicts different results. Once the cause is established,
do not require repeated smoke tests merely for ritual completeness.
