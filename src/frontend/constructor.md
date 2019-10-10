# A convenient function
If we want to create a flash card we have to write

```elm
{ front = "Wettervorhersage", back = "Weather forecast", face = Front }
```

That is a whooping 71 characters. Most of these characters are boilerplate.
Can't we do better than that?

## Functions to the rescue
Of course we can do better. We can create a function that helps us with creating
a flash card.

Let's think about a name for the function. It creates a flash card so
`flash_card` seems appropriate.

Having settled on the name let's think about the signature. We would create
flash cards facing `Front`. So the only parts that are moving are the front and
the back.
This means our functions needs to accept two `String`s and returns a
`FlashCard`. The way the describe that in Elm is

```elm
flash_card : String -> String -> FlashCard
```

It needs some getting used to, but there are good reasons why the signature
looks the way it does.

With the signature in place, we can go on to defining the function.

```elm
flash_card front back =
    { front = front, back = back, face = Front }
```

## Verification
We can now use the `flash_card` function. We do need some parenthesis, or else
Elm will get confused.

```elm
`main =
    view (flash_card "Wettervorhersage" "Weather forecast")
```

Other than that, everything should still work. As an other verification: what if
we wanted to pass which way the flash card is facing to our `flash_card`
function, how would the signature change?
