# Reading List

Use this as a targeted reading guide. Read only enough to unblock the current
exercise, then return to code.

The Rust Programming Language references use the 3rd edition table of contents.
Rust for C++ Developers references use the table of contents provided in this
repo context. Design Patterns and Best Practices in Rust references use the
table of contents provided in this repo context. Hands-On Concurrency with Rust
references use the table of contents provided in this repo context.
Asynchronous Programming in Rust references use the table of contents provided
in this repo context. Practical System Programming for Rust Developers
references use the table of contents provided in this repo context. Creative
Projects for Rust Programmers references use the table of contents provided in
this repo context. For other commercial books, use the named chapter or section
in your edition's table of contents until their exact ToCs are added here.

## Core Rule

Each exercise has:

- Primary reading: read before or during the exercise.
- Reference reading: skim only if stuck.
- Web companion: use for quick lookup or examples.

## Specific Section Assignments by Curriculum Phase

Use these as the default readings for each curriculum phase. For commercial
books, use the named chapter or section in your edition's table of contents
rather than relying on chapter numbers.

### 01 Ownership

Exercises:

- `001_ownership_basics`
- revisit in `015_shared_ownership`

Primary:

- The Rust Programming Language:
  - Chapter 4, "Understanding Ownership"
  - "What Is Ownership?"
  - "References and Borrowing"
  - "The Slice Type"
- Rust for C++ Developers:
  - Chapter 3, "The Rust Safety Model"
  - "Tracking ownership"
  - "The single ownership principle"
  - "Cleaning up old data"
  - "When shallow copies are enough"
  - "Borrowing data"
  - "Borrowing immutable data"
  - "Borrowing mutable data"
  - "Specifying lifetimes"
  - "Changing how we write code"
  - "Avoiding references in structures"
  - "Using copyable structures often"
  - "Learning not to fear cloning"
  - "Using indices instead of references"

Practice / Web:

- Rustlings:
  - `move_semantics`,
  - `references`,
  - relevant ownership exercises.
- Rust by Example:
  - "Ownership and moves",
  - "Borrowing",
  - "Lifetimes" only if the exercise forces it.

Do not read yet:

- smart pointers,
- interior mutability,
- concurrency ownership.

### 02 Structs and Enums

Exercises:

- `002_structs_and_enums`
- `007_error_handling`
- `008_modules_and_crates`

Primary:

- The Rust Programming Language:
  - Chapter 5, "Using Structs to Structure Related Data"
  - "Defining and Instantiating Structs"
  - "An Example Program Using Structs"
  - "Method Syntax"
  - Chapter 6, "Enums and Pattern Matching"
  - "Defining an Enum"
  - "The `match` Control Flow Construct"
  - "Concise Control Flow with `if let`"
  - Chapter 7, "Managing Growing Projects with Packages, Crates, and Modules"
  - Chapter 9, "Error Handling" sections on `Result` and propagation.
- Rust for C++ Developers:
  - Chapter 2, "Working with Rust Syntax"
  - "Declaring variables and structures"
  - "Working with structures"
  - "Using functions and methods"
  - "Understanding generic programming"
  - "Specifying generic behavior with traits"
  - "Learning pattern matching"
  - "Using supercharged enumerations in Rust"
  - "Matching patterns"
  - Chapter 6, "Reading and Writing Files"
  - "Handling errors in Rust"

Practice / Web:

- Rust by Example:
  - "Structs",
  - "Enums",
  - "Match",
  - "Error Handling".
- Cargo Book:
  - "Packages and Crates",
  - "Workspaces" only when multiple exercises need shared configuration.

### 03 Deterministic Tick Loop

Exercises:

- `003_tick_loop`
- `009_iterators_collections`

Primary:

- The Rust Programming Language:
  - Chapter 7, modules and visibility,
  - Chapter 8, "Common Collections",
  - "Storing Lists of Values with Vectors",
  - "Storing Keys with Associated Values in Hash Maps",
  - Chapter 11, "Writing Automated Tests".
