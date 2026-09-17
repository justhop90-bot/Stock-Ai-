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

The source-side production gap is now closed for all 21 `ENGINE_ACTION` consumers indexed by the consumer table. Every one of those rules was recovered to its complete predicate/action body and classified by the role played by `train-civ-goal`.

| Role | Count | Source conclusion |
|---|---:|---|
| `TRUE_DEMAND -> FEASIBILITY -> ACTION` | **14** | Villager production rules use `train-civ-goal == 1` as the active villager-production demand/enable state, then require `can-train villager` and execute `train villager`. |
| `STRATEGIC_GATE -> ACTION` | **7** | Four monk rules use `train-civ-goal == 1` as a general production authorization gate; three special-unit rules use `ri-chain-mail` or `-1` as resource/technology/production-mix gates. |
| **Total ENGINE_ACTION** | **21** | Complete source-side action set closed. |

The important distinction is that `ENGINE_ACTION` is an evidence classification, while the new 14/7 split identifies the semantic role of the `train-civ-goal` read inside each action rule.

## Six production boundaries

| # | Boundary | Status | Source finding |
|---|---|---|---|
| 1 | `train-* demand → feasibility` | **PROVEN-SOURCE** | 14 rules expose direct villager demand-to-feasibility, while 7 additional action rules use `train-civ-goal` as a strategic authorization gate. |
| 2 | `feasibility → production executor` | **PROVEN-SOURCE** | All 21 action rules place `can-train <unit>` in the condition set and `(train <unit>)` in the action set. |
| 3 | `production executor → engine command` | **SOURCE-ACTION CLOSED / ENGINE-ABI OPEN** | `(train <unit>)` is a source-visible production action. Its internal engine serialization/queue behavior is not represented by the `.per` body. |
| 4 | `engine command → pending production` | **OPEN / RUNTIME-ONLY** | The only production pending predicate is a pre-action `up-pending-objects c: villager <= 0` guard. No post-action pending write is source-visible. |
| 5 | `pending → completed unit` | **OPEN / RUNTIME-ONLY** | Unit-count predicates provide controller observation/reassessment, but the source does not expose a pending-to-completion transition. |
| 6 | `completion → reassessment` | **PROVEN-CONTROLLER / WORLD EDGE OPEN** | The controller repeatedly re-reads goals, counts, resources, research state, and resets; a specific completed-object causal edge remains unproven. |

## The 21 action edges

The complete closure is recorded in:

`docs/forensics/AI_HD_TRAIN_ENGINE_ACTION_CLOSURE_2026-09-17.md`

| Source range | Target | `train-civ-goal` role |
|---|---|---|
| 19427-19436 | villager | TRUE_DEMAND |
| 19444-19454 | villager | TRUE_DEMAND |
| 19466-19483 | villager | TRUE_DEMAND |
| 19484-19506 | villager | TRUE_DEMAND |
| 19507-19526 | villager | TRUE_DEMAND |
| 24646-24662 | villager | TRUE_DEMAND |
| 24663-24684 | villager | TRUE_DEMAND |
| 24691-24707 | villager | TRUE_DEMAND |
| 24708-24724 | villager | TRUE_DEMAND |
| 24725-24738 | villager | TRUE_DEMAND |
| 24739-24748 | villager | TRUE_DEMAND |
| 24749-24763 | villager | TRUE_DEMAND + pending guard |
| 24764-24779 | villager | TRUE_DEMAND |
| 24780-24806 | villager | TRUE_DEMAND |
| 28948-28962 | eagle-warrior-line | STRATEGIC_GATE (`ri-chain-mail`) |
| 29618-29629 | elephant-archer-line | STRATEGIC_GATE (`-1` alternative) |
| 29630-29643 | my-unique-unit-line | STRATEGIC_GATE (`-1` alternative) |
| 29943-29956 | monk | STRATEGIC_GATE (general authorization) |
| 29993-30006 | monk | STRATEGIC_GATE (general authorization) |
| 30007-30020 | monk | STRATEGIC_GATE (general authorization) |
| 30021-30038 | monk | STRATEGIC_GATE (general authorization) |

