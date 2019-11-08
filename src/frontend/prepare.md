# Prepare to receiving a FlashCard
We have transformed our sandbox into an actual element. This allows us to make
HTTP calls. We could put that to good use because our server is ready to send us
a flash card, we only need to ask.

In this chapter we will make a request for a flash card to our server, receive
it and display it in our client.

## Changing the model
Currently we assume we always have a flash card. Put since we are planning to
receive one over the internet, things could go wrong. In order to be honest
about this fact, we are going to change our model.

Currently we our model is an alias for `FlashCard`

```elm
type alias Model =
    Maybe FlashCard
```

Let's modify it to reflect that we _maybe_ don't have a flash card all the time.

```elm
type alias Model =
    Maybe FlashCard
```

This breaks a few things that we need to fix.

## `view`
The `view` accepts a model so we need to adopt it to our new definition.

Earlier we could just take the flash card and display a meaningful
representation. Now we first must make sure that we actual have a flash card and
show a helpful message when we don't.

We can achieve this with a pattern match. `Maybe` has two constructors, in our
case `Just card`, where `card` is a `FlashCard` or `Nothing`. So our `view`
functions needs to start with a pattern match like so

```elm
view : Model -> Html.Html Message
view model =
    case model of
        Just card ->
            -- details below

        Nothing ->
            -- details below
```

The `Just card` branch should do what we always did, changed to reflect the use
of the `card` variable.

```elm
let
    text =
        case card.face of
            Front ->
                card.front

            Back ->
                card.back
in
div []
    [ span [] [ Html.text text ]
    , button [ Event.onClick Flip ] [ Html.text "flip" ]
    ]
```

When we don't have a flash card, i.e. in the `Nothing` branch we need to report
this fact to the user.

```elm
div [] [ span [] [ Html.text "No flash card to show" ] ]
```

This wraps up our `view` function.

## `update`
Our `update` function also accepts a model, so it needs to change as well.
Before we could just call the `flip` function on our model when we received a
`Flip` message.

Now, because it is wrapped in a `Maybe` type, this will not work. The types
don't work out.

Luckily the [`Maybe` type][maybe] has a convenient function called [`map`][map].
The signature of `map` is

```elm
(a -> b) -> Maybe a -> Maybe b
```

which allows use to

> Transform a Maybe value with a given function

I.e. allow us to apply a function to `Maybe FlashCard` with out unpacking it
first. Our update function can therefore be

```elm
update : Message -> Model -> ( Model, Cmd Message )
update message model =
    case message of
        Flip ->
            ( Maybe.map flip model, Cmd.none )
```

## Initial model
In our `main` function we our creating a model by hand. At the moment it is just
a flash card, but it needs to account for the fact that maybe it isn't present.
The most dramatic change would be to pick `Nothing` as our starting value.

```elm
    Browser.element
        { init = \_ -> ( Nothing, Cmd.none )
        , view = view
        , update = update
        , subscriptions = subscriptions
        }
```

## Verification
When you build the client and serve it from the server, this time you should see
a message that there isn't a flash card.

Let's remedy that in the next chapter.

[maybe]: https://package.elm-lang.org/packages/elm/core/latest/Maybe
[map]: https://package.elm-lang.org/packages/elm/core/latest/Maybe#map