- Creative Projects for Rust Programmers:
  - Chapter 1, "Rust 2018: Productivity"
  - "Creating a Rust library crate"
  - "Building a binary crate"
  - "Running a command-line program"
  - Chapter 6, "Creating a WebAssembly Game Using Quicksilver" as deferred
    game-loop reference only
  - Chapter 7, "Creating a Desktop Two-Dimensional Game Using ggez"
  - "Understanding the ggez architecture"
  - "The game framework"
  - "Implementing the ggez game framework loop architecture"

Practice / Web:

- Rust by Example:
  - "Collections - Vectors",
  - "Collections - Hash Maps",
  - "Loops",
  - "Functions".
- Cargo Book:
  - package layout and command basics.

Do not read yet:

- ECS,
- async,
- game engine integration.

### 04 Serialization

Exercise:

- `004_serialization`

Primary:

- Practical System Programming for Rust Developers:
  - Chapter 1, "Tools of the Trade - Rust Toolchains and Project Structures"
  - "Structuring and managing software with Cargo"
  - "Documenting your project"
  - Chapter 2, "A Tour of the Rust Programming Language"
  - "Dealing with errors"
  - Chapter 6, "Working with Files and Directories in Rust"
  - "Understanding Linux system calls for file operations"
  - "Doing file I/O in Rust"
  - "Locating directory and path operations"
  - "Setting hard links, symbolic links, and performing queries"
  - Chapter 7, "Implementing Terminal I/O in Rust"
  - "Processing keyboard inputs and resizing"
  - Chapter 4, "Managing Environment, Command Line, and Time"
  - "Working with the standard library"
  - "Coding the image library"
- Serde documentation:
  - "Using derive",
  - "Attributes",
  - format crate examples such as `serde_json`.

Reference:

- Design Patterns and Best Practices in Rust:
  - Chapter 6, "Structural Patterns: Connecting and Aggregating Components"
  - "The Adapter pattern: integrating external libraries"
  - "Facades"
  - "Rust alternatives: modules and crates as facades"
  - Chapter 8, "Memento pattern: capturing and restoring state"
  - "Persistence with serialization"
  - Chapter 12, "The Result and Option patterns"
  - "Configuration loading with error composition"

Do not read yet:

- database persistence,
- binary format optimization,
- save-game migration/versioning.

### 05 Replay Testing

Exercises:

- `005_replay_testing`
- `010_state_hashing`
- `011_property_tests`
- `012_snapshot_tests`

Primary:

- The Rust Programming Language:
  - Chapter 9, "Error Handling"
  - Chapter 11, "Writing Automated Tests"
  - test organization,
  - failure messages,
  - `Result` in tests if useful.
- Rust API Guidelines:
  - naming,
  - ownership conventions,
  - dependability/predictability guidance.

Practice / Web:

- Rust by Example:
  - "Testing",
  - "Error Handling".
- `proptest` documentation:
  - getting started,
  - strategies,
  - shrinking basics.
- `insta` documentation:
  - snapshot assertions,
  - reviewing snapshot changes.

### 06 Traits

Exercise:

- `006_traits_boundaries`

Primary:

- The Rust Programming Language:
  - Chapter 10, "Generic Types, Traits, and Lifetimes"
  - "Traits: Defining Shared Behavior"
  - "Validating References with Lifetimes"
  - trait bounds,
  - generic type parameters,
  - lifetime syntax only as needed.
- Design Patterns and Best Practices in Rust:
  - Chapter 2, "Anti-Pattern: Designing for Object Orientation"
  - "Structs are not classes"
  - "Rust has a different take on polymorphism"
  - "Misusing traits"
  - "Using generic types to act like classes"
  - Chapter 6, "Proxies, decorators, and adapters"
  - Chapter 7, "Strategy pattern: swappable algorithms"
  - Chapter 10, "Sealed traits"
  - Chapter 13, "Composition over inheritance, naturally"
- Rust for C++ Developers:
  - Chapter 2, "Understanding generic programming"
  - "Using generic structures"
  - "Specifying generic behavior with traits"
  - Chapter 8, "Object-Oriented Programming"
  - "Abstracting behavior and encapsulating data"
  - "Composition over inheritance"
  - "Dynamic dispatch in Rust"
  - "Limitations of dynamic dispatch"
  - "Moving beyond object orientation"
  - "Modeling problems with Rust enums"

