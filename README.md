# tutorial
A [tutorial][] to create a flashcard app

## Development
This tutorial is written with [mdbook][], which can be obtained following these
[instructions][install.mdbook].

You can spin up a server that will rebuild the book when files are changed by
executing the following command:

```sh
mdbook serve -p 2273 -w 35174
```

you can now explore the book by opening
[http://localhost:2273](http://localhost:2273).

If you want to publish the changes, commit and push to this repository and the
will be automatically deployed.

[tutorial]: https://hermannebbinghaus.github.io/tutorial/index.html
[mdbook]: https://rust-lang-nursery.github.io/mdBook/
[install.mdbook]: https://github.com/rust-lang-nursery/mdBook#installation
