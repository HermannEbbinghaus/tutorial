# Moving out of the sandbox
Up until now we have been relying on Elm's sandbox. The sandbox allows for a
user to interact with the component in a limited way. For example, it is **not**
possible to make an HTTP call.

We would like to do just that, so it is time to move out of the sandbox.

## `Browser.element`
The next step up on the Elm ladder is [`Browser.element`][element]. From the
element documentation we learn

> Unlike a sandbox, an element can talk to the outside world in a couple ways

We will give a brief description of those ways, paying attention which are
relevant for us.

### Commands
Commands are a way to request the Elm runtime to do a task. Making an HTTP call
is an example.

Commands are a way to describe a certain action. This keeps your program _pure_,
i.e. function always return the same value when called with similar arguments.
The Elm runtime will respond by performing the command you specified.

The Elm runtime notifies you of the result by calling the update function.

### Subscriptions
Sometimes you are interested in something your component is not responsible for.
E.g. ticking of time, or mouse clicks. If you are interested in these things you
can _subscribe_ to these events.

Again, Elm runtime notifies you of an event from a subscription by calling the
update function.

### Flags
Let's we are creating our app and our customers want there name embossed on the
flash card. The functionality would not change, besides that our model would
keep track of the customer name.

One way to configure our application is by sending flags. This allows an
application to change behavior right from the start. E.g. one could pass in via
a flag the address one should retrieve flash cards from.

### Ports
If you want even more communications with the outside world, ports allow you to
send and receive messages. They are the defacto way of communicating with
anything outside the control of the Elm runtime.

For example if you want to make use of a JavaScript library that does not have
an native Elm counterpart one should use ports to establish a bridge

## Updating `update`
The `update` function needs to be updated because it needs to be able to fire of
commands. This dual responsibility is reflected in the signature. For
completeness we show the current signature.

```elm
update : Message -> Model -> Model
```

Besides updating the model, We could potentially also create a command, to be
executed by the Elm runtime. The new signature is


```elm
update : Message -> Model -> ( Model, Cmd Message )
```

This will break the implementation. For now it is enough to create a tuple with
as second component `Cmd.none`.

```elm
Flip ->
    ( Maybe.map flip model, Cmd.none )
```

## Default subscriptions
At the moment we don't want to subscribe to anything. We can tell Elm that by
configuring `Sub.none`, similar to `Cmd.none`.

In order to prepare for future extension we will be creating a subscriptions
definition that we will reference when we are creating a `Browser.element`.

```elm
subscriptions : Model -> Sub Message
subscriptions _ =
    Sub.none
```

## Updating init
When we will introduce a `Browser.element` our current `init` field from the
`Browser.sandbox`does not suffice anymore. Again. We could kick off our entire
process by doing a request. Furthermore, our initial model could depend on some
flags.

For now we want to ignore the flags, and don't want to send a command. It
suffices to change our init to.

```elm
init = \_ -> ( model, Cmd.none )
```

## Replace `Browser.sandbox` with `Browser.element`
Now we can replace `Browser.sandbox` with `Browser.element`. It will still
complain, because it is missing a `subscriptions` field. But we prepared for
that.

All in all our program definition looks like

```elm
Browser.element
    { init = \_ -> ( Nothing, cmd )
    , view = view
    , update = update
    , subscriptions = subscriptions
    }
```

## Verification
Building the app and opening the application would still allow you to learn the
translation of `Wettervorhersage`.

[element]: https://package.elm-lang.org/packages/elm/browser/latest/Browser#element
