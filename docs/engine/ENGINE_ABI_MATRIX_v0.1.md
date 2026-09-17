# ENGINE_ABI_MATRIX_v0.1

**Project:** Stock-Ai-
**Scope:** AoE2DE `.per` engine contract
**Status:** Sprint 0 — corpus-backed ABI reconstruction; Doc1 forensic mapping pass
**Authority rule:** current-DE runtime evidence outranks current-DE corpus evidence; current-DE corpus evidence outranks historical/community material
**Method:** REFERENCE → WRITE → REF → DELIVER

## 1. Purpose

This matrix is the working boundary between the AoE2DE engine and Stock-Ai architecture. It records what the `.per` interface is known to accept, expose, mutate, load, or trigger. It deliberately separates syntax, usage, semantics, and runtime realization. A symbol is not considered understood merely because it appears in a source file.

The matrix is intentionally sparse. It is not a giant command catalogue. Rows are added when they establish an ABI dependency, expose a dangerous semantic assumption, or close an important engine question.

This revision maps claims from `TheByzantineShadow/Doc1-Forensic-Engineering-Reference.txt` into the Stock-Ai evidence model. Doc1 is a forensic source, not an automatic authority: its claims are retained with their provenance and downgraded to `INFERRED` or `UNKNOWN` where the available evidence does not establish the current Stock-Ai target runtime.

## 2. Evidence tiers

Only these tiers are permitted:

- **VERIFIED-CORPUS** — directly established from the preserved AoE2DE/Promisory corpus, Doc1's preserved source/registry evidence, or another source artifact whose exact content is available. This proves presence/usage, not necessarily semantics.
- **VERIFIED-RUNTIME** — directly observed in a controlled current-DE runtime/replay experiment with reproducible build/script/setup evidence.
- **INFERRED** — interpretation supported by multiple observations or source relationships but not directly established by current-DE runtime evidence.
- **UNKNOWN** — insufficient evidence. This is a valid result and must remain explicit.
- **REJECTED** — a specific claim or interpretation was tested or contradicted strongly enough that it must not be used.

Historical/community sources may support provenance, but they do not silently become current-DE authority.

## 3. Evidence rules

1. **Usage ≠ declaration ≠ semantics.** A token appearing in `.per` proves use; it does not prove its complete ABI contract.
2. **Predicate ≠ action.** `can-build` and `build`, `can-train` and `train`, and analogous pairs are separate contracts.
3. **Command acceptance ≠ world-state completion.** The state ladder is `REQUESTED → AUTHORIZED → QUEUED/ISSUED → PENDING → OBSERVED_AVAILABLE → COMMITTED_USE → VERIFIED_EFFECT`.
4. **Negative evidence is first-class.** Absence must be established with the strongest available structural/lexical/runtime search, not by a failed guess.
5. **Conflicts remain visible.** Do not select the convenient interpretation when sources disagree.
6. **Runtime claims require reproducibility.** Record game build, script revision/hash, setup, test ID, observation, and artifact locator.
7. **External references are reference material until checked against the target installation.**
8. **Architecture may not silently depend on UNKNOWN.** An unresolved ABI edge must be isolated behind a guard, adapter, or explicit pending state.
9. **Load order is executable behavior.** A symbol's presence and effective behavior must be evaluated in module/load-order context.
10. **Do not promote replay chronology into object identity without a validated identity edge.**
11. **Doc1 evidence labels do not replace Stock-Ai evidence tiers.** `DIRECT`/`COMPOSED`/`CONFIRMED` from Doc1 are provenance descriptors; the matrix assigns the stricter Stock-Ai tier.
12. **Registry evidence proves interface presence, not complete runtime semantics.**
13. **Forensic failure evidence is ABI evidence.** A documented silent failure is useful even when it does not establish the intended successful contract.
14. **Cross-store prefixes are semantic operands.** `c:`, `g:`, and `s:` must be treated as typed store selectors, not cosmetic syntax.
15. **Jump targets are positional.** Until a current-DE runtime test establishes otherwise, jump regions are architecture hazards and must not be edited casually.

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

## 5. Populated matrix

