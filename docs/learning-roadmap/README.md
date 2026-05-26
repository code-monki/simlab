# Rust Learning Roadmap

This roadmap is split into focused documents so it can be used as a working guide instead of a single long reference file.

## Start Here

1. Read [foundation.md](foundation.md).
2. Follow the sequence in [curriculum.md](curriculum.md).
3. Pick the next exercise from [exercises.md](exercises.md).
4. Use [reading-list.md](reading-list.md) to choose the minimum useful reading.
5. Use [resources.md](resources.md) only to unblock the current exercise.
6. Check [architecture.md](architecture.md) before adding concurrency, ECS, Godot, or replay infrastructure.
7. Use [reference.md](reference.md) for anti-patterns, milestones, cadence, and glossary.

## Roadmap Sequence

1. Ownership
2. Structs and enums
3. Deterministic tick loop
4. Serialization
5. Replay testing
6. Traits
7. Concurrency
8. ECS experiments
9. Godot bridge

## Three-Part Map

The roadmap can also be read as three larger parts.

### Part 1: Foundation, Architecture, and Exercises 001-020

Use this part to establish the working model and get through the core Rust
learning sequence.

Includes:

- purpose and scope,
- engineering philosophy,
- simlab operating model,
- repo conventions,
- competency model,
- Rust learning strategy,
- reading roadmap,
- exercise catalog 001-020,
- ownership, borrowing, enums, traits, testing, serialization, and smart
  pointers,
- success criteria,
- anti-patterns,
- milestone definitions.

Primary files:

- [foundation.md](foundation.md)
- [curriculum.md](curriculum.md)
- [exercises.md](exercises.md)
- [resources.md](resources.md)
- [reference.md](reference.md)

### Part 2: Systems, Concurrency, ECS, and Integration

Use this part once the headless deterministic core is taking shape.

Includes:

- concurrency model,
- deterministic systems guidance,
- ECS and data-oriented design,
- persistence,
- replayability,
- profiling and performance,
- Godot integration,
- architecture spikes,
- networking foundations,
- async timing.

Primary files:

- [architecture.md](architecture.md)
- [curriculum.md](curriculum.md)
- [resources.md](resources.md)

### Part 3: Project Tracks and Reference

Use this part to choose where the Rust work goes next after the core learning
sequence is productive.

Includes:

- Traveller Economic Simulation track,
- Mayday tactical combat track,
- Stock analyzer track,
- Drone swarm manager track,
- specialization matrix,
- crate guidance,
- rabbit-hole management,
- cadence recommendations,
- proficiency model,
- appendices, cheat sheets, and glossary.

Primary files:

- [architecture.md](architecture.md)
- [resources.md](resources.md)
- [reference.md](reference.md)

## Documents

- [Foundation](foundation.md): purpose, scope, assumptions, engineering philosophy, operating model, repo structure, and competency model.
- [Curriculum](curriculum.md): phase-based learning path.
- [Exercises](exercises.md): detailed exercise catalog and exercise template.
- [Reading List](reading-list.md): exercise-to-reading map.
- [Resources](resources.md): books, web references, chapter-topic mapping, and recommended crates.
- [Architecture](architecture.md): spikes, project tracks, testing, performance, concurrency, ECS, Godot, networking, replay, and determinism.
- [Reference](reference.md): anti-patterns, milestones, cadence, deferred topics, commands, tools, and glossary.

## Restart Primer

When returning after a break:

1. Read `AGENTS.md`.
2. Read this index and the current phase in `curriculum.md`.
3. Open the latest exercise notes.
4. Run the current exercise tests.
5. Write down the next smallest assumption to validate.
6. Work for one short session.
7. Record friction, lessons, and the next follow-up.

Default next action:

```text
Pick the earliest unfinished roadmap step.
Create or resume one tiny exercise.
Write a test before expanding scope.
Capture the lesson before moving on.
```
