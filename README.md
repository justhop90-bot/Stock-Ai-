# Stock-Ai-

**A professional stock-style AI for Age of Empires II: Definitive Edition.**

Stock-Ai- is a ground-up AI engineering project for AoE2DE. The target is not a clever opening, a pile of build orders, or a large `.per` file that happens to survive a few games. The target is a durable decision system: one that can observe the game, maintain coherent state, choose priorities, issue legal actions, verify outcomes, recover from failure, and remain understandable when something goes wrong.

This repository is the project source of truth. If the code, documentation, a replay, or an assumption disagree, the disagreement gets investigated. It does not get papered over.

## Mission

Build a stock-quality AoE2DE AI with five properties:

- **Correctness:** legal commands, valid predicates, deterministic state transitions, and no dependence on accidental engine behavior.
- **Strategic competence:** economy, technology, military composition, map control, timing, scouting, and adaptation must interact rather than operate as isolated scripts.
- **Robustness:** the AI must survive missed timings, blocked construction, lost units, bad resource states, unexpected pressure, and partial failure.
- **Recoverability:** when a plan fails, the system must detect the failure and select a new legal course instead of continuing to believe the old plan succeeded.
- **Maintainability:** every important mechanism must have a defined owner, evidence basis, interface, and test path.

The standard is professional AI engineering. The bar is deliberately higher than “the game started and the bot built something.”

## Operating Doctrine

This project follows a strict engineering loop:

**REFERENCE → WRITE → REF → DELIVER**

1. **REFERENCE** — establish the engine behavior, source precedent, or observed runtime fact before designing around it.
2. **WRITE** — implement the smallest mechanism that satisfies the verified requirement.
3. **REF** — inspect the resulting code again: symbols, load order, ownership, conflicts, dead paths, parser safety, and interaction with existing systems.
4. **DELIVER** — only then treat the change as an accepted project artifact.

No “I think the engine probably does this.” No copying a rule because it looks useful. No declaring success because a command was issued. AoE2 AI work punishes assumptions, usually at the worst possible time.

## Hard Rules

These rules are binding unless explicitly superseded by a documented project decision.

### 1. Evidence before implementation

Do not invent engine semantics. Prefer evidence in this order:

1. Verified AoE2DE behavior and runtime observation.
2. Official/reference AI source and documented engine conventions.
3. Repeated replay or controlled-test evidence.
4. High-quality community AI implementations used as comparative evidence.
5. Explicitly marked inference.

Unknown behavior stays unknown until resolved. A guess is not an API contract.

### 2. Command issuance is not state confirmation

`train`, `build`, `research`, `attack`, `move`, `repair`, or similar commands prove only that the AI attempted an action. They do not prove that the world changed as intended.

Where practical, important decisions follow:

**OBSERVE → CLASSIFY → WRITE STATE → AUTHORIZE → EXECUTE → VERIFY → REASSESS**

If verification is unavailable, the limitation must be explicit.

### 3. One owner per responsibility

Every persistent goal, state variable, resource reservation, production decision, construction decision, military decision, and recovery mechanism must have a clear owner.

Duplicate writers are bugs until proven otherwise. Hidden arbitration is not architecture.

### 4. No uncontrolled global behavior

Shared state is an interface, not a dumping ground. A subsystem may read another subsystem's contract; it should not silently rewrite another subsystem's authority.

### 5. No magic numbers without provenance

Constants affecting timings, thresholds, distances, resource commitments, production ratios, threat levels, or recovery behavior require a reason. If the value is empirical, say so. If it is inherited, identify the source. If it is provisional, mark it provisional.

### 6. Fail closed

When required state is missing, contradictory, stale, or impossible, do not fabricate certainty. Fall back to a known-safe behavior, release the affected commitment, or defer the decision.

### 7. Recovery is a first-class system

Every significant commitment needs an escape path. A plan that cannot be cancelled, superseded, timed out, or rebuilt is not a robust plan.

### 8. Small changes, measurable consequences

