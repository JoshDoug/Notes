# Cargo

Rust's package manager and built tool.

## Commands

Generate a new project:

* `cargo new --bin hello`
  * This command creates a new package directory named `hello`, the `--bin` flag sets this as an executable, not a library. This will also initiliase git within the project root.
  * `--vcs none` tells `cargo` not to initialise git when creating a project