Reference:

- Rust API Guidelines:
  - trait naming,
  - ownership conventions,
  - flexibility and future compatibility.

Do not read yet:

- advanced lifetime-heavy APIs,
- procedural macros,
- unsafe abstractions.

### 07 Concurrency

Exercises:

- `014_concurrency_parallel_markets`
- `015_shared_ownership`
- `016_message_boundary`
- `017_async_io_edge`

Primary:

- The Rust Programming Language:
  - Chapter 15, "Smart Pointers"
  - `Box<T>`,
  - `Rc<T>`,
  - `RefCell<T>` and interior mutability,
  - Chapter 16, "Fearless Concurrency"
  - threads,
  - message passing,
  - shared-state concurrency,
  - `Send` and `Sync`.
- Hands-On Concurrency with Rust:
  - Chapter 4, "Sync and Send - the Foundation of Rust Concurrency"
  - "Sync and Send"
  - "Racing threads"
  - "Getting back to safety"
  - "Safety by exclusion"
  - "Using MPSC"
  - Chapter 5, "Locks - Mutex, Condvar, Barriers and RWLock"
  - "Read many, write exclusive locks - RwLock"
  - "Blocking until conditions change - condvar"
  - "Testing concurrent data structures"
  - Chapter 8, "High-Level Parallelism - Threadpools, Parallel Iterators and
    Processes"
  - "Thread pooling"
  - "Iterators"
  - "rayon - parallel iterators"
  - Chapter 6, "Atomics - the Primitives of Synchronization" only if a later
    exercise proves atomics are needed.

Practice / Web:

- Rayon docs:
  - parallel iterators,
  - deterministic collection/reduction patterns.
- Crossbeam docs:
  - channels,
  - scoped threads if used.

Async boundary reading:

- Asynchronous Programming in Rust:
  - Chapter 1, "Concurrency and Asynchronous Programming: a Detailed Overview"
  - "Concurrency versus parallelism"
  - "Comparing multithreading and asynchronous programming"
  - Chapter 2, "How Programming Languages Model Asynchronous Program Flow"
  - "Threads provided by the operating system"
  - "Callback-based approaches"
  - "Coroutines: promises and futures"
  - Chapter 6, "Futures in Rust"
  - "What is a future?"
  - "Leaf futures"
  - "Non-leaf futures"
  - Chapter 7, "Coroutines and async/await"
  - "Introduction to async/await"
  - "An example of hand-written coroutines"
  - "Futures made by async/await"
  - Chapter 8, "Runtimes, Wakers, and the Reactor-Executor Pattern"
  - "Improving our base example"
  - "Designing the central implementation"
  - "Step 1 - Improving our runtime design by adding a Reactor and a Waker"
  - Chapter 9, "Coroutines, Self-Referential Structs, and Pinning" only when
    pinning becomes unavoidable.
- Tokio Tutorial:
  - "Spawning",
  - "Shared state",
  - "Channels".

### 08 ECS Experiments

Exercises:

- `018_no_ecs_baseline`
- `019_minimal_ecs`
- `020_bevy_ecs_probe`
- `03x_ecs_experiment`

Primary:

- Bevy ECS / Bevy quick-start docs:
  - "ECS",
  - "Components",
  - "Resources",
  - systems,
  - queries,
  - schedules.
- Game Development with Rust and WebAssembly:
  - ECS or game-state architecture sections,
  - only after the no-ECS baseline exists.

Reference:

- Design Patterns and Best Practices in Rust:
  - Chapter 9, "Architectural Patterns"
  - "Data flows downward"
  - "Broker: controls mutations"
  - "Messages: immutable by design"
  - "Modules become interfaces"
  - "Pack lightly"
  - Chapter 13, "Use patterns natural to the language"

Do not read yet:

- rendering,
- asset systems,
- full game-engine architecture.

### 09 Godot Bridge

Exercise:

- `04x_godot_bridge`

Primary:

- godot-rust book:
  - "Introduction",
  - setup/getting started material,
  - "Hello World",
  - exporting/registering Rust classes and methods,
  - Godot object and `Gd<T>` ownership concepts as needed.
- Godot documentation:
  - GDExtension overview,
  - `.gdextension` file structure.

