# Detailed Exercise Catalog

Each exercise should include:

- Purpose
- Learning Objectives
- Readings
- Deliverables
- Success Criteria
- Common Failure Modes
- Architectural Relevance
- Estimated Effort
- Notes

Use [reading-list.md](reading-list.md) for the canonical exercise-to-reading
map. Per-exercise reading notes below are brief reminders.

Use [worked-answers.md](worked-answers.md) only after attempting an exercise.
The worked answers are comparison points, not the only acceptable solutions.

## Exercise README Template

```md
# Exercise Name

## Purpose

Why does this exercise exist?

## Learning Objectives

- What Rust concepts should this exercise teach?
- What simulation/design assumption is being tested?

## Readings

- Book or web sections to consult only as needed.

## Deliverables

- What code, tests, or notes should exist when done?

## Success Criteria

- How do we know the exercise is complete?

## Common Failure Modes

- What traps should be watched for?

## Architectural Relevance

- What future design decision does this inform?

## Estimated Effort

- Small | Medium | Large

## Notes

- Friction, lessons learned, follow-up.
```

## 001_ownership_basics

Purpose:
Learn how Rust ownership changes everyday design choices.

Learning Objectives:

- Understand move semantics.
- Distinguish owned values, borrows, and clones.
- Notice where classic object graphs fight the borrow checker.

Readings:

- Rust Book: ownership, references, borrowing.
- Rust for C++ Developers: ownership and RAII comparisons.
- Rustlings ownership exercises.

Deliverables:

- A tiny model implemented with owned values and borrows.
- Tests or compile examples showing valid and invalid ownership shapes.
- Notes on where borrowing helped or complicated the design.

Success Criteria:

- Compiler errors are understandable.
- Clones are explicit and justified.
- The exercise explains when ownership is clearer than references.

Common Failure Modes:

- Adding lifetimes before trying owned values.
- Cloning to silence compiler errors without naming the tradeoff.
- Designing a reference-heavy object graph.

Architectural Relevance:
Sets the baseline for world state ownership and simulation data flow.

Estimated Effort:
Small.

Notes:
Prefer simple domain objects over generic examples.

## 002_structs_and_enums

Purpose:
Model simulation concepts idiomatically with Rust data types.

Learning Objectives:

- Use structs for domain data.
- Use enums for state and variants.
- Use pattern matching instead of stringly typed state.
- Use newtypes for domain clarity.

Readings:

- Rust Book: structs, enums, pattern matching, modules.
- Rust by Example: enums and pattern matching.

Deliverables:

- Goods, quantities, prices, markets, and order states.
- Tests for legal and illegal transitions.

Success Criteria:

- Domain states are represented by types, not strings.
- Invalid states are hard or impossible to express.

Common Failure Modes:

- Overusing traits where enums are clearer.
- Using primitive types everywhere.
- Hiding domain transitions in ad hoc conditionals.

Architectural Relevance:
Establishes type-driven modeling for later simulation code.

Estimated Effort:
Small.

Notes:
Favor clarity over generic reuse.

## 003_tick_loop

Purpose:
Build the smallest deterministic fixed-step simulation loop.

Learning Objectives:

- Separate world state from tick logic.
- Keep simulation steps explicit.
- Avoid hidden IO and wall-clock time.

Readings:

- Rust Book: modules, tests.
- Creative Projects for Rust Programmers: simulation/game-loop examples as
  useful.

Deliverables:

- A fixed tick counter.
- A deterministic market update.
- Tests showing repeated runs produce identical results.

Success Criteria:

- Same initial state produces same final state.
- Tick logic can be tested without UI or runtime dependencies.

Common Failure Modes:

- Using current time inside rules.
- Hiding mutations across too many functions.
- Expanding into a full economic model too early.

Architectural Relevance:
Defines the core shape of the simulation engine.

Estimated Effort:
Small.

Notes:
Keep the model intentionally boring.

## 004_serialization

Purpose:
Make world state durable and round-trippable.

Learning Objectives:

- Use `serde` derives.
- Compare readable snapshot formats.
- Keep persistence outside the tick step.

Readings:

- Practical System Programming for Rust Developers: files and errors.
- `serde` documentation.

Deliverables:

- Snapshot serialization.
- Snapshot deserialization.
- Round-trip equality test.

Success Criteria:

- World state survives save/load without behavior changes.
- IO errors are explicit.

Common Failure Modes:

- Treating the first format as permanent.
- Mixing file IO into simulation rules.
- Serializing derived/cache state unnecessarily.

Architectural Relevance:
Supports save/load, replay setup, and future Godot inspection.

Estimated Effort:
Small.

Notes:
Start with readable formats before compact ones.

## 005_replay_testing

Purpose:
Prove deterministic behavior from seed plus command log.

Learning Objectives:

