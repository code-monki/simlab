# Learning Roadmap Foundation

## Purpose

Become productive with Rust quickly by building small, disposable exercises that
support deterministic simulation systems.

This is not a beginner programming roadmap. It assumes an experienced software
architect/developer with broad language experience and deep OOA/OOD/OOP
background. The focus is Rust-specific judgment: ownership, data modeling,
traits, explicit effects, deterministic execution, testing, serialization,
replay, concurrency, ECS tradeoffs, and Godot integration.

## Scope

In scope:

- Rust as an authoritative simulation core.
- Deterministic economic simulation probes.
- Small exercises that validate architectural assumptions.
- Replay, serialization, ECS, concurrency, and integration boundaries.
- Documentation of friction and lessons learned.

Out of scope for the early roadmap:

- production-quality applications,
- full UI development,
- feature completeness,
- premature optimization,
- web apps,
- blockchain-specific systems,
- broad framework exploration without a concrete exercise.

## Operating Assumptions

- Rust is being learned to build robust simulation cores.
- Godot is a presentation layer, not the first design driver.
- Python remains useful for exploration, prototyping, notebooks, and analysis.
- Exercises are disposable unless they prove a durable pattern.
- Determinism matters more than feature count.
- Tests are the main evidence that an architectural assumption holds.
- The first useful milestone is a headless deterministic mini market.

## Engineering Philosophy

The foundational design principle is elegant simplicity.

Systems should be built so their behavior is easy to reason about, defects are
visible near their cause, and fixes are straightforward. Functions and methods
are discrete elements, similar to components on a circuit board. Modules, crates,
and subsystems package those elements. Interfaces, messages, commands, events,
and data flow are the wiring between contact points.

This aligns with Alan Kay's original framing of object orientation as
communicating components, not inheritance hierarchies. For Rust work in this
repo, that maps naturally to data models, traits, commands, events, explicit
ownership boundaries, and deterministic transformations.

Abstraction discipline matters:

- build the concrete version first,
- observe the friction,
- name the repeated shape,
- extract only the abstraction that has earned its place,
- keep the abstraction small enough to delete if it was wrong.

Elegance is not achieved by adding layers. Elegance is achieved when the system
has no unnecessary parts and the necessary parts fit together plainly.

## Simlab Operating Model

Use this loop:

1. Pick a tiny exercise.
2. State the assumption being tested.
3. Implement the smallest useful version.
4. Write tests.
5. Observe Rust friction.
6. Record lessons learned.
7. Refactor understanding.
8. Move to the next exercise.

Primary project target: Traveller Economic Simulation.

Reasoning:

- It matches the repository purpose.
- It exercises determinism, replayability, serialization, ECS tradeoffs, and
  concurrency.
- It can stay headless while the Rust core matures.
- Godot can remain a later presentation layer.

## Learning Strategy

Do not read every book front to back.

Use books and web resources to unblock exercises. For each phase, read the
minimum material needed to attempt the next probe. The goal is Rust productivity,
not book completion.

## Repo Structure

Suggested shape:

```text
docs/
  learning-roadmap/
    foundation.md
    curriculum.md
    exercises.md
    resources.md
    architecture.md
    reference.md
  architecture-notes.md
  engineering-principles.md

notes/
  rust-notes.md
  ownership-observations.md
  gotchas.md

exercises/
  ownership_001_values_refs_ids/
  model_001_goods_prices/
  model_002_order_state/
  sim_001_fixed_tick/
  sim_002_market_tick/
  sim_003_commands_events/
  sim_004_replay/
  persist_001_snapshot/
```

## Rust Competency Model

Productive enough for this repo means being able to:

- create a small crate without fighting Cargo,
- model domain state with structs, enums, and newtypes,
- choose owned values, borrows, or IDs intentionally,
- write tests that lock down deterministic behavior,
- use `Result` and custom errors without cluttering the design,
- serialize and replay a small world state,
- design narrow trait boundaries without over-generalizing,
- explain when `dyn Trait` is appropriate,
- use concurrency without changing deterministic results,
- keep Godot or Python at the boundary instead of in the core.
