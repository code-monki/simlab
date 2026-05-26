# Setup

This document describes a practical Rust setup for simlab exercises.

## Install Rust

Install Rust through `rustup`:

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

After installation, restart the shell or source the environment file printed by
the installer.

Verify:

```sh
rustc --version
cargo --version
rustup --version
```

## Toolchain

Use stable Rust by default:

```sh
rustup default stable
rustup update
```

Install common components:

```sh
rustup component add rustfmt
rustup component add clippy
rustup component add rust-src
```

Optional but useful:

```sh
rustup component add rust-docs
```

## Core Commands

Use these constantly:

```sh
cargo new exercises/example_name
cargo test
cargo test -- --nocapture
cargo fmt
cargo clippy
cargo doc --open
```

For a single exercise:

```sh
cargo test -p exercise_name
```

Use workspace commands only after the repo actually has a Cargo workspace.

## VS Code

Recommended extensions:

- `rust-lang.rust-analyzer`
- `vadimcn.vscode-lldb`
- `tamasfe.even-better-toml`
- `fill-labs.dependi`, optional dependency/version inspection

Useful settings:

```json
{
  "editor.formatOnSave": true,
  "rust-analyzer.check.command": "clippy",
  "rust-analyzer.cargo.features": "all"
}
```

Keep editor automation modest. The compiler, tests, `rustfmt`, and Clippy are
the primary feedback loop.

## Debugging

Install CodeLLDB for VS Code debugging.

For command-line debugging on macOS, LLDB is available through Xcode command
line tools:

```sh
xcode-select --install
```

Use debugger setup only when print/debug assertions are insufficient for the
exercise.

## Useful Cargo Add-Ons

Install only when needed:

```sh
cargo install cargo-edit
cargo install cargo-watch
cargo install cargo-nextest
```

Usage:

```sh
cargo add serde --features derive
cargo watch -x test
cargo nextest run
```

Do not add tooling just because it exists. Add it when it removes repeated
friction.

## Documentation

Local Rust docs:

```sh
rustup doc
```

Useful online references:

- Rust Book: https://doc.rust-lang.org/book/
- Rust by Example: https://doc.rust-lang.org/rust-by-example/
- Cargo Book: https://doc.rust-lang.org/cargo/
- Standard library: https://doc.rust-lang.org/std/
- Rust API Guidelines: https://rust-lang.github.io/api-guidelines/

## First Verification Exercise

Create a throwaway smoke-test crate:

```sh
cargo new /tmp/rust_smoke_test
cd /tmp/rust_smoke_test
cargo test
cargo fmt
cargo clippy
```

Success criteria:

- `cargo test` passes,
- `cargo fmt` runs without errors,
- `cargo clippy` runs without errors,
- VS Code shows rust-analyzer diagnostics.

## Project-Specific Notes

- Use stable Rust unless an exercise explicitly requires nightly.
- Keep dependencies minimal.
- Prefer `cargo test` over manual inspection.
- Run `cargo fmt` before committing code.
- Treat Clippy warnings as prompts for judgment, not automatic law.
- Do not start with Godot, async, ECS, or networking setup. Add those only when
  the roadmap reaches that exercise.
