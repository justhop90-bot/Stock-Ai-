# AI-HD `train-civ-goal` ENGINE_ACTION Closure — 2026-09-17

**Target:** `justhop90-bot/Stock-Ai-` / `main`  
**Source:** `AI source` / `AI (HD version).per`  
**Verified source blob:** `49aae55413d9eadc7edd7a9a134515fd58702191`  
**Source bytes:** `1,240,320`  
**Source lines:** `38,218`  
**Source SHA-256:** `d7d10c337291076e26156d9ef2328767db56e479217db0bcb63337225c457199`  
**Runtime probes:** none

## Closure result

All 21 source-visible `ENGINE_ACTION` consumers indexed by `AI_HD_TRAIN_CONSUMER_TABLE_2026-09-17.md` were closed against their complete rule bodies.

| Role of `train-civ-goal` in the rule | Count | Interpretation |
|---|---:|---|
| `TRUE_DEMAND -> FEASIBILITY -> ACTION` | **14** | `train-civ-goal == 1` is the active villager-production demand/enable state; the rule additionally requires `can-train villager` and executes `train villager`. |
| `STRATEGIC_GATE -> ACTION` | **7** | The rule uses `train-civ-goal` as a broader production/resource/technology gate rather than as the unit-specific demand being acted on. |
| **Total** | **21** | All source-visible action edges closed. |

The seven strategic-gate rules divide into:
- **4 monk actions:** `train-civ-goal == 1` is a general production authorization combined with monk-specific tactical/resource/technology predicates.
- **3 non-villager special-unit actions:** `train-civ-goal` is used as `ri-chain-mail` or `-1` state gating around eagle/elephant/unique-unit production.

No source-visible `train-civ-goal` consumer performs explicit producer-building selection.

---

## 1. TRUE_DEMAND -> FEASIBILITY -> ACTION: 14 villager rules

These are the cleanest source-side production edges. In every case the rule contains `(goal train-civ-goal 1)`, a villager-specific feasibility predicate, and `(train villager)`. Age/resource/unit-count predicates constrain when the demand is actionable; they do not change the role of `train-civ-goal` from the active villager-production demand state.

### 1.1 `19427-19436` — baseline villager production

