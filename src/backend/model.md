# Model on server
If we want the server to send us a flash card, the server first have to have a
notion of what to send.

In this chapter we our going to model flash cards on the server.

## lib.rs
The skeletal project generated a `main.rs`. It would be possible to write all
the necessary code in this file, but that would quickly become unmaintainable.
Rust recognizes this fact and allows for code to write in a library instead.

Create a file `lib.rs` in the `src` directory with the following content

```rust
mod domain;
```

The above definition defines a module called `domain`. Let's go ahead and create it.

## domain/mod.rs
There are various ways to define a module. One way is to create a directory in
the `src` directory with the same name as the module, in our case `domain`, and
a file `mod.rs` in that directory.

## struct
We would like to focus on modeling flash cards on the server. We have some
experience on the client side. Luckily, that experience translates very well to
the server side.

Rust also knows about records. Rust calls them structs. Take a look at the
following code

```rust
pub struct FlashCard {
    front: String,
    back: String,
    face: Face,
}
```

You probably recognizes a lot from Elm's `FlashCard`. There are two noteworthy
things two point out.

First the `pub` keyword. This allows other modules to use this struct. The other
is the `Face` type. Rust doesn't know about it. So we better define it right
away.

## enum
Our modeling experience on the Elm side helps us on the Rust side as well.
Again, there is a naming difference, but take a look at `Face`

```rust
pub enum Face {
    Front,
    Back,
}
```

## Constructor
When we created our model in Elm, we quickly realized that it becomes tedious to
spell out the structures every time we needed it. To mitigate that we created a
constructor. Let's do the same in Rust.

It looks a bit different, but is similar enough that it is recognizable.

```rust
impl FlashCard {
    pub fn new<S>(front: S, back: S) -> Self where S: Into<String> {
        Self { front : front.into(), back : back.into(), face : Face::Front }
    }
}
```

The essence is the following line

```rust
        Self { front : front.into(), back : back.into(), face : Face::Front }
```

It looks a bit strange with the `front.into()` and `back.into()` but that is
because Rust knows different kinds of [strings][]. The input type `S :
Into<String>` allows us to conveniently add any type that knows how to transform
itself into a `String`.

## Verification
We haven't changed our server and only added code. It should still be able to
build our code.

```rust
cargo build
```

The command above should do just that. Other than given some warnings about our
new code not being used, it should compile our code.

[strings]: https://doc.rust-lang.org/rust-by-example/std/str.html
