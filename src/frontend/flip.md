# Flip the card
When we reloaded the application we still saw Wettervorhersage. The reason for
this is that the model we are viewing hasn't changed. In order to see something
different we need to flip the card.

## A `flip` function
Let's create a function that will do the flipping for us. We start by thinking
about the signature, i.e. what goes in the function and what should come out.
Since we want to flip a `FlashCard` picking that as a argument to our function
makes sense. The result should be a `FlashCard` again. So our `flip` function
has a signature of

```elm
flip: FlashCard -> FlashCard
```

When we start thinking of the implementation we quickly run into the problem of
determining the opposite of a face. I.e. when we are facing `Front` the opposite
should be `Back` and vice versa.

Let's cater to that now and so that we can use that function in the definition
of `flip`.

## An `opposite` function
Again, we start thinking of the signature of our function. In should go a `Face`
and out should come a `Face` again.

```elm
opposite: Face -> Face
```

We just learned about the `let`-expression, which comes in handy now. Because it
allows us to determine which value occurs so we can take action accordingly.

```elm
opposite : Face -> Face
opposite face =
    case face of
        Front ->
            Back

        Back ->
            Front
```

## `flip` reloaded
With a new brush in our art kit we are able to continue our implementation of
`flip`. We should return a `FlashCard` with the same front and back as our
input, but with the opposite face.

```elm
flip card =
    { front = card.front, back = card.back , face = opposite card.face }
```

Pfew, that was a lot of typing. Isn't there a better way? I certainly would not
want to type all those fields if our model grows.

## `flip` revolutions
Luckily Elm allows that. It basically allows us to say; take this flashcard and
only modify the fields we are interested in. The syntax is shown below and is
exactly similar to the code above.

```elm
flip card =
    { card | face = opposite card.face }
```

Sweet!

## Verification
We have a `flip` function, but we need to use it. 

```elm
main =
    view (flip (flash_card "Wettervorhersage" "Weather forecast"))
```

Reloading the web application now will show "Weather forecast", but at a cost of
a lot of parenthesis. Elm has a way to form a [pipeline][]. Below you can see
how it works.

```elm
main =
    flash_card "Wettervorhersage" "Weather forecast"
        |> flip
        |> view
```

Here we first create a flash card with the `flash_card` function. We pass that
flash card to the `flip` function via the `|>` operator. The result of the flip
function is in its turn passed to the `view` function via the same `|>`
operator.

We will take a closer look at the `|>` operator and other functions.

[pipeline]: https://elm-lang.org/docs/syntax#operators