Do not change economy, construction, strategy, and military logic simultaneously and then call the result a test. Isolate mechanisms whenever possible. Know what changed and what evidence supports the conclusion.

### 9. Static and runtime evidence stay separate

A parser check, symbol audit, or source inspection proves static properties. A replay proves observed runtime behavior. Neither is allowed to impersonate the other.

### 10. No paperwork theater

Documentation exists to preserve decisions, evidence, interfaces, and failure modes. It does not exist to make an empty system look mature. Keep artifacts short, dense, current, and useful.

## System Model

The intended control flow is:

```text
WORLD STATE
    ↓
PERCEPTION
    ↓
SITUATION / CLASSIFICATION
    ↓
STRATEGY
    ↓
PRIORITY ARBITRATION
    ↓
ECONOMY / CONSTRUCTION / PRODUCTION / MILITARY
    ↓
EXECUTION
    ↓
VERIFICATION
    ↓
RECOVERY / STATE UPDATE
    └──────────────→ REASSESSMENT
```

The architecture is intentionally closed-loop. The AI should not behave like a script that reaches the end of a build order and hopes the map cooperates.

## Planned Subsystems

The project will be built in controlled slices rather than as one giant script.

| Area | Responsibility |
|---|---|
| Boot / constants | Load order, immutable constants, engine-facing setup |
| State | Shared state contracts, goals, flags, timers, ownership |
| World model | Units, buildings, resources, map facts, enemy observations |
| Economy | Villager allocation, resource priorities, transitions, reserves |
| Construction | Building authorization, placement, progress, replacement, cancellation |
| Strategy | Strategic mode, objectives, timings, technology direction |
| Threat | Enemy classification, pressure, military risk, local danger |
| Production | Unit queues, composition, production priorities, feasibility |
| Military | Army control, attack/defend/retreat, target selection |
| Tactical | Local combat state and short-horizon behavior |
| Recovery | Timeout, failure detection, release, rebuild, fallback |
| Civilization | Byzantine-specific and future civilization-specific policy |
| Map intelligence | Resource geometry, chokepoints, expansion, terrain, scouting |
| Team logic | Allies, shared threats, coordinated objectives |
| Diagnostics | Debug state, telemetry, traceability, failure evidence |

These are responsibilities, not permission to create a hundred files immediately. Architecture comes first; file count comes last.

## Build Sequence

The project checklist is deliberately ordered. Do not skip ahead because a later feature is more interesting.

- [ ] **0 — Engineering foundation:** repository rules, naming, load-order discipline, evidence format, test conventions.
- [ ] **1 — AoE2DE ABI:** establish what the engine exposes, how `.per` interacts with it, and which behaviors are actually verified.
- [ ] **2 — Static validation:** parser safety, duplicate symbols, load-order checks, dependency checks, unreachable/dead-path detection where practical.
- [ ] **3 — State kernel:** define authoritative state and ownership before strategic complexity is added.
- [ ] **4 — Economic kernel:** reliable worker/resource control, reserves, transitions, and resource feasibility.
- [ ] **5 — Construction manager:** authorization, placement, progress, blockage, completion verification, and recovery.
- [ ] **6 — Strategic planner:** strategic modes, objectives, timing windows, and controlled transitions.
- [ ] **7 — Scouting/world model:** persistent enemy and map observations with freshness and confidence.
- [ ] **8 — Threat engine:** convert observations into actionable threat classes without confusing observation with interpretation.
- [ ] **9 — Production manager:** composition demand, queue arbitration, affordability, infrastructure, and release conditions.
- [ ] **10 — Military commander:** army lifecycle, objectives, engagement control, retreat, regrouping, and reassessment.
- [ ] **11 — Recovery engine:** detect failed assumptions and return the AI to a valid operating state.
- [ ] **12 — Civilization layer:** Byzantine identity and civilization-specific strategic policy.
- [ ] **13 — Map intelligence:** terrain, resources, expansion, defensive geometry, and map-dependent adaptation.
- [ ] **14 — Team behavior:** ally-aware strategy and coordinated military/economic decisions.
- [ ] **15 — Competitive validation:** controlled scenarios, ladder-style games, replay analysis, regression suites, and comparative benchmarking.

