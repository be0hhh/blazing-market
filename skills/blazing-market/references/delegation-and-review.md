# Agent cascade, recursive delegation and independent review

This is the portable agent-orchestration contract. It applies through the
agent platform's actual capabilities; it does not require a particular model,
agent filename, multi-agent API, token tier or orchestration service.
Explicit project rules replace corresponding workflow rules here; apply the
skill where they leave gaps, without calling overridden stages incomplete.

## Contents

- [Ownership and recursive tree](#ownership-of-the-whole-result)
- [Native coordination and strong branch owners](#native-coordination-and-strong-branch-owners)
- [Four-stage cascade and questions](#four-stage-cascade-with-feedback)
- [Roles, task capsules and owned scopes](#role-and-effort-selection)
- [Test orchestration and authorship](#test-orchestration-and-authorship)
- [Fresh independent plan review](#fresh-independent-plan-review)
- [Final independent code review](#review-independence-and-the-simplicity-specialist)

## Ownership of the whole result

- The **root orchestrator** receives the user's task, clarifies material
  choices, preserves the agreed outcome and authorization, integrates all
  branches, resolves contradictions, and owns final user communication.
- Research, design, implementation and review are different responsibilities.
  They may use the same available agent platform but must not treat their
  outputs as mutually substitutable evidence.
- A parent owns its accepted subtree and consolidates its child results before
  returning to its parent. The root retains the final integration responsibility.
- **Root approval is required for each proposed nested subtree**, not just for
  initial top-level branches. The prospective parent forwards the proposed
  role(s), actual supported model/effort where relevant, owned scope,
  dependencies, action permissions and reason to the root. The root approves,
  reduces or declines it within existing task authority before children are
  launched. This is an internal coordination gate, not a new user approval
  for every worker or an expansion of the user's permissions.
- Use recursion only for genuinely independent, well-bounded results that
  benefit from it. A small or tightly coupled task without test authorship can
  stay with one agent; needed test edits use the minimal separate subtree below.
  Concurrency and depth are bounded by the actual runtime, not by an arbitrary
  target number of workers.
- A nested agent may **propose** child roles, scopes, supported settings and
  required evidence to its parent; that parent consolidates the proposal to
  root, awaits approval, then owns the accepted branch and integrates its
  children's evidence. No child invents permission to edit, run, trade or
  contact the user directly.

## Recursive ownership tree

```mermaid
flowchart TD
    U["User"] <--> R["Root orchestrator"]
    R <--> X["Strong research owner"]
    R <--> P["Strong design owner"]
    R <--> I["Strong solution / domain coordinator"]
    R <--> V["Independent strong review orchestrator"]
    V <--> VS["Required independent specialist threads"]
    V <--> VH["Bounded read-only evidence helpers, if useful"]
    I <--> A["Strong production solver: Feed"]
    I <--> B["Strong production solver: Runtime"]
    A <--> A1["Strong substantive production child, if useful"]
    I <--> T["Shared strong test orchestrator: serves these solvers"]
    T <--> TA["Separate TEST_AUTHOR children"]
```

The double arrows denote task/plan delivery and feedback. Branches are
optional, never a mandatory agent quota. Child-to-parent reports are
consolidated upward; user questions go through the root, not direct child-user
side channels. Reviewers are independent of the author of the reviewed change.

## Native coordination and strong branch owners

For large work, place useful research, design, solution, test and review branches
under strong owners. Select branches for independent responsibilities rather
than requiring every phase or inserting empty levels. The solution/domain owner
owns coherent behavior, interfaces, dependencies and integration of its accepted
scope. Substantive production authors are strong agents. Read-only mechanical
helpers in solution or review branches receive complete bounded evidence tasks;
they do not make semantic decisions or author production changes. Mechanical
test authors retain the separate ready-specification rules below. Non-production
text/document mechanics may use mechanical workers under host policy.

An independent strong review orchestrator, separate from the solution branch,
test orchestrator and authors, owns risk coverage, reviewer assignments and
integrated findings. It does not write the implementation it reviews, replace
required independent specialist threads, override their concrete vetoes or
self-clear their gates. Findings return to the appropriate author through the
owner; repairs receive bounded re-review of the materially affected surface.
This coordination adds no new review gate beyond the applicable task rules.

All these roles are participants in the host's **same native agent swarm**:
use its exposed worker/helper and communication capabilities, coordinator and
available shared board/events. Parents own accepted child scopes and reports.
Do not add a second scheduler, dispatcher, queue, daemon, private API or vendor
patch to implement this tree. If native child helpers are unavailable, root
physically dispatches the approved leaf tasks and returns their results to the
branch owner. Report that flattened runtime honestly; conceptual ownership does
not prove that nested workers were physically launched. Use only capabilities
the host actually exposes and retain its permission and model-routing rules.

Send complete capsules with current decisions, bounded context and ownership;
a shared board does not establish review independence. Fresh reviewers still
receive fresh context and exclude peer opinions or prior verdicts under the
review rules below. Use stronger settings or an additional reasoning pass only
for a concrete bounded uncertainty under existing host routing; prompt wording
does not change actual runtime settings.

## Nested subtree approval and feedback

```mermaid
sequenceDiagram
    participant R as Root
    participant P as Parent agent
    participant C as Branch agent
    participant N as Proposed child
    C->>P: Propose child role, scope, settings, permissions
    P->>R: Consolidated subtree request
    R-->>P: Approve, narrow or decline
    P-->>C: Accepted scope and bounds
    C->>N: Launch only if approved and supported
    N-->>C: Result, anchors, remaining limits
    C-->>P: Integrated child findings
    P-->>R: Accepted branch result
```

A branch may recurse again through the same approval chain. The root retains
shared files, inter-branch reconciliation, all user decisions, and final
integration. Subtree approval does not expand the active authority for tests,
benchmarks, source edits, network actions or live trading.

## Four-stage cascade with feedback

```mermaid
flowchart TD
    A["1 · Research: real code and contracts"] --> ROOT["Root considers research findings"]
    ROOT --> EARLY["Early independent simplicity review"]
    EARLY --> B["2 · Separate designer: decision-complete solution"]
    B --> P["Fresh independent plan review"]
    P --> Q{"Material decision?"}
    Q -->|Yes| U["Root asks user"]
    U --> B
    Q -->|No| AG{"Ready solution agreed by user?"}
    AG -->|No| PLAN["Root presents solution; await agreement"]
    PLAN --> AG
    AG -->|Yes| G{"Execution authorized?"}
    G -->|No| STOP["Present plan; stop edits"]
    G -->|Yes| C["3 · Bounded implementation subtrees"]
    C --> I["Root integrates production and test changes"]
    C -.-> TA["Early test analysis and stable-part read-only review"]
    TA -.-> I
    I --> R["Independent hot/domain reviews"]
    R --> SIMPLE["Final independent simplicity review"]
    SIMPLE --> F{"Actionable finding?"}
    F -->|Yes| C
    F -->|No| T["4 · Verification under active policy"]
    T --> E{"Required evidence complete?"}
    E -->|No| N["done_unverified / blocked"]
    E -->|Yes| Z["verified"]
```

This depicts responsibilities and authorization boundaries, not automatic
execution. Verification follows the authority rules in
[workflow-and-plans.md](workflow-and-plans.md); an independent code review is
not a test or performance benchmark. Small direct tasks bypass the full cascade;
high-risk plans still receive fresh independent plan review, without requiring
a separate designer merely for risk. Simplicity stages apply to substantive
code tasks; report unavailable applicable stages without simulating clearance.
Test analysis and read-only review of stable parts may overlap remaining
implementation. Final review still consumes the integrated current snapshot;
the diagram does not impose a global sequential barrier on independent work.

## Questions and handoffs

```mermaid
sequenceDiagram
    participant U as User
    participant R as Root
    participant P as Branch owner
    participant C as Child agent
    C->>P: Material uncertainty + source anchor
    P->>R: Consolidated question / affected work
    R->>U: One material decision
    U->>R: Agreed constraint
    R->>P: Decision + authorized scope
    P->>C: Updated task capsule
    C->>P: Result + evidence limitations
    P->>R: Integrated branch report
```

The root deduplicates questions, resolves routine details from sources and
continues independent work while a dependent decision is outstanding. An
incidental status message does not revoke existing task authorization; an
explicit pause, cancellation or scope change does.

## Research, design and implementation sequencing

1. **Research:** inspect actual owners, relevant declarations, registrations,
   callers, production surfaces and failure paths. Give exact source anchors,
   not guesses. Return findings to root, which considers them before starting
   design. Research is read-only and does not pre-authorize implementation.
2. **Design:** root starts a separate designer with the relevant research
   findings, settled decisions and constraints. In a full cascade, a second
   reasoning pass by the researcher or root does not replace this agent.
   Settle observable behavior, normal/failure scenarios, ownership, interfaces,
   dependency closure, acceptance and evidence. Send material questions through
   root. A complex full-cascade or high-risk plan receives a fresh independent
   read-only review before the root asks the user to agree the ready design.
   The user agrees the integrated ready solution before first implementation
   in a non-trivial full cascade. An already agreed unchanged plan and active
   execution permission require no renewed approval.
3. **Implementation:** only after applicable agreement/permission, delegate
   atomic tasks with non-overlapping owners and near-patch specifications.
   The root owns shared registries/manifests/public integration files. A worker
   proposes bounded child roles/scopes/settings through its parent to root and
   may launch only after root approves and the runtime permits it; the parent
   returns consolidated results upstream. Production solvers do not author or
   repair tests; needed test work uses the separate subtree below. Test analysis
   and review of stable parts can proceed while other implementation continues.
4. **Integration/review/verification:** root inspects actual changed code and
   consumers, then obtains relevant independent reviews. Resolve veto findings
   within authority; re-review only changed/repaired critical surfaces. Tests,
   benchmarks, runtime and live checks retain their distinct evidence and
   authorization under the active user/project/runtime policy.

If an applicable separate designer or independent reviewer cannot be provided,
report which stage is unavailable. Continue independent authorized work without
claiming that self-review satisfies the missing independent stage; material
unresolved decisions still stop dependent implementation.

## Role and effort selection

- Select capability from the task, not a fixed model leaderboard: strong
  owners for substantive research/design, solution and review branches; strong
  production authors; independent specialist reviewers for critical risk.
  Use bounded read-only mechanical helpers for ready evidence tasks, and
  mechanical text/document workers only where host policy permits.
- Test orchestration requires a strong semantic owner. A separate strong
  test-author child handles critical or unclear tests; a mechanical author gets
  only a complete ready specification. These are portable capabilities, not
  fixed model names. Verify actual settings only where the platform exposes them.
- Give a mechanical helper only a complete, settled, bounded specification
  within the permitted responsibilities above; return design gaps to the
  parent instead of improvising new behavior.
- Increase reasoning depth for cross-boundary architecture, high-risk decisions,
  final critical review, or independent contradiction resolution. Broad
  escalation is occasional and must have a concrete purpose.
- Model names, numeric reasoning levels, and service tiers are environment
  choices. Prompt text does not switch the runtime's actual model or mode.
  Confirm only capabilities and selected settings that the platform exposes.
- Do not spawn all applicable roles by default. A single agent can apply
  several review lenses; distinct threads are justified by independent scope,
  useful parallelism or an independent-review requirement.
- Keep computation/memory latency, network latency and transport correctness
  as distinct capabilities. Computation/memory covers bounded work, allocation,
  locality, contention and scheduling; network latency covers RX/TX through
  protocol, socket, kernel and NIC costs. Transport correctness covers trust,
  framing, partial I/O, deadlines and session/recovery invariants. Endpoint and
  location evidence belongs to placement expertise, not kernel tuning. See
  [transport-and-readiness.md](transport-and-readiness.md) for network scope and
  shared system-context evidence.

## Test orchestration and authorship

### Tree and ownership

Production implementation agents may inspect tests and discuss scenarios, but
**never create or change tests**, including test repairs after failures or
review. Test edits belong exclusively to explicitly assigned **TEST_AUTHOR**
threads. A strong **TEST_ORCHESTRATOR** coordinates that work and does not edit
tests itself. These are task responsibilities, not required platform API names.

For a large tree, use root → domain coordinator → production solver → strong
test orchestrator → separate test-author children for an individual solver's
test scope. One shared orchestrator may instead serve several related solvers
as a child of their nearest common coordinator, as shown above; independent
domains may each have their own orchestrator. Do not insert an empty solver
level merely to host an orchestrator.
Assign common tests once at the nearest common coordinator; avoid duplicate or
competing test owners. For tiny justified test work, root → test orchestrator →
test author is enough. Do not add empty coordination levels, per-method or
per-scenario worker quotas, or a test subtree when no test work is needed.
Nested subtree proposals still use the root's existing internal approval gate;
they do not require an extra routine user permission exchange.

In a shared branch, assign disjoint production and test files before edits.
Keep each shared registration or manifest with one named integration owner;
authors supply the necessary integration change to that owner.
Do not introduce a new test framework merely to support this division of work.

### Orchestrator and author responsibilities

The orchestrator owns test-risk analysis and sufficient cases, independently
justified expected results, fixture realism, clock domains, units, object
lifetimes, registration closure and failure triage. Existing sufficient coverage
can close a risk without new tests. Expected values must follow the agreed
contract, a justified independent model or authoritative data; copying the
implementation's result into the assertion does not justify it. Consistency
checks may be useful evidence, but do not prove that the expected result was
chosen correctly.

The orchestrator gives each author exact owned files, intended behavior,
sufficient normal/failure cases, justified expected results, fixture constraints,
registration owner, snapshot identity and authorized actions. A strong author
resolves substantive test design within agreed semantics; material semantic gaps
return through the orchestrator to root. A mechanical author only implements a
complete ready specification and returns gaps without inventing expectations.
Production solvers supply contract and implementation context without gaining
test edit ownership. This separation applies to root acting as a production
solver as well as to ordinary workers.

### Current-task updates and stable evidence

At initial binding, contract changes, check failures, reviewer-driven repairs
and final freeze, the parent sends the orchestrator the current decisions and
owned diff or identified snapshot, including relevant production/test surfaces
and shared integration ownership. The orchestrator follows the **current task
tree** through these messages and bounded file reads. It is not a daemon that
monitors all chats, unrelated tasks or repositories.

Start risk analysis early and review stable parts read-only alongside remaining
implementation. Run selected tests only against an identified stable snapshot;
record what was exercised and re-establish that identity if concurrent edits
change the surface. Final required review inspects the integrated production and
test snapshot. Its reviewer is independent of both orchestrator and authors;
the orchestrator's assessment does not replace it. Use the task's applicable
review gates, without adding a universal separate review gate for every trivial
test. Repeat review only for materially changed surfaces. Add an adversarial
pair only for a concrete unresolved risk, not automatically for every complex
task.

On failure, separate production defects, test/fixture defects and infrastructure
blocks, and route each to its owner. Compiler or environment failure is
`BLOCKED`, not behavioral `RED`. Never weaken assertions or select easier
expected values merely to obtain `GREEN`; revise an expectation only when its
semantic justification was wrong, with that correction made explicit. Preserve
the failed evidence. Writing tests grants no run authority: host policy governs
commands, approvals, models, services and external actions under
[workflow-and-plans.md](workflow-and-plans.md).

## Task capsule and safe ownership

Provide a child a compact, self-contained assignment:

- Observable outcome; exact owned paths, symbols and structures.
- Relevant contracts, source anchors, settled decisions and available evidence.
- Branch behavior, affected callers/consumers/registrations, and shared owners.
- Test scenarios, acceptance criteria and explicit anti-criteria; production
  versus test edit ownership and the assigned test orchestrator when needed.
- Exact authorized actions/checks, if any; otherwise state **none**.
- Expected output and evidence limitations.

For research, design and implementation on a touched H0/H1 or computational
core, pass the relevant
[computation-ahead contract](hot-cold-paths.md#computation-ahead-of-the-event-and-specialization):
known compile/preparation/event inputs, preparation owner and refresh events,
agreed specialization/size limits, available codegen artifact identity and
evidence gaps. Include C where it prepares that path. Existing implementers
apply settled semantics; material new behavior or ownership choices return to
root. This does not require a new optimizer role, an unrelated audit or added
run/review gates; independent read-only reviewers remain separate from authors.

Workers do not edit outside their owned scope, revert others' changes, write
shared integration files, perform drive-by formatting, silently expand
requirements or mark their own work verified. A worker's report is a claim;
root reopens key source and integration edges. Resolve conflicting reports by
examining disputed anchors, not by counting agents.

Fresh-context workers should receive only the capsule and necessary rules.
Do not flood them with full chat history, unrelated files, old reviewer opinions
or suggested answers to the very question they must independently evaluate.
After context loss, pass compact agreed decisions and unfinished evidence;
reuse prior validated findings instead of restarting discovery.

## Fresh independent plan review

- For a high-risk plan or non-trivial full cascade, obtain one new read-only
  reviewer **independent of the writer, researcher and designer** before
  presenting the ready design for user agreement, when available. A follow-up
  conversation with an existing reviewer is not a new fresh review.
- Supply the **complete exact plan snapshot**, not a summary: all settled
  behavior, sequencing, ownership, affected interfaces, dependencies, normal
  and unknown/failure outcomes, permissions, acceptance and anti-criteria.
  Include applicable project rules and bounded source anchors; for an existing
  plan file, include its path and exact text/revision. An in-chat plan needs no
  artificial file merely to be reviewed.
- Exclude prior chat history, the author's rationale outside the plan,
  preceding reviewer findings, personal memories and leading answers. Fresh
  *conversation context* is not filesystem isolation or permission to ignore
  applicable repository rules.
- First have the reviewer **independently paraphrase** the intended result,
  invariants, change sequence and acceptance without filling missing details.
  Then inspect relevant anchored source and test hidden assumptions, actual
  callers, ownership conflicts, dependencies and failure behavior. Return
  `CLEAR` for a bounded inspected scope or actionable findings with severity,
  exact plan section/source anchor, violated condition and evidence limits.
- Root compares the paraphrase to user intent, checks disputed claims at the
  source and integrates findings. If the plan changed since the snapshot,
  the verdict applies **only to the reviewed revision**. A material change to
  behavior, ownership, interfaces, dependencies, permissions, failure policy
  or acceptance calls for another fresh review; editorial fixes do not.
- If a fresh independent reviewer, full snapshot or needed source is
  unavailable, state precisely that review was not completed. Never simulate
  independence, infer clearance from the writer's self-check, or treat plan
  review as final code-review or test proof.

## Review independence and the simplicity specialist

- For substantive code tasks, require an independent simplicity reviewer
  **early**, once scope is known and before choosing the implementation, and
  **late**, after integration and the relevant specialist reviews, when agents
  are available. Early review searches for reuse, unnecessary layers and sufficient
  existing verification; final review inspects the actual integrated change.
  Apply the [minimum-checks rule](architecture-and-contracts.md#minimum-necessary-checks-and-repeated-work)
  along the whole affected chain, including module boundaries, admission, sends
  and recovery. Trust established owner guarantees; find repeated validation,
  computations, reads, scans, conversions and copies. Ask what can actually
  change after the prior guarantee before retaining another check. Explain
  significant retained/added checks while preserving necessary correctness;
  require no per-if register, new proof wrappers or unrelated full-project audit.
  Assess production code, added tests, fixtures, helper APIs and verification
  scripts together for behavioral value, duplication, coupling to implementation
  details and maintenance cost. Follow
  [workflow-and-plans.md](workflow-and-plans.md#keep-verification-within-the-task)
  for test necessity, check scope and stopping rules. Declining an unjustified
  new test does not authorize deleting existing coverage or weakening required
  checks. Missing unrequested tests alone are not a veto or a new acceptance gate.
  Both consultations are read-only unless given a separate authorized
  implementation task. Findings go through the
  change owner and root; they do not automatically expand the assignment.
  Tiny mechanical tasks need neither a full cascade nor these consultations.
  If participation is unavailable, report the missing consultation and
  continue independent authorized work. Simplicity never replaces domain or
  latency review; material repairs to a critical surface repeat its affected
  specialist reviews before the final simplicity review.
- Select required critical reviewers from the matrix below. For the required
  network H0/H1 trio, network latency and transport correctness are independent
  roles; one cannot satisfy both.
- Critical reviewers must be independent of the author and inspect the final
  relevant source; report CLEAR or findings with severity, exact path/symbol,
  violated invariant, observed evidence and limits. A reviewer cannot grant
  build/test/live authority or claim passing tests from code inspection.
- Perform critical reviews against the **root-integrated** source after
  implementation, not a worker's proposed diff in isolation. Each required
  reviewer uses a distinct independent read-only thread when supported;
  neither reviewer nor simplicity review stands in for another required role
  or verification governed by the active policy.
- Documentation, test-only or strictly mechanical edits do not automatically
  trigger runtime reviews merely by naming a hot or network subsystem. An unchanged
  CLEAR surface needs no repeated review. Repeat only after a concrete repair
  or material change, and restrict to that affected surface.
- If a required independent reviewer or fresh context is unavailable, report
  that the gate did not run; do not simulate clearance. Independent findings
  are vetoes only when tied to a concrete violated or undefined contract.

## Critical review matrix

Apply by actual changed behavior, including configuration that changes that
behavior. The network H0/H1 row takes precedence over the ordinary H0/H1 pair.

| Changed surface | Minimum independent final reviewers |
| --- | --- |
| Actual non-network H0/H1 | Computation/memory latency + relevant parser, runtime, execution or other domain specialist |
| Actual network change affecting H0/H1 | Computation/memory latency + network latency + transport correctness: **three distinct threads** |
| Pure C/D network change with no hot-path effect | Expertise selected by concrete risk; no fixed reviewer quota |
| Substantive offline financial computation under an explicitly required strict compute contract | Computation/memory latency + quant/financial semantics |

Before using the pure C/D row, bound the inspection to affected callers,
shared code, configuration and contracts to establish that hot RX/TX behavior,
parameters consumed by H0/H1 and H0/H1 semantics are unaffected. Trading depending
on connection readiness alone is not a hot-path effect. Changes affecting those
hot operations or contracts require the trio even if edited in setup code. If uncertain, do not claim
the cold exemption: investigate and route material uncertainty through root
under the existing decision rules.

Add independent parser, runtime/execution or quant review when a network change
also changes substantial separate semantic invariants; the network trio does
not cover those by implication. Simplicity review never counts toward these
minimums. Classification as C does not impose blanket strict-H0 restrictions;
the selected project/profile still controls those restrictions. Report missing
agents or unsupported independent threads without simulating clearance.

## Root integration and terminal handoff

- The root merges duplicate findings, resolves contradictory claims against
  source, closes changed registrations and consumers, preserves unrelated work
  and carries agreed decisions into the final result.
- The parent returns outcomes, changed/inspected paths, exact checks actually
  run, limitations, blockers, dependent scopes, and any unresolved user choice.
- `done_unverified` is an integrated implementation, not passed tests.
  `verified` requires the selected evidence; the reviewer and worker cannot
  promote their own output just by asserting readiness.
