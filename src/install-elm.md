# Installing Elm
Since [Elm][elm] is one of the technologies we are using to create our flashcard app we
better start with installing it.

## Installation
How Elm can be installed is described in their [installation page][instal.elm].
This includes setting up elm in a number of editors. Which certainly will come
in handy.

What is missing do are some helpful tools. Most notably [`elm-test`][elm-test]
and [`elm-format`][elm-format].
`elm-test` is used to test your Elm code, a practice that provide even more
confidence in refactoring your code.
`elm-format` automatically formats your code, so that no wars can erupt over
where to place which comma.

You can learn how to [install `elm-test`][install.elm-test] from their README.
Similarly, how to [install `elm-format`][install.elm-format] is described in
their README as well.

## Verification
If everything worked out as planned you should be able to execute the following
commands

```sh
elm --version
```

This should respond with the latest version. At the time of writing that was
`0.19.0`.

Similarly, the following commands

```sh
elm-test --version
```

responds at the time of writing with `0.19.0-rev6`.

Finally, verifying that `elm-format` is a little different. The command does not
have a `--version` flag. Instead asking for `--help`


```sh
elm-format --help
```

Should declare it's version at the top of its help page. Again. At the time of
this writing that was `0.8.1`.

## Celebrate
You are now all set for the next chapter. But before you go and explore the
wonderful world of Elm, make sure you celebrate! Configuring your machine can be
very hard.

[elm]: https://elm-lang.org/
[install.elm]: https://guide.elm-lang.org/install.html
[elm-test]: https://github.com/elm-explorations/test
[install.elm-test]: https://github.com/elm-explorations/test#running-tests-locally
[elm-format]: https://github.com/avh4/elm-format
[install.elm-format]: https://github.com/avh4/elm-format#installation-
