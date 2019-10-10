# A custom type
We have created a fuller flash card. It has a front and a back. But what way is
it facing? Are we seeing the front or the back?

If we want to differentiate we should be able to express the difference. We will
do that with a custom type.

## Face
The following code introduces a new type `Face`. It will be used to determine
which way our flashcard is facing.

```elm
type Face
    = Front
    | Back
```

The `type` construct is an example of an [_algebraic data type_][adt]. That is a
fancy name saying that there are certain ways of combining different types into
more complex types. We will come back to that subject later on.

## Extending `FlashCard`
With a `Face` we should extend our `FlashCard` model. In the `FlashCard` type
alias add a field `face` of type `Face`.

```elm
type alias FlashCard =
    { front : String
    , back : String
    , face : Face
    }
```

This will break our program. This is because when we created a flash card we
should also specify which way it is facing.

```
{ front = "Wettervorhersage", back = "Weather forecast", face = Front }
```

## Verification
If it compiles, it should still show you "Wettervorhersage" when you reload the
app. 

[adt]: https://en.wikipedia.org/wiki/Algebraic_data_type
