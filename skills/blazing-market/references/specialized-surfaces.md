# Specialized surfaces: placement, recording, compression and observability

Read only for the selected domain. These are lenses, not a requirement to
introduce networking, compression, telemetry or a GUI into every project.

## Network placement and lane selection

- Separate DNS endpoint, edge/front-door, physical region, AZ and matching
  engine evidence. IP geolocation, ICMP ping or cloud label is not proof of
  matching-engine placement.
- Distinguish a diagnostic plan from an actual runtime route/lane mutation.
  A probe must not change live placement or routing authority implicitly.
- For transport-specific latency compare TCP/TLS/first frame and exchange ACK
  against relevant tails, jitter, failures, source tuple/lane ownership,
  anti-flap hysteresis and promotion windows when used.
- Route socket/kernel/NIC costs, CPU/IRQ/NUMA placement and queue pressure to
  [network latency expertise](transport-and-readiness.md#network-latency).
  Placement expertise owns endpoint/location claims; neither observation nor
  a placement finding authorizes routing, affinity or kernel changes.
- Keep snapshot and data-plane safety separate from control-plane decisions.

## Recording, corpus and compression

- Distinguish raw source bytes, a recorded corpus, normalized/replayed records,
  and the active live feed. Do not present recorder or backtest paths as proof
  of a production parser.
- For a lossless compression pipeline, verify full decode equality and
  corrupt/truncated behavior, not merely a compression ratio.
- Compare ratio, encode/decode latency, block size and overhead with named
  baseline codecs, matched corpus identity and stream family. Do not rank
  unrelated quote, trade and depth workloads as a single universal winner.
- Keep codec/pipeline identity, availability, extension, metadata, writer and
  reader contracts consistent. Planned or experimental codecs are not runtime
  capabilities until real encode/decode/inspection support is present.
- Keep offline research and diagnostics separate from hot runtime unless the
  project explicitly calls for and measures live integration.

## Observability and UI projections

- Treat deep logs, traces, status formatting, dashboard renderers, network
  probes and compression reports as `D` unless their measured bounded
  production-hot cost and ownership are explicit.
- Preserve working clocks, deadlines, gap counters, safety state and order
  truth when removing diagnostic-only instrumentation.
- Separate per-instance and aggregate metrics, missing versus zero samples,
  timestamp definitions, replay/synthetic versus live data provenance, and
  actually observed versus estimated latency.
- Keep a viewer or projection free of mutation, order and session-control
  capabilities, including through transitive dependencies. Choose enforcement
  for the architecture and preserve stricter project physical boundaries.
  A slow GUI, browser worker, context loss or log consumer must not create
  uncontrolled backpressure in the market-data producer.
