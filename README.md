# Simlab

Simlab is a Rust learning and architecture-validation workspace for
deterministic simulation systems.

The goal is to become productive with Rust by building small, disposable exercises that test specific assumptions around simulation design, replayability, serialization, concurrency, ECS, and eventual Godot integration.

## Operating Model

Work in small loops:

1. Pick a tiny exercise.
2. State the assumption being tested.
3. Implement the smallest useful version.
4. Validate it with tests.
5. Record friction and lessons learned.
6. Move to the next exercise.

Throwaway code is allowed. Unrecorded lessons are not useful.

## Architecture Bias

- Rust is the authoritative simulation core.
- Godot is a presentation layer.
- Python is for experimentation, prototyping, and analysis.
- Deterministic behavior is preferred.
- Correctness and clarity beat cleverness.
- Abstractions should be earned by concrete friction.

The guiding philosophy is elegant simplicity: small components, explicit interfaces, visible data flow, and behavior that is easy to reason about.

## What This Is Not

This is not a production application, UI project, or feature-complete game. It is not a place to optimize before behavior is correct, or to add frameworks before a small exercise proves the need.

## Documentation

- [Learning roadmap](docs/learning-roadmap/README.md)
- [Engineering principles](docs/engineering-principles.md)
- [Architecture notes](docs/architecture-notes.md)
- [Rust notes](notes/rust-notes.md)
- [Ownership observations](notes/ownership-observations.md)
- [Gotchas](notes/gotchas.md)

## First Target

The initial project target is a headless Traveller-style economic simulation:

- goods,
- markets,
- agents,
- fixed ticks,
- seedable RNG,
- command log,
- event log,
- replay test,
- snapshot round trip.

The first real success condition is simple: same seed plus same commands produces the same final state, proven by tests.
