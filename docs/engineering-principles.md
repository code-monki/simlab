# Engineering Principles

## Elegant Simplicity

The foundational design principle for this repository is elegant simplicity.

Systems should be constructed so their behavior is easy to reason about, defects
are visible near their cause, and fixes are straightforward. The desired result
is not minimal code for its own sake. The desired result is a system whose parts
fit together cleanly enough that incorrect behavior stands out.

## Circuit Board Model

Think of functions and methods as discrete elements, similar to resistors,
capacitors, and other circuit components.

Think of modules, crates, and subsystems as packages of those elements.

Interfaces are the contact points. Messages, commands, events, and data flow are
the wiring between those contact points.

Good design means the wiring is legible:

- each element has a clear purpose,
- interfaces are narrow and explicit,
- data flow is visible,
- side effects are intentional,
- components can be tested in isolation,
- failure modes are close to the component that caused them.

This aligns with Alan Kay's original framing of object orientation as systems of
communicating components, not inheritance hierarchies. For Rust work in this
repo, that maps naturally to data models, traits, commands, events, and explicit
ownership boundaries.

## Design Bias

- Prefer simple components with obvious contracts.
- Prefer explicit messages over hidden shared state.
- Prefer deterministic transformations over ambient effects.
- Prefer composition over inheritance-shaped designs.
- Prefer tests that validate the wiring between components.
- Prefer refactoring when a component's purpose becomes unclear.

The goal is robust, performant software where complexity is present only when it
earns its place.

## Abstraction Discipline

Premature abstraction is a constant temptation and should be resisted
deliberately.

Do not introduce abstractions because they might be useful later. Introduce them
only when the current code proves that they remove real complexity, clarify a
real boundary, prevent meaningful duplication, or make a tested behavior easier
to reason about.

This requires slowing down to go fast:

- build the concrete version first,
- observe the friction,
- name the repeated shape,
- extract only the abstraction that has earned its place,
- keep the abstraction small enough to delete if it was wrong.

Elegance is not achieved by adding layers. Elegance is achieved when the system
has no unnecessary parts and the necessary parts fit together plainly.