A checkbox is not evidence of completion. Each item requires an implementation, a verification method, and an acceptance result.

## Professional-AI Research

The project will study strong AoE2 AI implementations as engineering specimens, not as code-shopping catalogs. Relevant references may include the official/Promi ecosystem and serious community AIs such as Shadow, Barbarian, Rehoboam, The Duke, and other mature implementations.

For every borrowed idea, answer four questions:

1. **What problem does it solve?**
2. **What engine behavior does it rely on?**
3. **What are its failure and release paths?**
4. **What belongs in Stock-Ai-, and what does not?**

Mechanisms may be adopted. Assumptions are not adopted automatically. A sophisticated donor implementation can still contain context-specific compromises, obsolete engine knowledge, or architecture that is wrong for this project.

## Testing Standard

Testing progresses through increasingly expensive evidence:

**Level 0 — Syntax**

The AI parses, loads, and references only defined symbols.

**Level 1 — Mechanical correctness**

Commands produce the intended local behavior under controlled conditions.

**Level 2 — Strategic correctness**

The AI selects sensible actions from verified world states and changes plans when conditions change.

**Level 3 — Robustness**

The system survives pressure, missed timings, resource disruption, lost infrastructure, and other expected failures.

**Level 4 — Comparative performance**

Repeatable games and replay analysis determine whether the implemented mechanism improves actual competitive behavior.

The project does not accept “it looked good once” as a benchmark.

## Change Acceptance

A substantive change should be traceable through:

```text
Requirement
  ↓
Reference / evidence
  ↓
Design decision
  ↓
Implementation
  ↓
Static audit
  ↓
Controlled test
  ↓
Replay / runtime evidence
  ↓
Regression check
  ↓
Acceptance
```

If a stage cannot be performed, record the limitation instead of silently skipping it.

## Failure Philosophy

AoE2DE AI development is mostly an exercise in discovering how many ways a reasonable-looking rule can fail.

Expect:

- stale observations;
- resources arriving later than expected;
- buildings being blocked or destroyed;
- production queues competing for the same resources;
- military plans becoming invalid;
- scouting information becoming obsolete;
- strategic commitments surviving after their reason disappears;
- rules firing in an unexpected order;
- state being overwritten by an unintended writer;
- engine behavior differing from the apparent intent of the script.

The answer is not another exception taped onto the old rule. The answer is explicit state, ownership, arbitration, verification, and recovery.

## Development Checklist

Before writing:

- [ ] Identify the exact problem.
- [ ] Find authoritative/reference evidence.
- [ ] Identify existing owners and dependencies.
- [ ] Define the smallest acceptable change.
- [ ] Define how success will be verified.

Before delivery:

- [ ] Re-read the changed code.
- [ ] Check symbol definitions and load order.
- [ ] Check for duplicate writers and conflicting rules.
- [ ] Check failure and release paths.
- [ ] Run the appropriate static test.
- [ ] Run the smallest useful runtime test.
- [ ] Inspect the resulting replay/runtime evidence.
- [ ] Record unresolved uncertainty.
- [ ] Deliver only what the evidence supports.

## Project Status

**Current state:** foundation stage.

The repository currently begins with a minimal README and no established AI implementation surface. That is useful. We will define the engineering contract before filling the repository with code that later has to be excavated and untangled.

The immediate priority is **not** to write a giant AI. It is to establish the verified engine interface, source corpus, architecture boundaries, testing discipline, and first executable slice.

## The Standard

Stock-Ai- is not being built to win a screenshot, pass one opening, or accumulate impressive-looking `.per` files.

It is being built to make good decisions repeatedly under imperfect information and imperfect conditions.

That requires discipline. It will take time. There is no shortcut around the engine, the evidence, or the replays.

**Reference it. Write it. Re-read it. Test it. Then deliver it.**
