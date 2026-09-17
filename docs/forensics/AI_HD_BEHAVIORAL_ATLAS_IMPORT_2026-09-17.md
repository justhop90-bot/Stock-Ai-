# AI-HD Behavioral Atlas — Forensic Import Slice

**Date:** 2026-09-17  
**Target:** `justhop90-bot/Stock-Ai-` / `main`  
**Source corpus:** `justhop90-bot/AiByz` / `main`  
**AiByz source ref verified:** `fa46d1a0f1f74f0b0cdf5705344a5ea42e885e95`  
**Runtime probes:** NONE

## Purpose

This artifact consolidates already-established AiByz forensic work into the Stock-Ai behavioral atlas. It does not redo the underlying archaeology. Imported material is separated into current-stock evidence, current-DE reference analogues, and historical reference material.

## Import result

| Class | Count | Effect |
|---|---:|---|
| Current-stock source baseline | 1 | Supports existing stock identity/section-map claims |
| Current-DE AiBuilder reference | 2 | Reference only; does not close Stock-Ai production edges |
| Historical HD/Promisory reference | 1 | Reference only |
| State-ownership forensic import | 1 | Supports control/state model with R2 limitations |
| **Total imported records** | **5** | |

## Production lifecycle atlas

```text
train-* demand
    │
    ▼
Demand reassessment
    │
    ▼
Feasibility
    │
    ├─────────────── OPEN ───────────────┐
    ▼                                    │
Production executor                     │
    │                                    │
    ├─────────────── OPEN ───────────────┤
    ▼                                    │
Engine-facing production command         │
    │                                    │
    ├─────────────── OPEN ───────────────┤
    ▼                                    │
Pending production                      │
    │                                    │
    ├─────────────── OPEN ───────────────┤
    ▼                                    │
Completed unit                         │
    │                                    │
    ▼                                    │
Reassessment ────────────────────────────┘
```

### Existing closure carried forward

The imported corpus confirms the already-established distinction between policy state and execution state. The AiByz production authority matrix documents a native executor pattern of:

```text
policy writer
  ↓
desired-number-*
  ↓
executor
  ↓
unit count / feasibility
  ↓
can-train
  ↓
train
```

That pattern is **not promoted to Stock-Ai proof** because the inspected matrix targets the installed `AIByzBuild` corpus rather than the flattened Stock-Ai source.

### Historical closure carried forward

The consumer-provenance archaeology documents the historical pattern:

```text
traincamel
  ↓
stable selection
  ↓
can-train
  ↓
train/action
```

This is retained as `REFERENCE-ANALOG`, not current-DE evidence.

### Pending/completion boundary

The imported construction executor forensic establishes a general current-DE control distinction:

```text
command issued
    ≠
pending
    ≠
completed world state
```

It also identifies `up-pending-objects` and `up-pending-placement` as controller-visible pending guards. These are construction evidence and therefore remain an analogue for production until a production-specific Stock-Ai source path is established.

## Current Stock-Ai baseline imported from prior AiByz archaeology

The P0 stock deconstruction records the installed stock main corpus as:

- 36,141 lines
- 1,167,238 bytes
- SHA-256 `8a554a90a18f7983a949f7bef3b767e09732bce87dca3b9546fe782f098de51c`
- 2,429 `defrule` blocks
- 4,222 `defconst` declarations
- 79 `up-jump-rule` occurrences

It also maps the stock corpus into behavioral regions including strategy, resource/age, research, siege, villagers, buildings, units, navy, gatherers, attack/retreat, and town-size/placement support.

This is **direct source-baseline evidence** carried into the atlas with provenance. It does not by itself close the production execution boundary.

## State ownership import

The R2 ledger establishes the canonical ownership model:

```text
channel
→ symbol
→ declaration
→ initializer
→ writers
→ readers
→ guards
→ resetters
→ lifetime
→ owner
→ authority effect
→ downstream consumer
→ evidence grade
```

This imports a control-model rule into the atlas:

> A writer is not automatically an owner; a reader is not an authority; resetters define lifetime boundaries; engine-owned state must remain distinct from controller-owned state.

R2 remains explicitly **NOT CLEARED**, so the imported ownership model does not create a falsely complete state ledger.

## Edge status after consolidation

| AI-HD edge | Status after import | Reason |
|---|---|---|
| Stock source identity → effective corpus | CLOSED / carried forward | Direct stock baseline evidence |
| Stock corpus → behavioral section map | CLOSED / carried forward | Direct stock baseline evidence |
| State channel → writer/reader/owner model | CONTROL-PARTIAL | R2 seed ledger; complete ownership matrix remains open |
| `train-*` demand → feasibility | OPEN for this import pass | Existing target evidence must remain authoritative; imported executor analogues do not replace it |
| Feasibility → production executor | OPEN | No imported source establishes this Stock-Ai edge directly |
| Executor → engine production command | OPEN | No direct Stock-Ai source evidence imported here |
| Command → pending production | OPEN | Construction analogue only; no production-specific Stock-Ai proof |
| Pending → completed unit | OPEN | No imported world-state evidence |
| Completed unit → reassessment | OPEN | Count-based reassessment is known elsewhere but this import does not promote an analogue |
| Failure/cancellation → recovery | OPEN | No imported Stock-Ai production recovery closure |

## Important non-results

This consolidation intentionally does **not** claim:

- that `militaryUnits.per` is part of the Stock-Ai flattened source;
- that `can-train` is the Stock-Ai production boundary;
- that `train` is an engine-facing primitive in Stock-Ai merely because AiBuilder uses it;
- that pending production proves completion;
- that a runtime `DE_QUEUE` observation proves source-level command semantics;
- that historical Promisory behavior exists unchanged in the current Stock-Ai corpus.

## Falsification conditions

The imported atlas entries must be revised if:

1. the exact Stock-Ai source exposes a different production executor path;
2. an imported provenance identity is shown to refer to a different source revision;
3. current Stock-Ai source evidence contradicts an imported ownership/consumer claim;
4. a target-build runtime result establishes a different command/pending/completion boundary;
5. a previously analogue-only mechanism is independently proven in the Stock-Ai corpus.

## Conclusion

The consolidation reduces duplicate investigation. The existing AiByz evidence is now represented in the Stock-Ai atlas with provenance and explicit evidence boundaries. **No new Stock-Ai production lifecycle edge is closed by these imports.** The remaining production gap is therefore a targeted Stock-Ai consumer/executor question rather than a reason to repeat the entire production archaeology.