Reference:

- Game Development with Rust and WebAssembly:
  - boundary thinking only,
  - avoid importing browser/game-loop architecture unless needed.

Do not read yet:

- Godot UI architecture,
- full scene tooling,
- export pipelines,
- web export.

## Exercise Reading Map

| Exercise | Primary Reading | Reference Reading | Web Companion |
| --- | --- | --- | --- |
| `001_ownership_basics` | TRPL 3e Ch. 4: "Understanding Ownership"; "What Is Ownership?"; "References and Borrowing"; "The Slice Type" | Rust for C++ Developers Ch. 3: "Tracking ownership"; "Borrowing data"; "Changing how we write code" | Rustlings ownership; Rust by Example ownership |
| `002_structs_and_enums` | TRPL 3e Ch. 5: "Using Structs to Structure Related Data"; Ch. 6: "Enums and Pattern Matching" | Rust for C++ Developers Ch. 2: "Working with structures"; "Using supercharged enumerations in Rust"; "Matching patterns" | Rust by Example structs/enums |
| `003_tick_loop` | TRPL 3e Ch. 7: "Packages, Crates, and Modules"; Ch. 8: "Common Collections"; Ch. 11: "Writing Automated Tests" | Creative Projects Ch. 1: crates/command-line programs; Ch. 7: ggez architecture and game loop as reference only | Cargo Book package basics |
| `004_serialization` | Practical System Programming Ch. 2: "Dealing with errors"; Ch. 6: "Working with Files and Directories in Rust"; Ch. 4: command line/environment if building a tool | Design Patterns and Best Practices Ch. 8: "Memento pattern"; "Persistence with serialization"; Ch. 12: "Result and Option patterns" | `serde` docs |
| `005_replay_testing` | TRPL 3e Ch. 9: "Error Handling"; Ch. 11: "Writing Automated Tests" | Rust API Guidelines: predictable APIs | Rust by Example tests |
| `006_traits_boundaries` | TRPL 3e Ch. 10: "Generic Types, Traits, and Lifetimes"; Ch. 18: trait objects/state pattern as comparison | Design Patterns and Best Practices Ch. 2: "Misusing traits"; Ch. 7: "Strategy pattern"; Ch. 10: "Sealed traits" | Rust API Guidelines |
| `007_error_handling` | TRPL 3e Ch. 9: "Recoverable Errors with Result"; "Propagating Errors"; "To panic! or Not to panic!" | Practical System Programming Ch. 2: "Dealing with errors"; Ch. 8: "Handling panic, errors, and signals" | `thiserror` and `anyhow` docs |
| `008_modules_and_crates` | TRPL 3e Ch. 7: "Packages, Crates, and Modules"; Ch. 14: "Cargo Workspaces" if needed | Cargo Book: package layout | Cargo Book workspaces as needed |
| `009_iterators_collections` | TRPL 3e Ch. 8: vectors/hash maps; Ch. 13: "Iterators and Closures" | Rust Performance Book: collections only if needed | Rust by Example iterators |
| `010_state_hashing` | Serialization topics from `004_serialization` | Rust API Guidelines: deterministic behavior implications | Hashing/serialization crate docs |
| `011_property_tests` | TRPL 3e Ch. 11: "Writing Automated Tests" | Design Patterns and Best Practices Ch. 10: "Parse, don't validate"; Ch. 12: "Result and Option patterns" | `proptest` docs |
| `012_snapshot_tests` | TRPL 3e Ch. 11: "Writing Automated Tests" | Practical System Programming Ch. 6: "Doing file I/O in Rust"; "Locating directory and path operations" | `insta` docs |
| `013_data_layout_probe` | Hands-On Concurrency Ch. 2: "Sequential Rust Performance and Testing"; "Performance testing with Criterion"; Rust Performance Book: data layout | Rust for C++ Developers Ch. 10: "Understanding the performance of safe Rust"; "Moving and cloning"; "Benchmarking" | Criterion docs if measuring |
| `014_concurrency_parallel_markets` | Hands-On Concurrency Ch. 8: "High-Level Parallelism"; "Thread pooling"; "rayon - parallel iterators" | TRPL 3e Ch. 16: "Fearless Concurrency"; Hands-On Concurrency Ch. 4: "Sync and Send" | Rayon docs |
| `015_shared_ownership` | TRPL 3e Ch. 15: "Smart Pointers"; Ch. 16: shared-state concurrency | Rust for C++ Developers Ch. 3: "Avoiding references in structures"; "Using indices instead of references"; Ch. 11: "Atomic reference counting" | Rust by Example smart pointers |
| `016_message_boundary` | Hands-On Concurrency Ch. 4: "Using MPSC"; "A telemetry server"; Ch. 5: "Hopper--an MPSC specialization" | Asynchronous Programming in Rust Ch. 1: concurrency vs parallelism; Ch. 2: callbacks/coroutines/futures | Crossbeam docs |
| `017_async_io_edge` | Asynchronous Programming in Rust Ch. 6: "Futures in Rust"; Ch. 7: "Coroutines and async/await"; Ch. 8: "Runtimes, Wakers, and the Reactor-Executor Pattern" | Async Book; TRPL 3e Ch. 17 | Tokio Tutorial |
| `018_no_ecs_baseline` | Earlier simulation exercises | Design Patterns and Best Practices Ch. 9: "Data flows downward"; "Messages: immutable by design"; "Modules become interfaces" | Existing tests and notes |
| `019_minimal_ecs` | ECS concept overview from Bevy docs | Creative Projects Ch. 7: ggez game framework architecture as contrast; Game Development with Rust and WebAssembly if useful | Bevy ECS docs |
| `020_bevy_ecs_probe` | Bevy ECS docs | Rust API Guidelines: API clarity | Bevy ECS examples |
| `03x_ecs_experiment` | Bevy ECS docs for the specific question | Game Development with Rust and WebAssembly | `bevy_ecs` crate docs |
| `04x_godot_bridge` | godot-rust book | Creative Projects Ch. 5: Yew/WASM client app and Ch. 6: Quicksilver game only as presentation-boundary contrast | godot-rust examples |
| `05x_async_io` | Asynchronous Programming in Rust Ch. 7: async/await; Ch. 8: runtimes/wakers/reactor-executor; Ch. 10: "Creating Your Own Runtime" as advanced/deferred | Async Book | Tokio Tutorial |

