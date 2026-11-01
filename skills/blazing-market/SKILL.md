---
name: blazing-market
description: "Analyze, review, design, and develop crypto and financial-market software in any language: market-data feeds/parsers, hot/cold paths, network latency, trading/order execution, financial calculations, session recovery and evidence-based performance. Includes scoped delegation and independent review for complex tasks."
---

# Blazing Market

Apply the existing project's rules, the user's actual task and permissions, and
these portable engineering contracts. Do not assume a particular language,
exchange, build system, runtime, orchestration tool, trading model, or latency
target. The skill is an audit and implementation guide, not an authority grant.
Explicit project rules replace corresponding skill workflow rules; the skill
fills gaps. Do not report an overridden stage as incomplete.

## Route bounded context

1. Establish the requested observable outcome, affected scope, current behavior,
   authorized checks, and applicable repository instructions. Read root and
   nearest nested `AGENTS.md` or equivalent project policy. Read unchanged rules
   once per active context; revisit them when the scope or policy changes.
2. Discover relevant files and registrations before opening broad source trees.
   Search within the owning module, inspect declarations, callers, consumers,
   analogous implementations, and affected build or runtime registrations.
   Missing search results from incomplete tooling are not proof of absence.
3. Read only the references relevant to the task; do not load the entire bundle
   merely because the task mentions performance or agents:

| Trigger | Read |
| --- | --- |
| Ownership, API/ABI, layout, dependencies, compiler, structure, reuse, duplication, repeated checks/work or unnecessary layers | [architecture-and-contracts.md](references/architecture-and-contracts.md) |
| Hot path, computation/memory latency, allocation, queues, cache or pipeline | [hot-cold-paths.md](references/hot-cold-paths.md) |
| Feeds, normalizers, parser registration, snapshots/deltas, timestamps | [market-data-and-parsers.md](references/market-data-and-parsers.md) |
| Network RX/TX latency, DNS, TCP/UDP, TLS/SSL, WS/REST/FIX/gRPC, socket/kernel/NIC, Linux system context, sessions or readiness | [transport-and-readiness.md](references/transport-and-readiness.md) |
| Strategy, order, accounting, risk, bounded runtime and terminal send | [runtime-and-execution.md](references/runtime-and-execution.md) |
| Backpressure, recovery, partial state, credentials, trust boundaries | [security-and-reliability.md](references/security-and-reliability.md) |
| Benchmarks, compiler evidence, latency claims and verification | [measurement-and-evidence.md](references/measurement-and-evidence.md) |
| Code changes, test necessity, check scope, permissions, plans and completion | [workflow-and-plans.md](references/workflow-and-plans.md) |
| Substantive code work, complex or high-risk work, agent delegation, simplicity, unnecessary test/fixture complexity or specialist review | [delegation-and-review.md](references/delegation-and-review.md) |
| Network placement, compression, recording, diagnostics or UI | [specialized-surfaces.md](references/specialized-surfaces.md) |
| Explicit LOW LATENCY market/trading system, selected strict profile or strict compute contract | [ultra-low-latency-profile.md](references/ultra-low-latency-profile.md) |
| Significant findings, code-review report or handoff | [report-contract.md](references/report-contract.md) |

## Core workflow

1. **Prove the active surface.** Establish actual entry/registration, selected
   protocol/wire, compiled or loaded implementation, runtime dispatch, data
   publication, consumer, and (if in scope) execution/send tail. Distinguish
   test/benchmark/compatibility code and offline calculations from production.
   If the relevant build/route artifact is absent, say `surface unavailable`;
   continue source analysis without pretending the route is proven.
2. **Classify the work.** Mark critical steady-state work `H0`, adjacent state
   and handoffs `H1`, lifecycle/control `C`, and deep diagnostics `D`. Classify
   by actual execution, not filename. Cold safety may gate H0 without being H0
   latency. A project may impose H0-like compute restrictions on offline code
   without asserting an active live route.
3. **Trace semantics before cost.** Inspect event identity/order, epochs,
   timestamps and freshness, numeric units/scale/overflow, lifetime, capacity,
   backpressure, recovery and consumers. For execution, include order IDs,
   ACK/fill/cancel races, authority, reservations and unknown outcomes. Preserve
   actual observable behavior unless a change was explicitly agreed.
4. **Find the root cause.** Inspect allocations, growth, locks, blocking, copies,
   atomics, cache/false sharing, scheduler, batch fairness, I/O and diagnostics
   only on the proven path. Seek an existing owner and suitable implementation
   before introducing a helper, abstraction or parallel implementation.
   Apply the [minimum-checks rule](references/architecture-and-contracts.md#minimum-necessary-checks-and-repeated-work)
   across the whole affected chain, including module boundaries, admission,
   sends and recovery: trust established owner guarantees and remove redundant
   checks/work while preserving necessary correctness guarantees.
5. **Apply the selected constraint profile.** Bounded ownership, semantic
   correctness and truthful evidence always apply. The
   [ultra-low-latency profile](references/ultra-low-latency-profile.md) applies
   to hot operations when user/project explicitly identifies the market/trading
   system as LOW LATENCY, or explicitly selects that profile. H0 labels, market
   data or “fast” alone do not select it; clarify unclear intent. Project policy
   controls scope; offline strict computation needs an explicit extra requirement.
6. **Respect task authority.** Follow the active user/project/runtime policy in
   [workflow-and-plans.md](references/workflow-and-plans.md). Study/review is
   read-only; a plan or worker naming a command grants no permission. This
   skill adds no separate approval requirement for ordinary tests already
   covered by that policy. For substantive code work or a non-trivial cascade,
   read the delegation contract even when the user did not mention agents.
   The root retains shared-file ownership, user decisions and integration.
7. **Check and report honestly.** Preserve required tests and contracts; prefer
   sufficient existing verification. Add a focused regression for a concrete
   uncovered defect or substantial behavioral risk under
   [workflow-and-plans.md](references/workflow-and-plans.md), which owns test
   necessity, verification scope and stopping rules. Separate static, schema, build,
   targeted-test, runtime, performance and live evidence. A source-level
   optimization is a `candidate` until comparable before/after measurements
   prove a result. Report blockers and unrun verification distinctly.

## Review gates and decisions

- For substantive code tasks, require early and final independent simplicity
  review when agents are available. Select critical reviewers from the
  [canonical review matrix](references/delegation-and-review.md#critical-review-matrix),
  including its separate network latency and transport correctness roles.
  Review integrated code; report unavailable reviews without simulating them.
- For risky cross-boundary design, settle behavior, failure semantics, ownership,
  and acceptance with the user before dependent edits. For a high-risk or
  non-trivial full-cascade plan, request a fresh independent plan review before
  user agreement when available. A small task needs no full cascade or durable file.
- For a complex full cascade, research returns to root before a separate
  designer starts. Obtain user agreement on the ready solution before first
  implementation; an unchanged agreed plan needs no renewed approval.
- Do not assume a global stale-data, gap-recovery, order-resend, or fallback
  policy. If the owning contract is unspecified and the difference is material,
  mark a blocker and ask. Independent authorized work may continue.
- Preserve unrelated work, project permissions, source of truth, generated
  registrations, and current consumer closure. No hook or agent grants authority.

## Output

Use [report-contract.md](references/report-contract.md) for non-trivial
findings. Lead with the concrete result and severity; identify exact
paths/symbols, active route and H0/H1/C/D classification, semantic risk,
evidence level, narrow next check, and any unresolved decision. Omit empty
checklists and unsupported speedup or readiness claims.
