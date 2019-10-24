# Skeletal Rust project
We used our frontend tooling to create a skeletal project for us. Just like with
our frontend, our backend tooling allows us to do the same.

## cargo new
The `cargo` command is the go to place for Rust development.

```sh
cargo --help
```

Shows all sort of sub-commands available. The one we are interested in is the
`cargo new` command.

```
cargo new --help
```

shows use

> Create a new cargo package at <path>

It has some options that we are going to use. The following command

```plain
cargo new --bin --name 'flashcard-server' server 
```

will produce the structure below.

```plain
server
├── Cargo.toml
└── src
    └── main.rs
```

The `Cargo.toml` files describes the project and there already is a `main.rs`
source file scaffold.

## Verification
Go into the `server` directory and run the

```sh
cargo run
```

command. This will compile your sources and greet you with a friendly `Hello, world!`.
