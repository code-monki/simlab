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

## 01 Ownership

Goal: understand ownership well enough to make deliberate design choices.

Focus:

- ownership and borrowing,
- move semantics,
- references and lifetimes,
- owned values versus stable IDs,
- cloning as an explicit tradeoff.

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

Done when:

- ECS is a measured choice,
- iteration order and determinism are understood,
- the core architecture can justify its data model.

## 09 Godot Bridge

Goal: connect the authoritative Rust simulation core to Godot after the core is
stable.

Done when:

- Godot can display simulation state from Rust,
- Godot can send commands into Rust,
- deterministic replay remains testable without Godot.
