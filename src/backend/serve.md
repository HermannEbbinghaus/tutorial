# Serving the frontend
Wouldn't it be interesting to serve the frontend from our server? Let's work on
that in this chapter.

For this it is best to have an `assets` directory that will hold all of our
static assets. In the server directory create an `assets` directory and move the
`index.html` to it.

```plain
assets/
└── index.html
```

## Serving static files
Gotham allows us to define a _router_. A router allows you to control which
handlers get to handle certain requests. In order to use it we need some
imports.

```rust
use gotham::router::builder::{build_simple_router, DefineSingleRoute, DrawRoutes};
```

We don't need the `HELLO_WORLD`, or `say_hello`, so we can get rid of it.
Instead we will define the router to serve our `index.html`. We use the 
`build_simple_router` factory for that.

```rust
let router = build_simple_router(|route|{
    route.get("/").to_file("assets/index.html");
});
```

The `build_simple_router` accepts a _closure_ that enables us to configure the
routes. We want to respond with `index.html` when we make a get request.

## Server with routes
We now need to start the server with our router.

```rust
gotham::start(addr, router);
```

## Verification
Restart the server by shutting it down and running `cargo run` again. This will
recompile the server and start waiting for requests. Open your browser and open
the application. It should serve the frontend application.
