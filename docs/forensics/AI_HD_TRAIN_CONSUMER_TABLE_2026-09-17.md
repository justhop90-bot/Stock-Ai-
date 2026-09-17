# AI-HD `train-*` / Production Consumer Table — 2026-09-17

**Target:** `justhop90-bot/Stock-Ai-` / `main`  
**Source artifact:** `AI source` / `AI (HD version).per` Git blob  
**Verified Git blob SHA-1:** `49aae55413d9eadc7edd7a9a134515fd58702191`  
**Recovered bytes:** `1,240,320`  
**Recovered source lines:** `38,218`  
**Recovered raw-byte SHA-256:** `d7d10c337291076e26156d9ef2328767db56e479217db0bcb63337225c457199`  
**Runtime probes:** none  
**AiByz re-archaeology:** none  
**Source corpus modified:** no

## Integrity gate

The blob was recovered through the authenticated GitHub Git-object path and independently re-read on the authorized local machine. The local byte stream produced the same Git blob SHA-1:

```text
blob 49aae55413d9eadc7edd7a9a134515fd58702191
bytes: 1240320
sha1:  49aae55413d9eadc7edd7a9a134515fd58702191
sha256: d7d10c337291076e26156d9ef2328767db56e479217db0bcb63337225c457199
```

The previously unavailable monolith is therefore now **byte-verified and semantically searchable**. GitHub code-search no-match results are no longer used as evidence for the source findings below.

## Production-demand symbol enumeration

After stripping semicolon comments and enumerating identifiers beginning with `train`:

| Symbol | Result |
|---|---|
| `train-civ-goal` | **1 active definition**, line 33 |
| `train-forward-timer` | timer symbol, not production-demand state, line 161 |
| Other active `train*` goal identifiers | **none found** |
| Historical/non-hyphenated examples (`trainvillager`, `trainarcher`, `traincamel`, `trainknight`, `trainram`) | **none active**; `trainram` occurs only in a comment at line 27650 |

Definition:

```text
33  (defconst train-civ-goal 5)
```

Therefore the recovered Stock-Ai monolith does **not** contain the previously hypothesized family of active `train-villager`, `train-archer`, `train-camel`, etc. goal symbols. Its active controller-level production-demand register in this source is `train-civ-goal`.

## Consumer classification

Classification is attached to each active **read** of `train-civ-goal`.

- `STATE_ONLY`: reads the demand/state register but does not share the rule with a direct `can-train` + `train` production action.
- `ENGINE_ACTION`: the same rule reads `train-civ-goal`, contains `can-train`, and contains a direct `(train ...)` action. This is a source-visible production-action edge. It is not runtime proof of command emission or world completion.
- `FEASIBILITY_GATE`: no demand-state read was found whose primary role is a separate feasibility-only consumer; the feasibility predicate appears embedded in the `ENGINE_ACTION` rules.
- `PRODUCER_SELECTION`: no explicit producer-selection consumer of `train-civ-goal` was found.
- `RESET`: applies to writers/resets, not reads; reset writers are summarized below.
- `UNKNOWN`: none among active `train-civ-goal` reads after byte recovery.

### Every active `train-civ-goal` read site

| Source line | Classification | Source role / note |
|---:|---|---|
| 5493 | STATE_ONLY | strategic controller read |
| 5495 | STATE_ONLY | strategic controller read |
| 15081 | STATE_ONLY | strategic/resource-control read |
| 16840 | STATE_ONLY | resource-control read |
| 16858 | STATE_ONLY | resource-control read |
| 16869 | STATE_ONLY | research-reservation state read |
| 17829 | STATE_ONLY | economy/production policy read |
| 18787 | STATE_ONLY | resource-control read |
| 18815 | STATE_ONLY | research-reservation read |
| 18816 | STATE_ONLY | research-reservation read |
| 18907 | STATE_ONLY | research-reservation read |
| 18923 | STATE_ONLY | research-reservation read |
| 18941 | STATE_ONLY | research-reservation read |
| 18954 | STATE_ONLY | research-reservation read |
| 18968 | STATE_ONLY | research-reservation read |
| 18992 | STATE_ONLY | research-reservation read |
| 19014 | STATE_ONLY | research-reservation read |
| 19200 | STATE_ONLY | resource-control read |
| 19216 | STATE_ONLY | resource-control read |
| 19241 | STATE_ONLY | resource-control read |
| 19428 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 19445 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 19467 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 19485 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 19508 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 19939 | STATE_ONLY | research/resource-control read |
| 20138 | STATE_ONLY | research-reservation read |
| 20140 | STATE_ONLY | research-reservation read |
| 22205 | STATE_ONLY | research/resource-control read |
| 22243 | STATE_ONLY | strategic production-state read |
| 23116 | STATE_ONLY | resource-control read |
| 23926 | STATE_ONLY | reset-state inspection (`goal ... -1`) |
| 23936 | STATE_ONLY | reset-state inspection (`goal ... -1`) |
| 24654 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 24672 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 24701 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 24718 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 24726 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 24740 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 24750 | ENGINE_ACTION | `can-train villager` + `train villager`; adjacent pending-object guard exists in the following rule |
| 24765 | ENGINE_ACTION | `can-train villager` + `train villager` + `up-pending-objects` guard |
| 24785 | ENGINE_ACTION | `can-train villager` + `train villager` |
| 28950 | ENGINE_ACTION | `can-train eagle-warrior-line` + `train eagle-warrior-line`; `train-civ-goal` is used as a resource-control/research gate |
| 29622 | ENGINE_ACTION | `can-train elephant-archer-line` + `train elephant-archer-line` |
| 29637 | ENGINE_ACTION | `can-train my-unique-unit-line` + `train my-unique-unit-line` |
| 29945 | ENGINE_ACTION | `can-train monk` + `train monk` |
| 29995 | ENGINE_ACTION | `can-train monk` + `train monk` |
| 30009 | ENGINE_ACTION | `can-train monk` + `train monk` |
| 30023 | ENGINE_ACTION | `can-train monk` + `train monk` |

