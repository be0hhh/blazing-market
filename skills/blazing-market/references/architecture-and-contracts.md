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
- Split code for distinct responsibilities, mixed hot/cold ownership, unsafe
  review boundaries or deep nesting; combine or inline accidental layers.
  Neither short files nor blanket DRY deduplication is a goal. Keep meaningful
  venue/protocol differences and explicit failure handling.
- Avoid speculative abstractions, duplicate runtimes, copies of linked SDKs,
  staged alternative production graphs and app-local overrides of a shared
  authoritative rule.
- Close changes through real declarations, callers, registrations, source
  lists, generated inputs, CLI consumers and operational recipes. Search
  remaining old names within the affected closure; historical artifacts and
  intentionally similar identifiers are not necessarily stale references.
- Preserve unrelated changes, tests, public behavior and project code style.
  Do not reformat third-party, generated or format-frozen code without scope.

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
