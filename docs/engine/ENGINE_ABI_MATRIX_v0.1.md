# ENGINE_ABI_MATRIX_v0.1

**Project:** Stock-Ai-
**Scope:** AoE2DE `.per` engine contract
**Status:** Sprint 0 — corpus-backed ABI reconstruction
**Authority rule:** current-DE evidence outranks historical/source-derived material
**Method:** REFERENCE → WRITE → REF → DELIVER

## 1. Purpose

This matrix is the working boundary between the AoE2DE engine and Stock-Ai architecture. It records what the `.per` interface is known to accept, expose, mutate, load, or trigger. It deliberately separates syntax, usage, semantics, and runtime realization. A symbol is not considered understood merely because it appears in a source file.

The matrix is intentionally sparse. It is not a giant command catalogue. Rows are added when they establish an ABI dependency, expose a dangerous semantic assumption, or close an important engine question.

## 2. Evidence tiers

Only these tiers are permitted:

- **VERIFIED-CORPUS** — directly established from the preserved AoE2DE/Promisory corpus or a source artifact whose exact content is available. This proves presence/usage, not necessarily semantics.
- **VERIFIED-RUNTIME** — directly observed in a controlled current-DE runtime/replay experiment with reproducible build/script/setup evidence.
- **INFERRED** — interpretation supported by multiple observations or source relationships but not directly established by current-DE runtime evidence.
- **UNKNOWN** — insufficient evidence. This is a valid result and must remain explicit.
- **REJECTED** — a specific claim or interpretation was tested or contradicted strongly enough that it must not be used.

Historical/community sources may support a row's provenance, but they do not silently become current-DE authority.

## 3. Evidence rules

1. **Usage ≠ declaration ≠ semantics.** A token appearing in `.per` proves use; it does not prove its complete ABI contract.
2. **Predicate ≠ action.** `can-build` and `build`, `can-train` and `train`, and analogous pairs are separate contracts.
3. **Command acceptance ≠ world-state completion.** The state ladder is `REQUESTED → AUTHORIZED → QUEUED/ISSUED → PENDING → OBSERVED_AVAILABLE → COMMITTED_USE → VERIFIED_EFFECT`.
4. **Negative evidence is first-class.** Absence must be established with the strongest available structural/lexical/runtime search, not by a failed guess.
5. **Conflicts remain visible.** Do not select the convenient interpretation when sources disagree.
6. **Runtime claims require reproducibility.** Record game build, script revision/hash, setup, test ID, observation, and artifact locator.
7. **External references are reference material until checked against the target installation.**
8. **Architecture may not silently depend on UNKNOWN.** An unresolved ABI edge must be isolated behind a guard, adapter, or explicit pending state.
9. **Load order is executable behavior.** A symbol's presence and its effective behavior must be evaluated in module/load-order context.
10. **Do not promote replay chronology into object identity without a validated identity edge.**

## 4. Required row fields

| Field | Requirement |
|---|---|
| CONTRACT_ID | Stable identifier; never reused for a different claim |
| NAMESPACE | RULE, FACT, ACTION, GOAL, TIMER, SN, CONST, OPERATOR, OBJECT, TECH, RESOURCE, LOAD, DEBUG, etc. |
| SYMBOL / MECHANISM | Exact token/mechanism spelling |
| TYPE | Engine contract type |
| SYNTAX | Exact invocation/declaration form, or UNKNOWN |
| OPERAND TYPES | Proven operand types |
| CARDINALITY | Operand count/shape |
| VALID EXAMPLE | Minimal supported example |
| INVALID EXAMPLE | Known invalid form, or NOT TESTED |
| CURRENT-DE EVIDENCE | What actually establishes the claim |
| EVIDENCE TIER | One of the five permitted tiers |
| SOURCE | Exact file/rule/section/URL/version/hash where available |
| READ/WRITE ROLE | READ, WRITE, READ-WRITE, REQUEST, LOAD, QUERY, etc. |
| SIDE EFFECTS | Known engine/state/queue effects; UNKNOWN if not established |
| LIFETIME | Persistent, one-shot, timer-gated, goal-gated, load-time, engine-owned, UNKNOWN |
| KNOWN WRITERS | Rules/modules/subsystems that modify it |
| KNOWN CONSUMERS | Rules/modules/subsystems that read/use it |
| OWNERSHIP | ENGINE, STOCK/PROMI, PROJECT, SHARED, UNKNOWN |
| RUNTIME TEST ID | Controlled test identifier or NONE |
| RUNTIME RESULT | Narrow observed result, not interpretation |
| CONTRADICTIONS | Conflicting evidence retained verbatim enough to locate both sides |
| CONFIDENCE | Confidence in the claim, separate from evidence tier |
| OPEN QUESTIONS | Unresolved ABI questions |
| LAST VERIFIED | Date/build of most recent verification |
| STATUS | OPEN, VERIFIED, REJECTED, SUPERSEDED |

