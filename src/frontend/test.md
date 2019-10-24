# Testing Elm
We would like to send data from the server to the client, interpret the data as
a flash card. There are a lot of things that can go wrong. In order to gain some
confidence that some things are going right, we can write automated tests.

This chapter will setup everything that is needed to start writing tests for our
Elm code.

## Using `elm-test`
We have installed `elm-test` but we haven't used it yet. Now is a good time. Go
over to the `client` directory and run the following command

```sh
elm-test init
```

This will ask to update `elm.json` with packages that enable us to writing
tests. Agree with the proposed plan. When the command finished there is a new
directory `tests`.

```plain
tests/
└── Example.elm
```

We can rename `Example.elm` to `FlashCardTest.elm`

## run the test suite
Running the test suite amounts to executing the command

```sh
elm-test
```

It responds with the following overview

```plain
TEST RUN INCOMPLETE because there is 1 TODO remaining

Duration: 253 ms
Passed:   0
Failed:   0
Todo:     1
↓ FlashCardTest
◦ TODO: Implement our first test. See https://package.elm-lang.org/packages/elm-explorations/test/latest for how to do this!
```

The reason it reports that there is a TODO is because the generated test file
provided it. Let's change that

## Write a Test
Replace the `todo` with the following code

```elm
    describe "FlashCard"
        [ test "updating a flash card with a `Flip` message flips the flash card" <|
            \_ ->
                let
                    a_flash_card =
                        flash_card "Wettervorhersage" "Weather forecast"

                    expected =
                        flip a_flash_card

                    actual =
                        update Flip a_flash_card
                in
                Expect.equal actual expected
        ]
```

Let's start understanding this from the top. First is the `describe` function.
It accepts a `String` that should tell you what is under test and a list of other
tests.

Next we see a `test` function. It also accepts a `String` that should tell you
what we are testing. Furthermore, `test` accepts as it's second argument a
function that can do the actual testing.

In our case the function is a _closure_, i.e. an anonymous function. In the
function we use a `let`-expression to set up some variable bindings which we use
to express our expectations. This is achieved with the `Expect.equal` function.

For this to work we need to import our precious `FlashCard` functions and types.
We can do this with the following line

```elm
import FlashCard exposing (..)
```

## Verification
We have learned a lot about how a test is written, but does it work? Run the
`elm-test` command and it should report

```plain
TEST RUN PASSED

Duration: 214 ms
Passed:   1
Failed:   0
```
