# Cargo

Rust's package manager and built tool.

## Commands

Generate a new project:

* `cargo new --bin hello`
  * This command creates a new package directory named `hello`, the `--bin` flag sets this as an executable, not a library. This will also initiliase git within the project root.
  * `--vcs none` tells `cargo` not to initialise git when creating a project

Running a project:

* `cargo run`
  * This command can be run from any directory in the package to build and run the program.
  * This builds the executable and places it in the `target` subdirectory at the top of the package.