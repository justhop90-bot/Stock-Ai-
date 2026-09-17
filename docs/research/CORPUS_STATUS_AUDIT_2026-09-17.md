# Stock-Ai- Corpus Status Audit — 2026-09-17

**Purpose:** Record exactly which Source Corpus Checklist items can be closed from the repository plus current online/reference evidence, without promoting unresolved runtime semantics.

**Method:** REFERENCE → WRITE → REF → DELIVER.

## Result

The current `SOURCE_CORPUS_CHECKLIST_v0.1.md` contains **90 atomic checklist items** across sections A–H. A prior status note reported 87 because it used stale section cardinalities; this revision reconciles the count against the actual checklist file, including 11 A-items, 17 B-items, and 7 D-items.

**51 items can be checked off now.**

That is **51/90 = 56.7%** of the corpus checklist.

The remaining **39 items stay open**. Runtime evidence remains the largest intentionally blocked block: no runtime probes are being used for this donor audit, so runtime semantics remain UNKNOWN/OPEN rather than being inferred from source.

## Evidence-backed checkoffs

### A. Current Engine — 0/11

No A-item is closed from GitHub/online evidence alone. The checklist requires acquisition from the exact AoE2DE installation/build used by Stock-Ai-. The project has a known target build from prior work, but the exact installation corpus, executable/resource hashes, complete local documentation, and current local registry have not been frozen inside Stock-Ai-.

### B. Official / Promi AI — 15/17

Closed at the **corpus-inventory level**:

- [x] Main loader chain — `Naga.per` enumerates the modular load graph.
- [x] Constants and shared symbols — `Naga/defaultConstants.per`, `customConstants.per`, and related constant files are present.
- [x] General state/control logic — initialization/control material is present.
- [x] Economy and worker management — `gatherers.per` and related economy material are present.
- [x] Construction/building logic — `buildings.per` and `builders.per` are present.
- [x] Technology/research logic — `technologies.per` is present.
- [x] Production logic — production/unit logic is present in the preserved Naga corpus.
- [ ] Scouting — not yet isolated and documented as a complete subsystem.
- [x] Military behavior — `militaryMacro.per` and `militaryMicro.per` are present.
- [x] Attack/defense state handling — military macro/micro corpus contains the relevant control machinery.
- [x] Strategic-number writers — widespread SN writers are present across the corpus.
- [x] Goal writers — goal mutation/use is present across the corpus.
- [x] Timer writers — timer definitions/usage are present in the corpus.
- [x] Escrow/reservation logic — `Naga/escrow.per` is present.
- [ ] Civilization-specific policy — not yet isolated as a complete policy subsystem with ownership/dependency mapping.
- [x] Conditional-load branches — `Naga.per` contains `#load-if-defined` / `#load-if-not-defined` branches.

These are **corpus checkoffs**, not claims that every subsystem's runtime effect has been verified.

### C. Mature Community AIs — 17/25

#### Shadow — 8/8

Previously closed through the TheByzantineShadow forensic corpus.

#### Barbarian — 6/6

The public `darkeclipz/aoe2-ai` mirror preserves Barbarian 2.18 as a 1,877,137-byte `Barbarian.per` plus a readable modular `Barbarian/` corpus. Indexed source excerpts establish:

- [x] Economy control — explicit escrow percentage changes, escrow release, and resource-spending control in strategy/research modules.
- [x] Build-order abstraction — named FC, drush, walls, castle-drop, boom, and civ/map-specific strategy modules select state through goals and gated rules.
- [x] Production/composition logic — unit-count, `can-train`, unique-unit, siege, and enemy-composition predicates drive production choices.
- [x] Military planning — dedicated rush, raid, castle, siege, monk/trebuchet, wonder, and defensive strategy modules exist.
- [x] Strategic-number usage — strategy modules explicitly change military/response SNs.
- [x] Conditional/civilization behavior — extensive `#load-if-defined` / `#load-if-not-defined` branches cover civ, map, difficulty, and mode specialization.

The monolithic Barbarian file itself was too large for the connector's text endpoint during this pass; the six closures rely on the readable modular corpus and indexed excerpts, not an unsupported claim that the monolith was fully read.

#### Rehoboam — 0/5

Public community sources identify Rehoboam as a serious custom AI, but this audit did not locate a trustworthy public AoE2 `.per` source corpus. GitHub repository-name and code searches returned unrelated Rehoboam projects and no usable `Rehoboam.per` donor. Therefore no Rehoboam mechanism row is promoted.

