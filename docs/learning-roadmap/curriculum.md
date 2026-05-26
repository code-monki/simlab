# Phase-Based Curriculum

Follow this sequence:

1. Ownership
2. Structs and enums
3. Deterministic tick loop
4. Serialization
5. Replay testing
6. Traits
7. Concurrency
8. ECS experiments
9. Godot bridge

Use [reading-list.md](reading-list.md) for the complete exercise-to-reading
map and specific chapter/section assignments. The readings below are the
phase-level minimums.

## 01 Ownership

Goal: understand ownership well enough to make deliberate design choices.

Focus:

- ownership and borrowing,
- move semantics,
- references and lifetimes,
- owned values versus stable IDs,
- cloning as an explicit tradeoff.

Readings:

- Primary: The Rust Programming Language, ownership/references/borrowing.
- Primary: Rust for C++ Developers, ownership and RAII comparisons.
- Practice: Rustlings ownership exercises.
- Lookup: Rust by Example, ownership and borrowing.
- Exercises: `001_ownership_basics`, then revisit in `015_shared_ownership`.

Done when:

- compiler errors are understandable,
- ownership choices are deliberate,
- reference-heavy object graphs no longer feel like the default design.

## 02 Structs and Enums

Goal: model simulation concepts idiomatically.

Focus:

- structs,
- enums,
- pattern matching,
- `Option`,
- `Result`,
- modules,
- newtypes for domain clarity.

Readings:

- Primary: The Rust Programming Language, structs/enums/pattern matching.
- Primary: The Rust Programming Language, `Option`, `Result`, and modules.
- Lookup: Rust by Example, structs/enums/pattern matching.
- Reference: Rust for C++ Developers, algebraic data types if covered.
- Exercises: `002_structs_and_enums`, `007_error_handling`,
  `008_modules_and_crates`.

Done when:

- simple models use enums and newtypes naturally,
- tests describe intended behavior.

## 03 Deterministic Tick Loop

Goal: build a small deterministic market simulation.

Focus:

- fixed ticks,
- seedable RNG,
- stable ordering,
- command input,
- event output,
- no hidden IO inside the simulation step.

Readings:

- Primary: The Rust Programming Language, tests/modules/collections.
- Reference: Creative Projects for Rust Programmers, simple simulation or game
  loop examples.
- Lookup: Cargo Book, package basics.
- Exercises: `003_tick_loop`, `009_iterators_collections`.

Done when:

- same seed plus same initial state produces the same result,
- simulation state can be inspected without presentation code.

## 04 Serialization

Goal: make deterministic state durable and comparable.

Focus:

- `serde`,
- snapshots,
- round-trip tests,
- format tradeoffs.

Readings:

- Primary: Practical System Programming for Rust Developers, files and error
  handling.
- Primary: `serde` documentation.
- Reference: Design Patterns and Best Practices in Rust, API boundaries.
- Exercises: `004_serialization`.

Done when:

- state can be saved and restored,
- serialization is outside the core tick logic.

## 05 Replay Testing

Goal: prove deterministic behavior from recorded inputs.

Focus:

- command logs,
- event logs,
- replay from seed plus commands,
- stable state hashing,
- golden tests.

Readings:

- Primary: The Rust Programming Language, testing and error handling.
- Primary: Rust API Guidelines, predictable APIs and ownership conventions.
- Lookup: Rust by Example, tests.
- Reference: `proptest` and `insta` documentation when adding generated or
  snapshot tests.
- Exercises: `005_replay_testing`, `010_state_hashing`,
  `011_property_tests`, `012_snapshot_tests`.

Done when:

- same seed plus same commands produces the same result,
- command replay reconstructs state,
- tests catch nondeterministic behavior.

## 06 Traits

Goal: learn Rust architecture patterns without over-abstracting.

Focus:

- trait bounds,
- associated types,
- generic dispatch,
- `dyn Trait`,
- object safety,
- module boundaries,
- public API design.

Readings:

- Primary: The Rust Programming Language, traits and generics.
- Primary: Design Patterns and Best Practices in Rust, trait/API design.
- Reference: Rust for C++ Developers, generics and trait comparisons.
- Reference: Rust API Guidelines.
- Exercises: `006_traits_boundaries`.

Done when:

- traits clarify boundaries,
- generics are not leaking everywhere,
- public APIs avoid lifetime-heavy signatures unless justified.

## 07 Concurrency

Goal: use concurrency without compromising determinism.

Focus:

- `Send`,
- `Sync`,
- ownership transfer,
- channels,
- scoped threads,
- Rayon-style parallelism,
- deterministic reductions.

Readings:

- Primary: Hands-On Concurrency with Rust, threads, shared state, and channels.
- Primary: The Rust Programming Language, concurrency and smart pointers.
- Reference: Asynchronous Programming in Rust for boundary concepts only.
- Lookup: Rayon and Crossbeam docs as needed.
- Exercises: `014_concurrency_parallel_markets`,
  `015_shared_ownership`, `016_message_boundary`, `017_async_io_edge`.

Done when:

- parallel code remains deterministic,
- shared mutable state is rare and justified,
- repeated tests pass without nondeterministic failures.

## 08 ECS Experiments

Goal: decide whether ECS helps the simulation core.

Focus:

- entity IDs,
- components as data,
- systems as transformations,
- schedule order,
- deterministic iteration,
- local ECS versus external ECS.

Readings:

- Primary: Bevy ECS docs.
- Reference: Game Development with Rust and WebAssembly, ECS/game structure
  sections only if useful.
- Reference: Design Patterns and Best Practices in Rust, data modeling.
- Exercises: `018_no_ecs_baseline`, `019_minimal_ecs`,
  `020_bevy_ecs_probe`, then `03x_ecs_experiment`.

Done when:

- ECS is a measured choice,
- iteration order and determinism are understood,
- the core architecture can justify its data model.

## 09 Godot Bridge

Goal: connect the authoritative Rust simulation core to Godot after the core is
stable.

Readings:

- Primary: godot-rust book.
- Reference: Game Development with Rust and WebAssembly for boundary thinking,
  not for engine-driven architecture.
- Exercises: `04x_godot_bridge`.

Done when:

- Godot can display simulation state from Rust,
- Godot can send commands into Rust,
- deterministic replay remains testable without Godot.
