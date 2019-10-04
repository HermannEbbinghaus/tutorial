# A custom type
We annotated our `view` function with it's type, but something does not feel
right. Shouldn't a flash card have a front and a back? Just a single `String`
does not cut it.

Let's remedy this with a [record][].

## Records
A record

> can hold many values, and each value is associated with a name.

Our flash card has a front and a back, so describe the flash card type with
record seems a nice fit.

Instead of accepting a `String` as the argument to our `view` function, we
should accept a record that has a `front` and a `back`.

```elm
view : { front : String, back : String } -> Html ()
```

Now the argument name of `text` isn't very well chosen anymore. Lets change it
to `card`.

```elm
view card =
   ...
```

Since we renamed the argument from `text` to `card`, we can't use `text` in the
body of the function anymore. Let's replace it with the front of the card

```elm
    div []
        [ span [] [ Html.text card.front ]
        ]
```

We now introduced a new type; a record with a `front` and a `back`, both of type
`String`. But we haven't changed to argument we are calling the `view` function
with.

```elm
main =
    view { front = "Wettervorhersage", back = "Weather forecast" }
```

## Verification
If you reload the web app once more. You should still see "Wettervorhersage".

[record]: https://guide.elm-lang.org/core_language.html
