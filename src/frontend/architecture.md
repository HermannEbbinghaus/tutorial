# Elm Architecture
We are capable to flip a card, but we want to control when we flip it. At the
moment we are only generating static content. How does Elm allow values to
change.

In this chapter we will look into the _Elm architecture_.

## Model-View-Update
The [Elm architecture][architecture] is a pattern that help in structuring
an interactive application.

It revolves around a Model, a View and a way to Update the model. Two of the
parts are in place already. Our model is a `FlashCard` with `view` as it's View
function.

What is missing is the Update function and how it interacts with Elm.

## Pure functions
Functions in Elm are _pure_. A pure function is

> a function that has the following properties:
>
> 1. Its return value is the same for the same arguments (no variation with
>   local static variables, non-local variables, mutable reference arguments or
>   input streams from I/O devices). 
> 2. Its evaluation has no side effects (no mutation of local static variables,
>   non-local variables, mutable reference arguments or I/O streams).

This property has some nice benefits. But how do we change things, if functions
should always return the same on the same input?

## Elm runtime
The Elm runtime is the escape hatch that allows change in our web app. The
runtime is responsible for the Model. It will use a View function to show our
application. It will Update the model in the way we tell it to.

The way we tell it to is by sending a Message. This Message allows the Update
function to differentiate how to update the model.

We will be sending Message from the application, e.g. by clicking a button.

This probably all sounds very abstract. It will become clear in the next
chapter. Note that every Elm application is structured, even recursively, with
the Elm architecture. This helps developers in managing their code base.

[architecture]: https://guide.elm-lang.org/architecture/
[pure]: https://en.wikipedia.org/wiki/Pure_function
