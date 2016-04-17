# Hello docker

Here a basic example that write "Hello docker" on your shell.

```bash
$ docker run alpine echo "Hello docker"
Unable to find image 'alpine:latest' locally
latest: Pulling from alpine
f58d61a874be: Pull complete 
Digest: sha256:41eb14107cd1c1a5b50c2cedc534d53e8c1904c5f9e81070426feb23b424b28e
Status: Downloaded newer image for alpine:latest
Hello docker
```

Let's understand what's happens!

We have asked docker to run alpine[^1] and display "Hello docker" in the output.

So docker has pulled the latest Alpine image from the Docker registry, create
a new container from this image, start the container run `echo "Hello docker"`
inside this container and stop the containter.

**Wow wow, wait, I don't understand what you are saying...**


Let's have an overview of the architecture then 

# Architecture

![Docker architecture](images/architecture.svg)


## The Docker daemon

As shown in the diagram above, the Docker daemon runs on a host machine.
The user does not directly interact with the daemon, but instead through the
Docker client.

## The Docker client

The Docker client, in the form of the docker binary, is the primary user
interface to Docker. It accepts commands from the user and communicates back 
and forth with a Docker daemon.

To understand Docker’s internals let's go in deep with **images**, 
**containers**, **registries**


[^1]: Alpine Linux is a Linux distribution (as Debian, Ununtu, CentOs) built 
      around musl libc and BusyBox. 
      [Alpine image](https://hub.docker.com/_/alpine/) is only 5 MB in size.