| CONTRACT_ID | NAMESPACE | SYMBOL / MECHANISM | TYPE | SYNTAX | OPERAND TYPES | CARDINALITY | VALID EXAMPLE | INVALID EXAMPLE | CURRENT-DE EVIDENCE | EVIDENCE TIER | SOURCE | READ/WRITE ROLE | SIDE EFFECTS | LIFETIME | KNOWN WRITERS | KNOWN CONSUMERS | OWNERSHIP | RUNTIME TEST ID | RUNTIME RESULT | CONTRADICTIONS | CONFIDENCE | OPEN QUESTIONS | LAST VERIFIED | STATUS |
|---|---|---|---|---|---|---:|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| ABI-RULE-001 | RULE | `defrule` | rule declaration | `(defrule <facts> => <actions>)` | facts/actions | variadic by grammar | `(defrule (true) => (disable-self))` | malformed/missing `=>` | Repeated corpus usage; Doc1 describes the same rule form and pass model | VERIFIED-CORPUS | Doc1 §2.4, §5.1; AiByz PER contract | DECLARE | Installs a rule into the rule set | persistent unless disabled/gated | rule set | rule engine | ENGINE | NONE | NONE | Exact current-DE evaluation/order semantics remain unclosed | high syntax; medium semantics | exact evaluation order; same-pass visibility; action ordering; re-evaluation timing | 2026-09 | OPEN |
| ABI-RULE-002 | RULE | `disable-self` | rule lifetime action | `(disable-self)` | none | 0 | `(defrule (true) => (disable-self))` | arguments | Doc1 gives direct corpus evidence and explicitly records next-pass disable behavior | VERIFIED-CORPUS | Doc1 §5.2; Shadow DC7 witnesses | WRITE | Disables the firing rule | one-shot; exact engine timing still needs runtime confirmation | initialization rules | rule lifetime | ENGINE | NONE | NONE | Doc1's next-pass claim is corpus/registry evidence, not a Stock-Ai runtime test | high existence/use; medium timing | whether remaining actions execute before disable; same-pass re-fire | 2026-09 | OPEN |
| ABI-RULE-003 | RULE | rule pass ordering | execution semantics | `(defrule ...)` source order | rules | N/A | N/A | treating order as unspecified | Doc1 explicitly states each pass evaluates rules in source order | INFERRED | Doc1 §5.1 | READ | Determines execution ordering | per-pass | all rules | all rules | ENGINE | NONE | NONE | Source-order statement lacks independent current-DE runtime confirmation in Stock-Ai | medium | controlled ordering test with two observable rules | 2026-09 | OPEN |
| ABI-GOAL-001 | GOAL | `goal` storage/read | persistent AI state | `(goal <goal-id> <value>)` | integer goal ID/value | 2 | `(goal 6 1)` | non-integer operands | Doc1 gives direct registry syntax; corpus shows goals used as persistent AI state | VERIFIED-CORPUS | Doc1 §3.2 | READ | Reads goal state | persistent | goal writers | strategic rules | ENGINE | NONE | NONE | Exact current-DE registry/range remains open | high | goal ID registry; range; compare semantics | 2026-09 | OPEN |
| ABI-GOAL-002 | GOAL | `set-goal` | state write action | `(set-goal <goal-id> <value>)` | integer goal ID/value | 2 | `(set-goal 6 1)` | goal/SN expression in value position unless explicitly supported | Doc1 gives registry syntax and a confirmed forensic failure showing a goal-to-goal copy written the constant ID instead of the intended value | VERIFIED-CORPUS | Doc1 §3.2, §4 | WRITE | Mutates goal state | persistent until overwritten/reset | strategic rules | goal predicates/actions | ENGINE | NONE | NONE | Exact same-pass visibility remains unclosed | high syntax; high failure mode; medium timing | value operand typing; write visibility; engine-owned goals | 2026-09 | OPEN |
| ABI-GOAL-003 | GOAL | `up-modify-goal` | goal arithmetic/state action | `(up-modify-goal <goal-id> <math-op> <value>)` | goal ID + operator + `c:`/`g:`/`s:` operand | 3 | `(up-modify-goal bwc-regime g:= bwc-best)` | `g:max` when intending an SN read | Doc1 directly documents syntax and a forensic wrong-store case | VERIFIED-CORPUS | Doc1 §4, §6 | READ-WRITE | Reads selected store and writes goal | persistent | strategic rules | strategic rules | ENGINE | NONE | NONE | Prefix semantics and exact operator set need current-DE confirmation | high syntax/failure; medium full semantics | complete math operator ABI; same-pass visibility; store typing | 2026-09 | OPEN |
| ABI-GOAL-004 | GOAL | `up-compare-goal` | goal comparison | `(up-compare-goal <goal-id> <compare-op> <value>)` | goal ID + comparison op + `c:`/`g:`/`s:` operand | 3 | `(up-compare-goal bwc-t s:>= sn-home-exploration-time)` | malformed store prefix | Doc1 provides direct registry usage, including goal-vs-SN comparison | VERIFIED-CORPUS | Doc1 §3.2, §4 | READ | Compares goal against selected store | query | none | strategic rules | ENGINE | NONE | NONE | Full operator/store typing still requires target-build closure | high syntax; medium semantics | comparison operator registry; type checking; coercion | 2026-09 | OPEN |
| ABI-SN-001 | SN | strategic-number registry | engine control interface | `(strategic-number <sn> <compare-op> <value>)`; `(set-strategic-number <sn> <value>)`; `(up-modify-sn ...)` | SN + operator/value | varies by command | `(set-strategic-number sn-enable-new-building-system 1)` | unknown SN / malformed operand | Official DE release notes plus Doc1 registry/corpus evidence establish a large SN interface; Update 42848 documented expansion of supported capacity | VERIFIED-CORPUS | Doc1 §3.3, §6; Official AoE2DE Update 42848 | READ-WRITE | Changes or tests engine control settings; effects are SN-specific | engine-owned/persistent until changed | many modules | many engine subsystems | ENGINE | NONE | NONE | Registry values and individual SN semantics remain version-bound | high interface; medium individual semantics | complete current registry; type/range/default/effect per SN | 2026-09 | OPEN |
| ABI-SN-002 | SN | `sn-current-age` | strategic number | `(strategic-number sn-current-age ...)` | SN + comparison/value | UNKNOWN | usage exists | write/type assumptions not tested | Prior AiByz ABI work records usage but not a closed declaration/type/semantics contract | UNKNOWN | AiByz prior ABI research | READ | UNKNOWN | UNKNOWN | UNKNOWN | age/strategy rules | ENGINE | NONE | NONE | Doc1 does not close this specific symbol | medium | exact ID; value encoding; writable/read-only; update timing | 2026-09 | OPEN |
| ABI-SN-003 | SN | threat-counter SN reuse | volatile SN state pattern | `(up-modify-sn <sn> ...)` | SN + operator/value | 3 | `(up-modify-sn sn-ranged s:+ sn-archers)` | assuming SN value persists as historical memory | Doc1 directly witnesses zero → census accumulation → roll-up in Naga threat logic | VERIFIED-CORPUS | Doc1 §3.3; Naga `threats.per` witnesses | READ-WRITE | Mutates reused SN slots used as threat counters | per-pass/volatile by corpus pattern | threat census rules | threat/strategy rules | PROJECT/ENGINE SHARED | NONE | NONE | This establishes a source pattern, not a universal engine rule that all SNs are volatile | high pattern; low universalization | which SNs are engine-owned vs safe scratch; cross-pass persistence | 2026-09 | OPEN |
| ABI-STORE-001 | OPERAND | `c:` / `g:` / `s:` prefixes | typed store selector | `c:<constant>`, `g:<goal>`, `s:<sn>` | store-qualified operand | 1 | `(up-modify-goal temporary-goal2 g:= my-mpop)` | `(up-modify-goal bwc-bel-arch g:max sn-ranged)` when `sn-ranged` is intended | Doc1 directly describes prefix semantics and confirmed wrong-store forensic cases | VERIFIED-CORPUS | Doc1 §4 | READ | Selects constant, goal, or SN value source | expression-scoped | source store writers | command operands | ENGINE | NONE | NONE | Exact command-by-command prefix legality remains open | high | complete typed operand matrix | 2026-09 | OPEN |
| ABI-FACT-001 | FACT | `fc-transit` | fact | UNKNOWN | UNKNOWN | UNKNOWN | usage exists in prior corpus | NOT TESTED | Prior AiByz ABI work records usage but could not close declaration/type semantics; Doc1 does not resolve it | UNKNOWN | AiByz prior ABI research | READ | UNKNOWN | UNKNOWN | UNKNOWN | unknown | ENGINE | NONE | NONE | Do not infer type from token name | low | exact syntax, operands, return semantics, current-DE availability | 2026-09 | OPEN |
| ABI-FACT-002 | FACT | `ci-transit` | fact | UNKNOWN | UNKNOWN | UNKNOWN | usage exists in prior corpus | NOT TESTED | Same unresolved state as `fc-transit`; Doc1 does not resolve it | UNKNOWN | AiByz prior ABI research | READ | UNKNOWN | UNKNOWN | UNKNOWN | unknown | ENGINE | NONE | NONE | Do not infer type from token name | low | exact syntax, operands, return semantics, current-DE availability | 2026-09 | OPEN |
| ABI-BUILD-001 | BUILD | `can-build` / `up-can-build` | feasibility predicate | `(can-build <building>)` / `up-can-build ...` | building/object operands | command-specific | `(can-build farm)` | treating predicate as construction command | AiByz distinguishes feasibility from action; official DE update documents `up-can-build` wall behavior fix; Doc1 command-contract section treats command families separately | VERIFIED-CORPUS | AiByz KB; Official Update 42848; Doc1 §6 | READ | Feasibility query only | instantaneous/query | none | construction planner | ENGINE | NONE | NONE | Exact overload/operand forms need registry row-by-row extraction | high role separation; medium exact syntax | full `up-can-build` signature; pending-object semantics; capacity semantics | 2026-09 | OPEN |
| ABI-BUILD-002 | BUILD | `build` | construction action | `(build <building>)` | building identifier | 1 | `(build farm)` | NOT TESTED | Repeated in AiByz/community corpus; command-vs-completion boundary remains explicit | VERIFIED-CORPUS | AiByz KB; community `.per` corpus; Doc1 command-contract section | REQUEST | Requests construction; does not prove completion | pending/world-state lifecycle | construction rules | construction system | ENGINE | NONE | NONE | No current-DE construction completion bridge established | high request role; medium completion | action acceptance; foundation; completion; cancellation | 2026-09 | OPEN |
| ABI-PROD-001 | PRODUCTION | `can-train` | feasibility predicate | `(can-train <unit>)` | unit/unit-line identifier | 1 | `(can-train villager)` | treating it as queue admission | AiByz and community corpus establish the predicate/action split; official DE history documents `can-train`/`train` scripting support | VERIFIED-CORPUS | AiByz KB; Official Update 47820; Doc1 §6 | READ | Training feasibility query | instantaneous/query | none | production planner | ENGINE | NONE | NONE | Exact queue/resource semantics remain open | high role | queue capacity; resource reservation; unit-line semantics | 2026-09 | OPEN |
| ABI-PROD-002 | PRODUCTION | `train` | production action | `(train <unit>)` | unit/unit-line identifier | 1 | `(train villager)` | treating action acceptance as unit completion | AiByz corpus plus runtime queue evidence establish the command/completion distinction | VERIFIED-CORPUS | AiByz KB; Doc1 §6; AiByz runtime production passes | REQUEST | Requests queue work | pending until verified effect | production rules | production system | ENGINE | NONE | NONE | `DE_QUEUE` proves queue admission but not produced-object identity/completion | high | queue capacity, reservation, creation, completion, identity lineage | 2026-09 | OPEN |
| ABI-PROD-003 | PRODUCTION | `DE_QUEUE` replay operation | runtime observation | `[player_id, object_ids, amount, unit_id, sequence]` | player, producer IDs, amount, unit ID, sequence | fixed observed shape | `{"player_id":2,"object_ids":[1],"amount":1,"unit_id":83,"sequence":3579}` | treating `object_ids` as created-unit identity | Direct AiByz replay/parser observation | VERIFIED-RUNTIME | AiByz Runtime Controlled Observability Pass 16; Production Lifecycle Pass 15 | OBSERVE | Records queue admission/producer-side IDs | event | replay parser | diagnostics/research | SHARED | AiByz Pass 15/16 | Queue admission observed; produced-object identity absent from this payload | none | high | what current-DE event closes queue→created-object identity | 2026-09 | VERIFIED |
| ABI-TIMER-001 | TIMER | `enable-timer` / `timer-triggered` | timer interface | `(enable-timer <id> <duration>)`; `(timer-triggered <id>)` | timer ID + duration | 2 write / 1 read | `(enable-timer 7 60)`; `(timer-triggered 7)` | malformed ID/duration | Doc1 gives direct corpus witnesses and timer state values; current-DE runtime timing remains untested in Stock-Ai | VERIFIED-CORPUS | Doc1 §5.3; Naga/Shadow timer witnesses | READ-WRITE | Enables/rearms and tests timers | timer-gated | timer rules | timer predicates | ENGINE | NONE | NONE | Doc1's timer-state semantics are not yet current-DE runtime verified | high interface; medium timing | duration unit; trigger timing; rearm semantics; state transitions | 2026-09 | OPEN |
| ABI-TIMER-002 | TIMER | timer states | timer state constants | `timer-disabled`, `timer-triggered`, `timer-running` | timer state/value | 1 | state comparisons in corpus | treating triggered as permanently running | Doc1 composes Naga defaultConstants evidence into three state values | VERIFIED-CORPUS | Doc1 §5.3; Naga `defaultConstants.per` | READ | Reports timer state | engine-owned | timer engine | timer rules | ENGINE | NONE | NONE | State values need target-build confirmation | medium/high | exact numeric values and transition timing | 2026-09 | OPEN |
| ABI-LOAD-001 | LOAD | `(load "...")` / root loader | module loading | `(load "path/module")` | module path | 1 | `(load "Naga\\defaultConstants")` | missing load target | Doc1 reproduces Naga's 32-line root load graph and identifies load order as executable behavior | VERIFIED-CORPUS | Doc1 §2.2; Naga.per | LOAD | Makes module rules/symbols available according to load order | load-time | root/inner loaders | loaded modules | ENGINE | NONE | NONE | Exact current-DE duplicate-load, resolution, and failure semantics remain open | high | authoritative loader graph; duplicate loads; symbol visibility; error behavior | 2026-09 | OPEN |
| ABI-LOAD-002 | LOAD | inner `(load ...)` | nested loader | `(load "module")` within a module | module path | 1 | Naga initialization inner loads | assuming all loads occur only from root | Doc1 directly cites initialization.per and gatherers.per inner loads | VERIFIED-CORPUS | Doc1 §2.2 | LOAD | Expands dependency graph during load | load-time | modules with inner loads | downstream modules | ENGINE | NONE | NONE | Need current-DE load-order/error experiment | high | whether duplicate/nested load is idempotent; cycle handling | 2026-09 | OPEN |
| ABI-LOAD-003 | LOAD | `#load-if-defined` / `#load-if-not-defined` / `#else` / `#end-if` | conditional compilation | preprocessor directives | symbol predicates | block | `#load-if-defined TINY-MAP ... #end-if` | malformed nesting | Doc1 directly cites Shadow/Naga conditional blocks and validator error classes | VERIFIED-CORPUS | Doc1 §2.3 | LOAD | Selects which code is compiled/loaded | load-time | preprocessor | compiled rule set | ENGINE | NONE | NONE | Exact engine-defined symbol set and target-build nesting limits remain open | high syntax; medium semantics | full symbol registry; nested limit; branch visibility | 2026-09 | OPEN |
| ABI-LOAD-004 | LOAD | preprocessor nesting | structural rule | nested conditional blocks | directives | nested | four nested Naga blocks | assuming every `#else` after `#end-if` is invalid | Doc1 gives a direct nested witness and explicitly warns against shallow nesting repairs | VERIFIED-CORPUS | Doc1 §2.3 | READ | Changes compiled rule set | load-time | preprocessor | loader/compiler | ENGINE | NONE | NONE | Need parser/runtime reproduction on target build | high pattern | nesting depth limit; exact `#else` association | 2026-09 | OPEN |
| ABI-JUMP-001 | CONTROL | `up-jump-rule` | positional control flow | `(up-jump-rule <rule-delta>)` | integer delta | 1 | `(up-jump-rule -2)` | jump target assumption across inserted rules | Doc1 directly witnesses forward, backward, loop, guard-skip, and dispatch patterns | VERIFIED-CORPUS | Doc1 §5.4; Shadow DC7; Naga strategies | CONTROL | Alters next rule evaluation position | per-pass/positional | jump rules | downstream rules | ENGINE | NONE | NONE | Doc1's positional interpretation is not independently runtime-verified in Stock-Ai | high pattern; medium universal semantics | exact delta semantics; disabled-rule counting; cross-preprocessor behavior | 2026-09 | OPEN |
| ABI-JUMP-002 | CONTROL | disabled rules count toward jump positions | jump indexing | implicit | rule count | N/A | Shadow witness | assuming disabled rules disappear from jump count | Doc1 states disabled rules remain counted by jump commands | VERIFIED-CORPUS | Doc1 §5.2 | READ | Affects positional landing | per-pass | rule set | jump rules | ENGINE | NONE | NONE | Requires target-build controlled test before architecture depends on it | medium | exact count semantics after conditional compilation | 2026-09 | OPEN |
| ABI-JUMP-003 | CONTROL | jump retargeting on insertion | positional hazard | N/A | rule layout | N/A | N/A | treating jump targets as symbolic labels | Doc1 records a forensic insertion that changed an `up-jump-rule 3` landing | INFERRED | Doc1 §5.2, §5.4 | READ | Can silently change control flow after edits | source-layout dependent | developers | jump regions | PROJECT | NONE | NONE | The hazard is strongly supported but the full engine model still needs a controlled reproduction | high engineering risk; medium semantic closure | establish exact rule-index model; build-flag interaction | 2026-09 | OPEN |
| ABI-CONST-001 | CONST | `defconst` | named integer constant | `(defconst <name> <value>)` | symbol + integer/string-like constant | 2 | `(defconst min-scout-hp1 12)` | conflicting duplicate definition | Doc1 directly cites registry syntax and a large corpus audit | VERIFIED-CORPUS | Doc1 §3.1 | DECLARE | Binds a symbolic constant | load-time/static | constants modules | all expressions | ENGINE | NONE | NONE | Exact duplicate-definition precedence and current parser behavior need runtime/negative tests | high syntax | duplicate conflict semantics; alias-cycle behavior | 2026-09 | OPEN |
| ABI-CONST-002 | CONST | numeric namespace separation | state-store separation | same integer may name goal and SN | integer IDs | N/A | goal 213 vs SN 213 as distinct stores | assuming numeric equality means same state | Doc1 explicitly states goals and SNs are different engine stores and numeric reuse is normal | VERIFIED-CORPUS | Doc1 §3.1 | READ | Prevents accidental cross-store aliasing | persistent | goal/SN writers | typed operands | ENGINE | NONE | NONE | Current registry namespaces still need exhaustive mapping | high | complete store namespaces and collision rules | 2026-09 | OPEN |
| ABI-ERROR-001 | ERROR | duplicate/missing load diagnostics | validator/error contract | diagnostic codes | file/module identifiers | N/A | `missing-load-target`, `load-cycle`, `duplicate-per-load-target` | ignoring structural errors | Doc1 records validator error classes from a real audited package | VERIFIED-CORPUS | Doc1 §2.3–2.4 | REPORT | Produces diagnostics; exact engine-vs-validator boundary unclear | validation-time | validator | developers | PROJECT/TOOLING | NONE | NONE | Validator diagnostics are not automatically engine runtime errors | high for validator evidence; low for engine semantics | exact native engine errors; recovery behavior | 2026-09 | OPEN |
| ABI-ERROR-002 | ERROR | wrong-store operand mismatch | silent semantic failure | typed operand misuse | store prefix + operand | N/A | N/A | `(up-modify-goal bwc-bel-arch g:max sn-ranged)` when SN value intended | Doc1 records a confirmed forensic failure: `g:max` read goal #213 instead of SN #213 | VERIFIED-CORPUS | Doc1 §4 | READ | Can produce silent wrong-value behavior while remaining structurally valid | rule evaluation | offending rule | dependent rules | ENGINE | NONE | NONE | This is a failure-mode contract, not proof that every wrong prefix is diagnosed | high | exact runtime/static diagnostic coverage | 2026-09 | OPEN |
| ABI-ERROR-003 | ERROR | goal-value constant/goal confusion | silent state corruption | `(set-goal <goal> <value>)` | goal + constant-like value | 2 | use constant value intentionally | `(set-goal bwc-regime bwc-best)` when copying another goal's value | Doc1 records a confirmed forensic case where the destination became constant 3115 rather than the intended goal value | VERIFIED-CORPUS | Doc1 §4 | WRITE | Writes wrong state while remaining syntactically valid | persistent | offending rule | downstream strategy | ENGINE | NONE | NONE | Need controlled current-DE reproduction to determine diagnostic behavior | high failure mode | exact operand typing and whether any runtime warning exists | 2026-09 | OPEN |
| ABI-STATIC-001 | DEBUG | static validity boundary | validator contract | balanced scopes, resolvable loads, known commands | syntax/structure | N/A | clean audited package | assuming clean static validation proves semantic correctness | Doc1 states a 33-file tree passed structural validation while wrong-store reads and incorrect `set-goal` semantics still silently misbehaved | VERIFIED-CORPUS | Doc1 §2.4 | READ | Establishes boundary between static and semantic validation | validation-time | validator | engineering process | PROJECT/TOOLING | NONE | NONE | Validator capabilities are tooling-specific, not native engine guarantees | high | exact Stock-Ai validator coverage; semantic lint rules | 2026-09 | OPEN |
| ABI-OBS-001 | OBSERVATION | replay `SYNC` aggregate state | runtime observation | normalized SYNC payload | time/resources/aggregate object counts | observed fixed shape | aggregate `current_time`/resource/object fields | treating aggregate counts as object identity | AiByz runtime observability pass directly inspected rich SYNC records | VERIFIED-RUNTIME | AiByz Runtime Controlled Observability Pass 16 | READ | Aggregate corroboration only | event/observation | replay parser | diagnostics/research | SHARED | Pass 16 | Aggregate state observed; no normalized per-object production lineage | none | high | current-DE richer object-state source | 2026-09 | VERIFIED |
| ABI-OBS-002 | OBSERVATION | production completion identity | replay/object lineage | UNKNOWN | object identity | UNKNOWN | NONE | treating `DE_QUEUE.object_ids` as produced-object identity | AiByz runtime evidence shows queue admission but not created-object identity; Doc1 does not override that boundary | UNKNOWN | AiByz runtime passes; Doc1 §6 command-contract principle | READ | UNKNOWN | UNKNOWN | UNKNOWN | runtime evidence pipeline | SHARED | NONE | NONE | No current-DE identity bridge established | high uncertainty | identify replay operation or runtime trace that closes creation/completion identity | 2026-09 | OPEN |
| ABI-ABI-001 | META | Doc1 evidence mapping | provenance contract | N/A | N/A | N/A | N/A | treating Doc1 `DIRECT` as runtime proof | Doc1 was generated from live corpus + registry evidence, but the supplied artifact itself does not constitute a controlled Stock-Ai runtime experiment | VERIFIED-CORPUS | TheByzantineShadow `Doc1-Forensic-Engineering-Reference.txt` | READ | Governs evidence promotion | research-time | corpus | matrix | PROJECT | NONE | NONE | None | high | attach exact source offsets/hash for every promoted row | 2026-09 | OPEN |