## 5. Initial populated matrix

| CONTRACT_ID | NAMESPACE | SYMBOL / MECHANISM | TYPE | SYNTAX | OPERAND TYPES | CARDINALITY | VALID EXAMPLE | INVALID EXAMPLE | CURRENT-DE-EVIDENCE | EVIDENCE TIER | SOURCE | READ/WRITE ROLE | SIDE EFFECTS | LIFETIME | KNOWN WRITERS | KNOWN CONSUMERS | OWNERSHIP | RUNTIME TEST ID | RUNTIME RESULT | CONTRADICTIONS | CONFIDENCE | OPEN QUESTIONS | LAST VERIFIED | STATUS |
|---|---|---|---|---|---|---:|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| ABI-RULE-001 | RULE | `defrule` | rule declaration | `(defrule <facts> => <actions>)` | facts/actions | variadic by grammar | `(defrule (true) => (disable-self))` | malformed/missing `=>` | Used throughout verified AI/Promisory corpus; community formatter also parses `.per` rule structure | VERIFIED-CORPUS | AiByz practical coding KB; AoE2 AI parser/formatter references | DECLARE | Installs a rule into the AI rule set | persistent unless disabled/gated | rule set | rule engine | ENGINE | NONE | NONE | Exact current-DE evaluation order and same-pass/action-order semantics remain unclosed | high for syntax; medium for execution semantics | rule evaluation order; same-pass behavior; action ordering; re-evaluation timing | 2026-09 | OPEN |
| ABI-RULE-002 | RULE | `disable-self` | rule lifetime action | `(disable-self)` | none | 0 | `(defrule (true) => (disable-self))` | arguments | Demonstrated repeatedly in corpus and current community `.per` examples as a one-shot rule pattern | VERIFIED-CORPUS | AiByz practical coding KB; community examples | WRITE | Disables the firing rule | one-shot after firing, exact timing unclosed | initialization rules | rule lifetime | ENGINE | NONE | NONE | Exact disable timing relative to other actions/re-evaluation is not directly closed | high for existence/use; medium for timing | whether disable occurs before/after remaining actions; same-cycle re-fire semantics | 2026-09 | OPEN |
| ABI-GOAL-001 | GOAL | goal storage/read family | persistent AI state | `(goal <goal-id> <value>)` | integer goal ID/value | 2 | `(goal 6 1)` | non-integer goal/value | Verified as a standard predicate pattern in `.per` sources; AiByz documents goals as strategic state channels | VERIFIED-CORPUS | AiByz practical coding KB; community `.per` examples | READ | Reads engine goal state | persistent | goal writers | strategic rules | ENGINE | NONE | NONE | Exact range/type registry and compare semantics not closed | high | goal ID registry; value range; compare operators; overwrite timing | 2026-09 | OPEN |
| ABI-GOAL-002 | GOAL | `set-goal` | state write action | `(set-goal <goal-id> <value>)` | integer goal ID/value | 2 | `(set-goal 6 1)` | invalid/non-integer operands | Verified in AiByz-derived examples and community `.per` corpus | VERIFIED-CORPUS | AiByz practical coding KB; community `.per` examples | WRITE | Mutates goal state | persistent until overwritten/reset | strategic rules | goal predicates/actions | ENGINE | NONE | NONE | Goal mutation is established; exact same-pass visibility to subsequent predicates is not | high for syntax; medium for timing | write visibility; valid ranges; engine-owned goals | 2026-09 | OPEN |
| ABI-SN-001 | SN | strategic-number registry | engine control interface | `(strategic-number <sn>)`, `(set-strategic-number <sn> <value>)` | SN identifier + integer value | read 1; write 2 | `(set-strategic-number sn-enable-new-building-system 1)` | unknown SN name / malformed operand | Official DE release notes document strategic-number additions, fixes, and expansion of supported SN capacity; AiByz practical KB documents extensive SN use | VERIFIED-CORPUS | Official AoE2DE Update 42848; AiByz practical coding KB | READ-WRITE | Changes engine control parameters; effects are SN-specific | engine-owned/persistent until changed | many modules | many engine subsystems | ENGINE | NONE | NONE | Historical/community lists contain values not independently verified against target build | high for interface existence; medium for individual SN semantics | exact current registry; per-SN type/range/default/side effects; overwrite ownership | 2026-09 | OPEN |
| ABI-SN-002 | SN | `sn-current-age` | strategic number | `(strategic-number sn-current-age)` | SN + integer result | 1 read | `(strategic-number sn-current-age) == 2` | write without verified setter semantics | Prior AiByz corpus work records usage but not a closed declaration/type/semantics contract | UNKNOWN | AiByz prior ABI research record | READ | UNKNOWN | UNKNOWN | UNKNOWN | age/strategy rules | ENGINE | NONE | NONE | Usage establishes presence only; no closed type/range/ownership proof | medium | exact ID; whether writable; value encoding; update timing | 2026-09 | OPEN |
| ABI-FACT-001 | FACT | `fc-transit` | fact | source-dependent predicate | UNKNOWN | UNKNOWN | usage exists in corpus | NOT TESTED | Prior AiByz ABI work records usage but could not close declaration/type semantics | UNKNOWN | AiByz prior ABI research | READ | UNKNOWN | UNKNOWN | UNKNOWN | unknown | ENGINE | NONE | NONE | Do not infer type from token name | low/medium | exact syntax, operands, return semantics, scope, current-DE availability | 2026-09 | OPEN |
| ABI-FACT-002 | FACT | `ci-transit` | fact | source-dependent predicate | UNKNOWN | UNKNOWN | usage exists in corpus | NOT TESTED | Prior AiByz ABI work records usage but could not close declaration/type semantics | UNKNOWN | AiByz prior ABI research | READ | UNKNOWN | UNKNOWN | UNKNOWN | unknown | ENGINE | NONE | NONE | Same evidence rule as `fc-transit` | low/medium | exact syntax, operands, return semantics, scope, current-DE availability | 2026-09 | OPEN |
| ABI-BUILD-001 | BUILD | `can-build` | feasibility predicate | `(can-build <building>)` | building identifier | 1 | `(can-build farm)` | NOT TESTED | AiByz practical KB explicitly identifies `can-build` as a feasibility check; current DE release notes state `up-can-build` behavior for walls was fixed | VERIFIED-CORPUS | AiByz practical coding KB; official AoE2DE Update 42848 | READ | Reports build feasibility; does not itself issue a build command | instantaneous/query | construction rules | construction planner | ENGINE | NONE | NONE | Do not merge with `build`; `up-can-build` is a distinct interface | high for role/syntax; medium for exact semantics | exact valid IDs; pending-object interaction; villager/build-capacity semantics | 2026-09 | OPEN |
| ABI-BUILD-002 | BUILD | `build` | construction action | `(build <building>)` | building identifier | 1 | `(build farm)` | NOT TESTED | Repeated in AiByz-derived coding patterns and current community `.per` examples; separate from `can-build` | VERIFIED-CORPUS | AiByz practical coding KB; community `.per` examples | REQUEST | Requests construction; does not by itself prove completion | command/pending/world-state lifecycle | construction rules | engine construction system | ENGINE | NONE | NONE | Runtime production evidence establishes the general command-vs-completion distinction, but this specific action's completion bridge is not closed | high for request role; medium for completion semantics | action acceptance; pending foundation; completion observation; failure/cancellation | 2026-09 | OPEN |
| ABI-PROD-001 | PRODUCTION | `can-train` | feasibility predicate | `(can-train <unit>)` | unit/unit-line identifier | 1 | `(can-train villager)` | NOT TESTED | AiByz KB describes `can-train` as a feasibility gate; current community `.per` sources show it preceding `train` | VERIFIED-CORPUS | AiByz practical coding KB; community `.per` examples | READ | Reports current training feasibility | instantaneous/query | production rules | production planner | ENGINE | NONE | NONE | Exact queue/resource semantics remain unclosed | high | whether queued capacity counts; escrow interaction; unit-line vs unit semantics | 2026-09 | OPEN |
| ABI-PROD-002 | PRODUCTION | `train` | production action | `(train <unit>)` | unit/unit-line identifier | 1 | `(train villager)` | NOT TESTED | Repeated in AiByz KB and community `.per` sources; replay archaeology proves DE_QUEUE records contain producer IDs, unit ID, amount, player, sequence but not produced-object identity | VERIFIED-CORPUS | AiByz practical coding KB; AiByz Runtime Production Lifecycle Pass 15/16 | REQUEST | Adds/requests production queue work | pending until completion observed | production rules | production system | ENGINE | NONE | `DE_QUEUE` records prove queue command admission; object completion remains unclosed | high for request; high that command != completion | queue capacity, resource reservation, object creation, completion, identity lineage | 2026-09 | OPEN |
| ABI-PROD-003 | PRODUCTION | `DE_QUEUE` replay operation | runtime evidence surface | replay payload `[player_id, object_ids, amount, unit_id, sequence]` | player, producer object IDs, amount, unit ID, sequence | fixed observed shape | `{"player_id":2,"object_ids":[1],"amount":1,"unit_id":83,"sequence":3579}` | treating `object_ids` as created-unit identity | AiByz runtime passes directly inspected replay/parser behavior | VERIFIED-RUNTIME | AiByz Runtime Controlled Observability Pass 16; Runtime Production Lifecycle Pass 15 | OBSERVE | Records queue command and producer-side object identity | event record | replay/parser | runtime evidence pipeline | SHARED | AiByz runtime Pass 15/16 | Queue admission observed; produced-object identity not present in the DE_QUEUE payload | none | high | whether another current-DE observation closes queue→created-object identity | 2026-09 | VERIFIED |
| ABI-TIMER-001 | TIMER | `enable-timer` / `timer-triggered` | timer state interface | `(enable-timer <id> <duration>)`; `(timer-triggered <id>)` | timer ID + duration | 2 write / 1 read | `(enable-timer 1 60)`; `(timer-triggered 1)` | malformed ID/duration | Current community `.per` examples and AiByz-derived material show timer initialization and trigger patterns; exact unit/time semantics remain unclosed | VERIFIED-CORPUS | Community `.per` examples; AiByz research corpus | READ-WRITE | Creates/enables and tests timer state | timer-gated | timer writers | timer predicates | ENGINE | NONE | NONE | Exact duration unit and trigger evaluation timing need current-DE closure | high for interface; medium for timing | time unit; retrigger semantics; same-pass trigger visibility; disable behavior | 2026-09 | OPEN |
| ABI-LOAD-001 | LOAD | `.per` module loading | loader mechanism | `.ai`/loader-dependent include/load mechanism | file/module reference | UNKNOWN | existing modular AI source | NOT TESTED | AiByz corpus explicitly treats loader chain and load order as executable behavior; 2024 official DE notes also state the editor can load AIs from all file locations | VERIFIED-CORPUS | AiByz source corpus; official AoE2DE Update 107882 | LOAD | Determines which rules/symbols become active | load-time | loader | loaded modules | ENGINE | NONE | NONE | Exact target `.ai`/`.per` resolution order, duplicate loading, conditional loading, missing-file behavior and symbol visibility are not closed | high for importance; medium for exact mechanism | authoritative loader graph; duplicate module behavior; error handling; `.ai` boundary | 2026-09 | OPEN |
| ABI-OBS-001 | OBSERVATION | replay `SYNC` aggregate state | runtime observation | normalized SYNC payload | current time, resource totals, aggregate object counts | observed fixed shape | `current_time`, `total_res`, `dp_obj_count`, `dp_obj_ttl`, `obj_count` | treating aggregate counts as object identity | AiByz runtime observability pass directly inspected rich SYNC records | VERIFIED-RUNTIME | AiByz Runtime Controlled Observability Pass 16 | READ | Provides aggregate corroboration only | event/observation | replay parser | diagnostics/research | SHARED | Pass 16 | Aggregate counts observed; no normalized per-object production lineage | none | high | current-DE richer object-state source; whether any other replay operation closes identity | 2026-09 | VERIFIED |
| ABI-ERR-001 | ERROR | parser/runtime error behavior | error contract | UNKNOWN | UNKNOWN | UNKNOWN | NOT TESTED | NOT TESTED | AiByz source corpus repeatedly flags parser/error behavior as a required ABI question but does not close it here | UNKNOWN | AiByz PER engine contract/source corpus doctrine | UNKNOWN | UNKNOWN | UNKNOWN | UNKNOWN | unknown | ENGINE | NONE | NONE | Do not invent failure semantics from successful examples | high that it is unresolved | syntax error behavior; missing symbol; duplicate declaration; invalid operand; load failure; recovery behavior | 2026-09 | OPEN |

