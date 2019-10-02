# Type annotations
We have just created a custom function. It is lacking one of the Elm strongest
features. I.e. [_type information_][data-type].

Types help a compiler to determine if programs are correct. They can be used to
verify that the expectations you have about functions and programs are met, even
before the program is run.

Up until now, Elm has _inferred_ the types of our functions. But relying on the
type inference could hide some problems. So let's annotate our `view` function
with it's type.

## Common types
Elm has some built in types that you can use right out of the gate. One that we
already have used is [`String`][String]. It is a chunk of text. Elm also
provides a myriad of functions for `String` but now we are only interested in
it's type.

Remember that Elm is a [functional language][functional]? Because functions are
so important you can provide type information for them as well. This is done
with an arrow `->`.

On the left side of the arrow you place the type of the argument of the
function. To the right of the arrow you place the type of the return value. But
what is that? Let's guess it to by `String` and see what Elm makes of it.

Providing type information for the `view` function is done by

```elm
view : String -> String
```

This is placed right above the definition of the `view` function.

## Verification
If you reload the application you will be greated by a friendly message from the
Elm compiler

> -- TYPE MISMATCH --------------------------------------------- src/FlashCard.elm
> 
> Something is off with the body of the `view` definition:
>
> 11|>    Html.div []
> 12|>        [ Html.span [] [ Html.text text ]
> 13|>        ]
> 
> This `div` call produces:
> 
>     Html.Html msg
> 
> But the type annotation on `view` says it should be:
> 
>     String

We guessed the return type for the `view` function to be `String`. But that is not
correct. Elm noticed that the type difference from what actually is returned.
Let's change the type signature of the `view` function to

```elm
view : String -> Html.Html ()
```

for now. We will go into the convoluted `Html.Html ()` later.

Once you reload the application again. You should be greeted by "Wettervorhersage".

[data-type]: https://en.wikipedia.org/wiki/Data_type
[String]: https://package.elm-lang.org/packages/elm/core/latest/String
[functional]: https://en.wikipedia.org/wiki/Functional_programming