## 6. Claims deliberately NOT promoted from Doc1

The following remain **UNKNOWN** or **INFERRED** rather than being promoted merely because Doc1 states them:

1. Complete current-DE fact/action registry.
2. Complete current-DE goal registry, defaults, ranges, and comparison semantics.
3. Complete current-DE strategic-number registry with per-SN type, range, default, and side effects.
4. Exact same-pass visibility of goal/SN writes.
5. Exact action ordering within a rule.
6. Exact rule re-evaluation timing.
7. Exact timer duration units and trigger timing.
8. Exact `.ai` → root `.per` resolution and package-loading behavior for the Stock-Ai target installation.
9. Duplicate-load behavior and symbol visibility across nested/conditional loads.
10. Native engine error behavior versus validator/tooling diagnostics.
11. Construction start/completion/cancellation semantics.
12. Production queue reservation/completion/object identity.
13. Research queue/completion semantics.
14. Escrow reservation/release semantics.
15. `sn-current-age`, `fc-transit`, and `ci-transit` full ABI contracts.
16. Universal positional-jump semantics under every preprocessor/build configuration.
17. Any claim that a source-level forensic observation is automatically a current-DE runtime guarantee.

## 7. REJECTED interpretations

No Doc1 claim is rejected merely because it originated in TheByzantineShadow. `REJECTED` is reserved for a specific interpretation that evidence disproves.

