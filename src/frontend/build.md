# Building the frontend
A browser can not execute Elm. We first must make our Elm code into a form that
the browser will understand.

Luckily the `elm` command knows how to do that.

## `elm` make
There is a sub-command that is able to create files that the browser knows
about. It is called `elm make`. Running `elm make --help` show 

```plain
The `make` command compiles Elm code into JS or HTML:

    elm make <zero-or-more-elm-files>

For example:

    elm make src/Main.elm

This tries to compile an Elm file named src/Main.elm, putting the resulting
JavaScript code in an elm.js file.
```

We left out the flags that can be passed to this sub command.

Let's use the sub command to make an `index.html`. This way we don't need to
reactor to show our app.

```sh
elm make src/FlashCard.elm
```

The command above should create an `index.html` in the current work directory.

## Verification
Open the just generated `index.html` with a browser, and check that
Wettervorhersage still means Weather forecast.
