# Architecture, ownership, layout and dependency contracts

Read for public interfaces, cross-module changes, storage, compiler/target
choices, architecture and structural simplification.

## One authoritative owner

- Identify the actual producer, consumer, state owner, dependency direction,
  registration and build target before moving functionality. One semantic rule
  and mutable financial or market fact has one canonical authority.
- Keep exchange/venue-specific endpoints, fields, wire formats, auth, protocol
  quirks, subscribe grammar, routing and fallback policy with their venue owner.
  Share bounded, data-independent mechanics; don't mistake similar syntax for
  identical semantics.
- Keep strategies/risk, native sessions and transport I/O, recording, and
  diagnostics with their proper product/domain owners. Do not make a low-level
  core depend on an application or strategy merely to avoid a small adapter.
- Preserve the project's single-current contract where it exists: migrate
  producers, consumers, tools and registrations together. Do not add silent
  legacy readers, fallback formats or duplicate state. Respect externally
  versioned protocols, existing persisted data, ABI compatibility commitments
  and explicit migration policies rather than erasing them.
- Do not claim a contract exists in production merely because a type/header,
  configuration, mock or alternative build contains it. Trace the selected
  compiled/loaded route and its consumer closure.

## Code shape and change quality

- Read the actual declaration, affected caller and analogous implementation
  before a non-trivial edit. Reuse a suitable existing helper. Prefer cohesive
  ownership, purpose-named functions and the smallest complete change.
- Trace the affected producer-to-consumer path across module boundaries. Look
  for repeated rules, computations and stored facts, unnecessary adapters,
  intermediate models, conversions and copies. Prefer one appropriate owner
  for shared semantics. Preserve snapshots, caches and copies justified by
  lifetime, thread ownership, representation or contracts; similar syntax alone
  does not establish equivalent behavior. Bound the search to the affected path.
- Prefer small files with one narrow responsibility; closely related small types
  and functions may stay together. Split distinct responsibilities, mixed hot/cold
  ownership, unsafe review boundaries or deep nesting; combine or inline accidental
  layers. Use no fixed line limit and avoid fragmentation that merely adds
  navigation. Preserve meaningful venue/protocol differences and failure handling.
- Design for a concrete near-term extension or known future consumer; a second
  implemented consumer is not a prerequisite for considering that design. Name
  the scenario and discuss material assumptions under the active project policy.
  Preserve dependency and shared-component boundaries. Examine layers and options
  without a current or concretely identified near-term consumer; avoid abstractions
  for unspecified future use, duplicate runtimes, copies of linked SDKs, staged
  alternative production graphs and app-local overrides of an authoritative rule.
- Include adjacent cleanup only when necessary for the complete current-task
  solution; report other findings separately. Finding a duplicate does not itself
  expand the assignment. For significant decisions, briefly identify the suitable
  analogue, chosen owner and reasons for preserved differences in the ordinary
  result, without a separate artifact or a checklist for every helper.
- Close changes through real declarations, callers, registrations, source
  lists, generated inputs, CLI consumers and operational recipes. Search
  remaining old names within the affected closure; historical artifacts and
  intentionally similar identifiers are not necessarily stale references.
- Preserve unrelated changes, tests, public behavior and project code style.
  Do not reformat third-party, generated or format-frozen code without scope.

## Minimum necessary checks and repeated work

Minimize runtime checks and repeated work along the entire affected
producer-to-consumer chain: external/private inputs, network and parsing,
publication/handoffs, computation/strategy/finance, admission, action preparation
and send, sessions and recovery. Trust guarantees already established by code
and the canonical owner, including across modules. A module boundary or a
defensive coding preference alone does not justify revalidation.

Establish immutable conditions during preparation/binding. Maintain mutable
conditions through owner events where semantics allow. Retain a check for a
fact not yet guaranteed or a relevant change after the prior guarantee that
is not already accounted for, including async, queue, thread or session changes.
Remove redundant computations, reads, scans, conversions and copies as well
as checks. Preserve necessary external-input, memory/arithmetic, lifetime,
capacity, current authority and unknown-outcome guarantees at sufficient owners.

Explain significant retained or added checks with concrete failure/change
scenarios. Do not require a per-if register or new proof-wrapper framework.
Trace the whole affected chain; a full-project audit needs its own task scope.
This rule does not remove tests or change verification permissions.

## Layout, memory and numeric meaning

- For an API/ABI, wire/storage layout or shared hot state, inspect `sizeof`,
  alignment, field order, padding, stack-frame use, cache-line placement,
  lifetime, integer units/scales, timestamps, sentinel/unknown values,
  signedness, valid range, overflow and rounding. Check all producers and
  consumers, not the struct name alone.
- Every growing sequence requires owner, maximum or allocation phase, capacity
  and terminal overflow/refusal policy. Preallocate or use fixed-capacity state
  where the selected hot-path contract requires it. A refactor must not silently
  enlarge a constrained H0/H1 object, stack frame or allocation count.
- Use checked arithmetic and declared rounding for financial conversions.
  Distinguish exact/reference oracles from production fixed-point models.

## Compiler and deployment evidence

- Confirm the actual selected compiler, language/runtime version, ABI, linker,
  build mode, CPU/architecture target, flags, dependencies and production
  translation unit or loaded package. Avoid accidental compiler/toolchain,
  target or source-graph fallbacks.
- Build success on one host is not evidence of target-host performance or
  readiness. Machine code confirms generated instructions, not that a runtime
  route called them or that latency improved.
- Keep portable, diagnostic, test and optimized build surfaces distinct when
  they have different contracts. Incompatible artifacts should be reported,
  not silently treated as matching production evidence.
