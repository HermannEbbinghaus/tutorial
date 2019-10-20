# Showing the back
We have been staring at Wettervorhersage for a while now. We would like to
convince ourselves that we still know it's translation. Time to leverage the
`face` of our `FlashCard` and show a different side.

## Let expression
In our view function we hard-coded to show the front of the flash card.

```elm
view card =
    div []
        [ span [] [ Html.text card.front ]
        ]
```

We like to be able to change which text we show depending on the face that is
showing. For this we are going to introduce a [`let`-expression][let] in our
`view` function.

A `let` expression is useful when

> when an expression is getting large. You can make a let to break it into
> smaller definitions and put them all together in a smaller expression. 

We first use it to introduce a name for the text we want to show.

```elm
view card =
    let
        text = card.front
     div []
        [ span [] [ Html.text text ]
        ]

```

In it self this isn't a big change. It only allows us to define a name. But the
value we bind this name is now under our control.

## Showing the back
We would like to show the a different text when we face the back.We can achieve
that by matching on the flash cards face.

```elm
text =
    case card.face of
        Front ->
            card.front

        Back ->
            card.back
```

this makes use of new concept: [Pattern matching][case]. A `case` expression

>  allows us to branch based on which variant we happen to see.

So if our card faces `Front` we want our card to show the `card.front`. And when
it faces `Back` we want to see `card.back`.

## Verification
Make a prediction what would happen when you reload the web application. If your
prediction matches the reality you probably know what is up next.

[let]: https://elm-lang.org/docs/syntax#let-expressions
[case]: https://guide.elm-lang.org/types/pattern_matching.html
