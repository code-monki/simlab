# Architecture Notes

Durable architecture observations from simlab exercises.

This is not a design document written in advance. It is a lightweight
decision/observation log that grows as exercises reveal useful lessons.

## What Belongs Here

- ownership and data-shape lessons that affect future exercises,
- determinism rules discovered in practice,
- ECS tradeoffs after comparing implementations,
- replay and serialization decisions,
- Godot boundary decisions,
- concurrency patterns that worked or failed,
- abstractions that earned their place.

## What Does Not Belong Here

- raw Rust syntax notes,
- temporary debugging notes,
- book summaries,
- implementation TODOs,
- speculative architecture before an exercise proves it matters.

## Entry Template

```md
### YYYY-MM-DD - Short Title

Context:
What exercise or question produced this note?

Observation:
What did we learn?

Decision:
What should we do differently next time?

Status:
Provisional | Accepted | Revisit
```

## Notes