## Consumer classification

The full source-level consumer table remains:

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

The 21 action rules are no longer an undifferentiated set: **14 are direct demand/action bridges and 7 are strategic authorization/action bridges.**

## Immediate predicate map

### TRUE_DEMAND rules

The 14 villager rules vary their local constraints, but the causal pattern is stable:

```text
train-civ-goal == 1
        ↓
local population / age / resource / research constraints
        ↓
can-train villager
        ↓
train villager
```

Relevant local constraints include:
- custom population and population caps;
- villager-count targets;
- Dark/Feudal/Castle age;
- food/gold thresholds;
- rush/boom/fast-Imperial strategy;
- wheel-barrow and hand-cart research-pending state;
- Wonder-race population targets;
- one explicit `up-pending-objects c: villager <= 0` guard.

The pending predicate is **pre-action**. It does not prove that `(train villager)` creates a pending object.

### STRATEGIC_GATE rules

The seven rules demonstrate three distinct uses:

1. **General production authorization:** four monk rules require `train-civ-goal == 1` but use monastery count, Sanctity/Pikeman research state, food/gold, Castle age, cavalry threat, anti-monk threat, and unit/control goals to determine whether to train a monk.
2. **Technology/resource reservation:** the eagle rule reads `train-civ-goal == ri-chain-mail` inside a NAND gate, preventing the action while chain-mail resources are reserved unless the gold condition permits it.
3. **Production-mix suppression:** elephant-archer and unique-unit rules accept `train-civ-goal == -1` as an alternative gate to sufficient unique-unit food, effectively using the state as a villager-training/production-mix condition rather than as unique-unit demand.

## Producer selection

No source-visible consumer of `train-civ-goal` explicitly selects a production building. The action supplies only the unit target:

```text
(train villager)
(train monk)
(train eagle-warrior-line)
(train elephant-archer-line)
(train my-unique-unit-line)
```

Therefore:

```text
controller demand/authorization
    -> can-train <target>
    -> train <target>
    -> [ENGINE ABI / producer selection]
```

The `.per` source closes the target-level action but not the producer-selection implementation.

## Pending evidence

The recovered monolith contains **84** active `up-pending-objects` occurrences. Only one action rule combines `train-civ-goal`, a pending-object predicate, and a direct train action:

```text
24749-24763
(goal train-civ-goal 1)
(up-pending-objects c: villager <= 0)
...
(can-train villager)
=>
(train villager)
```

This is a pre-action duplicate/pending guard. No source-visible post-action pending write or pending-to-completion transition is established by the 21 rules.

## Negative evidence / falsification

The byte-verified source supports these bounded negative findings:

- No active production-demand goal family other than `train-civ-goal` was found.
- No explicit `PRODUCER_SELECTION` consumer of `train-civ-goal` was found.
- No post-action pending-production write is visible in the closed 21 action rules.
- No source-visible pending-to-completed-object transition is established.
- No alternative source-level action bridge contradicting the 14/7 split was found in the recovered monolith.

The closure would need revision if the same byte-verified corpus yielded an additional active action rule, an alternate production-demand register, an explicit producer-selection rule, or a source-visible completion protocol.

## Remaining six-boundary status

| Boundary | Current closure |
|---|---|
| demand → feasibility | **CLOSED / SOURCE** |
| feasibility → action | **CLOSED / SOURCE** |
| action → engine command serialization | **OPEN / ENGINE-ABI** |
| engine command → pending state | **OPEN / RUNTIME** |
| pending → completed unit | **OPEN / RUNTIME** |
| completion → reassessment causal edge | **CONTROLLER-CLOSED / WORLD EDGE OPEN** |

No runtime probe was run in this pass. Historical/Donor/AiByz material was not used to promote any Stock-Ai source finding.