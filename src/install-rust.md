# Installing Rust
We will use [Rust][rust] to create a web server. Before we can start writing our
web server, we should install Rust.

## Installation
Rust can be installed and updated via a handy tool called `rustup` as described
on the [installation page](https://www.rust-lang.org/tools/install). This allows
you to have multiple different versions of Rust live next to each other.

When you execute the installation command, the install script will asks some
questions. Make sure you read and understand what the script will try to
achieve. For this tutorial no customization is necessary.

When the scripts finished Rust is installed. This comes with a couple of tools.

## Verification
To make sure that the installation was successful the following commands should
run without error.

```sh
cargo --version
```

The above command should respond with the installed cargo version. At the time
of this writing that was `1.38.0`.

```sh
rustc --version
```

Should respond with the same version.

[rust]: https://www.rust-lang.org/
