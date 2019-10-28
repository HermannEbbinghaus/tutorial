# Sending FlashCard
We are capable to serialize a flash card to JSON. The next step is to send it to
the frontend. We will do this by making an end point where the frontend can
request a flash card.

This probably will be a somewhat longer chapter because there are a lot of
moving pieces. So make sure to fetch yourself a nice drink and strap in for the
ride.

## Dependencies
We will be using some dependencies that need to be declared in the `Cargo.toml`.
Specifically the following dependencies

```toml
hyper = "0.12.35"
mime = "0.3.14"
```

## Create a new route
The next step is to dream up a new route. Where should the frontend get a
flash card from. We are offering an API and it is reasonable to adhere to the
[REST][rest] model. One suggestion is to choose `/api/flashcard`.

In `main.rs` we have configured a router. We can extend it with a route for a
flash card

```rust
route.get("/api/flashcard").to(get_flash_card);
```

the `get_flash_card` handler is something that does not yet exist. But it is
something we like. In order to use it we should do

1. Announce the use of an external crate. In `main.rs` at the top add

```rust
extern crate flashcard_server;
```

2. Use the `get_flash_card` function. Also in `main.rs` add an other `use`
   expression
   
```rust
use flashcard_server::handler::flashcard::*;
```

## Create a new module
From the usage we learn that there should be a `handler`. So we need to announce
that in out `lib.rs`

```rust
pub mod handler;
```

We will create this module by using a sub-directory `handler` that contains a
`mod.rs` file. We probably are going to create a lot of handlers for this
applications so the contains of the `handler/mod.rs` could look like this.

```rust
pub mod flashcard;
```

This just announces an other module. This time do, we are not creating a
sub-directory. Instead we are creating a file named `flashcard.rs` in the
`handler` directory. This is the other way of creating a module.

`flashcard.rs` should have our definition of `get_flash_card`.

## `get_flash_card`

A handler has a particular signature for the gotham web framework to work with
it. In goes a `State`, a provided by gotham. At goes a tuple of a state, and
whatever you want to return. All in all this amounts to the following code.

```rust
use gotham::state::State;
use crate::domain::FlashCard;


pub fn get_flash_card(state: State) -> (State, FlashCard) {
    let flash_card = FlashCard::new("Kodieren", "Encode");

    (state, flash_card)
}
```

Here we create a new flash card and remove it with the state unaltered.

## Response
The web is build about requests and responses. Each response can be of a certain
[_MIME_][mime] type, but it can't know everything that could be send back. So we
will need to tell gotham how to create a real response from a flash card.

There is a [_trait_][trait] that you can implement that does precisely that. It
is called `IntoResponse` and it will allow us to specifiy how to turn a flash
card into a response.

In order to use it we need to declare it, and related type.

```rust
use gotham::handler::IntoResponse;
use gotham::helpers::http::response::create_response;
use gotham::state::State;
use hyper::{Body, Response, StatusCode};
```

Next we should implement the `IntoResponse` trait.

```rust
impl IntoResponse for FlashCard {
    fn into_response(self, state: &State) -> Response<Body> {
        create_response(
            state,
            StatusCode::OK,
            mime::APPLICATION_JSON,
            serde_json::to_string(&self).expect("serialized flash card"),
        )
    }
}
```

Here we use the `create_response` function to create a valid response, which
contains JSON with a body of a string representation of the flash card.

## Verification
When you restart the application and open a terminal you should be able to
execute the following curl command

```sh
curl -X GET http://localhost:8886/api/flashcard
```

and the server should respond with

```plain
{"front":"Kodieren","back":"Encode","face":"Front"}⏎
```

[rest]: https://en.wikipedia.org/wiki/Representational_state_transfer
[mime]: https://en.wikipedia.org/wiki/MIME
[trait]: https://doc.rust-lang.org/1.8.0/book/traits.html