- [ ] Strategic planning.
- [ ] Economy transitions.
- [ ] Production arbitration.
- [ ] Scouting/intelligence.
- [ ] Military decision logic.

#### The Duke — 3/4

The public `tim-kos/the_duke_ai` repository exposes a modular `.per` controller with a central loader and named subsystem files.

- [x] Economy and construction mechanisms — loader and source include `buildings`, `commodity`, `resource_control`, and `training_villagers` modules.
- [x] Military organization — separate `attack`, `defense`, `military_parity`, `military`, `counter_units`, and target-selection modules.
- [x] Reusable rule abstractions — named state goals, modular loading, one-shot `disable-self` initialization, and conditional module inclusion are repeatedly used.
- [ ] Failure/recovery behavior — resignation/defense/late-game code exists, but no sufficiently explicit general failed-action recovery protocol was established.

### D. Tooling Corpus — 5/7

Closed:

- [x] AoE2 AI parser/linter implementations.
- [x] Syntax-highlighting/command registries.
- [x] Static symbol/dependency analyzers.
- [x] Replay parsers/replay-analysis tooling.
- [x] Runtime/debug tooling.
- [ ] Scenario/test harnesses where reliable — the previous automated scenario-loader path is intentionally retired; no replacement is being counted as closed.
- [ ] Existing AI development libraries that expose engine facts/actions — useful public libraries exist, but this is not yet frozen as a Stock-Ai corpus artifact.

### E. Historical Corpus — 5/5

Closed at the reference-corpus level:

- [x] Computer Player Strategy Builder lineage/reference.
- [x] Classic AoE2 AI scripting guides.
- [x] UserPatch/HD scripting references.
- [x] Older expert-system explanations of goals/timers/SNs/escrow/load behavior.
- [x] Historical command/fact/action lists and community references.

### F. Runtime Evidence Corpus — 0/16

No F-item is closed in this audit. Source evidence and online references do not substitute for controlled current-DE runtime evidence.

### G. Corpus Rules — 8/8

- [x] Freeze before interpretation.
- [x] Preserve originals.
- [x] Separate source from interpretation.
- [x] Track provenance.
- [x] Do not promote by repetition.
- [x] Prefer complete subsystems.
- [x] Capture negative evidence.
- [x] Record version boundaries.

### H. First Deliverable — 1/1

- [x] `ENGINE_ABI_MATRIX_v0.1` exists and is populated.

## Current closure math

**A 0 + B 15 + C 17 + D 5 + E 5 + F 0 + G 8 + H 1 = 51 closed.**

**11 + 17 + 25 + 7 + 5 + 16 + 8 + 1 = 90 total.**

Therefore the defensible current corpus position is **51/90 (56.7%)**.

## What remains before Checklist 0–1 can close

1. Freeze the exact target AoE2DE installation corpus and hashes inside Stock-Ai-.
2. Finish the authoritative current-DE command/fact/action registry mapping.
3. Complete goal ownership and SN ownership/range/default/side-effect mapping.
4. Finish loader/conditional-load and parser/error contract boundaries.
5. Isolate scouting and civilization-policy ownership in the source corpus.
6. Acquire a trustworthy Rehoboam source corpus before extracting its mechanisms.
7. Decide whether a distinct AI development library adds enough evidence to close D7.
8. Keep all runtime-semantic questions explicitly OPEN until independently established.

## Current architecture gate

**Checklist 0:** closed.

**Checklist 1:** substantially reconstructed, but **not closed**.

**Checklist 2 runtime semantics:** deferred by project decision; no probe results are being promoted.

**Checklist 3 architecture:** not started. No production/construction/military architecture should be declared final until the remaining ABI boundaries are documented.

## Important retrieval-integrity finding

The GitHub tree records a non-empty Git object for `AI (HD version).per`, but the repository contents retrieval used during the earlier corpus audit did not return usable textual content for that path. Therefore the file is **not** being treated as readable corpus evidence yet. This remains a retrieval-integrity item to resolve before using that donor file as a primary source.

## Bottom line

The mature-AI pass materially advances the corpus: Barbarian is now fully closed at the six-row mechanism level, The Duke is closed on three of four rows, and Rehoboam remains intentionally unpromoted because its actual source was not recovered. The corrected checklist arithmetic puts Stock-Ai at **51 of 90 corpus items closed (56.7%)**, not the earlier 41 of 87 figure. That correction is itself important forensic hygiene: checklist cardinality must come from the actual current checklist, not a stale summary. None of this changes the runtime-semantic gate. Source mechanisms can tell us what a donor tried to make the engine do; they do not prove what the current engine actually did.
