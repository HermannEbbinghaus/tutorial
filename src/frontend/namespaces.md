# Namespaces
We have just specified the return type of the `view` function to be 
`Html.Html ()`. Why are there two mentions of `Html`? We will answer that
question in this chapter.

Look at the top of the file. There is an import line.

```elm
import Html
```

This imports the [`Html` module][package] from the `Htmll` package. As can be
seen from the documentation, this package provides a lot of useful functions.
In order to use these functions you have to use there fully qualified name. E.g.
if you want to use the function `div` that will render a div element on the
page. You write

```elm
Html.div
```

The reason for using the fully qualified name is to avoid _name clashes_. Let's
illustrate a name clash with an example.

## Favorite number
We are going to ask somebody to create a module providing us with their
favorite number. Kirsty told us that her favorite number is `42`. Daan favorite
on the other hand is 37. We could create modules that record these favorites.

We will settle on the name `number` to record the respective favorite number. If
we wanted to use both numbers in one program, we would not have a problem. We
can use fully qualify the name and we would still know which number we mean.

If we wanted to use Kirsty's number we would write `Kirsty.number` and get 42.
If instead we wanted to use Daan's number, we would wirte `Daan.number`.

## Second `Html`
We learned about the first `Html` in the signature of the `view` function. It is
the Html _namespace_. A namespace will prevent name clashes between different
modules. But what about the second `Html`.

If you take a look at the [`Html` documentation][package] you will find it
exposes a type alias [`Html`][Html]. The `Html` type can be used to annotate
functions like our `view` function that it is returning Html.

## Exposing names
Sometimes there is no danger of name clashes. E.g. it will be unlikely that we
will using two `Html` types. In order to shorten the `Html.Html` part to just
the type `Html` we can expose the `Html` type into our own namespace.

We can expose names from modules when we import them. In order to expose the
`Html` type from the `Html` module we would write

```elm
import Html exposing (Html)
```

This allows us to write the signature of the view function ascii

```elm
view : String -> Html ()
```

If you find it tedious to have to fully qualify the `div` and `span` functions
from the `Html` module. the import line would read

```elm
import Html exposing (Html, div, span)
```

## Verification
In this chapter you learned about namespaces, fully qualified names and
exposing names in your own namespace. In order to verify if you have grasped
these concept, try to answer the following question.

Why can't we expose the `text` function from the `Html` module?

[package]: https://package.elm-lang.org/packages/elm/html/latest/
[Html]: https://package.elm-lang.org/packages/elm/html/latest/Html#Html
