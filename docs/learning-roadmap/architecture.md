# Architecture Guidance

## Architecture Spikes

Use spikes to answer design questions with code. A spike is larger than a normal
exercise, but it still needs explicit stop criteria.

Each spike should produce:

- the smallest demonstration that answers the question,
- tests or a repeatable verification step,
- a short note in `docs/architecture-notes.md` or the spike README,
- a decision: continue, defer, or discard.

### traveller_market

Question:
Can a tiny Traveller-style market be represented clearly with Rust structs,
enums, stable IDs, fixed ticks, and deterministic price changes?

Stop Criteria:

- goods, markets, agents, and prices exist,
- fixed tick update is deterministic,
- same seed and commands produce same state,
- additional work would become feature design.

### deterministic_replay

Question:
Can seed plus command log rebuild the same world state?

Stop Criteria:

- command log is persisted,
- replay reconstructs final state,
- state hash or canonical comparison is stable,
- nondeterministic ordering has been identified or ruled out.

### godot_bridge

Question:
Can Godot display Rust state and send commands without owning simulation rules?

Stop Criteria:

- Godot reads a Rust-produced snapshot,
- Godot sends at least one command into Rust,
- replay tests still run without Godot,
- no domain rule is duplicated in Godot.

### network_tick_sync

Question:
What minimal command/tick protocol would support synchronized simulation later?

Stop Criteria:

- tick number, command ordering, and seed assumptions are explicit,
- prototype works locally without real networking if possible,
- failure modes are documented,
- no production networking stack is built.

### economic_engine

Question:
Which data shape best supports markets, supply, demand, agents, and trade routes?

Stop Criteria:

- two data layouts are compared,
- behavior tests are shared,
- readability and determinism tradeoffs are documented,
- no optimization is accepted without measurement or clear simplification.

### combat_resolution

Question:
Can Mayday-style tactical resolution be modeled as deterministic commands,
state transitions, and events?

Stop Criteria:

- one combat interaction is modeled,
- legal and illegal transitions are tested,
- outputs are deterministic,
- UI and full rule coverage are deferred.

### swarm_coordination

Question:
Can a drone swarm command/control model preserve a single authoritative state
while accepting concurrent inputs?

Stop Criteria:

- command ingestion is modeled,
- authoritative state has one writer,
- ordering semantics are explicit,
- concurrency does not change deterministic results.

### stock_pipeline

Question:
Can Rust handle deterministic compute while Python remains the exploration layer?

Stop Criteria:

- one indicator or backtest is implemented in Rust,
- Python can call or consume the result,
- data loading and compute boundaries are clear,
- plotting/UI concerns are deferred.

## Project Specialization Tracks

Traveller Economic Simulation:

- primary track,
- deterministic market core,
- replay and serialization first,
- Godot after the headless core is stable.

Stock Market Analyzer:

- later Python/Rust integration track,
- Rust for indicators, backtests, and deterministic compute,
- Python for notebooks, plotting, and exploration.

Mayday:

- later Rust/Godot tactical combat track,
- useful once Godot bridge patterns are proven.

Security Drone Swarm Manager:

- later concurrency and command/control track,
- useful after deterministic single-writer patterns are comfortable.

## Specialization Matrix

| Project                       | Primary Rust Lessons                                       | Integration Bias                   | Start After                                       |
| ----------------------------- | ---------------------------------------------------------- | ---------------------------------- | ------------------------------------------------- |
| Traveller Economic Simulation | deterministic ticks, replay, serialization, ECS comparison | Godot presentation later           | ownership, structs/enums, deterministic tick loop |
| Mayday                        | tactical state machines, command/event flow, Godot bridge  | Godot presentation                 | replay and Godot snapshot viewer                  |
| Stock Market Analyzer         | data pipelines, backtesting, Python acceleration           | Python via PyO3                    | serialization and testing discipline              |
| Security Drone Swarm Manager  | concurrency, command/control, async edges                  | service or visualization layer TBD | deterministic single-writer model                 |

## Testing / Verification Discipline

Every exercise should include at least one test or explicit verification step.

Prefer tests that prove:

- deterministic tick behavior,
- valid state transitions,
- command-to-event behavior,
- snapshot round trips,
- replay equivalence,
- stable hashes,
- deterministic parallel reductions.

## Profiling / Performance

Performance matters after correctness and determinism.

Use this order:

1. Make behavior correct.
2. Make behavior deterministic.
3. Add tests.
4. Measure.
5. Optimize the measured bottleneck.

Early performance probes:

- compare data layouts,
- measure serialization formats,
- compare single-threaded and parallel market updates,
- inspect allocation-heavy code only after behavior stabilizes.

## Concurrency Strategy

Concurrency is phase 7, not phase 1.

Default model:

- single authoritative simulation writer,
- explicit command input,
- explicit event output,
- parallelism only for isolated, deterministic work,
- stable result ordering after parallel computation.

Use threads/Rayon for CPU-bound work. Use async/Tokio for IO-bound edges. Do not
make the core simulation async unless a concrete exercise proves the need.

## ECS Strategy

Do not start with ECS.

First build a non-ECS baseline. Then compare:

1. direct data model,
2. minimal local ECS,
3. `bevy_ecs`.

The decision should be based on clarity, testability, deterministic iteration,
and friction, not on architecture fashion.

## Godot Integration Path

Godot integration comes after the headless Rust core can replay deterministically.

Path:

1. Rust simulation core.
2. Snapshot export.
3. Godot snapshot viewer.
4. Godot command bridge.
5. Replay test that does not require Godot.

Rules:

- Rust remains authoritative.
- Godot presents snapshots and sends commands.
- Do not duplicate simulation rules in Godot.

## Networking / Replay / Determinism

Networking is deferred until replay is boring.

Determinism rules:

- no wall-clock time inside simulation rules,
- no implicit global randomness,
- explicit seeds,
- stable iteration order,
- command logs as inputs,
- events as outputs,
- reproducible state hashes.

Replay is the bridge between local simulation, future networking, save/load, and
debugging.
