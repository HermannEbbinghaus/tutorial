# Serialize FlashCard
We have modeled flash cards on the server. We now need to turn it into JSON
before we can send it to the client.

In this chapter we will use [serde][] to automatically serialize our flash
cards.

## Dependency
We will need two dependencies that we need to list in our `Cargo.toml`. Together
they allow us to serialize flash cards into JSON. Add `serde` and `serde_json`
to the dependencies table in `Cargo.toml`.

```toml
serde = { version = "1.0.101", features = [ "derive" ] }
sserde_json = "1.0.41"
```

## Use serde
In order to leverage the serialization capabilities of `serde_json` we need to
create a `serde` serializer. There is a very cool trick that `serde` knows that
makes this a breeze.

The first thing we need to do is to announce we our needing `serde`.

```rust
use serde::Serialize;
```

The other thing is that we need to tell `serde` that we would like it to
_derive_ serializers for our data types. We can do this by annotating both
`FlashCard` and `Face` with a `derive` annotation. E.g. `Face` would be
annotated like

```rust
#[derive(Serialize)]
pub enum Face {
    Front,
    Back,
}
```

## Verification
With the automatic part of serde done, it is good to see if serialization works
like we expect. The best way to do this is to test is. Rust integrates testing
right at the place where the source is created. Add the following code at the
end of `src/domain/mod.rs`.

```rust
#[cfg(test)]
mod test {
    use super::*;
    use serde_json;

    #[test]
    fn flash_card_can_be_serialized_to_json() {
        let flash_card = FlashCard::new("Wettervorhersage", "Weather forecast");

        let actual = serde_json::to_string(&flash_card).unwrap();

        let expected = r#"{"front":"Wettervorhersage","back":"Weather forecast","face":"Front"}"#.to_owned();
        assert_eq!(actual, expected);
    }
}
```

There is some boilerplate to let the test framework know about what we want to
test. The actual test is

```rust
        let flash_card = FlashCard::new("Wettervorhersage", "Weather forecast");

        let actual = serde_json::to_string(&flash_card).unwrap();

        let expected = r#"{"front":"Wettervorhersage","back":"Weather forecast","face":"Front"}"#.to_owned();
        assert_eq!(actual, expected);
```

It creates a `FlashCard`, serializes it to JSON with `serde_json`, sets up an
expectation, and checks it the expectation is met.

If you run

```sh
cargo test
```

it should give the all green.

[serde]: https://docs.serde.rs/serde/
