# Images

## Récupérer une image sur un registre

Récupérons l'image Nginx stable sur la distriubtion Alpine.

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

## Créons une image en commitant un container
 
Installons curl dans un container Alpine

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

Vous remarquerez, si vous lancez de nouveau la commande 
``docker run -it alpine sh`` cela crée un nouveau container avec l'image Alpine
qui ne contient pas curl.

Vous pourriez redémarrer le Docker existant mais ça ne vous permet pas de créer
de nouveaux containers Docker avec curl inclus.

```bash
$ docker start -i 623e39ab887f
$ curl --version
curl 7.x...
$ exit
```

Nous committons donc ce container pour le sauvegarder comme image Docker

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

> **Attention** Ayez en tête que par défaut lors de la copie d'un container
> Docker il est mis en pause le temps de créer l'image.


## Construisons une image depuis un ``Dockerfile``

Faisons la même chose dans un docker file ``/tmp/alpinecurl/Dockerfile``:

```Dockerfile
FROM alpine
RUN apk update 
RUN apk add curl
```

> **Attention** Ce Dockerfile ne suit pas les bonnes pratiques, nous verrons
> pourquoi un peu plus loin


[Dockerfile documentation](https://docs.docker.com/engine/reference/builder/
"RTFM")

Construisez l'image docker depuis le Dockerfile ci-dessus

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


## Lister les images

```bash
docker images
```

## les couches (Layers)

> **Info** La plus part des commandes du Dockerfile crée des images
> intermédiares

```bash
docker images -a
```

> **Attention** Docker utilise ces images intermédiaires comme cache[^1] lors de
> la construction d'une nouvelle image, le comportement dépendant de la commande.

```Dockerfile
FROM alpine
RUN apk update && apk add curl
```


## Tags

> **Attention** La mise à jour d'une image existante ne met pas à jour les
> containers existants

## Supprimer des images

```bash
docker rmi alpinecurl
```


## definition

Une image Docker est un modèle en lecture seule, Par exemple, une image est
basée sur un système d'exploitation, peut contenir Nginx et votre application
web installée dedans.

Les images sont utilisées pour créer les containers docker.


[^1]: [Comportement du cache lors du build](https://github.com/docker/docker/
blob/master/docs/userguide/eng-image/dockerfile_best-practices.md#build-cache)