## 6. What is now filled

The combination of the AiByz research corpus and public AoE2DE release notes closes a useful first layer:

- `.per` rule structure and common rule lifetime patterns are established as source-level contracts.
- Goals are established as persistent state channels with explicit read/write forms, while exact registry/range/timing semantics remain open.
- Strategic numbers are established as a major engine control interface; official release notes confirm that the supported SN surface has changed across DE versions, including an expansion from 303 to 511 in Update 42848.
- `can-build` versus `build`, and `can-train` versus `train`, are explicitly separated.
- Timer interfaces are established at the source-pattern level.
- The runtime evidence boundary around production is unusually strong: `DE_QUEUE` proves command admission but does not prove creation, completion, or object identity.
- Rich replay `SYNC` data is established as aggregate evidence, not an object ledger.
- Loader behavior is identified as ABI-critical but not yet closed.
- Several previously observed tokens (`sn-current-age`, `fc-transit`, `ci-transit`) remain deliberately UNKNOWN rather than being promoted from usage to semantics.

## 7. What cannot yet be filled responsibly

The following require the target installation or a controlled current-DE test before architecture is allowed to depend on them:

1. complete current-DE fact/action registry;
2. exact goal registry, ranges, defaults, and comparison semantics;
3. complete strategic-number registry with per-SN type/range/default/side effects;
4. rule evaluation order and same-pass visibility;
5. action ordering within a rule;
6. timer duration units and trigger timing;
7. `.ai` to `.per` loader graph and conditional loading semantics;
8. duplicate symbol/load behavior;
9. parser error and recovery behavior;
10. construction start/completion/cancellation observability;
11. production queue/resource reservation/completion semantics;
12. research queue/completion semantics;
13. escrow reservation/release semantics;
14. object/unit/building/technology ID authority for the target build;
15. current-DE semantics for `sn-current-age`, `fc-transit`, and `ci-transit`.

