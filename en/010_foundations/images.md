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

If you run it again ``docker run -it alpine sh`` that will create a new
container on alpine image without curl installed.


***TODO: Finalyze this chapter

## Build image from a ``Dockerfile``

Let's do the same using a ``Dockerfile``:

```Dockerfile
FROM alpine
RUN apk update 
RUN apk add curl
```

## List images



## Layers

```Dockerfile
FROM alpine
RUN apk update && apk add curl
```


## Remove images

## Tags

## Image definition

A Docker image is a read-only template. For example, an image could contain a
Debian operating system with Nginx and your web application installed.

Images are used to create Docker containers.
