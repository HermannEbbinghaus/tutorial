# Simple Server
In this chapter we are going to create a simple server. Our goal is to make it
greet us when we make a request.

## Gotham
We will be leveraging the Rust eco-system instead of reinventing the wheel our
self. There are a lot of packages available to us. They live at [crates.io][].
One of the packages we will be using is Gotham.

[Gotham][gotham] is a

> flexible web framework that promotes stability, safety, security and speed.

## Add dependency
Before we can use a package we need to declare it as a dependency. This is done
in the `Cargo.toml`. We need to add our dependency to the `dependencies` table.

```toml
[dependencies]
gotham = "0.4.0"
```

## Hello, world!
Next we will create a minimal server that responds with `Hello, world!` with
every request.

Change `main.rs` with

```rust
extern crate gotham;

use gotham::state::State;

const HELLO_WORLD: &'static str = "Hello World!";

pub fn say_hello(state: State) -> (State, &'static str) {
    (state, HELLO_WORLD)
}

pub fn main() {
    let addr = "localhost:8886";
    println!("Listening for requests at http://{}", addr);
    gotham::start(addr, || Ok(say_hello))
}
```

This is taken from the hello-world example from the Gotham page.

## Verification
Run the server with the command

```sh
cargo run
```

This will compile `main.rs` and the transitive dependencies. This can take some
time. When it finishes it announces

```plain
Listening for requests at http://localhost:8886
```

Now open a browser and navigate to
[`http://localhost:8886`](http://localhost:8886) and you will be greeted with an
`Hello, world!`.

[crates.io]: https://crates.io/
[gotham]: https://gotham.rs/
