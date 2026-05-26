# Resources

For exercise-specific assignments, use [reading-list.md](reading-list.md).

## Reading Sequence

Primary books:

- The Rust Programming Language, 3rd edition, Steve Klabnik et al.
- Rust for C++ Developers, Dan Olson
- Design Patterns and Best Practices in Rust, Evan Williams
- Hands-On Concurrency with Rust, Brian L. Troutwine
- Asynchronous Programming in Rust, Carl Fredrik Samson

Secondary books:

- Creative Projects for Rust Programmers, Carlo Milanesi
- Practical System Programming for Rust Developers, Prabhu Eshwarla
- Speed Up Your Python with Rust, Maxwell Flitton
- Game Development with Rust and WebAssembly, Eric Smith

Defer:

- Rust Web Development with Rocket
- Rust Web Programming
- Rust for Blockchain Application Development

## Web Resources

- Rust Book: https://doc.rust-lang.org/book/
- Rust by Example: https://doc.rust-lang.org/rust-by-example/
- Rustlings: https://github.com/rust-lang/rustlings
- Cargo Book: https://doc.rust-lang.org/cargo/
- Rust API Guidelines: https://rust-lang.github.io/api-guidelines/
- Rust Performance Book: https://nnethercote.github.io/perf-book/
- Async Book: https://rust-lang.github.io/async-book/
- Tokio Tutorial: https://tokio.rs/tokio/tutorial
- Bevy ECS docs: https://docs.rs/bevy/latest/bevy/ecs/
- godot-rust book: https://godot-rust.github.io/book/
- PyO3 guide: https://pyo3.rs/
- wasm-bindgen guide: https://wasm-bindgen.github.io/wasm-bindgen/

## Chapter Mapping

Use chapter topics rather than fixed chapter numbers, because editions and book
formats vary.

- Ownership chapters: `ownership_001_values_refs_ids`.
- Structs, enums, pattern matching: `model_001_goods_prices`,
  `model_002_order_state`.
- Modules, packages, tests: every exercise after `model_001_goods_prices`.
- Error handling: persistence, command handling, and integration exercises.
- Generics and traits: `api_001_rng_boundary`, `api_002_storage_boundary`,
  `api_003_system_boundary`.
- Collections and iterators: market, agent, and ECS exercises.
- Smart pointers and interior mutability: only after a concrete need appears.
- Threads, channels, shared state: `concurrency_001_parallel_markets`,
  `concurrency_002_message_boundary`.
- Async/futures: edge exercises after replay is stable.
- FFI and embedding: Godot and Python integration tracks.

## Crate Guidance

Use crates only when they support a specific exercise. Every dependency should
have a reason to exist.

### Serialization

Crates:

- `serde`
- `serde_json`
- `ron`
- `bincode`

Why:
Snapshots, command logs, event logs, and replay fixtures.

When:
Use once the world state exists and needs round-trip tests.

When Not:
Do not pick a permanent format before the data model stabilizes.

### Testing

Crates:

- `proptest`
- `insta`

Why:
Property tests validate invariants. Snapshot tests make command/event output
easy to review.

When:
Use after simple unit tests exist and the invariant or output shape is clear.

When Not:
Do not use snapshot tests for unstable ordering or property tests with
meaningless generated inputs.

### CLI

Crates:

- `clap`
- `argh`

Why:
Small tools for running simulations, replaying logs, or inspecting snapshots.

When:
Use when command-line repetition becomes useful.

When Not:
Do not build a CLI before the exercise can be run directly with tests.

### ECS

Crates:

- `bevy_ecs`
- `hecs`
- `shipyard`

Why:
Compare established ECS models against a direct data-model baseline.

When:
Use after `018_no_ecs_baseline` and `019_minimal_ecs`.

When Not:
Do not introduce ECS before the non-ECS baseline proves what pain exists.

### Logging

Crates:

- `tracing`
- `tracing-subscriber`
- `log`

Why:
Inspect command flow, replay, and integration boundaries.

When:
Use when print debugging becomes noisy or structured context matters.

When Not:
Do not let logging become part of deterministic simulation behavior.

### Profiling

Crates / tools:

- `criterion`
- `pprof`
- `flamegraph`

Why:
Measure actual bottlenecks after correctness and determinism.

When:
Use once a behavior is stable and there is a concrete performance question.

When Not:
Do not profile speculative architecture or optimize before tests exist.

### Networking

Crates:

- `tokio`
- `quinn`
- `axum`
- `tungstenite`

Why:
Future command transport, tooling, or synchronized tick experiments.

When:
Use only after replay and command ordering are well understood.

When Not:
Do not start networking before local deterministic replay is boring.

### Async

Crates:

- `tokio`
- `futures`

Why:
IO-bound edges such as command servers, persistence workers, or tooling.

When:
Use after the synchronous simulation core is stable.

When Not:
Do not make the core simulation async by default.

### Database

Crates:

- `sqlx`
- `rusqlite`

Why:
Persist large experiment outputs, market histories, or stock-analysis data.

When:
Use when files are no longer enough and querying is a real need.

When Not:
Do not add a database for early snapshots or command logs.

### Math

Crates:

- `nalgebra`
- `glam`
- `ndarray`

Why:
Vector math, transforms, matrices, or numerical analysis.

When:
Use when project math exceeds standard-library clarity.

When Not:
Do not add math crates for basic arithmetic or simple economic rules.

### Randomness

Crates:

- `rand`
- `rand_chacha`

Why:
Seeded deterministic randomness and reproducible replay tests.

When:
Use as soon as randomness enters simulation rules.

When Not:
Do not use implicit global randomness or unseeded random sources in the core.

### Benchmarking

Crates:

- `criterion`

Why:
Compare data layouts, serialization formats, or parallel update strategies.

When:
Use after correctness tests exist for both implementations being compared.

When Not:
Do not benchmark code paths whose behavior is still changing.

### Error Handling

Crates:

- `thiserror`
- `anyhow`

Why:
Typed errors for library/domain code; convenient errors for binaries and
prototypes.

When:
Use `thiserror` for reusable boundaries and `anyhow` for top-level tools.

When Not:
Do not hide meaningful domain failures behind generic strings.

### Integration

Crates:

- `godot`
- `pyo3`
- `wasm-bindgen`

Why:
Godot presentation, Python analysis, and browser delivery.

When:
Use after the Rust API boundary is stable enough to expose.

When Not:
Do not let integration frameworks shape the core simulation rules.
