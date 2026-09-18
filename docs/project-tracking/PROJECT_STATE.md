# Stock-Ai- Project Tracking

## Project identity
- Repository: justhop90-bot/Stock-Ai-
- Default branch: main
- Purpose: forensic reconstruction of the AoE2DE stock AI followed by design of a new stock-grade AI.
- Muse = primary engineering/reconstruction agent; ChatGPT = QC and architectural review.
- Implementation gate: NO NEW AI IMPLEMENTATION until Stage A and Stage B pass QC.

## Stage A — Stock forensic reconstruction
Reconstruct the actual reachable stock AI graph before designing the replacement architecture.

Primary evidence:
- AoE2DE installed /ai corpus.
- AI source stock monolith.
- Naga mature modular AI.
- Promisory.
- Shadow DC7 / Shadow source as mature-AI research.
- empires2_x2_p1.dat.
- civilizations.json.
- airef engine/reference material.

Every logical module is documented with:
1. identity
2. purpose
3. responsibilities
4. inputs
5. outputs
6. state ownership
7. writers/consumers
8. authority
9. engine primitives
10. dependencies
11. dependents
12. failure/recovery
13. reassessment
14. architectural rationale, separating source fact from inference
15. evidence class

Required role distinctions:
- FILE
- LOGICAL MODULE
- STATE OWNER
- WRITER
- CONTROLLER
- CONSUMER
- EXECUTOR
- VERIFIER

Dependency classes:
- D1 definition
- D2 initialization
- D3 read
- D4 write
- D5 ordering
- D6 engine-state
- D7 optional
- D8 recovery

## State-lifecycle matrix
Mandatory for strategic state, goals, strategic numbers, timers, escrow, pending-object state, technology commitments, scouting state, threat state, military demand, and recovery state.

Required lifecycle fields:
STATE | CREATED BY | INIT | WRITERS | CONTROLLING PREDICATES | CONSUMERS | ENGINE CONSEQUENCE | VERIFICATION | INVALIDATION | RELEASE/RESET | REASSESSMENT | OWNER | EVIDENCE

## Escrow forensic track
Escrow is reconstructed independently from general economy logic.

Required lifecycle:
intent -> reservation -> increment -> dependency reservation -> protected amount -> spending -> verification -> partial release -> full release -> invalidation -> emergency override -> recovery

Evidence must distinguish:
- PROVEN stock behavior
- PROVEN-ENGINE semantics
- INFERRED strategic interpretation
- OPEN runtime questions

## Current QC status
- initialization.per: Forensic Pass 1 accepted; architectural boundary NOT accepted.
- initialization.per ownership vs writer/controller distinctions remain under review.
- Stage A load-graph reconstruction: IN PROGRESS
- Stage A state matrices: IN PROGRESS
- Stage B boundary synthesis: BLOCKED until Stage A completion
- Empty new /ai architecture scaffold: NOT YET CREATED
- Module implementation: BLOCKED

## Current next forensic target
### hunting.per
Required analysis:
- 15-field forensic record
- D1-D8 dependency classification
- state-lifecycle matrix
- resource census vs hunt control vs execution separation
- sn-home lifecycle
- livestock/scouting coupling
- boar control
- deer control
- per-TC behavior
- actual executor/verifier boundaries
- hunting/economy/construction/scouting contracts
- adversarial/failure analysis
- provisional logical decomposition
- evidence and falsification conditions

Important hunting state:
- sn-home
- current-livestock-food
- total-livestock-food
- current-boar
- current-deer
- deer-luring
- hunt-count
- livestock-food-counter
- scouting-unit

## Architecture gate
Stage B may only begin after the complete reachable stock graph is reconstructed.

The new architecture must NOT:
- copy Naga's file layout
- copy Shadow's file layout
- reproduce the stock monolith mechanically
- assume one physical file equals one logical module
- promote inferred designer intent to proven fact
- treat command acceptance as world-state completion
- simplify stock behavior before its purpose is understood

Stage B must derive logical module boundaries from:
responsibilities + state ownership + contracts + engine behavior + dependency structure + failure/recovery + maintainability

## Future scaffold gate
After Stage B QC approval:
1. Create empty module directories under the new project's /ai.
2. Add contract/workflow documentation only.
3. No implementation yet.
4. Create a module-specific professional engineering workflow for every approved logical module.
5. Begin implementation only after each module's workflow and contract pass QC.

Common workflow phases:
0. Evidence Lock
1. Boundary Lock
2. Contract Definition
3. State Model
4. Rule-Family Design
5. Priority/Ordering Analysis
6. Engine ABI Audit
7. Normal-Path Implementation
8. Dependency Implementation
9. Failure/Recovery Implementation
10. Reassessment
11. Adversarial Review
12. Static Verification
13. Behavioral Verification
14. Cross-Module Verification
15. Regression Verification
16. QC Acceptance

## QC principle
A module is not architecturally accepted until we can explain:
- why it exists
- what responsibility it owns
- what state it owns
- who writes the state
- who consumes it
- what contract it provides
- what engine behavior it invokes
- what dependencies must exist
- how failure is detected
- how resources/state are recovered
- what causes reassessment
- what evidence supports each conclusion

First effort is a hypothesis. Second-pass analysis establishes architecture.
