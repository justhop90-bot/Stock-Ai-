# RUNTIME_SEMANTICS_PROBE_MATRIX_v0.1

**Project:** Stock-Ai-
**Scope:** Current-DE runtime closure for unresolved `.per` engine semantics
**Status:** Sprint 0 — prioritized probe specification
**Method:** REFERENCE → WRITE → REF → DELIVER
**Evidence rule:** A probe closes only the proposition it measures. Command issuance, rule firing, queue admission, replay chronology, or source structure must not be promoted into world-state completion without an observed bridge.

## 1. Purpose

This matrix converts the unresolved Stock-Ai engine questions into a small, ordered runtime campaign. It deliberately favors narrow probes over large AI runs. Each probe should answer one semantic proposition, produce a reproducible artifact, and either close an ABI edge or leave it explicitly UNKNOWN.

The campaign covers seven unresolved areas:

1. same-pass visibility;
2. action ordering;
3. timers;
4. jumps;
5. production completion;
6. construction completion;
7. object identity.

The first four establish the execution model required to interpret the last three. Production, construction, and identity then establish the world-state boundary needed by Stock-Ai's `REQUESTED → ... → VERIFIED_EFFECT` lifecycle.

## 2. Priority model

| Priority | Meaning | Gate |
|---|---|---|
| **P0** | Engine-semantic prerequisite; unresolved result can invalidate controller architecture | Must close before relying on the affected mechanism in core architecture |
| **P1** | Critical lifecycle boundary; needed for reliable production/construction/state verification | Run immediately after P0 prerequisites are stable |
| **P2** | Higher-order identity/lineage closure; valuable but dependent on P1 evidence | Run only after prerequisite observation edges are proven |

## 3. Campaign order

```text
P0-01  SAME-PASS GOAL VISIBILITY
   ↓
P0-02  SAME-PASS SN / STORE VISIBILITY
   ↓
P0-03  ACTION ORDERING
   ↓
P0-04  TIMER TRIGGER / REARM SEMANTICS
   ↓
P0-05  JUMP TARGET / PASS SEMANTICS
   ↓
P1-01  PRODUCTION LIFECYCLE
   ↓
P1-02  CONSTRUCTION LIFECYCLE
   ↓
P2-01  OBJECT IDENTITY / LINEAGE
```

P0-01 and P0-02 may be executed as separate tests in one controlled harness, but their propositions must remain separate. P2-01 must not be attempted as a substitute for the production/construction lifecycle probes.

## 4. Evidence requirements for every probe

Every run records:

- target AoE2DE build/executable identity;
- exact script revision and SHA-256;
- probe ID and revision;
- map/scenario/game setup;
- player/civ setup;
- starting resources and relevant state;
- expected observation;
- actual observation;
- timestamp/sequence where available;
- replay/log/debug artifact locator;
- pass/fail/ambiguous result;
- falsification condition;
- architectural consequence;
- confidence and evidence tier.

A successful probe should preferably have a positive control and a negative control. If the observation channel cannot distinguish the competing hypotheses, the result is **UNKNOWN**, not a forced conclusion.

## 5. Probe matrix

