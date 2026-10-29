# Reporting, handoff and evidence contract

Lead a non-trivial report with the concrete outcome or finding, not a generic
checklist. Be concise, answer in the user's language and omit empty sections.
Use exact project-specific paths/symbols only in results, never invent anchors.

## Severity

| Label | Meaning |
| --- | --- |
| `BLOCKER` | Undefined or violated contract that must be resolved before dependent use/change |
| `HIGH` | Likely production/live correctness or safety defect |
| `MEDIUM` | Material correctness, reliability or maintenance issue |
| `LOW` | Scoped cleanup or improvement |
| `NOTE` | Observation without a confirmed actionable defect |

## Proof labels

| Label | Claim it supports |
| --- | --- |
| `static-only` | Source, config, build-graph or diff inspection; no commands claimed run |
| `schema proof` | Named schema/lint/format verification and result |
| `build proof` | Named selected build with final result |
| `targeted-test proof` | Selected affected tests and results |
| `runtime proof` | Named local binary/process and observed behavior |
| `browser proof` | Actual UI action, result and fixture/real provider origin |
| `model proof` | Exact authorized model evaluation and result |
| `performance proof` | Before/after matching workload and environmental measurement |
| `live proof` | Exact authorized exchange/network/trading or production-like exercise |

Proof types are independent. A successful compilation doesn't prove runtime
readiness; a local smoke does not prove live exchange capability; disassembly
does not prove latency; a worker/reviewer statement is not test proof.
For each declared check, report the exact selected command, working directory,
relevant target/profile and **latest completed integer exit code**. `verified`
requires every task-required evidence type and every declared command to have
latest exit code `0` for the current revision. Preserve failed and successful
attempt history; a newer failure overrides an older pass for the gate, not the
history. `done_unverified` may be an honest completed implementation when
tests were not selected or their required evidence is unavailable.

## Review and audit report

Include only relevant items:

- Result and verdict (`CLEAR` for inspected scope only, or findings).
- Scope and actual source anchors (path, symbol, registration, consumer).
- Proven or unavailable build/route surface and H0/H1/C/D classification.
- Violated invariant, event/failure semantics, suspected cost and severity.
- Exact commands/results actually observed, with evidence type and limits.
- Smallest safe next test or source change, its authorization needs and risks.
- Unresolved decisions, foreign owner or blocked boundary.

For performance, explicitly separate `candidate` from measured `improvement`.
State workload, machine, compiler, build profile, affinity, sample/timing
definition and metric before a numeric speedup claim.

## Worker handoff

- Outcome, inspected/changed paths, concrete source evidence and affected
  callers, consumers, registrations or shared owners.
- Exact checks run and exit statuses; tests not run remain unrun.
- Limitations, remaining risk, dependency, material question and integration
  action. A worker does not mark its own task verified.
- When reports conflict, supply disputed claim and anchors, not only opinions.

Truncation in displayed output must be labeled and narrowed on the next read;
retain complete logs for selected checks. Do not use empty error excerpts as
proof of success. Avoid unsupported precision in latency, placement, readiness
and financial conclusions.
