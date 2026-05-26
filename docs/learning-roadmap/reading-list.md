# Reading List

Use this as a targeted reading guide. Read only enough to unblock the current
exercise, then return to code.

Chapter numbers are intentionally omitted because editions and formats vary.
Use the topic names in each book's table of contents.

## Core Rule

Each exercise has:

- Primary reading: read before or during the exercise.
- Reference reading: skim only if stuck.
- Web companion: use for quick lookup or examples.

## Exercise Reading Map

| Exercise | Primary Reading | Reference Reading | Web Companion |
| --- | --- | --- | --- |
| `001_ownership_basics` | Rust Book: ownership, references, borrowing | Rust for C++ Developers: ownership and RAII | Rustlings ownership; Rust by Example ownership |
| `002_structs_and_enums` | Rust Book: structs, enums, pattern matching | Rust for C++ Developers: algebraic data types if covered | Rust by Example structs/enums |
| `003_tick_loop` | Rust Book: modules, tests | Creative Projects for Rust Programmers: simple simulation/game loop examples | Cargo Book package basics |
| `004_serialization` | Practical System Programming for Rust Developers: files/errors | Design Patterns and Best Practices in Rust: API boundaries | `serde` docs |
| `005_replay_testing` | Rust Book: testing and error handling | Rust API Guidelines: predictable APIs | Rust by Example tests |
| `006_traits_boundaries` | Rust Book: traits and generics | Design Patterns and Best Practices in Rust: trait/API design | Rust API Guidelines |
| `007_error_handling` | Rust Book: recoverable errors | Practical System Programming for Rust Developers: error handling | `thiserror` and `anyhow` docs |
| `008_modules_and_crates` | Rust Book: packages, crates, modules | Cargo Book: package layout | Cargo Book workspaces as needed |
| `009_iterators_collections` | Rust Book: collections and iterators | Rust Performance Book: collections only if needed | Rust by Example iterators |
| `010_state_hashing` | Serialization topics from `004_serialization` | Rust API Guidelines: deterministic behavior implications | Hashing/serialization crate docs |
| `011_property_tests` | Rust Book: tests | Design Patterns and Best Practices in Rust: correctness patterns | `proptest` docs |
| `012_snapshot_tests` | Rust Book: tests | Practical System Programming for Rust Developers: files | `insta` docs |
| `013_data_layout_probe` | Rust Performance Book: data layout and allocation | Rust for C++ Developers: memory model comparisons | Criterion docs if measuring |
| `014_concurrency_parallel_markets` | Hands-On Concurrency with Rust: threads/shared state | Rust Book: fearless concurrency | Rayon docs |
| `015_shared_ownership` | Rust Book: smart pointers | Rust Book: concurrency shared state | Rust by Example smart pointers |
| `016_message_boundary` | Hands-On Concurrency with Rust: channels | Asynchronous Programming in Rust: boundary concepts | Crossbeam docs |
| `017_async_io_edge` | Asynchronous Programming in Rust: futures/runtimes | Async Book | Tokio Tutorial |
| `018_no_ecs_baseline` | Earlier simulation exercises | Design Patterns and Best Practices in Rust: data modeling | Existing tests and notes |
| `019_minimal_ecs` | ECS concept overview from Bevy docs | Game Development with Rust and WebAssembly: ECS/game structure if useful | Bevy ECS docs |
| `020_bevy_ecs_probe` | Bevy ECS docs | Rust API Guidelines: API clarity | Bevy ECS examples |
| `03x_ecs_experiment` | Bevy ECS docs for the specific question | Game Development with Rust and WebAssembly | `bevy_ecs` crate docs |
| `04x_godot_bridge` | godot-rust book | Game Development with Rust and WebAssembly for boundary thinking | godot-rust examples |
| `05x_async_io` | Asynchronous Programming in Rust | Async Book | Tokio Tutorial |

## Book Priority by Phase

### 01 Ownership

Primary:

- The Rust Programming Language
- Rust for C++ Developers

Use Rustlings for compiler-driven practice.

### 02 Structs and Enums

Primary:

- The Rust Programming Language
- Rust by Example

Use Design Patterns and Best Practices in Rust only when the model starts
needing API boundaries.

### 03 Deterministic Tick Loop

Primary:

- The Rust Programming Language: tests, modules, collections
- Creative Projects for Rust Programmers: small simulation examples

Avoid game-engine material here.

### 04 Serialization

Primary:

- Practical System Programming for Rust Developers
- `serde` documentation

Use readable formats before compact formats.

### 05 Replay Testing

Primary:

- Rust Book: testing and error handling
- Rust API Guidelines

Focus on commands, events, and deterministic comparison.

### 06 Traits

Primary:

- The Rust Programming Language
- Design Patterns and Best Practices in Rust
- Rust for C++ Developers

Read only enough to compare concrete APIs, generics, and `dyn Trait`.

### 07 Concurrency

Primary:

- Hands-On Concurrency with Rust
- Rust Book concurrency chapter

Use Rayon docs when the exercise is CPU-bound.

### 08 ECS Experiments

Primary:

- Bevy ECS docs
- Game Development with Rust and WebAssembly, selectively

Do not read ECS material before the non-ECS baseline exists.

### 09 Godot Bridge

Primary:

- godot-rust book

Read after replay and serialization are working.

## Deferred Reading

Defer until a project creates a concrete need:

- Rust Web Development with Rocket
- Rust Web Programming
- Rust for Blockchain Application Development
- WASM packaging material
- database-specific material
- advanced unsafe Rust material

## Reading Notes Rule

Put book notes in `notes/rust-notes.md` only when they affect an exercise.

Put architecture conclusions in `docs/architecture-notes.md` only after code or
tests reveal a reusable lesson.
