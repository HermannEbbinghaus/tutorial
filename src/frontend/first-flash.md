# A first flash card
Let's focus on how the structure of the Html should look like. In order to use
the capabilities of Elm way of doing Html we imported the `Html`
[_module_][module].

```elm
import Html
```

A _module_

> let you break your code into multiple files

You can define you own modules, but we will wait until the opportunity arises.
First we will be using modules defined in _packages_ as found on [Elm packages][packages]

## `Html` module
The `Html` module has [documentation][] as found in the Elm packages. It needs a
little getting used to, but eventually you will get the hang of it.

If we would write plain Html that would display a flash card, we could write
something like this

```html
<div>
  <span>Wettervorhersage</span>
</div>
```

Note that _wettervorhersage_ is a German word meaning _weather forecast_. Maybe
the snippet of Html is missing some attributes and classes, but for now we will
focus on the structure.

To mimick the snippet in Elm, we would write the following code in elm

```elm
main =
    Html.div []
        [ Html.span [] [ Html.text "Wettervorhersage" ]
        ]
```

There are several things going on here. Not that Elm is a [_functional
language_][functional]. This means that functions are the building blocks of
creating programs.

There are three functions used to recreate the Html. `Html.div`, `Html.span` and
`Html.text`. Almost all functions in the Html module that produce tags accept
two arguments. A list of attributes, and a list of content.

We haven't defined attributes yet so the first argument of `Html.div` and
`Html.span` is the _empty list_: `[]`. The second argument of `Html.div` is a
list with content, i.e. a span that itself contains text.

We will have more to say about functions but for now we can verify that
everything works as expected.

## Verification
When you reload the flash card app in the browser, you should see the German
word for weather forecast.

[module]: https://guide.elm-lang.org/webapps/modules.html
[packages]: https://package.elm-lang.org/
[documentation]: https://package.elm-lang.org/packages/elm/html/latest/
[documentation.div]: https://package.elm-lang.org/packages/elm/html/latest/Html#div 
[functional]: https://en.wikipedia.org/wiki/Functional_programming
