# AoE2DE `.per` Engine Contract v0.1

**Status:** Working contract — evidence-backed where marked, provisional where marked.

**Purpose:** Define the engine boundary that Stock-Ai- must respect before architecture is designed. This is a contract, not a claim that every engine detail has already been experimentally proven.

## 1. Execution Model

AoE2DE AI scripting is a rule-based expert system. A `.per` script defines rules containing **facts/conditions** before `=>` and **actions** after it. The engine evaluates rules repeatedly during a match; active rules remain active until disabled or otherwise prevented from firing. citeturn0search6turn0search27

**Engineering consequence:** `.per` is fundamentally a continuously evaluated reactive system, not a conventional sequential program. Any architecture that assumes “run function A, then B, then C” without accounting for repeated rule evaluation is suspect.

## 2. Rule Contract

Canonical shape:

```text
(defrule
    (fact-1)
    (fact-2)
    =>
    (action-1)
    (action-2)
)
```

Facts gate execution. Actions execute when the rule's conditions are satisfied. Parentheses are syntactically significant; whitespace is not. citeturn0search27

A rule may disable itself, which is the standard mechanism for one-shot behavior. citeturn0search27turn0search6

**Stock-Ai rule:** Every rule must have an explicit intended lifetime: persistent, one-shot, timer/goal gated, or state gated. “It will only fire once because the game state probably changes” is not a lifetime contract.

## 3. Facts and Actions

The engine exposes commands used as facts and/or actions. Facts answer questions or establish predicates; actions cause requests or changes. Some command families can have dual fact/action semantics depending on placement. citeturn0search16

**Stock-Ai rule:** Treat every engine command according to its documented role. Do not infer that a successful predicate implies persistent world state, and do not infer that an action completed merely because the action was accepted by the rule engine.

## 4. State Is Distributed

Important AI state is represented through multiple engine mechanisms, including goals, timers, strategic numbers, and other engine-maintained values. Strategic numbers can both influence built-in behavior and be read/set by scripts. citeturn0search0turn0search7

**Stock-Ai rule:** State ownership must be explicit. A strategic number is not automatically “ours” merely because a rule can write it. Before using one, determine whether stock/Promi logic also writes it and whether the value has engine-side semantics beyond simple storage.

## 5. Strategic Numbers

Strategic numbers are a major control surface for the built-in AI behavior. They influence decisions such as resource allocation, exploration, military behavior, and other engine-managed behavior. Public scripting references demonstrate both reading and writing strategic numbers. citeturn0search0turn0search7

**Unresolved contract items:** exact DE strategic-number registry, default values, legal ranges, side effects, writer ownership in the current stock AI, and which values are safe for project-owned policy.

These must be extracted from the installed/current DE source corpus before architecture assigns strategic-number ownership.

## 6. Loading and Modularity

AoE2 AI projects commonly use a small entry `.per` that loads other `.per` files. Public DE discussion confirms that the stock/Promi system is modular and that a main loader can exist outside the obvious AI directory. citeturn0search13

Conditional loading exists and makes loading decisions while the parser is processing the script; it is therefore not equivalent to a conventional preprocessor. Historical scripting documentation also notes that syntax checking can cover rules that are not ultimately loaded for a particular game setting. citeturn0search4

**Stock-Ai rule:** Load order is part of the program. A module is not independent merely because it is in a separate file.

## 7. `.ai` / `.per` Boundary

Historical and community documentation describes a paired `.ai`/`.per` entry model for custom AIs. The `.ai` identifies the AI while the `.per` contains the scripting logic; modern DE distributions also use modular `.per` loading. citeturn0search27turn0search13

**Current-DE verification required:** exact current entry-file behavior, personality registration, loader resolution, and which files are authoritative in the installed build.

## 8. Evaluation Semantics We Must Prove

Before writing architecture, the following engine behaviors must be experimentally or source verified:

- rule evaluation order;
- whether all eligible rules can fire during one pass;
- action ordering within a rule;
- effects of one action on later facts in the same evaluation cycle;
- rule re-evaluation timing;
- `disable-self` timing;
- goal and timer semantics;
- strategic-number write visibility;
- command acceptance versus command completion;
- queue/resource reservation behavior;
- construction-start versus construction-complete observability;
- unit/task assignment side effects;
- conditional-load behavior in current DE;
- error behavior for undefined symbols, duplicate definitions, malformed rules, and unavailable commands.

Until these are verified, they are **engine unknowns**, not architecture assumptions.

## 9. State-Transition Discipline

Stock-Ai will model important decisions as closed-loop control:

```text
OBSERVE
  ↓
CLASSIFY
  ↓
WRITE / UPDATE STATE
  ↓
AUTHORIZE
  ↓
ISSUE ACTION
  ↓
VERIFY WORLD CHANGE
  ↓
REASSESS
```

A command is an attempt. Verification is evidence. This distinction is mandatory because the rule engine can repeatedly re-evaluate the same conditions and therefore amplify an incorrect assumption into repeated commands.

## 10. Resource and Commitment Boundary

Escrow, resource availability, production queues, construction commitments, and technology commitments require separate investigation. Public scripting material confirms escrow as a scripting subsystem, but the exact current-DE semantics and interaction with stock logic must be established from the DE source corpus. citeturn0search7

**Stock-Ai rule:** No subsystem may reserve a resource without defining who owns the reservation, what releases it, and what evidence proves the intended expenditure occurred.

## 11. Engine ABI Checklist

Before Checklist 1 is accepted, we need a verified registry covering:

- facts/predicates;
- actions;
- goals;
- timers;
- strategic numbers;
- constants and `defconst` behavior;
- operators and boolean composition;
- object/unit/building identifiers;
- technology identifiers;
- resource/commodity interfaces;
- production/build/research commands;
- military/task commands;
- scouting/map queries;
- escrow interfaces;
- conditional loading;
- file loading and include conventions;
- debug/trace facilities available to `.per`;
- parser limits and syntax restrictions.

Each registry entry must identify its evidence source and confidence.

## 12. Evidence Labels

Use only these labels in engine documentation:

- **DIRECT:** verified from current DE source, installed files, or controlled runtime behavior.
- **COMPOSED:** multiple DIRECT facts combined without adding an unverified semantic claim.
- **INFERRED:** technically reasonable interpretation not directly proven.
- **REFERENCE:** observed in a mature external AI or historical scripting reference; not automatically current-DE truth.
- **UNCERTAIN:** unresolved.

External documentation can establish a research lead. It cannot silently become a current-DE contract.

## 13. Acceptance Gate

Checklist 1 is complete only when the project can answer, with evidence, **what `.per` can observe, what `.per` can request, how rules execute, how state persists, how modules load, and which engine behaviors remain unknown.**

Until then, architecture work is premature.
