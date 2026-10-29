# Latency, throughput, compiler and verification evidence

## Separate evidence classes

- Source/registration inspection: static evidence only.
- Compiler/build target and generated machine code: compilation and codegen
  evidence, not active runtime routing or performance proof.
- Targeted unit/integration test: the named behavior exercised at its scope.
- Runtime/local replay: the selected local binary and workload, not live venue.
- Performance: a measured comparable baseline and changed version.
- Live: explicitly authorized real exchange, account or deployed session
  path. Never infer from any earlier evidence category.

All named tests/checks require the exact authorization imposed by the active
user/project workflow. Missing unrequested checks limit conclusions; they do
not turn a static source correction into a falsely failed implementation.

## Baseline before promotion

Before claiming a measured speedup, record and match:

- Exact source revision and affected production translation unit or runtime.
- Compiler version, standard library, optimizer flags, LTO/linker, CPU target,
  dependencies, portable/native selection, and binary actually executed.
- Hardware model, CPU affinity, thread/core placement, SMT/turbo and relevant
  memory/cache state, virtualization and background load.
- Input corpus, market/feed shape, parser wire, payload sizes, distributions,
  burst conditions, queue state, warm-up and sample definition.
- Timestamp location and clock domain, metrics mode/instrumentation overhead,
  measurement duration and number of independent trials.
- Throughput, saturation, backlog/queue age, error/drop rate and latency
  percentiles (especially tails such as p99/p99.9) appropriate to the goal.

Avoid false precision and compare like-for-like. A reduction in instructions,
an inline annotation, a new SIMD branch or a microbenchmark does not prove an
end-to-end improvement. State the cost/benefit and the unmeasured remainder of
the actual selected path.

## Useful measurement discipline

- State objective and relevant latency/throughput/capacity budget before
  proposing a change; distinguish exchange/network RTT from local processing
  and cold lifecycle timings.
- Inspect optimizer output and assembly for instruction selection, register
  pressure, vectorization, branches, code size, object/stack layout and actual
  target flags only when available and relevant. Assembly inspection is still
  separate from runtime evidence.
- Prefer a matched reproducible before/after experiment on a representative
  workload. Check semantics with independent assertions; do not optimize by
  silently dropping messages, weakening bounds or reducing correctness tests.
- Separate functional clocks and deadlines from optional diagnostic metrics.
  Diagnostic probes need a declared owner and measured production-hot cost
  before they are retained in a critical loop.
- Preserve selected command, working directory, exit status and full log.
  Static candidates may be proposed without running unauthorized checks.
- Promote an optimization from `candidate` to measured `improvement` only when
  its exact reported metric has supported evidence. Explain unresolved noise,
  environmental mismatches or insufficient sample sizes.