| ID | Priority | Proposition | Minimal setup | Stimulus | Required observation | Competing hypotheses | Pass condition | Falsification / failure | Architectural consequence | Dependency |
|---|---|---|---|---|---|---|---|---|---|---|
| **P0-01** | P0 | A state mutation made by Rule A is visible to Rule B during the same rule pass. | Two otherwise inert rules; dedicated private goal/state slot; deterministic trigger. | Rule A writes sentinel `0→1`; Rule B tests for `1` and writes a second sentinel. Repeat with A before B and B before A. | Rule-fire order plus both sentinel values after the pass and on the next pass. | H1: immediate same-pass visibility. H2: next-pass visibility only. H3: state-type-specific behavior. | At least one ordering produces an unambiguous observation distinguishing H1/H2; repeatable across runs. | No observable distinction, inconsistent pass boundaries, or only replay-level inference. | Determines whether Stock-Ai may use write-then-read chains inside one pass or must insert explicit next-pass state transitions. | None |
| **P0-02** | P0 | Goal, SN, and typed-store mutations have the same or different visibility timing. | Three isolated state channels: goal, SN, and `c:/g:/s:` operand reads where legal. | Rule A mutates one channel; Rule B immediately reads it; repeat per channel and with timer-separated control. | Channel-specific before/after values and rule-fire sequence. | H1: all mutable stores visible identically. H2: goals/SNs differ. H3: operand resolution differs from direct predicate reads. | Each tested channel has a reproducible visibility classification. | A channel cannot be observed independently or result depends on unrecorded engine state. | Prevents accidental abstraction of goals/SNs as interchangeable state stores. | P0-01 |
| **P0-03** | P0 | Multiple actions in one rule execute in deterministic source order and produce observable ordering effects. | One rule with two or more state/action operations whose order can be independently detected. | Variant A: `action-1` then `action-2`; Variant B reversed. Include a state write followed by a dependent action where legal. | Final state, command records, and any intermediate observable effect. | H1: strict source order. H2: actions reordered/batched. H3: same-rule actions execute but external visibility is deferred. | Repeated runs distinguish the ordering model. | Only final state is observable and both hypotheses converge. | Determines whether Stock-Ai can rely on intra-rule sequencing or must split actions across rules/passes. | P0-01/P0-02 |
| **P0-04** | P0 | Timer trigger, timer state, rearm, and rule-pass interaction have deterministic semantics. | One timer, one trigger rule, one observation rule; no economic/military noise. | Start timer; observe running/triggered/disabled states; rearm; attempt repeated trigger at controlled intervals. | Timer state transitions, rule firings, and elapsed game time. | H1: trigger occurs on fixed pass boundary. H2: trigger is time-based but sampled by passes. H3: rearm is immediate/next-pass. | At least one timer lifecycle can be mapped unambiguously from arm → running → trigger → rearm/disable. | Trigger timing varies beyond expected engine granularity or observation cannot distinguish state transitions. | Establishes valid timer guards and cooldown design; prevents assuming wall-clock precision from source syntax. | P0-01/P0-03 |
| **P0-05** | P0 | `up-jump-rule` target selection, negative jumps, source-order indexing, and disabled-rule interaction behave as assumed. | Tiny rule bank with uniquely observable rule IDs; no gameplay dependencies. | Execute forward jump, backward/negative jump if legal, and insert/disable a rule in a controlled script variant. | Exact rule firing sequence per pass. | H1: positional source index; H2: label/identity semantics; H3: jump target resolves dynamically. | Baseline and controlled insertion/disable variants yield a deterministic mapping. | Target changes unexpectedly, loop behavior cannot be isolated, or disabled-rule indexing cannot be distinguished. | Determines whether Stock-Ai can safely use jump-based dispatch and establishes source-edit hazards for generated/maintained rules. | P0-01/P0-03 |
| **P1-01** | P1 | `train` / production command can be separated into request, queue admission, pending, creation, and availability. | One production building; one unmistakable unit type; controlled resources; no competing production. | Issue exactly one production command after feasibility check. | Command/action record, queue state if observable, aggregate object count, later object/order evidence, timing. | H1: queue admission implies completion. H2: queue admission is only pending. H3: object creation is observable but identity remains unresolved. | Repeatably distinguish at least `ISSUED/QUEUED`, `PENDING`, and `CREATED/AVAILABLE`, or explicitly prove the observation channel cannot. | No reliable bridge from queue record to created object. | Production controller must retain `PENDING` and require independent availability evidence before assignment/use. | P0 campaign |
| **P1-02** | P1 | `build` can be separated into command acceptance, foundation/pending state, completion, and usable-building state. | One builder, one unmistakable building, clear placement, controlled resources, no competing construction. | Issue one build command after feasibility check. | Build/action record, foundation/placement evidence, object count/type, construction completion evidence, later building use where observable. | H1: build action implies completion. H2: build establishes pending construction. H3: completion is observable only through later world state. | Repeatably identify command, pending/foundation, and completed/usable states; otherwise retain unresolved stages. | Completion cannot be distinguished from command issuance or foundation existence. | Construction must use explicit `PENDING` state and verification; no immediate completion assumptions. | P0 campaign |
| **P2-01** | P2 | A produced object can be linked to its exact production command/producer without relying solely on chronology. | One producer, one unit request, unmistakable unit type, no same-type confounders; repeat with controlled sequence. | Issue one request and observe object birth plus subsequent controllable behavior. | Producer identity, requested unit ID, object identity if exposed, sequence/time, later object actions, type/count snapshots. | H1: direct object identity bridge exists. H2: producer/time/type gives only probabilistic lineage. H3: no defensible identity bridge. | A reproducible identity edge links producer → command → created object → later use, preferably with direct object ID or equivalent validated identity. | Identity relies only on temporal adjacency, aggregate count, or assumed unit ordering. | If H1 closes, Stock-Ai may verify production at object level. If H2/H3, retain `AVAILABLE` only from independent availability evidence and never assign lineage without proof. | P1-01 |

