# Skeletal Elm project
With all the `Elm` tools installed. It is time to take them for a spin. Right
from the Elm is a very friendly language. When you ask Elm for help

```sh
elm --help
```

It will thank you for trying out Elm, give you some pointers where to find
[more information][guide] and tell you about some command options. We are
interested in the `elm init` command. It promises to

> Start an Elm project. It creates a starter elm.json file and provides a link
> explaining what to do from there.

This is a nice starting point. Run the command to start an Elm project. The
skeletal project creates the following files and directories.


```plain
.
├── elm.json
└── src
```

The `elm.json` describes the Elm project. We describe it in more detail later in
the tutorial. Besides the `elm.json` file there is a directory called `src`.
This is where all the source files go.

An empty `src` directory is an unhappy `src` directory. So let's go ahead and
create a file named `FlashCard.elm` inside the `src` directory with the
following content

```elm
module FlashCard exposing (..)

import Html


main =
    Html.text "Hello, World!"

```

## Verification
One of the cool things about Elm is that it can serve your files. By spinning up
a reactor Elm will look at your files, create a web server, serve your files and
when necessary compile them on the fly.

```sh
elm reactor
```

The above command will start the Elm reactor. The message that it returns with
asks you to got to [http://localhost:8000](http://localhost:8000). Going to that
address you will find a file navigation pane. Navigate it to `src` >
`FlashCard.elm` and be greeting by your very own `Hello, World!`

[guide]: https://guide.elm-lang.org