Current explicit rejected class:

- **Do not treat replay `DE_QUEUE.object_ids` as created-unit identity.** AiByz runtime evidence contradicts that interpretation: the payload establishes queue/producer-side evidence, not a produced-object identity ledger.

Additional rejected claims should be added only when a controlled test or stronger contradictory evidence exists.

## 8. Doc1 → Stock-Ai promotion rules

| Doc1 source label | Stock-Ai treatment |
|---|---|
| `CONFIRMED` | Usually `VERIFIED-CORPUS`; promote to `VERIFIED-RUNTIME` only when the underlying current-DE controlled experiment is independently reproducible |
| `DIRECT` | `VERIFIED-CORPUS` for exact source/registry presence; semantics remain separate |
| `COMPOSED` | `VERIFIED-CORPUS` when every component source is preserved and the composition is descriptive; otherwise `INFERRED` |
| `INFERRED` | `INFERRED` unless independently demonstrated |
| `AEGIS-GENERALIZATION` | `INFERRED` at most; never treated as native engine terminology |
| `UNCERTAIN` | `UNKNOWN` unless Stock-Ai evidence independently closes the claim |

## 9. Immediate runtime closure targets

The Doc1 mapping changes the test priority. The highest-value controlled tests are now:

1. **Rule ordering:** two adjacent rules with independently observable writes.
2. **Same-pass state visibility:** rule A writes a goal/SN; rule B immediately reads it.
3. **`disable-self` timing:** verify remaining actions, next-pass suppression, and same-cycle behavior.
4. **Store-prefix typing:** intentionally compare `g:` and `s:` reads against distinct values.
5. **Timer state machine:** enable → running → triggered → re-arm, with exact elapsed time.
6. **Load graph:** root load, nested load, duplicate load, missing load, conditional load, and load-cycle behavior.
7. **Jump indexing:** verify disabled-rule counting and insertion retargeting on the target build.
8. **Construction:** request → foundation/pending object → completion → failure/cancellation.
9. **Production:** request → queue admission → resource reservation → unit creation → identity/completion.
10. **Parser/validator boundary:** deliberately malformed and semantically wrong scripts, recording which failures are rejected and which silently pass.

## 10. Current conclusion

Doc1 materially strengthens the Stock-Ai ABI reconstruction, especially around **typed state stores, goals, strategic numbers, rule lifetime, timers, jumps, load graphs, preprocessor behavior, and forensic failure modes**. It does not close the engine ABI by itself.

The correct use is surgical: import the evidence, preserve the source location, retain the uncertainty, and then run targeted current-DE experiments against the highest-risk semantics. The matrix is now substantially more useful for architecture work without pretending that source-level forensic evidence is runtime proof.