- Model commands as inputs.
- Model events as outputs.
- Rebuild state from recorded inputs.
- Detect nondeterminism with tests.

Readings:

- Rust Book: error handling and testing.
- Rust API Guidelines: predictable APIs and ownership conventions.

Deliverables:

- Command log.
- Event log.
- Replay test.
- Stable state comparison or hash.

Success Criteria:

- Same seed plus same commands produces same final state.
- Replay test fails if ordering or randomness changes.

Common Failure Modes:

- Treating events as inputs.
- Using unordered iteration where order matters.
- Hiding randomness behind global state.

Architectural Relevance:
Replay is the debugging, networking, save/load, and validation foundation.

Estimated Effort:
Medium.

Notes:
This is the first major milestone.

## 006_traits_boundaries

Purpose:
Use traits only where they clarify real boundaries.

Learning Objectives:

- Compare concrete APIs, generics, and `dyn Trait`.
- Understand object safety.
- Avoid abstraction before repeated friction.

Readings:

- Rust Book: traits and generics.
- Design Patterns and Best Practices in Rust: API boundaries.
- Rust API Guidelines.

Deliverables:

- RNG or storage boundary implemented two ways.
- Notes comparing clarity, coupling, and testability.

Success Criteria:

- The chosen trait boundary has a concrete reason.
- Public APIs avoid unnecessary lifetimes and generic sprawl.

Common Failure Modes:

- Recreating inheritance with trait objects.
- Making every dependency a trait.
- Abstracting before the concrete version hurts.

Architectural Relevance:
Guides API boundaries for simulation core, persistence, and integrations.

Estimated Effort:
Medium.

Notes:
Concrete first.

## 007_error_handling

Purpose:
Handle expected failures without obscuring simulation logic.

Learning Objectives:

- Use `Result` idiomatically.
- Choose between `thiserror` and `anyhow`.
- Keep domain errors distinct from IO/prototype errors.

Readings:

- Rust Book: recoverable errors.
- `thiserror` and `anyhow` docs.

Deliverables:

- Domain error enum.
- Persistence error handling.
- Tests for failed operations.

Success Criteria:

- Errors are explicit and readable.
- Call sites are not cluttered with irrelevant detail.

Common Failure Modes:

- Using strings for every error.
- Over-designing error hierarchies.
- Losing domain meaning behind generic errors.

Architectural Relevance:
Keeps command handling, persistence, and integration boundaries honest.

Estimated Effort:
Small.

Notes:
Library-style code should prefer typed errors.

## 008_modules_and_crates

Purpose:
Organize small Rust exercises without creating architecture ceremony.

Learning Objectives:

- Use modules cleanly.
- Understand crate layout.
- Keep public APIs intentional.

Readings:

- Rust Book: packages, crates, modules.
- Cargo Book: package basics.

Deliverables:

- One exercise crate with clear module boundaries.
- Minimal public API.

Success Criteria:

- Tests can access what they need.
- Implementation details are not accidentally public.

Common Failure Modes:

- Splitting files before responsibilities are clear.
- Making everything `pub`.
- Creating framework-like structure too early.

Architectural Relevance:
Prevents early exercises from becoming messy or overbuilt.

Estimated Effort:
Small.

Notes:
Structure follows discovered responsibility.

## 009_iterators_collections

Purpose:
Use collections and iteration without compromising determinism.

Learning Objectives:

- Use vectors, maps, and iterators idiomatically.
- Identify ordering-sensitive code.
- Prefer stable ordering where results depend on order.

Readings:

- Rust Book: collections and iterators.
- Rust Performance Book: collections when needed.

Deliverables:

- Market or agent collection update.
- Test proving stable output ordering.

Success Criteria:

- Iteration order is explicit where it matters.
- Iterator code remains readable.

Common Failure Modes:

- Using unordered maps in deterministic calculations.
- Over-compressing logic into unreadable iterator chains.
- Mutating while iterating without a clear plan.

Architectural Relevance:
Market simulations will be collection-heavy.

Estimated Effort:
Small.

Notes:
Readable loops are acceptable.

## 010_state_hashing

Purpose:
Create stable fingerprints for replay validation.

Learning Objectives:

- Decide what state matters.
- Exclude irrelevant or derived data.
- Produce stable comparison output.

Readings:

- Serialization docs.
- Hashing crate docs if a crate is used.

Deliverables:

- State digest or canonical comparison.
- Tests showing identical replays match.

Success Criteria:

- Hashes are stable across repeated runs.
- Hash input ordering is deterministic.

Common Failure Modes:

- Hashing unordered data without sorting.
- Including timestamps or nondeterministic fields.
- Treating hash equality as a substitute for all tests.

Architectural Relevance:
Useful for replay, regression testing, and future networking.

Estimated Effort:
Small.