## Book Priority by Phase

### 01 Ownership

Primary:

- The Rust Programming Language, 3rd ed.:
  - Chapter 4, "Understanding Ownership"
- Rust for C++ Developers:
  - Chapter 3, "The Rust Safety Model"

Use Rustlings for compiler-driven practice.

### 02 Structs and Enums

Primary:

- The Rust Programming Language, 3rd ed.:
  - Chapter 5, "Using Structs to Structure Related Data"
  - Chapter 6, "Enums and Pattern Matching"
  - Chapter 7, "Packages, Crates, and Modules"
  - Chapter 9, "Error Handling" sections on `Result`
- Rust for C++ Developers:
  - Chapter 2, "Working with Rust Syntax"
  - Chapter 6, "Reading and Writing Files" section "Handling errors in Rust"
- Rust by Example

Use Design Patterns and Best Practices in Rust only when the model starts
needing API boundaries.

### 03 Deterministic Tick Loop

Primary:

- The Rust Programming Language, 3rd ed.:
  - Chapter 7, "Packages, Crates, and Modules"
  - Chapter 8, "Common Collections"
  - Chapter 11, "Writing Automated Tests"
  - Chapter 13, "Functional Language Features: Iterators and Closures" as
    needed
- Rust for C++ Developers:
  - Chapter 4, "Managing Rust Projects with Cargo"
  - Chapter 5, "Data Structures"
  - Chapter 7, "Understanding Iterators"
- Creative Projects for Rust Programmers:
  - Chapter 1, "Rust 2018: Productivity"
  - "Creating a Rust library crate"
  - "Building a binary crate"
  - "Running a command-line program"
  - Chapter 7, "Creating a Desktop Two-Dimensional Game Using ggez"
  - "Understanding the ggez architecture"
  - "The game framework"
  - "Implementing the ggez game framework loop architecture"

Avoid game-engine material here.

### 04 Serialization

Primary:

- Practical System Programming for Rust Developers:
  - Chapter 2, "A Tour of the Rust Programming Language"
  - "Dealing with errors"
  - Chapter 6, "Working with Files and Directories in Rust"
  - "Doing file I/O in Rust"
  - "Locating directory and path operations"
  - Chapter 4, "Managing Environment, Command Line, and Time" only if building
    a snapshot/replay CLI
- `serde` documentation

Use readable formats before compact formats.

### 05 Replay Testing

Primary:

- The Rust Programming Language, 3rd ed.:
  - Chapter 9, "Error Handling"
  - Chapter 11, "Writing Automated Tests"
- Hands-On Concurrency with Rust:
  - Chapter 2, "Sequential Rust Performance and Testing"
  - "Testing with QuickCheck"
  - "Testing with American Fuzzy Lop" as awareness only
  - "Performance testing with Criterion"
- Rust API Guidelines

Focus on commands, events, and deterministic comparison.

### 06 Traits

Primary:

- The Rust Programming Language, 3rd ed.:
  - Chapter 10, "Generic Types, Traits, and Lifetimes"
  - Chapter 18, "Object-Oriented Programming Features" as a comparison point
  - Advanced Features: "Advanced Traits" and "Advanced Types" only if needed
- Design Patterns and Best Practices in Rust
- Rust for C++ Developers:
  - Chapter 2, "Understanding generic programming"
  - Chapter 8, "Object-Oriented Programming"

Read only enough to compare concrete APIs, generics, and `dyn Trait`.

### 07 Concurrency

Primary:

- Hands-On Concurrency with Rust:
  - Chapter 4, "Sync and Send - the Foundation of Rust Concurrency"
  - Chapter 5, "Locks - Mutex, Condvar, Barriers and RWLock"
  - Chapter 8, "High-Level Parallelism - Threadpools, Parallel Iterators and
    Processes"
- The Rust Programming Language, 3rd ed.:
  - Chapter 15, "Smart Pointers"
  - Chapter 16, "Fearless Concurrency"
  - Chapter 17, "Fundamentals of Asynchronous Programming" only for async edge
    work
- Asynchronous Programming in Rust, only for `017_async_io_edge` and later:
  - Chapter 1, "Concurrency and Asynchronous Programming: a Detailed Overview"
  - Chapter 6, "Futures in Rust"
  - Chapter 7, "Coroutines and async/await"
  - Chapter 8, "Runtimes, Wakers, and the Reactor-Executor Pattern"
  - Chapter 9, "Coroutines, Self-Referential Structs, and Pinning" only if
    pinning becomes unavoidable

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
- Creative Projects for Rust Programmers:
  - Chapter 2, "Storing and Retrieving Data" until storage experiments need
    CSV/JSON/SQLite/PostgreSQL/Redis examples
  - Chapter 3, "Creating a REST Web Service" until a service wrapper is needed
  - Chapter 4, "Creating a Full Server-Side Web App" until web UI is relevant
  - Chapter 5, "Creating a Client-Side WebAssembly App Using Yew" until browser
    presentation is relevant
  - Chapter 6, "Creating a WebAssembly Game Using Quicksilver" until browser
    game-loop comparison is useful
  - Chapter 8, "Using a Parser Combinator for Interpreting and Compiling" until
    command DSL or scenario scripting appears
  - Chapter 9, "Creating a Computer Emulator Using Nom" until binary parsing or
    emulator-style experiments are useful
  - Chapter 10, "Creating a Linux Kernel Module" as low ROI for current goals
  - Chapter 11, "The Future of Rust" as background only
- Practical System Programming for Rust Developers:
  - Chapter 9, "Managing Concurrency" unless system threads are the exercise
  - Chapter 10, "Working with Device I/O" unless hardware/device IO appears
  - Chapter 11, "Learning Network Programming" until replay is stable
  - Chapter 12, "Writing Unsafe Rust and FFI" until an FFI boundary is needed
- advanced unsafe Rust material

## Reading Notes Rule

Put book notes in `notes/rust-notes.md` only when they affect an exercise.

Put architecture conclusions in `docs/architecture-notes.md` only after code or
tests reveal a reusable lesson.
