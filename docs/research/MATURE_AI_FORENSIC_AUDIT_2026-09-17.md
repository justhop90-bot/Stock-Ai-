# Mature AI Forensic Audit — Barbarian, Rehoboam, The Duke

**Date:** 2026-09-17
**Project:** Stock-Ai-
**Method:** REFERENCE → WRITE → REF → DELIVER
**Purpose:** Extract mechanism-level evidence from Barbarian, Rehoboam, and The Duke without promoting donor behavior to current-DE engine authority.

## Evidence rule

These are donor implementations. They are useful for mechanism extraction only. Current-DE runtime semantics remain governed by the Stock-Ai engine ABI and runtime evidence gates. Public claims about strength or compatibility are contextual evidence, not proof of implementation semantics.

## 1. Barbarian 2.18

### Corpus identity

A public GitHub mirror preserves `Barbarian 2.18/Barbarian.per` as a 1,877,137-byte monolithic file with blob SHA `558f20088fa02e5d4d29adbd48fc33786bccb957`. The same tree contains a substantial modular `Barbarian/` directory, including strategy and subsystem files. The monolithic file was too large for the GitHub text fetch endpoint used in this audit, so mechanism extraction below relies on the readable modular corpus and indexed source excerpts rather than pretending the monolith was fully read.

### Economy control — CHECKED

The corpus contains explicit resource/escrow control tied to strategy transitions. Examples include `WallAndBoom.per`, `WarGalleys.per`, `Castles.per`, `MayanEagleRush.per`, `DeathMatch.per`, `AztecSuperRush.per`, and `MonksAndTrebs.per`. The rules set escrow percentages, release escrow, and change spending permissions around research and strategic commitments. This is direct donor-source evidence of deliberate resource reservation/release behavior.

### Build-order abstraction — CHECKED

The strategy corpus is organized into named build/strategy modules rather than one undifferentiated controller. Indexed examples include `FC3.per`, `FC16.per`, `MUSH.per`, `WALLS.per`, `MONGOLBOOM.per`, `EternalDrush.per`, `SuicidalKnightRush.per`, `Turtles.per`, `WarGalleys.per`, and other strategy-specific modules. Rules select strategy states using explicit goals and then gate subsequent behavior with age, time, building, unit, map, and civilization predicates.

### Production/composition logic — CHECKED

Production decisions are tied to strategic state and observed composition. Examples include unit-count predicates, `can-train`, unique-unit conditions, siege thresholds, and opponent composition checks. `MONGOLBOOM.per`, `SuicidalKnightRush.per`, `Castles.per`, and `WarGalleys.per` provide readable evidence that production/composition is conditional rather than a single fixed queue.

### Military planning — CHECKED

The corpus contains specialized offensive and defensive strategies, including raid/camp pressure, rushes, castle drops, wonder assault, monk/trebuchet handling, siege and cavalry plans, and strategy-specific composition gates. `EternalDrush.per` and `WonderAssault.per` demonstrate explicit timing, force-count, building-count, and enemy-state predicates; `Castles.per` includes enemy siege and monk-related conditions.

### Strategic-number usage — CHECKED

The donor uses strategic-number writes as part of strategy control. `WarGalleys.per` changes `sn-percent-enemy-sighted-response`; other readable donor material sets attack-group and military-control numbers. This establishes that SNs are used as a strategy/execution control surface in the donor, not merely as passive configuration.

### Conditional/civilization behavior — CHECKED

The corpus makes extensive use of `#load-if-defined` / `#load-if-not-defined` around civilization, map, difficulty, and mode conditions. Readable examples include `FC16.per`, `MUSH.per`, `WALLS.per`, `RaidTheCamps.per`, `HardestCheats.per`, and `UnusualSwitch.per`. Civilization-specific and map-specific strategy modules are therefore an explicit architectural mechanism in Barbarian.

### Additional forensic finding

Barbarian's architecture is heavily strategy-module driven. Strategy selection is represented in goals such as `gl-strategy`, with strategy modules imposing local economic, production, technology, and military consequences. The corpus also contains explicit difficulty-specific cheating logic (`HardestCheats.per`). Public community material independently describes Barbarian 2.18 as a build-order/strategy based AI and notes that the DE adaptation was not updated for newer civilizations; this contextual evidence is consistent with the source structure but does not establish current-DE correctness.

## 2. The Duke

### Corpus identity

The public repository `tim-kos/the_duke_ai` has 323 commits, default branch `master`, and a `Genero per` codebase. The main `the_duke_ai.per` explicitly loads a modular library including constants, buildings, diplomacy, resign, cheating, commodity, target-player selection, defense, late-game, attack, rush, age advancement, technologies, unique technologies, blacksmith technologies, wonder, unit combinations, military parity, military, counter units, resource control, and villager training. The source is therefore readable as a genuine modular controller rather than a single flat script.