Notes:
Canonical serialized state may be enough early.

## 011_property_tests

Purpose:
Use generated cases to validate invariants.

Learning Objectives:

- Understand property testing.
- Express simulation invariants.
- Avoid brittle example-only tests.

Readings:

- `proptest` documentation.
- Rust Book: tests.

Deliverables:

- Property tests for quantities, prices, or order transitions.

Success Criteria:

- Tests find invalid edge cases or prove basic invariants.
- Generated inputs are constrained meaningfully.

Common Failure Modes:

- Writing properties that restate implementation.
- Generating impossible domain values.
- Letting tests become slow and noisy.

Architectural Relevance:
Validates core rules beyond hand-picked examples.

Estimated Effort:
Medium.

Notes:
Use sparingly at first.

## 012_snapshot_tests

Purpose:
Use golden snapshots for readable regression checks.

Learning Objectives:

- Understand snapshot testing.
- Decide when textual output is worth locking down.

Readings:

- `insta` documentation.

Deliverables:

- Snapshot test for command/event output or serialized state.

Success Criteria:

- Reviewable output changes are easy to inspect.
- Snapshots do not lock down irrelevant noise.

Common Failure Modes:

- Snapshotting unstable ordering.
- Accepting snapshots without understanding changes.
- Snapshotting too much.

Architectural Relevance:
Helpful for command/event logs and replay outputs.

Estimated Effort:
Small.

Notes:
Use after output formats stabilize a little.

## 013_data_layout_probe

Purpose:
Compare simple data layouts before performance matters.

Learning Objectives:

- Understand array-of-structs versus struct-of-arrays.
- Measure only after behavior is correct.

Readings:

- Rust Performance Book: data layout and allocation topics.

Deliverables:

- Two market storage layouts.
- Notes comparing readability and likely performance.

Success Criteria:

- Both versions pass the same behavior tests.
- No optimization decision is made without measurement or clarity.

Common Failure Modes:

- Prematurely optimizing away readability.
- Changing behavior while changing layout.

Architectural Relevance:
Informs future economic engine storage.

Estimated Effort:
Medium.

Notes:
This is a probe, not a commitment.

## 014_concurrency_parallel_markets

Purpose:
Parallelize isolated market updates deterministically.

Learning Objectives:

- Use ownership transfer or scoped borrowing safely.
- Preserve deterministic result ordering.
- Understand when Rayon fits.

Readings:

- Hands-On Concurrency with Rust.
- Rayon docs.

Deliverables:

- Parallel market update.
- Test comparing sequential and parallel output.

Success Criteria:

- Parallel result matches sequential result.
- Repeated test runs are stable.

Common Failure Modes:

- Shared mutable state everywhere.
- Nondeterministic reduction order.
- Parallelizing before independent work exists.

Architectural Relevance:
Tests concurrency without corrupting determinism.

Estimated Effort:
Medium.

Notes:
Prefer isolated data partitions.

## 015_shared_ownership

Purpose:
Understand smart pointers and shared ownership without defaulting to them.

Learning Objectives:

- Use `Box`, `Rc`, `Arc`, `RefCell`, and `Mutex` deliberately.
- Understand interior mutability tradeoffs.
- Recognize when stable IDs are simpler.

Readings:

- Rust Book: smart pointers and concurrency chapters.
- Rust for C++ Developers: pointer comparisons.

Deliverables:

- Same relationship modeled with IDs and shared ownership.
- Notes comparing clarity and risk.

Success Criteria:

- Shared ownership is used only with a clear reason.
- The exercise explains why IDs may be better for world state.

Common Failure Modes:

- Replacing borrow-checker friction with `Rc<RefCell<T>>`.
- Using `Arc<Mutex<T>>` as a default architecture.
- Hiding mutation behind shared handles.

Architectural Relevance:
Critical for avoiding object-graph designs in simulation state.

Estimated Effort:
Medium.

Notes:
This should be comparative, not prescriptive.

## 016_message_boundary

Purpose:
Feed commands to a single authoritative simulation owner.

Learning Objectives:

- Use channels or queues.
- Preserve single-writer semantics.
- Separate IO edge from simulation core.

Readings:

- Hands-On Concurrency with Rust: channels.
- Crossbeam docs if used.

Deliverables:

- Command queue or channel boundary.
- Simulation worker or explicit command pump.

Success Criteria:

- Simulation state has one owner.
- Commands are ordered and testable.

Common Failure Modes:

- Multiple writers mutate world state.
- Command order is implicit.
- Tests require real threads unnecessarily.

Architectural Relevance:
Foundation for async edges, networking, and Godot command input.

Estimated Effort:
Medium.

Notes:
Keep a synchronous test path.

## 017_async_io_edge

Purpose:
Learn async at the boundary without making the core async.

Learning Objectives:

- Understand futures and runtimes.
- Use async for IO-bound work.
- Keep simulation tests runtime-free.

Readings:

- Asynchronous Programming in Rust.
- Async Book.
- Tokio Tutorial.

Deliverables:

- Async command or persistence edge.
- Synchronous simulation core.

Success Criteria:

- Async code feeds commands or performs IO.
- Core replay tests do not require Tokio.

Common Failure Modes:

- Making all simulation code async.
- Letting runtime concerns leak into domain logic.
- Confusing CPU parallelism with async IO.

Architectural Relevance:
Prepares for servers, tools, and external integrations.

Estimated Effort:
Medium.

Notes:
Do this after replay is stable.

## 018_no_ecs_baseline

Purpose:
Build a direct data-model baseline before trying ECS.

Learning Objectives:

- Keep systems as plain transformations.
- Understand what pain ECS is supposed to solve.

Readings:

- Existing simulation exercises.

Deliverables:

- Market/agent loop without ECS.
- Tests and notes on clarity/friction.

Success Criteria:

- Baseline behavior is clear and tested.
- ECS evaluation has something concrete to compare against.

Common Failure Modes:

- Skipping straight to ECS.
- Designing the baseline to make ECS look necessary.

Architectural Relevance:
Prevents architecture fashion from driving the design.

Estimated Effort:
Medium.

Notes:
This is the control case.

## 019_minimal_ecs

Purpose:
Implement a tiny local ECS shape for comparison.

Learning Objectives:

- Understand entities, components, and systems.
- Observe schedule and iteration-order concerns.

Readings:

- ECS overview material.
- Bevy ECS docs only for comparison concepts.

Deliverables:

- Minimal ECS version of the market/agent loop.
- Comparison notes against direct baseline.

Success Criteria:

- Same behavior as baseline.
- Added complexity is visible and evaluated.

Common Failure Modes:

- Building a framework.
- Losing deterministic ordering.
- Treating ECS as automatically better.

Architectural Relevance:
Clarifies whether ECS fits economic simulation.

Estimated Effort:
Medium.

Notes:
Keep it tiny.

## 020_bevy_ecs_probe

Purpose:
Compare a real ECS crate against the baseline and local ECS.

Learning Objectives:

- Use `bevy_ecs` without adopting the whole engine.
- Understand schedule, queries, resources, and determinism.

Readings:

- Bevy ECS docs.

Deliverables:

- `bevy_ecs` version of the same loop.
- Written comparison across all three approaches.

Success Criteria:

- Same behavior is reproduced.
- Determinism and schedule order are understood.

Common Failure Modes:

- Pulling in full engine concerns.
- Accepting nondeterministic iteration.
- Comparing different behavior across versions.

Architectural Relevance:
Informs ECS decision for Traveller and Mayday.

Estimated Effort:
Large.

Notes:
Stop once the comparison is clear.

## 03x_ecs_experiment

Purpose:
Reserve future ECS experiments after the 001-020 baseline.

Learning Objectives:

- Explore ECS scheduling, resources, and data layout only after baseline
  comparisons.

Deliverables:

- One focused ECS question per exercise.

Success Criteria:

- Each experiment answers one architecture question.

Common Failure Modes:

- Turning ECS exploration into engine building.

Architectural Relevance:
Supports informed ECS adoption or rejection.

Estimated Effort:
Medium to Large.

Notes:
Use `03x` numbering for focused follow-ons.

## 04x_godot_bridge

Purpose:
Integrate Godot after deterministic core behavior is proven.

Learning Objectives:

- Expose snapshots to Godot.
- Accept commands from Godot.
- Keep Rust authoritative.

Readings:

- godot-rust book.

Deliverables:

- Snapshot viewer.
- Command bridge.
- Replay test independent of Godot.

Success Criteria:

- Godot displays state and sends commands.
- Core rules are not duplicated in Godot.

Common Failure Modes:

- Moving simulation rules into Godot.
- Letting presentation needs reshape core state prematurely.

Architectural Relevance:
Defines the Rust/Godot boundary.

Estimated Effort:
Large.

Notes:
Do after replay and serialization.

## 05x_async_io

Purpose:
Explore async IO after the simulation core is stable.

Learning Objectives:

- Accept network or tool commands asynchronously.
- Persist or stream data outside the tick step.

Readings:

- Async Book.
- Tokio Tutorial.
- Asynchronous Programming in Rust.

Deliverables:

- Async command server or persistence worker.
- Core replay tests unchanged.

Success Criteria:

- Async remains at the edge.
- Deterministic core does not depend on a runtime.

Common Failure Modes:

- Making domain logic async.
- Mixing IO timing into simulation rules.

Architectural Relevance:
Prepares for tools, networking, and service wrappers.

Estimated Effort:
Large.

Notes:
Only when a real IO edge exists.