## 6. Probe-specific acceptance standards

### P0-01 / P0-02 — state visibility

The test is not "did the final value change?" The test is **when another rule could legally observe the mutation**. A final-state match does not close same-pass visibility. The harness must create an observable dependency between Rule A's write and Rule B's read and record the execution sequence.

### P0-03 — action ordering

The test must distinguish three propositions:

1. action calls are accepted in source order;
2. engine-side effects occur in source order;
3. other rules can observe those effects before the rule completes.

These are separate claims. Closing only the first does not close the latter two.

### P0-04 — timers

The probe must not infer real-time precision from a timer's nominal interval. Establish the relationship between timer state and rule passes first. A timer may be time-based internally but only become observable through the AI evaluation cycle.

### P0-05 — jumps

The baseline script must have unique rule-side sentinels so that the observed firing sequence identifies the target without relying on debug text alone. A source-edit variant is mandatory because positional jump hazards matter directly to maintainability.

### P1-01 — production

The minimum accepted lifecycle is:

```text
REQUESTED
  ↓
AUTHORIZED / FEASIBLE
  ↓
ISSUED
  ↓
QUEUED
  ↓
PENDING
  ↓
OBSERVED_CREATED
  ↓
AVAILABLE
```

If the engine/replay exposes only the first four states, the remaining states remain **UNKNOWN**. Do not infer them from elapsed time.

### P1-02 — construction

Use an unmistakable building and controlled placement. The probe must distinguish the construction request from foundation/pending state and from completed/usable state. Resource expenditure or command logging alone is not completion evidence.

### P2-01 — object identity

This is deliberately last. Object identity is only useful once production completion is independently observable. A sequence number, nearby replay record, object count increment, or temporal adjacency is not sufficient by itself to establish lineage.

## 7. Expected evidence outcomes

Each probe ends in exactly one of these states:

- **VERIFIED-RUNTIME** — competing hypotheses were experimentally distinguished.
- **INFERRED** — observations narrow the semantics but do not close the proposition.
- **UNKNOWN** — observation channel is insufficient.
- **REJECTED** — a tested interpretation is contradicted by reproducible evidence.

`VERIFIED-CORPUS` is not a successful runtime result. Corpus evidence remains attached as prior provenance but does not replace the runtime result.

## 8. Architecture gates

| Gate | Required closure | Stock-Ai consequence |
|---|---|---|
| **G0 Execution model** | P0-01 through P0-05 | Core state/control architecture may rely on measured pass, action, timer, and jump semantics. |
| **G1 Production** | P1-01 | Production may advance beyond `PENDING` only on verified world observation. |
| **G2 Construction** | P1-02 | Construction may advance beyond `PENDING` only on verified completion/usable evidence. |
| **G3 Identity** | P2-01 | Object-level lineage may be used only if a defensible identity edge is established. |

Until G0 closes, Stock-Ai should prefer explicit state machines over same-pass assumptions. Until G1/G2 close, production and construction remain asynchronous pending workflows. Until G3 closes, object identity must remain an explicitly unresolved dimension.

## 9. Required artifact set

Each completed probe should produce, at minimum:

```text
probes/<ID>_<short_name>.per
probes/<ID>_README.md
probes/<ID>_expected.md
probes/<ID>_result.md
```

The result artifact must contain the target build, script hash, setup, observation table, conclusion, evidence tier, confidence, and architectural consequence. The probe script itself should remain disposable and retail-safe: no dependence on the full Stock-Ai controller.

## 10. Final operating rule

Do not build abstractions around an unresolved semantic edge merely because the source code strongly suggests an answer. The correct Stock-Ai response to missing runtime evidence is a state such as `PENDING`, `UNKNOWN`, or `UNVERIFIED`, followed by a probe. The purpose of this matrix is not to make the engine look understood; it is to identify the smallest experiments that make the engine prove itself.
