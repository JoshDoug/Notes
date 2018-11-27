# Programming Rust - Fast, Safe Systems Development

## Chapter 1: Why Rust

A general introduction to the reasons for the language existing.

## Chapter 2: A Tour of Rust

### Downloading and Installing Rust

Rustup, a tool to install Rust and manage its versions, can be downloaded from [rustup.rs](https://rustup.rs), although pre-built packages can also be downloaded from the [rust-lang.org](https://www.rust-lang.org) site.

This install three new commands, `rustup`, `cargo`, `rustc`, and `rustdoc`.

* `cargo` is Rust's compilation/build manager, package manager, and general purpose tool. It can be used to start a new project, build and run a program from source, and manage any external libraries a project depends on.

* `rustc` is the Rust compiler, normally invoked by `cargo`, but can be used directly.

* `rustdoc` is Rust's documentation tool, which can extract documentation from comments using a specific syntax and convert them into HTML viewable in a browser.