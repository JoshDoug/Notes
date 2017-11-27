# The Rust Programming Language Book

Notes from the 2nd edition of TRPL.

* [TRPL 2nd Edition](https://doc.rust-lang.org/book/second-edition/)

## 1. Introduction

Rust, safer than C, expressive like Python.

### 1.1 Installation

Installing on Rust on Linux or macOS can be done by running a single line in a shell copied from [rustup.rs](https://www.rustup.rs): `curl https://sh.rustup.rs -sSf | sh`. This installs the rustc compiler, documentation, crates, and rustup itself which can be used to manage and update rust installations. This also adds `~/.cargo/env` to the `$PATH` environment variable. On Windows there's an exe to download and install.

* Updating: `rustup update`
* Uninstalling: `rustup self uninstall`
* Local Documentation: `rustup doc`
* Version: `rustc --version` or `rustc -V` (lowercase v is for verbose output)
  * Output: `rustc 1.22.1 (05e2e1c41 2017-11-22)`:`rustc x.y.z (commit-hash yyyy-mm-dd)`
