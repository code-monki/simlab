Purpose
--------
This repository is for Rust learning, architectural experiments,
and simulation validation.

Goals
-----
- Learn Rust for deterministic simulation systems
- Validate architectural assumptions
- Explore ECS, replayability, serialization, concurrency
- Keep exercises disposable

Non-goals
---------
- Production-quality application
- UI development
- Premature optimization
- Feature completeness

Engineering Rules
-----------------
- KISS
- Deterministic behavior preferred
- Small isolated exercises
- Document lessons learned
- Prefer correctness and clarity over cleverness
- Validate assumptions with tests
- Avoid abstractions until concrete exercises prove the need

Architecture Philosophy
-----------------------
Rust = authoritative simulation core
Godot = presentation layer
Python = experimentation/prototyping

Architecture Notes Discipline
-----------------------------
- Use docs/architecture-notes.md as a durable observation log
- Add notes only after an exercise reveals a reusable lesson
- Capture context, observation, decision, and status
- Do not use architecture notes for raw syntax notes, temporary debugging,
  book summaries, TODOs, or speculative design
- Keep speculative architecture out until code/tests expose the need

Workflow
--------
1. Tiny exercise
2. Observe friction
3. Record lessons
4. Refactor understanding
5. Move to next exercise
