# Updating the model
Let's work on applying the Elm architecture and update the model.

## Message
We first start to think about the message our model understands. At the moment
we are only interested in flipping a card. A good message would be `Flip`. Let's
start from there

```elm
type Message
    = Flip
```

Now we created the ability to express the fact that we want to change our model.

## Model
We keep talking about our model. We know that it is a flash card, but that could
change in the future. Aligning our code with the Elm way has some benefits. So
let's introduce an alias.

```elm
type alias Model =
    FlashCard
```

This way we can talk about `Model` in our signatures and it will align with Elm,
but we haven't lost the ability to address is as a `FlashCard`.

## Update
Let's create an `update` function. The signature of the update model is
determined by Elm. It should benefits

```elm
update : Message -> Model -> Model
```

We give it a `Message` and a `Model`. Update will return a `Model` depending on
the two. The implementation is straight forward, since there is only one
instance of the `Message` type.

```elm
update message model =
    case message of
        Flip ->
            flip model
```

Match on the message, and for each case, even when there is only one, determine
what to do. The `flip` function is what we need in the `Flip` case.

## Wire it all together
Now we need to tell Elm how these parts work together. There is a 
[`Browser` module][browser] that offers different programs. We will be
interested in `sandbox`.

In order to be able to use the `Browser` module we need to import it.

```elm
import Browser
```

The sandbox needs a structure with the following fields

* `init`. The initial model.
* `view`. The view function used to display the model.
* `update`. an finally the update function used.

We all have those in place. So we can

## Verification
Change the `main` variable to

```elm
main =
    let
        model =
            flash_card "Wettervorhersage" "Weather forecast"
    in
    Browser.sandbox
        { init = model
        , view = view
        , update = update
        }
```

And now we can finally flip the flash card.

[browser]: https://package.elm-lang.org/packages/elm/browser/latest/
