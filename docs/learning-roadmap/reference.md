# Roadmap Reference

## Anti-Patterns and Rabbit Holes

- Translating inheritance hierarchies directly into trait object graphs.
- Adding lifetimes to public APIs before trying owned values or IDs.
- Using `Arc<Mutex<T>>` as a default design tool.
- Making the simulation core async.
- Letting Godot own simulation rules.
- Adding ECS before a non-ECS baseline exists.
- Optimizing before determinism is tested.
- Depending on wall-clock time inside simulation rules.
- Using unordered maps where iteration order affects results.
- Hiding randomness behind implicit global state.
- Treating serialization format as stable too early.
- Expanding an exercise into a product feature.
- Reading broadly instead of building the next smallest probe.
- Introducing abstractions before repeated concrete friction proves the need.

## Proficiency Milestones

First milestone: deterministic mini market.

Includes:

- goods,
- markets,
- agents,
- fixed ticks,
- seedable RNG,
- command log,
- event log,
- replay test,
- snapshot round trip.

Success criteria:

- `cargo test` proves deterministic replay,
- the core has no Godot dependency,
- state transitions are clear,
- lessons learned are documented.

Second milestone: architecture comparison.

- direct model versus ECS,
- concrete API versus trait boundary,
- single-threaded versus deterministic parallel update.

Third milestone: Godot bridge.

- Godot displays Rust state,
- Godot sends commands to Rust,
- replay remains independent of Godot.

## Retirement-Era Suggested Cadence

Use a cadence that favors consistency over long sessions.

- 3 to 5 sessions per week.
- 60 to 120 minutes per session.
- One exercise or sub-exercise per session.
- Start with tests or a tiny compile target.
- End by writing the lesson learned.
- Every fifth session, review notes and prune the next exercise.

Avoid marathon sessions that produce lots of code but no captured learning.

## Deferred / Low ROI Topics

Defer these until a roadmap step creates a real need:

- unsafe Rust,
- procedural macros,
- custom allocators,
- advanced lifetime-heavy APIs,
- networking protocols,
- databases,
- web frameworks,
- blockchain-specific tooling,
- WASM packaging,
- production observability,
- plugin architectures,
- save-game migration systems,
- distributed simulation,
- real-time multiplayer,
- full Godot UI.

## Appendix

Useful commands:

```sh
cargo new exercises/example_name
cargo test
cargo test -- --nocapture
cargo fmt
cargo clippy
cargo doc --open
```

Tools:

- `cargo`: package manager and build tool.
- `rustfmt`: formatter.
- `clippy`: lints and idiom checks.
- `rustdoc`: documentation generator.
- `rustlings`: compiler-driven learning exercises.

Glossary:

- Command: input request to the simulation.
- Event: output fact produced by the simulation.
- Snapshot: serialized world state at a point in time.
- Replay: rebuilding behavior from seed plus command log.
- Determinism: same inputs produce same outputs.
- Stable ID: durable identifier used instead of long-lived references.
- Boundary: explicit interface where effects or responsibilities cross.
