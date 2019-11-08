# Docker
We are able to ask for a flash card from the server and show it in the client.
That is amazing! If you haven't already celebrated that, go ahead and do that
now.

One of the improvements still ahead of us is being able to show many flashcards.
At the moment the flash card shown is hard coded on the server. We would rather
be able to retrieve it from a database.

We will be installing docker. [Docker][docker] allows us to run applications,
such as a database, inside of a container. This elevates us from keeping our
machine up to date with the latest database software. Instead, we can just run a
different container.

## Install
Tot install docker you can visit their [installation guide][install.docker]. It
provides many option that are to numerous to reproduce here. So go ahead and
follow the instructions that fits your specific situation.

## Verification
You can verify if the installation was successful by running the following
command

```sh
docker --version
```

It should respond with the version of docker that you installed. For me it
responds with

```plain
Docker version 18.09.7, build 2d0083d
```

With docker installed, we are all set to starting containers.

[docker]: https://www.docker.com/
[install.docker]: https://docs.docker.com/v17.12/install/
