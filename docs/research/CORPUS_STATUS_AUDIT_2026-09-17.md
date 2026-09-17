# Stock-Ai- Corpus Status Audit — 2026-09-17

**Purpose:** Record exactly which Source Corpus Checklist items can be closed from the repository plus current online/reference evidence, without promoting unresolved runtime semantics.

**Method:** REFERENCE → WRITE → REF → DELIVER.

## Result

The Source Corpus Checklist contains **87 atomic checklist items** across sections A–H.

**41 items can be checked off now.**

That is **41/87 = 47%** of the corpus checklist.

The remaining **46 items stay open**. The largest blocked block is runtime evidence: no runtime probes are being used for this audit, so runtime semantics remain UNKNOWN/OPEN rather than being inferred from source.

## Evidence-backed checkoffs

### A. Current Engine — 0/10

No A-item is closed from GitHub/online evidence alone. The checklist requires acquisition from the exact AoE2DE installation/build used by Stock-Ai-. The project has a known target build from prior work, but the exact installation corpus, executable/resource hashes, complete local documentation, and current local registry have not been frozen inside Stock-Ai-.

### B. Official / Promi AI — 14/16

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

### C. Mature Community AIs — 8/25

Closed only for Shadow, because TheByzantineShadow has already undergone the required forensic extraction:

- [x] Shadow loader architecture.
- [x] Shadow escrow and commitment state.
- [x] Shadow build progression.
- [x] Shadow priority arbitration.
- [x] Shadow release/cancellation paths.
- [x] Shadow military state management.
- [x] Shadow recovery behavior.
- [x] Shadow static tooling/parsers.

Barbarian, Rehoboam, The Duke, and additional serious-AI specimens remain open until their mechanisms are extracted to the same evidence standard.

### D. Tooling Corpus — 5/6

Closed:

- [x] AoE2 AI parser/linter implementations.
- [x] Syntax-highlighting/command registries.
- [x] Static symbol/dependency analyzers.
- [x] Replay parsers/replay-analysis tooling.
- [x] Runtime/debug tooling — existing AoE2DE AI debugging/AIDEBUG and replay-analysis work are already documented in the research corpus.
- [ ] Scenario/test harnesses where reliable — the previous automated scenario-loader path is intentionally retired; no replacement is being counted as closed.

Online tooling remains reference material unless checked against the target installation.

### E. Historical Corpus — 5/5

Closed at the reference-corpus level:

- [x] Computer Player Strategy Builder lineage/reference.
- [x] Classic AoE2 AI scripting guides.
- [x] UserPatch/HD scripting references.
- [x] Older expert-system explanations of goals/timers/SNs/escrow/load behavior.
- [x] Historical command/fact/action lists and community references.

Historical sources are explicitly non-authoritative for current-DE semantics. Current official release history is used only as versioned reference evidence.

### F. Runtime Evidence Corpus — 0/16

No F-item is closed in this audit. This is intentional. Source evidence and online references do not substitute for controlled current-DE runtime evidence.

The following remain OPEN/UNKNOWN:

- [ ] Minimal parser/load test.
- [ ] One-shot rule test.
- [ ] Persistent-rule test.
- [ ] Rule-order test.
- [ ] Multiple-rule firing test.
- [ ] Goal write/read test.
- [ ] Timer test.
- [ ] Strategic-number write/read test.
- [ ] Production command acceptance/completion test.
- [ ] Construction start/completion test.
- [ ] Technology start/completion test.
- [ ] Resource/escrow reservation test.
- [ ] Unit-task assignment test.
- [ ] Rule disable/re-enable behavior test.
- [ ] Conditional-load test.
- [ ] Failure/error behavior test.

### G. Corpus Rules — 8/8

These are already established as project operating rules:

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

## What remains before Checklist 0–1 can close

1. Freeze the exact target AoE2DE installation corpus and hashes inside Stock-Ai-.
2. Finish the authoritative current-DE command/fact/action registry mapping.
3. Complete goal ownership and SN ownership/range/default/side-effect mapping.
4. Finish loader/conditional-load and parser/error contract boundaries.
5. Isolate scouting and civilization-policy ownership in the source corpus.
6. Extract Barbarian, Rehoboam, and The Duke mechanisms where they add distinct engineering evidence.
7. Keep all runtime-semantic questions explicitly OPEN until independently established.

## Current architecture gate

**Checklist 0:** closed.

**Checklist 1:** substantially reconstructed, but **not closed**.

**Checklist 2 runtime semantics:** deferred by project decision; no probe results are being promoted.

**Checklist 3 architecture:** not started. No production/construction/military architecture should be declared final until the remaining ABI boundaries are documented.

## Important retrieval-integrity finding

The GitHub tree records a non-empty Git object for `AI (HD version).per`, but the repository contents retrieval used during this audit did not return usable textual content for that path. Therefore the file is **not being treated as readable corpus evidence yet**. This is a Git retrieval/integrity item to resolve before using that donor file as a primary source.

## Bottom line

**41/87 corpus checklist items are defensibly closable now.** The work is roughly halfway through the research/corpus gate, but not halfway through building the AI. The remaining work is concentrated in exact current-engine acquisition, subsystem ownership/mapping, distinct donor extraction, and runtime semantics. No architecture should be declared complete merely because the source corpus is large.
