# Stock-Ai- Source Corpus Checklist v0.1

**Purpose:** Freeze the evidence we need before designing the AI architecture. The corpus is organized by authority, not by convenience.

## A. Current Engine — Mandatory

**Authority: DIRECT / highest priority**

Acquire from the exact AoE2DE installation/build used for Stock-Ai-:

- [ ] AI directory and all stock/Promi `.per` entry and loader files.
- [ ] Any `.ai` personality/registration files relevant to custom AI loading.
- [ ] Current DE AI documentation under the installation's documentation tree.
- [ ] Complete current fact/action reference available with the installation.
- [ ] Strategic-number registry and documentation.
- [ ] Goal and timer documentation.
- [ ] Escrow documentation.
- [ ] Building/unit/technology/object identifier references.
- [ ] Conditional-loading documentation.
- [ ] Parser/error behavior documentation.
- [ ] Exact game build number and executable/resource hashes.

**Why:** this is the only corpus allowed to define the project's current engine ABI without qualification.

## B. Official / Promi AI — Primary Reference

**Authority: REFERENCE, promoted to DIRECT only when the material is verified against the current installation**

Inventory the complete stock/Promi system, not selected interesting files:

- [x] Main loader chain.
- [x] Constants and shared symbols.
- [x] General state/control logic.
- [x] Economy and worker management.
- [x] Construction/building logic.
- [x] Technology/research logic.
- [x] Production logic.
- [ ] Scouting.
- [x] Military behavior.
- [x] Attack/defense state handling.
- [x] Strategic-number writers.
- [x] Goal writers.
- [x] Timer writers.
- [x] Escrow/reservation logic.
- [ ] Civilization-specific policy.
- [x] Conditional-load branches.

For every subsystem, record **inputs, outputs, writers, dependencies, load order, release paths, and observed purpose**.

## C. Mature Community AIs — Mechanism Corpus

Study strong implementations as engineering specimens. Do not copy architecture merely because it is large.

### Shadow

- [x] Loader architecture.
- [x] Escrow and commitment state.
- [x] Build progression.
- [x] Priority arbitration.
- [x] Release/cancellation paths.
- [x] Military state management.
- [x] Recovery behavior.
- [x] Static tooling/parsers.

### Barbarian

- [x] Economy control.
- [x] Build-order abstraction.
- [x] Production/composition logic.
- [x] Military planning.
- [x] Strategic-number usage.
- [x] Conditional/civilization behavior.

### Rehoboam

- [ ] Strategic planning.
- [ ] Economy transitions.
- [ ] Production arbitration.
- [ ] Scouting/intelligence.
- [ ] Military decision logic.

**Rehoboam evidence status:** public community references establish that Rehoboam is a serious custom AI, but no trustworthy public AoE2 `.per` source corpus was located in this audit. No Rehoboam mechanism row is promoted without primary source evidence.

### The Duke

- [x] Economy and construction mechanisms.
- [x] Military organization.
- [x] Reusable rule abstractions.
- [ ] Failure/recovery behavior.

### Other serious AIs

Add only implementations that provide a distinct mechanism or useful counterexample. Do not collect projects for the sake of collecting projects.

## D. Tooling Corpus

The AI itself is only half the engineering problem. We also need tools that can tell us when the script is lying.

- [x] AoE2 AI parser/linter implementations.
- [x] Syntax-highlighting/command registries.
- [x] Static symbol/dependency analyzers.
- [x] Replay parsers and replay-analysis tooling.
- [x] Runtime/debug tooling.
- [ ] Scenario/test harnesses where reliable.
- [ ] Existing AI development libraries that expose engine facts/actions.

The public AoE2 AI parser ecosystem is useful for identifying command families and syntax, but its registries remain reference material until checked against the current DE installation.

## E. Historical Corpus

Historical documentation is useful for understanding semantics that the modern documentation may not explain well:

- [x] Computer Player Strategy Builder documentation.
- [x] Classic AoE2 AI scripting guides.
- [x] UserPatch/HD scripting references.
- [x] Older expert-system explanations.
- [x] Historical command/fact/action lists.

These sources explain lineage and can expose concepts such as rule lifetime, facts/actions, strategic numbers, goals, timers, escrow, and conditional loading. They are **not** sufficient evidence for current-DE behavior by themselves.

## F. Runtime Evidence Corpus

Source inspection alone is not enough. Build a controlled evidence set.

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
- [ ] Rule disable/re-enable behavior test where applicable.
- [ ] Conditional-load test.
- [ ] Failure/error behavior test.

Every runtime result gets the exact game build, script revision, test setup, timestamp, replay/save artifact where applicable, and a narrow conclusion.

## G. Corpus Rules

1. **Freeze before interpretation.** Record hashes and versions before changing or normalizing source files.
2. **Preserve originals.** Never edit donor material in place.
3. **Separate source from interpretation.** Notes are not source.
4. **Track provenance.** Every important claim must point to a file, section, rule, runtime test, or external reference.
5. **Do not promote by repetition.** Ten community scripts repeating the same claim do not make it current-DE truth.
6. **Prefer complete subsystems.** A single interesting rule without its writers, callers, loaders, and release paths is weak evidence.
7. **Capture negative evidence.** Failed tests and unsupported assumptions are valuable corpus entries.
8. **Record version boundaries.** A behavior observed in an older engine must not be presented as current behavior without verification.

## H. First Deliverable From This Corpus

The corpus phase produces one compact artifact before architecture begins:

**`ENGINE_ABI_MATRIX_v0.1`**

Columns:

```text
Symbol / Mechanism
Type
Current-DE Evidence
Source
Read/Write Role
Side Effects
Lifetime
Known Writers
Known Consumers
Runtime Verification
Confidence
Open Questions
```

That matrix becomes the gate between research and architecture.

## Exit Condition

Checklist 0–1 is complete when:

- the exact current engine/source baseline is frozen;
- the loader and module graph are known;
- the `.per` command surface is catalogued;
- state mechanisms and their ownership risks are mapped;
- the major stock/Promi subsystems are inventoried;
- mature-AI mechanisms have been extracted without treating donors as authority;
- the first runtime semantics tests exist;
- unresolved engine questions are explicitly listed.

Only then do we design the Stock-Ai architecture.
