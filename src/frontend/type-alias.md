# Type alias
Our flash card type now is `{ front : String, back : String }` which, to say the
least, does not roll off the tongue easily. Instead we would like to name our
flash card type `FlashCard`.

This can be achieved with a _type alias_. A type alias will introduce a name
for a different type. This has several benefits. Among them it allows you to
have a recognizable name for a type.

If you want to introduce a type alias you use the `type alias` keywords. In our
case you could use it like

```elm
type alias FlashCard =
    { front : String, back : String }
```

With the type alias introduced we can clean up the signature of the `view`
function by changing it to

```elm
view : FlashCard -> Html ()
```

## Verification
Fundamentally, nothing changed to the program, we only introduced a name for a
familiar thing. The application should still show "Wettervorhersage" when
reloaded.

