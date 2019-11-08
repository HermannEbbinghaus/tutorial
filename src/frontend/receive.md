# Receiving FlashCard
All the pieces are aligned for receiving a flash card from the server. Let's
dive right into it.

## New message
The Elm runtime needs a way to tell us that there is a new flash card from the
server. The Elm runtime wants to do that by sending the `update` function a
message. Let's create a message for that specific event.

We want to be notified from a result from the server. Since we will be receiving
it over the network, a lot of things can go wrong. To acknowledge this we will
be making use of an other Elm type: [`Result`][result]

>  A Result is the result of a computation that may fail. This is a great way to
>  manage errors in Elm.

Since the errors that occur will be coming from the network, we will be needing
types from the standard library.

```elm
import Http
```

Let's use it in our `Message`. We will be creating a message that the Elm
runtime can use to inform us.

```elm
type Message
    = Flip
    | Received (Result Http.Error FlashCard)
```

The new addition is `Received`. It has a parameter of type 
`Result Http.Error Flashcard`. This tells us that we will receive the result of
a "computation" that when successful will return a `FlashCard`.

## Creating a command
At the moment we initialize our main definition with `Nothing` as a model. We
would like to receive a flash card from the server. So we will _command_ the Elm
runtime to fetch it for use.

We do need to tell the Elm runtime how to do that. We can do that by returning
an actual command instead of `Cmd.none`. Let's focus on the let-block in the
`main` function.

```elm
let
    cmd =
        Http.get
            { url = "/api/flashcard"
            , expect = Http.expectJson Received decode
            }
in
```

Here we create a command `cmd` by calling `Http.get`. It needs a structure with
an `url` field. You might recognize the URL from when we routed it in the
server.

The structure also needs an expect field which needs to be a `Http.Expect a`.
One way of creating such an `Expect` is with the `Http.expectJson` function.

In it's turn the `expectJson` function needs two arguments. The first argument
is a way to turn a `Result Http.Error a` into a `Message`. Remember that we
created a `Recieve` message constructor. This constructor is precisely the
function we need.
The second argument is telling the Elm runtime how to transform the JSON from
the server into a type we are interested in. Remember that we created a 
`Decoder FlashCard` for that. It was bound to `decode`.

This wraps up the creation of the command. Let's focus on sending it.

## Sending a command
Sending the command is a bit anti-climactic. It is nothing more than replacing
the `Cmd.none` in the `init` field of the structure fed to the `Browser.element`
function with our `cmd`.

```elm
init = \_ -> ( Nothing, cmd )
```

## Verification
This is the moment of truth. Building the client and restarting the server
should, when you open the application, show a flash card. It isn't the by now
familiar `Wettervorhersage` one.

Instead it should show you the flash card defined on the server. It is placed
there to remind you of a job well done.

[result]: https://package.elm-lang.org/packages/elm/core/latest/Result
