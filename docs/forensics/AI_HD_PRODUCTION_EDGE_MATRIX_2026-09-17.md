# AI-HD Production Edge Matrix — Verified Source Closure

**Date:** 2026-09-17  
**Target:** `justhop90-bot/Stock-Ai-` / `main`  
**Source artifact:** `AI source` / `AI (HD version).per`  
**Verified Git blob SHA-1:** `49aae55413d9eadc7edd7a9a134515fd58702191`  
**Recovered bytes:** `1,240,320`  
**Recovered lines:** `38,218`  
**Recovered SHA-256:** `d7d10c337291076e26156d9ef2328767db56e479217db0bcb63337225c457199`  
**Runtime probes:** none  
**Source corpus modified:** no

## Result

The production-source gap is materially closed at the controller/action boundary. The recovered Stock-Ai monolith contains one active production-demand goal, `train-civ-goal`, and **21 rules where that goal is consumed in the same rule as `can-train` and a direct `(train ...)` action**.

This changes the prior 0/6 result. The source now proves the following causal path for the identified rules:

```text
train-civ-goal state
        ↓
    can-train
        ↓
   train <unit>
```

The remaining open boundaries are engine/world lifecycle boundaries, not source-retrieval gaps.

## Six production boundaries

| # | Boundary | Status | Source finding |
|---|---|---|---|
| 1 | `train-* demand → feasibility` | **PROVEN-SOURCE** | 21 rules read `train-civ-goal` and also require `can-train`; 28 additional reads are state-only. |
| 2 | `feasibility → production executor` | **PROVEN-SOURCE** | The same 21 rules place `can-train` immediately in the condition set and `(train <unit>)` in the action set. |
| 3 | `production executor → engine command` | **SOURCE-ACTION CLOSED / ENGINE-ABI OPEN** | `(train <unit>)` is a source-visible production action. The source alone does not prove the engine's internal command/queue emission semantics. |
| 4 | `engine command → pending production` | **OPEN / RUNTIME-ONLY** | One rule uses `up-pending-objects c: villager <= 0` as a **pre-action guard**. No source-visible post-action pending write was found. |
| 5 | `pending → completed unit` | **OPEN / RUNTIME-ONLY** | Unit-count predicates exist, but no source-visible pending-object-to-completion transition is established. Pending is not completion proof. |
| 6 | `completion → reassessment` | **PROVEN-CONTROLLER / WORLD EDGE OPEN** | The controller repeatedly re-reads goals and unit/resource state, including resets, but no source-visible causal link from a specific completed production object to reassessment is established. |

## Source production-demand enumeration

After comment stripping and full-byte enumeration:

- Active production-demand goal: `train-civ-goal` — definition line **33**.
- `train-forward-timer` is a timer, not a production-demand register.
- No active `train-villager`, `train-archer`, `train-camel`, `train-knight`, `train-ram`, or equivalent hyphenated production-goal family.
- No active `trainvillager`, `trainarcher`, `traincamel`, `trainknight`, or `trainram` goals.
- `trainram` appears only in a comment at line 27650.

## Consumer classification

The full source-level consumer table is recorded in:

`docs/forensics/AI_HD_TRAIN_CONSUMER_TABLE_2026-09-17.md`

Counts:

| Classification | Count |
|---|---:|
| `STATE_ONLY` | 28 |
| `FEASIBILITY_GATE` as a separate demand consumer | 0 |
| `PRODUCER_SELECTION` | 0 |
| `ENGINE_ACTION` | 21 |
| `RESET` read sites | 0; resets are writes |
| `UNKNOWN` | 0 |
| **Active `train-civ-goal` reads** | **49** |

The 21 `ENGINE_ACTION` sites are rule-local source bridges containing `train-civ-goal` + `can-train` + `train`.

## Pending evidence

The recovered monolith contains **84** active `up-pending-objects` occurrences. Only one rule combines `train-civ-goal` with a pending-object predicate and a direct train action:

```text
24764-24779
(goal train-civ-goal 1)
(up-pending-objects c: villager <= 0)
...
(can-train villager)
=>
(train villager)
```

The ordering establishes a pre-action duplicate/pending guard. It does not establish that `(train villager)` creates the pending object, nor that the pending object later becomes a completed unit.

No active `up-pending-placement` or `status-pending` production path was found.

## Producer selection

No source-visible consumer of `train-civ-goal` explicitly selects a production building. The action specifies the train target:

```text
(train villager)
(train monk)
(train eagle-warrior-line)
(train elephant-archer-line)
(train my-unique-unit-line)
```

The source therefore proves target-level production invocation but does not expose a separate TC/monastery/barracks/etc. producer-selection step.

## Falsification / remaining closure criteria

The source findings would be falsified by recovering an active alternative production-demand family, a producer-selection rule consuming `train-civ-goal`, or a source-visible post-action pending/completion protocol not captured by the current full-byte enumeration.

The remaining runtime/engine questions are:

1. Does `(train <unit>)` serialize into an engine production/queue command exactly as assumed?
2. What engine state is created immediately after the action?
3. Does `up-pending-objects` observe that state after the action, and when?
4. How is pending linked to the completed unit?
5. What happens on queue rejection, cancellation, or producer loss?
6. Which state change causes the controller to reassess production demand?

These were intentionally **not runtime-probed**.

## Evidence rule

The previous GitHub code-search absence is retired as evidence for the recovered source. All findings in this matrix are based on the byte-verified blob itself. Imported AiByz and historical evidence remain reference/analogue evidence only and were not used to promote these Stock-Ai source claims.