```text
(defrule
    (goal train-civ-goal 1)
    (up-compare-goal custom-civ-pop < max-civ)
    (population < del-civ-pop)
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit-count predicate: none.
- Resource predicate: none.
- Age predicate: none.
- Pending predicate: none.
- Feasibility: `can-train villager`.
- Action: `train villager`.

### 1.2 `19444-19454` — wheel-barrow pending gate

```text
(defrule
    (goal train-civ-goal 1)
    (up-research-status c: ri-wheel-barrow >= research-pending)
    (up-compare-goal custom-civ-pop < max-civ)
    (population < del-civ-pop)
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit-count predicate: none.
- Research gate: `ri-wheel-barrow >= research-pending`.
- Resource predicate: none.
- Age predicate: none.
- Pending-production predicate: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.3 `19466-19483` — hand-cart pending gate

```text
(defrule
    (goal train-civ-goal 1)
    (up-research-status c: ri-hand-cart >= research-pending)
    (up-compare-goal custom-civ-pop < max-civ)
    (population < del-civ-pop)
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit-count predicate: none.
- Research gate: `ri-hand-cart >= research-pending`.
- Resource predicate: none.
- Age predicate: none.
- Pending-production predicate: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.4 `19484-19506` — low-resource / age villager gate

```text
(defrule
    (goal train-civ-goal 1)
    (up-compare-goal custom-civ-pop < max-civ)
    (population < del-civ-pop)
    (or
        (and (current-age == feudal-age)
             (gold-amount < 170))
        (and (and (unit-type-count-total villager < 30)
                  (food-amount < 900))
             (current-age == dark-age)))
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: `villager < 30` in the dark-age branch.
- Resources: `gold < 170` in Feudal branch; `food < 900` in Dark branch.
- Age: Feudal or Dark, as above.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.5 `19507-19526` — rush/boom Feudal villager production

```text
(defrule
    (goal train-civ-goal 1)
    (current-age == feudal-age)
    (up-compare-goal custom-civ-pop < max-civ)
    (population < del-civ-pop)
    (or
        (goal strategy-goal rush)
        (goal strategy-goal boom))
    (or
        (food-amount < 760)
        (current-age-time < 30))
    (or
        (current-age-time < 55)
        (starting-age == feudal-age))
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: none.
- Resources: `food < 760` alternative.
- Age/time: Feudal; age-time thresholds.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.6 `24646-24662` — wonder-race villager target

```text
(defrule
    (up-compare-goal custom-civ-pop < max-civ)
    (population < del-civ-pop)
    (or
        (or
            (and (current-age <= dark-age)
                 (unit-type-count-total villager < villager-wonder-dark))
            (and (current-age >= feudal-age)
                 (unit-type-count-total villager < villager-wonder-feudal)))
        (strategic-number sn-current-age >= ci-transit))
    (goal train-civ-goal 1)
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: villager below wonder-era target, or bypassed by current-age strategic threshold.
- Resource: none.
- Age: Dark/Feudal-or-later via target branch; `sn-current-age >= ci-transit` alternative.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.7 `24663-24684` — fast-Imperial villager production

```text
(defrule
    (up-compare-goal custom-civ-pop < max-civ)
    (population < max-civ-pop)
    (or
        (and (current-age == dark-age)
             (unit-type-count-total villager < 33))
        (current-age == feudal-age))
    (up-compare-goal unit-goal != wonder)
    (unit-type-count-total villager < 35)
    (goal strategy-goal fast-imp)
    (goal train-civ-goal 1)
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: villager `<33` in Dark branch and `<35` overall.
- Resource: none.
- Age: Dark or Feudal.
- Strategy: `fast-imp`; unit goal cannot be Wonder.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.8 `24691-24707` — Dark-age standard villager gate

```text
(defrule
    (strategic-number sn-current-age == dark)
    (unit-type-count-total villager < 31)
    (nor
        (goal strategy-goal flush)
        (strategic-number sn-minimum-water-body-size-for-dock == water-islands))
    (or
        (unit-type-count-total villager < dark-age-villager)
        (or
            (food-amount < 700)
            (unit-type-count-total villager < villager-feudal)))
    (or
        (food-amount < 820)
        (unit-type-count-total villager < 23))
    (goal train-civ-goal 1)
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: `<31`, `< dark-age-villager`, `< villager-feudal`, or `<23` depending branch.
- Resources: food `<700` or `<820` in alternative branches.
- Age: `sn-current-age == dark`.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.9 `24708-24724` — Dark flush/islands villager gate

```text
(defrule
    (strategic-number sn-current-age == dark)
    (unit-type-count-total villager < 31)
    (or
        (goal strategy-goal flush)
        (strategic-number sn-minimum-water-body-size-for-dock == water-islands))
    (nand
        (unit-type-count-total villager >= villager-flush)
        (food-amount >= 500))
    (or
        (unit-type-count-total villager < villager-feudal)
        (food-amount < 440))
    (goal train-civ-goal 1)
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: `<31`, `< villager-feudal`; `nand villager >= villager-flush AND food >=500`.
- Resource: food `<440` alternative.
- Age: Dark.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.10 `24725-24738` — Feudal flush/sling villager gate

```text
(defrule
    (goal train-civ-goal 1)
    (current-age == feudal-age)
    (or
        (goal strategy-goal flush)
        (goal strategy-goal sling))
    (or
        (not (research-available castle-age))
        (or
            (food-amount < 740)
            (gold-amount < 160)))
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: none.
- Resources: food `<740` or gold `<160`, unless Castle research is unavailable.
- Age: Feudal.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.11 `24739-24748` — Feudal food-priority villager gate

```text
(defrule
    (goal train-civ-goal 1)
    (food-amount < 500)
    (strategic-number sn-current-age == feudal)
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: none.
- Resource: food `<500`.
- Age: Feudal.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.12 `24749-24763` — explicit pending guard

```text
(defrule
    (goal train-civ-goal 1)
    (up-pending-objects c: villager <= 0)
    (food-amount >= 750)
    (building-type-count archery-range == 0)
    (building-type-count stable == 0)
    (building-type-count market == 0)
    (strategic-number sn-current-age == feudal)
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: none.
- Resource: food `>=750`.
- Age: Feudal.
- Pending: `up-pending-objects c: villager <= 0` — **pre-action duplicate/pending guard**.
- Building constraints: no archery range, stable, or market.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.13 `24764-24779` — Castle-age villager production

```text
(defrule
    (goal train-civ-goal 1)
    (current-age >= castle-age)
    (up-compare-goal custom-civ-pop < max-civ)
    (or
        (population < max-civ-pop)
        (game-time < 1500))
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: no direct villager count; population/custom-pop bounds instead.
- Resource: none.
- Age: Castle or later.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

### 1.14 `24780-24806` — Castle knight/elephant extra-villager gate

```text
(defrule
    (strategic-number sn-minimum-water-body-size-for-dock < water-islands)
    (population < max-civ-pop)
    (up-compare-goal custom-civ-pop < max-civ)
    (up-compare-goal custom-civ-pop < 140)
    (goal train-civ-goal 1)
    (strategic-number sn-current-age == castle)
    (food-amount > 200)
    (gold-amount < 600)
    (or
        (goal unit-goal knight)
        (or
            (goal unit-goal battle-elephant)
            (or
                (civ-selected khmer)
                (civ-selected persian))))
    (can-train villager)
=>
    (disable-timer FDrop)
    (enable-timer FDrop 21)
    (train villager))
```

- Demand: `train-civ-goal == 1`.
- Unit count: none.
- Resources: food `>200`, gold `<600`.
- Age: Castle.
- Strategic condition: knight/battle-elephant goal or Khmer/Persian civ.
- Pending: none.
- Feasibility/action: `can-train villager` -> `train villager`.

---

## 2. STRATEGIC_GATE -> ACTION: special-unit rules

These seven rules are not seven independent unit-demand registers. They demonstrate that `train-civ-goal` is also used as a general authorization/resource-control state around other production actions.

### 2.1 `28948-28962` — Eagle Warrior: chain-mail reservation gate

```text
(defrule
    (strategic-number sn-resource-control < 1)
    (nand
        (goal train-civ-goal ri-chain-mail)
        (gold-amount < 160))
    (or
        (food-amount >= 52)
        (or
            (town-under-attack)
            (and
                (goal control-goal aggressive-rush)
                (current-age-time < 240))))
    (goal unit-goal eagle-warrior)
    (goal strategy-goal rush)
    (can-train eagle-warrior-line)
=>
    (train eagle-warrior-line)
)
```

**Classification:** `STRATEGIC_GATE -> ACTION`.

- `train-civ-goal` value: `ri-chain-mail`, not `1`.
- Function: blocks the eagle action while chain-mail is reserved unless gold is already below the threshold; it is resource/technology reservation state, not eagle demand.
- Unit count: none in this rule.
- Resources: gold `<160` is inside the NAND; food `>=52` is an alternate action-enabling condition.
- Age/time: aggressive-rush branch requires age-time `<240`.
- Pending: none.
- Feasibility/action: `can-train eagle-warrior-line` -> `train eagle-warrior-line`.

### 2.2 `29618-29629` — Elephant Archer: villager-training-off gate

```text
(defrule
    (strategic-number sn-resource-control < 1)
    (can-train elephant-archer-line)
    (or
        (up-compare-goal custom-civ-pop >= 75)
        (or
            (goal train-civ-goal -1)
            (food-amount >= unique-unit-food)))
    (or
        (current-age == castle-age)
        (gold-amount > 100))
=>
    (train elephant-archer-line)
)
```

**Classification:** `STRATEGIC_GATE -> ACTION`.

- `train-civ-goal` value: `-1`.
- Function: the `-1` state is an alternative gate to sufficient food for the unique unit; it is not elephant-archer demand.
- Unit count: none.
- Resource: `food >= unique-unit-food` alternative; `gold >100` alternative age/resource gate.
- Age: Castle or gold-rich alternative.
- Pending: none.
- Feasibility/action: `can-train elephant-archer-line` -> `train elephant-archer-line`.

### 2.3 `29630-29643` — Unique Unit: villager-training-off gate

```text
(defrule
    (strategic-number sn-resource-control < 1)
    (can-train my-unique-unit-line)
    (or
        (up-research-status c: my-unique-unit-upgrade >= research-pending)
        (or
            (goal unit-goal my-unique-unit-line)
            (goal control-goal my-unique-unit-line)))
    (or
        (up-compare-goal custom-civ-pop >= 75)
        (or
            (goal train-civ-goal -1)
            (food-amount >= unique-unit-food)))
    (or
        (current-age == castle-age)
        (gold-amount > 100))
=>
    (train my-unique-unit-line)
)
```

**Classification:** `STRATEGIC_GATE -> ACTION`.

- `train-civ-goal` value: `-1`.
- Function: one branch means villager training is disabled/removed from the current production mix; it does not specify unique-unit demand.
- Unit count: none in this rule.
- Research: unique-unit upgrade pending is a separate authorization branch.
- Resources: food `>= unique-unit-food` alternative.
- Age: Castle or gold `>100`.
- Pending: none.
- Feasibility/action: `can-train my-unique-unit-line` -> `train my-unique-unit-line`.

---

## 3. STRATEGIC_GATE -> ACTION: four monk rules

These four rules all read `train-civ-goal == 1`, but the actual monk decision is formed from monk-specific tactical/resource/technology conditions. `train-civ-goal` is therefore a **general production authorization gate**, not a monk-specific demand register.

### 3.1 `29943-29956` — monk production under low food/high gold

```text
(defrule
    (strategic-number sn-resource-control < 1)
    (goal train-civ-goal 1)
    (or
        (and
            (up-compare-goal ranged-unit-type-goal != monk)
            (up-research-status c: ri-sanctity >= research-pending))
        (unit-type-count-total monastery-class < 6))
    (food-amount < 150)
    (gold-amount > 200)
    (goal anti-monk-threat-goal 0)
    (can-train monk)
=>
    (train monk)
)
```

- Role of `train-civ-goal`: general production authorization.
- Unit count: `monastery-class < 6` in one branch.
- Resources: food `<150`, gold `>200`.
- Age: none explicit.
- Pending: none.
- Research: Sanctity pending can enable one branch.
- Feasibility/action: `can-train monk` -> `train monk`.

### 3.2 `29993-30006` — monk response to cavalry/mix state

```text
(defrule
    (strategic-number sn-resource-control < 1)
    (goal train-civ-goal 1)
    (or
        (up-research-status c: ri-sanctity >= research-pending)
        (unit-type-count-total monastery-class < 6))
    (up-research-status c: ri-pikeman >= research-pending)
    (goal anti-monk-threat-goal 0)
    (strategic-number sn-cavalry-threat >= 1)
    (or
        (goal unit-goal mix)
        (goal unit-goal skirmisher))
    (can-train monk)
=>
    (train monk)
)
```

- Role of `train-civ-goal`: general production authorization.
- Unit count: monastery-class `<6` alternative.
- Resources: none explicit.
- Age: none explicit.
- Research: Sanctity/Pikeman pending gates.
- Pending production: none.
- Threat/strategy: no anti-monk threat; cavalry threat >=1; mix/skirmisher unit goal.
- Feasibility/action: `can-train monk` -> `train monk`.

### 3.3 `30007-30020` — Castle monk production

```text
(defrule
    (strategic-number sn-resource-control < 1)
    (goal train-civ-goal 1)
    (or
        (up-research-status c: ri-sanctity >= research-pending)
        (unit-type-count-total monastery-class < 6))
    (food-amount < 100)
    (gold-amount >= 300)
    (current-age == castle-age)
    (goal anti-monk-threat-goal 0)
    (strategic-number sn-cavalry-threat > 1)
    (can-train monk)
=>
    (train monk)
)
```

- Role of `train-civ-goal`: general production authorization.
- Unit count: monastery-class `<6` alternative.
- Resources: food `<100`, gold `>=300`.
- Age: Castle.
- Research: Sanctity pending alternative.
- Pending: none.
- Threat: anti-monk threat `0`, cavalry threat `>1`.
- Feasibility/action: `can-train monk` -> `train monk`.

### 3.4 `30021-30038` — Castle aggressive-rush monk production

```text
(defrule
    (strategic-number sn-resource-control < 1)
    (goal train-civ-goal 1)
    (or
        (up-research-status c: ri-sanctity >= research-pending)
        (unit-type-count-total monastery-class < 6))
    (gold-amount >= 200)
    (current-age == castle-age)
    (goal anti-monk-threat-goal 0)
    (strategic-number sn-cavalry-threat > 1)
    (goal unit-goal cavalry-archer)
    (goal control-goal aggressive-rush)
    (can-train monk)
=>
    (train monk)
)
```

- Role of `train-civ-goal`: general production authorization.
- Unit count: monastery-class `<6` alternative.
- Resource: gold `>=200`.
- Age: Castle.
- Research: Sanctity pending alternative.
- Pending: none.
- Threat/strategy: anti-monk threat `0`; cavalry threat `>1`; cavalry-archer unit goal; aggressive-rush control goal.
- Feasibility/action: `can-train monk` -> `train monk`.

---

## 4. Immediate predicate/action map

| Rules | Target | `train-civ-goal` role | Unit-count evidence | `can-train` | Resource/tech | Age | Pending |
|---|---|---|---|---|---|---|---|
| 19427-19436 | villager | TRUE_DEMAND | none | villager | none | none | none |
| 19444-19454 | villager | TRUE_DEMAND | none | villager | Wheel-barrow pending | none | none |
| 19466-19483 | villager | TRUE_DEMAND | none | villager | Hand-cart pending | none | none |
| 19484-19506 | villager | TRUE_DEMAND | `<30` branch | villager | gold/food thresholds | Dark/Feudal | none |
| 19507-19526 | villager | TRUE_DEMAND | none | villager | food threshold | Feudal/time | none |
| 24646-24662 | villager | TRUE_DEMAND | wonder-villager targets | villager | none | age/transition | none |
| 24663-24684 | villager | TRUE_DEMAND | `<33`, `<35` | villager | none | Dark/Feudal | none |
| 24691-24707 | villager | TRUE_DEMAND | `<31`, `<dark-age-villager>`, `<villager-feudal>`, `<23` | villager | food thresholds | Dark | none |
| 24708-24724 | villager | TRUE_DEMAND | `<31`, `<villager-feudal>`, flush threshold | villager | food thresholds | Dark | none |
| 24725-24738 | villager | TRUE_DEMAND | none | villager | food/gold | Feudal | none |
| 24739-24748 | villager | TRUE_DEMAND | none | villager | food `<500` | Feudal | none |
| 24749-24763 | villager | TRUE_DEMAND | none | villager | food `>=750` | Feudal | `villager <=0` |
| 24764-24779 | villager | TRUE_DEMAND | population bounds | villager | none | Castle+ | none |
| 24780-24806 | villager | TRUE_DEMAND | population/custom-pop bounds | villager | food/gold | Castle | none |
| 28948-28962 | eagle-warrior-line | STRATEGIC_GATE | none | eagle | food/gold + chain-mail gate | time branch | none |
| 29618-29629 | elephant-archer-line | STRATEGIC_GATE | none | elephant archer | unique-unit food / gold | Castle/gold | none |
| 29630-29643 | my-unique-unit-line | STRATEGIC_GATE | none | unique unit | unique-upgrade / food / gold | Castle/gold | none |
| 29943-29956 | monk | STRATEGIC_GATE | monastery-class `<6` branch | monk | food/gold + Sanctity | none | none |
| 29993-30006 | monk | STRATEGIC_GATE | monastery-class `<6` branch | monk | Sanctity/Pikeman pending | none | none |
| 30007-30020 | monk | STRATEGIC_GATE | monastery-class `<6` branch | monk | food/gold + Sanctity | Castle | none |
| 30021-30038 | monk | STRATEGIC_GATE | monastery-class `<6` branch | monk | gold + Sanctity | Castle | none |

## 5. What this closes

### Closed at source level

1. `train-civ-goal` is the only active production-demand register in the recovered Stock-Ai monolith.
2. Fourteen rules are direct villager demand/action bridges:
   `train-civ-goal == 1 -> can-train villager -> train villager`.
3. Four monk rules use `train-civ-goal == 1` as a general production authorization gate while monk-specific predicates decide the actual action.
4. Three special-unit rules use `train-civ-goal` as a strategic/resource gate with values `ri-chain-mail` or `-1`.
5. No source-visible consumer selects a specific TC/monastery/barracks/etc. producer.
6. The one production pending predicate is a **pre-action villager duplicate guard**, not a post-action pending write.

### Not closed by this pass

- Whether `(train <unit>)` serializes to an engine queue command.
- Which producer the engine selects for a unit target.
- Whether the engine creates a pending object immediately after the action.
- Queue insertion/availability semantics.
- Pending-to-completion object lineage.
- Completion/cancellation/failure semantics.
- Whether a completed object itself triggers reassessment versus ordinary controller polling/rule re-evaluation.

These remain engine/world boundaries and were intentionally not runtime-probed.

## Falsification conditions

This source closure would need revision if byte-verified Stock-Ai source reveals:

1. an additional active production-demand goal family;
2. a source-visible `train-civ-goal` consumer that performs producer selection;
3. a source-visible post-action pending-production write associated with `(train <unit>)`;
4. a source-visible pending-to-completion transition that links the production action to object completion;
5. an alternative active rule body contradicting the 14/7 role split.

The absence claims are bounded to the recovered 1,240,320-byte monolith and do not establish universal engine absence.
