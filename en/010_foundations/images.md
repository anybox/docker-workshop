# Images

## Pulling from registries

Let's get an image with Nginx stable on Alpine Linux distribution

```bash
$ docker pull nginx:stable-alpine
alpine: Pulling from nginx
be700e4956df: Pull complete 
4b9bf1642656: Pull complete 
51abb4d2846b: Pull complete 
47131f1f575f: Pull complete 
43053ae02e28: Pull complete 
cea3e203a9a4: Pull complete 
24ba19347287: Pull complete 
15d695f22e63: Pull complete 
f58d61a874be: Already exists 
54fdf50e0ac6: Already exists 
Digest: sha256:7d4a186f16ec00463ada491d62e12f60755e8aa2ea27ba1e6e0b26a9034347f6
Status: Downloaded newer image for nginx:stable-alpine
```

## Create image by committing a Docker container
 
Let's install curl in an alpine container:

```bash
$ docker run -it alpine sh
/ # curl
sh: curl: not found
/ # apk update
fetch http://dl-cdn.alpinelinux.org/alpine/v3.3/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.3/community/x86_64/APKINDEX.tar.gz
v3.3.3-24-g74309b7 [http://dl-cdn.alpinelinux.org/alpine/v3.3/main]
v3.3.3-9-gfc38db2 [http://dl-cdn.alpinelinux.org/alpine/v3.3/community]
OK: 5858 distinct packages available
/ # apk add curl
(1/4) Installing openssl (1.0.2g-r0)
(2/4) Installing ca-certificates (20160104-r2)
(3/4) Installing libssh2 (1.6.0-r1)
(4/4) Installing curl (7.47.0-r0)
Executing busybox-1.24.1-r7.trigger
Executing ca-certificates-20160104-r2.trigger
OK: 7 MiB in 15 packages
/ # curl https://anybox.fr > anybox.html
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 25783  100 25783    0     0   131k      0 --:--:-- --:--:-- --:--:--  159k
/ # exit
```

If you run it again ``docker run -it alpine sh`` notice that will create a new
container with alpine image but without curl installed.

You could start the existing Docker container but this won't meet our goal to
recreate a new docker container with curl included.

```bash
$ docker start -i 623e39ab887f
$ curl --version
curl 7.x...
$ exit
```

So we can commit this container to save it as Docker image

```bash
$ docker commit -m "install curl" 623e39ab887f alpine:curl
44791c39942caa99974e2ca861c046384519c141195e4e21245fc20acff953ab
$ docker run -it alpine:curl sh
/ # curl https://anybox.fr > anybox.html
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 25739  100 25739    0     0  93126      0 --:--:-- --:--:-- --:--:--  103k
/ # exit
```

> **Warning** Be aware the copied Docker container is paused by default while
> creating the new image.


## Build image from a ``Dockerfile``

Let's do the same using a ``/tmp/alpinecurl/Dockerfile``:

```Dockerfile
FROM alpine
RUN apk update 
RUN apk add curl
```

> **Warning** This Dockerfile contains some bad practices. We will see late why


[Dockerfile documentation](https://docs.docker.com/engine/reference/builder/
"RTFM")

Build a Docker image using this Dockerfile:

```bash
/tmp/alpinecurl$ docker build -t alpinecurl .
Sending build context to Docker daemon 2.048 kB
Sending build context to Docker daemon 
Step 0 : FROM alpine
 ---> 2a250d324882
Step 1 : RUN apk update
 ---> Running in 17b53395dc3c
fetch http://dl-cdn.alpinelinux.org/alpine/v3.3/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.3/community/x86_64/APKINDEX.tar.gz
v3.3.3-28-gef388c9 [http://dl-cdn.alpinelinux.org/alpine/v3.3/main]
v3.3.3-9-gfc38db2 [http://dl-cdn.alpinelinux.org/alpine/v3.3/community]
OK: 5858 distinct packages available
 ---> 8054303790e2
Removing intermediate container 17b53395dc3c
Step 2 : RUN apk add curl
 ---> Running in 0f88f742a236
(1/4) Installing openssl (1.0.2g-r0)
(2/4) Installing ca-certificates (20160104-r2)
(3/4) Installing libssh2 (1.6.0-r1)
(4/4) Installing curl (7.47.0-r0)
Executing busybox-1.24.1-r7.trigger
Executing ca-certificates-20160104-r2.trigger
OK: 7 MiB in 15 packages
 ---> bd3c413e1d5e
Removing intermediate container 0f88f742a236
Successfully built bd3c413e1d5e
```


## List images

```bash
docker images
```

## Layers

> **Info** Each Dockerfile command create an intermediate image.

```bash
docker images -a
```

> **Warning** Docker use intermediate images as cache[^1] depending commands
> that can produce an expected behaviors

```Dockerfile
FROM alpine
RUN apk update && apk add curl
```


## Tags

> **Warning** Updating an existing Docker image do not update existing container 

## Remove images

```bash
docker rmi alpinecurl
```


## Image definition

A Docker image is a read-only template. For example, an image could contain a
Debian operating system with Nginx and your web application installed.

Images are used to create Docker containers.


[^1]: [Build cache](https://github.com/docker/docker/blob/master/docs/userguide/
eng-image/dockerfile_best-practices.md#build-cache)