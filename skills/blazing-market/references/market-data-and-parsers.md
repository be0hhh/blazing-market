# Market-data, parser and event-semantics contracts

## Active parser and normalization

- Start at exchange/feed registration, selected wire and actual runtime
  dispatch/callback; then follow the concrete parser, normalized event/book
  representation and consumer. A nearby parser file or static symbol match is
  not proof that the live path uses it.
- Trace each requested **logical stream to its selected physical exchange wire**,
  endpoint/subscription and parser callback. A physical wire may carry several
  logical streams: verify explicit bounded fanout, dispatch identity and each
  downstream consumer rather than assuming one wire equals one logical feed.
  Keep venue-specific routing/schema ownership with the venue/normalizer owner;
  do not duplicate wire decisions in unrelated applications.
- Distinguish binary, text, FIX/SBE, protobuf, REST snapshots, reference data,
  compatibility layers, private user messages and direct strategy-fed streams.
  Capability or configuration presence does not prove runtime readiness.
- Put transport framing and decompression at the transport boundary; keep
  venue schema parsing and numeric interpretation at the owning parser, and
  emit a coherent typed/normalized contract to consumers.
- Audit the selected wire's **field coverage**, required/optional normalized
  fields and flags, absent-vs-zero meaning and schema drift. A parser that
  accepts a frame but silently loses fields used by consumers is not complete;
  changed normalized contracts require consumer closure.
- Bound every parse cursor, field length, decode depth, escape, element count,
  frame/decompression capacity and write extent. Specify malformed/partial
  input behavior, parsing failure and overflow without data invention.
- For explicit strict-hot profiles, prefer borrowed spans/views with proved
  lifetimes, prepared storage, known-field scanning and bounded binary cursors.
  Do not force one language's parser library prohibition onto other runtimes.

## Public versus private capacity

- For throughput-first public ingestion, enforce bounded queues and explicit
  overload, lag and drop accounting. Preserve sequence/gap and freshness
  evidence; a drop must not masquerade as a complete event stream.
- For private user, account, order-command and execution-feedback paths,
  insufficient bounded command/feedback capacity must **refuse admission
  before terminal submission** or use an explicitly defined non-H0 backpressure
  mechanism. Already accepted commands and authoritative feedback still need
  owned tracking/reconciliation; never silently discard either.
- Inspect backpressure at every shared wire, logical-stream fanout, consumer
  and private/order feedback boundary. Do not make public ingestion wait on
  dashboards, persistence or slow independent consumers without an explicit
  product contract.

## Semantic correctness gate

Apply to actual live-event changes and to offline computations whose result
contract is consumed by live code:

- **Identity and order:** event/update/sequence IDs, duplicates, out-of-order
  delivery, gaps, source/session epoch and reconnect boundaries.
- **Book semantics:** snapshot/delta alignment, replay, rebase, gap recovery,
  ordering and readiness. Do not universally require a snapshot before any
  delta processing or assume a globally safe recovery action. Preserve the
  venue's and owning consumer's declared semantics.
- **Time/freshness:** exchange event/processing time, local receive time and
  monotonic elapsed time are distinct clock domains. Preserve units,
  precision, skew assumptions, warm-up, stale thresholds and generation.
- **Numeric meaning:** price/size scaling, tick and lot increments, rounding,
  signedness, sentinels, range, overflow, decimal conversion and minimum
  constraints where applicable. Avoid unannounced floating-point semantic
  changes even when the host language supports floating point.
- **Ownership:** lifetime of every borrowed frame, normalized view, shared
  book, publication, ID and queued event; capacity and terminal refusal/drop
  behavior. Prove that producer storage outlives its consumers.
- **Degraded data:** stale, missing, partial, unknown, reconnecting, recovery,
  and resynchronization states must have subsystem-owned policy. No global
  fail-closed, last-good, automatic fallback or silent recovery default.
- **Preservation:** explicitly distinguish behavior that stays unchanged from
  intentional updates. An optimization must not change event identity, units,
  readiness, ordering or failure semantics accidentally.

If degraded/recovery semantics materially affect the proposed H0/H1 change
but are undefined, mark `BLOCKER`, ask for the owning decision and stop the
dependent edit. Static route discovery alone cannot establish a live feed.
