---
name: blazing-market
description: Analyze, review, design, and develop software for crypto and other financial markets in any language. Use for market-data feeds and parsers, hot/cold paths, network latency, trading and order execution, financial calculations, session recovery, and evidence-based performance work. Includes scoped agent delegation and independent review for complex market-software tasks.
---

# Blazing Market

Apply the existing project's rules, the user's actual task and permissions, and
these portable engineering contracts. Do not assume a particular language,
exchange, build system, runtime, orchestration tool, trading model, or latency
target. The skill is an audit and implementation guide, not an authority grant.

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
| Ownership, API/ABI, layout, dependencies, compiler or structure | [architecture-and-contracts.md](references/architecture-and-contracts.md) |
| Hot path, computation/memory latency, allocation, queues, cache or pipeline | [hot-cold-paths.md](references/hot-cold-paths.md) |
| Feeds, normalizers, parser registration, snapshots/deltas, timestamps | [market-data-and-parsers.md](references/market-data-and-parsers.md) |
| Network RX/TX latency, DNS, TCP/UDP, TLS/SSL, WS/REST/FIX/gRPC, socket/kernel/NIC, Linux system context, sessions or readiness | [transport-and-readiness.md](references/transport-and-readiness.md) |
| Strategy, order, accounting, risk, bounded runtime and terminal send | [runtime-and-execution.md](references/runtime-and-execution.md) |
| Backpressure, recovery, partial state, credentials, trust boundaries | [security-and-reliability.md](references/security-and-reliability.md) |
| Benchmarks, compiler evidence, latency claims and verification | [measurement-and-evidence.md](references/measurement-and-evidence.md) |
| Code changes, permissions, checks, plans and completion | [workflow-and-plans.md](references/workflow-and-plans.md) |
| Substantive code work, complex or high-risk work, agent delegation, simplicity or specialist review | [delegation-and-review.md](references/delegation-and-review.md) |
| Network placement, compression, recording, diagnostics or UI | [specialized-surfaces.md](references/specialized-surfaces.md) |
| Explicit ultra-low-latency or no-heap/no-floating-point H0 contract | [ultra-low-latency-profile.md](references/ultra-low-latency-profile.md) |
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
5. **Apply the selected constraint profile.** Bounded ownership, semantic
   correctness and truthful evidence always apply. Hard no-heap/no-float/
   no-virtual/no-RTTI restrictions apply when the user or project selects the
   [ultra-low-latency profile](references/ultra-low-latency-profile.md), not
   silently to every Java, Go, Rust, C++, C#, or other runtime.
6. **Respect task authority.** Follow the active user/project/runtime policy in
   [workflow-and-plans.md](references/workflow-and-plans.md). Study/review is
   read-only; a plan or worker naming a command grants no permission. This
   skill adds no separate approval requirement for ordinary tests already
   covered by that policy. For substantive code work or a non-trivial cascade,
   read the delegation contract even when the user did not mention agents.
   The root retains shared-file ownership, user decisions and integration.
7. **Check and report honestly.** Preserve required tests and contracts; add a
   focused regression only when useful. Separate static, schema, build,
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
  and acceptance with the user before dependent edits. For a high-risk or full
  cascade plan, request a fresh independent plan review before user agreement
  when available. A small task needs no full cascade or durable file.
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
