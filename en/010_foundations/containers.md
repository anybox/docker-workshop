# Containers

Let's play with basics containers commands

## Running interactive container

```bash
$ docker run -it alpine sh
```

## Running a daemon container

```bash
$ docker run -d nginx:alpine
d1dc44ce216d097a4892489908fd4888bcb3cbeb009b50eac0df2a9577c53ba6
```

## Listing containers

```bash
$ docker ps
CONTAINER ID  IMAGE          COMMAND    CREATED  STATUS  PORTS   NAMES
d1dc44ce216d  nginx:alpine   "nginx -g  3 s ago  Up 3 s  80/tcp  stoic_pike
```


```bash
$ docker ps -a
CONTAINER ID  IMAGE          COMMAND    CREATED  STATUS  PORTS   NAMES
d1dc44ce216d  nginx:alpine   "nginx -g  3 s ago  Up 3 s  80/tcp  stoic_pike
e3b97eaa0c87  alpine:latest  "sh"       2 h ago  Exited          evil_stallman
```

## Remove a container

```bash
$ docker rm evil_stallman
```

## Stopping a running container

```bash
$ docker stop stoic_pike
$ stoic_pike
$ docker ps
CONTAINER ID  IMAGE          COMMAND    CREATED  STATUS  PORTS   NAMES
$
```

## Start a container


```bash
$ docker start stoic_pike
$ stoic_pike
$ docker ps
CONTAINER ID  IMAGE          COMMAND    CREATED  STATUS  PORTS   NAMES
d1dc44ce216d  nginx:alpine   "nginx -g  3 s ago  Up 3 s  80/tcp  stoic_pike
$
```

## Connect to a running container


```bash
$ docker exec -it stoic_pike sh
/ #
```

## Define a Docker container

A Docker container holds everything that is needed for an application to run.
Each container is created from a Docker image. Docker containers can be run,
started, stopped, moved, and deleted. Each container is an isolated application
platform.