**Counts:** 49 active read sites = **28 STATE_ONLY + 21 ENGINE_ACTION**. No active `PRODUCER_SELECTION`, separate `FEASIBILITY_GATE`, or `UNKNOWN` read site was identified.

## Direct action linkage

The 21 `ENGINE_ACTION` reads resolve to these source rule ranges:

```text
19427-19436    villager
19444-19454    villager
19466-19483    villager
19484-19506    villager
19507-19526    villager
24646-24662    villager
24663-24684    villager
24691-24707    villager
24708-24724    villager
24725-24738    villager
24739-24748    villager
24749-24763    villager
24764-24779    villager + pending-object pre-action guard
24780-24806    villager
28948-28962    eagle-warrior-line
29618-29629    elephant-archer-line
29630-29643    my-unique-unit-line
29943-29956    monk
29993-30006    monk
30007-30020    monk
30021-30038    monk
```

The source pattern is explicit in these rules:

```text
(goal train-civ-goal ...)
(can-train <unit>)
=>
(train <unit>)
```

This is the previously unresolved source-side demand/feasibility/action bridge for the subset of production rules that actually consume `train-civ-goal`.

## Pending-production evidence

The recovered source contains 84 active occurrences of `up-pending-objects`. Only one rule combines `train-civ-goal` with a pending-object predicate:

```text
24764-24779
(goal train-civ-goal 1)
(up-pending-objects c: villager <= 0)
...
(can-train villager)
=>
(train villager)
```

This proves a **pre-action pending/duplicate-suppression guard** in the Stock controller. It does **not** prove that `(train villager)` writes a pending object, nor that the pending object later becomes a completed unit.

No active `up-pending-placement` or `status-pending` production path was found in the recovered monolith.

## Producer-selection result

No source-visible rule consuming `train-civ-goal` performs explicit building/producer selection. The direct action supplies the unit target (`villager`, `monk`, `eagle-warrior-line`, etc.). The source therefore establishes:

```text
controller state
    -> can-train target
    -> train target
```

but does **not** establish a separate source-level:

```text
train demand -> choose TC/monastery/barracks/etc.
```

Producer selection remains an engine/implicit-action boundary unless another source mechanism is found.

## Negative evidence after byte recovery

These are now bounded source-level negative findings, not GitHub-index failures:

- No active `train-villager`, `train-archer`, `train-camel`, `train-knight`, `train-ram`, or equivalent hyphenated production-goal family was found.
- No active non-hyphenated `trainvillager`, `trainarcher`, `traincamel`, `trainknight`, or `trainram` goal was found.
- `trainram` occurs only in a comment at line 27650.
- No active `train-*` goal other than `train-civ-goal` was found.
- No explicit `PRODUCER_SELECTION` consumer of `train-civ-goal` was found.
- No post-action pending-production write is visible around the `train-civ-goal` action rules.
- No source-visible pending-to-completed-object transition is established by these rules.

These are bounded source findings only; they do not establish universal engine absence.

## Evidence boundary

`(train <unit>)` is now **PROVEN-SOURCE as a direct source-visible production action**. The source also proves that, in 21 rules, `train-civ-goal` is read in the same rule as `can-train` and `train`.

This does **not** by itself prove:

- engine command serialization,
- queue insertion as a world-state event,
- pending-object creation caused by the command,
- object identity/lineage,
- completion timing,
- cancellation/failure semantics,
- completion-triggered reassessment.

Those remain runtime/engine-boundary questions and were intentionally not probed.