## 8. Research priority

Populate the next rows in this order:

`RULE GRAMMAR → FACTS → ACTIONS → RULE LIFETIME → GOALS → TIMERS → STRATEGIC NUMBERS → CONSTANTS/OPERATORS → OBJECT/UNIT/BUILDING IDs → TECH IDs → RESOURCES → PRODUCTION/CONSTRUCTION/RESEARCH → MILITARY/TASK → ESCROW → LOADER → DEBUG/ERRORS`

No production AI architecture should claim these interfaces closed until the matrix says so.

## 9. External references

Primary online authority used for engine-change claims:

- Age of Empires II: Definitive Edition Update 42848 — scripting changes, strategic-number capacity expansion, `up-can-build` correction, and other AI scripting behavior.
- Age of Empires II: Definitive Edition Update 107882 — AI scripting/editor loading changes.
- Age of Empires II: Definitive Edition Update 153015 — later AI scripting changes and current-era scripting behavior.

Community `.per` sources are used only as syntax/pattern corroboration, not as authoritative current-DE semantics.

## 10. Gate

**ENGINE_ABI_MATRIX_v0.1 is not complete.** It is useful enough to prevent several common architecture mistakes, but not complete enough to authorize a full Stock-Ai engine abstraction.

The next hard gate is a frozen current-DE corpus followed by targeted runtime tests for the unresolved execution semantics. Until then, UNKNOWN stays UNKNOWN.
