# A custom function
We have created our first flash card, but it can only show "Wettervorhersage".
Although it is a great word, we would like to be able to show different words.
Let's make that possible with the introduction of a custom function.

What we would like to achieve is to write

```elm
main =
    view "Wettervorhersage"
```

and let the `view` function return the Html for the flash card. For this we need
to create a function. Functions are defined by stating their name, i.e. `view`,
and their arguments. For us that would be the text that we want to show, so
let's call the argument for our function `text`.

Next would comes the body of the function and it defined the return value. For
us that looks very similar to our first flash card. The only difference is that
instead of the hard coded `"Wettervorhersage"`, we want to show the argument,
I.e. `text`.

Putting all this together, the `view` function comes down together

```elm
view text =
    Html.div []
        [ Html.span [] [ Html.text text ]
        ]
```

## Verification
If your reload the application you should still see our flash card that displays
"Wettervorhersage". Changing the argument of the view function and reloading
should reflect in the app.
