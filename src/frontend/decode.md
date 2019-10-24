# Decoding a FlashCard
We would like the let the server decide which flash card to show. In order for
that to work, we need to be able to receive JSON data and decode that into a
`FlashCard`.

This chapter we will be working on that.

## json package
There is a [`json` package][json] that will help us decode, and encode, JSON
into datatypes that we are interested in. Before we can use it we need to
install it.

```sh
elm install elm/json
```

## `Json.Decode`
We will be using the `Json.Decode` module from the `json` package. Because we
want to avoid typing `Json.Decode` everywhere when we want to refer to a type
from that module, we are importing it with a different name.

Since we will be defining a `Decoder` we will expose that type into our
name space. 

```elm
import Json.Decode as Decode exposing (Decoder)
```

## `Decoder`
We want a `Decoder` for `FlashCard`. The type therefore should be

```elm
decode : Decoder FlashCard
```

Decoders work by composing primitive decoders into more elaborate once.
Primitive decoders include

* `Decode.string` that will decode a string value.
* `Decode.int` that will decode an int value.
* `Decode.bool` that will, well you can probably guess what type of value it
  decodes.

More elaborate decoders are for example `Decode.map` or variants. It's signature
is 

```elm
Decode.map : (one -> other) -> Decoder one -> Decoder other
```

It takes a function that maps one type into the other, a decoder for one and
will produce a decoder for other. Under the cover the one decoder is used and
when successful the transformation is applied to the result.

## JSON
Below we will give an example of the JSON we expect to receive. It probably does
not surprise you that it looks like

```json
{ "front": "Wettervorhersage", "back": "Weather forecast", "face": "front" }
```

## Decoder FlashCard
We will create a decoder that will ignore the face field of the JSON. When we
have a little more experience we will come back and decode that as well. That
means that the decoder becomes

```elm
decode : Decoder FlashCard
decode =
    Decode.map3 FlashCard
        (Decode.field "front" Decode.string)
        (Decode.field "back" Decode.string)
        (Decode.field "face" <| Decode.succeed Front)
```

We use `Decode.map3` and the `FlashCard` constructor, which got automatically
created when we introduced the type alias, to map three different values into a
`FlashCard`.

We extensively use the [`Decode.field`][field] decoder. It

> decodes a JSON object, requiring a particular field. The object can have other
> fields. Lots of them! The only thing this decoder cares about is if a field is
> present and that the value there is an of a certain type. 

Lastly we use `Decode.succeed` to hard code the face value to be Front.

## Verification
We have created a decoder but how do we know that it behaves correctly? We can
write a test to see if our decoder can decode some JSON.

In `tests/FlashCardTest.elm` write the following code after our other test.

```elm
        , test "decode a flash card from JSON" <|
            \_ ->
                let
                    input = """{ "front": "Wettervorhersage", "back": "Weather forecast", "face": "back" }"""

                    expected =
                        flash_card "Wettervorhersage" "Weather forecast"
                        |> Ok

                    actual =
                        decodeString FlashCard.decode input
                in
                Expect.equal actual expected
```

and all the tests should still work when you import

```elm
import Json.Decode exposing (decodeString)
```

[json]: https://package.elm-lang.org/packages/elm/json/latest/
[field]: https://package.elm-lang.org/packages/elm/json/latest/Json-Decode#field