### Economy and construction mechanisms — CHECKED

The main loader explicitly includes `buildings`, `commodity`, `resource_control`, and `training_villagers`. The startup code initializes economic/build-state goals, and the dedicated training module changes villager-training state and escrow percentage. The loader also separates age advancement, technologies, construction, military, and economic control into named modules.

### Military organization — CHECKED

The loader separates `attack`, `defense`, `military_parity`, `military`, and `counter_units`. Indexed source evidence shows explicit attack personality, military-parity states, counter-unit handling, target-player selection, wonder assault, and attack-state goals. The military system is therefore organized around multiple cooperating control modules rather than a single generic attack rule set.

### Reusable rule abstractions — CHECKED

The Duke uses a library structure with named modules and a consistent state-goal convention. The main controller initializes state with one-shot rules using `disable-self`; modules communicate through named goals such as `RUSH-CONTROL`, `ATTACK-PERSONALITY`, `MILITARY-PARITY`, `TRAIN-VILLAGERS`, `WONDER-ATTEMPT`, and research/upgrade state goals. Conditional compilation is used for map, civilization, difficulty, victory-mode, and wonder-mode behavior.

### Failure/recovery behavior — OPEN

The corpus contains resignation, late-game, defense, and state-control modules, but this audit did not find enough explicit recovery semantics to close the checklist item at the same forensic standard as Shadow's documented recovery system. In particular, no direct source evidence was established for a general failed-action recovery protocol with pending-state detection, retry arbitration, and resource/state release. Keep this item open.

### Additional forensic finding

The Duke exposes a useful pattern for Stock-Ai: a relatively clean module boundary with a central loader, named state goals, explicit one-shot initialization, conditional module inclusion, and separate strategic/military modules. Its source also demonstrates user/ally command hooks through taunts, including commands that change attack, villager production, navy behavior, resource transfer, and unit-composition preferences. Those interfaces are donor-specific and should not be copied as architecture without need.

## 3. Rehoboam

### Source acquisition status — NOT CHECKED OFF

Public web and GitHub searches found community references identifying Rehoboam as a serious AoE2 AI, including historical AI-ladder discussion and current custom-AI references. However, the searches did not locate a trustworthy public repository containing the actual Rehoboam `.per` source corpus. GitHub repository-name searches produced unrelated software projects rather than an AoE2 Rehoboam source repository, and GitHub code search did not return a `Rehoboam.per` source file.

Therefore none of the five Rehoboam mechanism checklist items is checked off. Community descriptions such as Rehoboam being particularly strong in certain settings are retained only as contextual evidence. They do not substitute for source extraction.

### What remains needed

A preserved Rehoboam source archive, readable `.per` corpus, or equivalent primary source is required before checking strategic planning, economy transitions, production arbitration, scouting/intelligence, or military decision logic.

## 4. Current mature-AI checklist effect

### Shadow

Previously checked: 8/8.

### Barbarian

Checked now: 6/6.

### Rehoboam

Checked now: 0/5.

### The Duke

Checked now: 3/4.

### Mature-AI subtotal

**17/25 mechanism items checked.**

The remaining eight are: all five Rehoboam items, The Duke failure/recovery, and the two reserved slots under Other serious AIs. This preserves the original 25-item C-section accounting rather than inventing new checklist rows.

## 5. Architectural takeaways for Stock-Ai

Barbarian contributes strong evidence for strategy-as-state, modular build-order selection, composition gates, civilization/map specialization, and explicit escrow/resource transitions. The Duke contributes a clean central-loader/module graph, named goal-state interfaces, separated attack/defense/parity/counter modules, and reusable one-shot initialization patterns. Rehoboam currently contributes only external performance/context evidence, not source-level mechanism evidence. None of these donors changes the current-DE ABI, proves runtime semantics, or authorizes direct copying.

## 6. Evidence boundary

No runtime claim is promoted by this audit. In particular, source use of goals, strategic numbers, escrow, `disable-self`, conditional loading, or production commands does not establish their exact current-DE pass timing, visibility, completion semantics, or failure semantics. Those remain governed by the Stock-Ai runtime-semantic gate.

## Acceptance

**Barbarian:** forensic mechanism extraction sufficient to close all six checklist rows.

**The Duke:** forensic mechanism extraction sufficient to close three of four checklist rows; recovery remains open.

**Rehoboam:** source acquisition failure; zero mechanism rows closed.

**Overall mature-AI corpus:** 17/25 closed.
