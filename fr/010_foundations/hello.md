# Hello Docker

Un premier exemple simple qui écrit "Hello docker" dans votre console:

```bash
$ docker run alpine echo "Hello docker"
Unable to find image 'alpine:latest' locally
latest: Pulling from alpine
f58d61a874be: Pull complete 
Digest: sha256:41eb14107cd1c1a5b50c2cedc534d53e8c1904c5f9e81070426feb23b424b28e
Status: Downloaded newer image for alpine:latest
Hello docker
```

Analysons ce qui vient de se produire.

Nous venons de demander à Docker de lancer Alpine[^1] et afficher "Hello docker"
dans la sortie standard de votre console.

Donc Docker a récupéré (``pull``) la dernière (``latest``) image Alpine depuis
le registre Docker, puis a créé un nouveau container depuis cette dernière et
enfin à démarré le container et exécuté ``echo "Hello Docker" dans le container
avant de l'arrêter.

**Attends, attends je ne comprends pas 2 mots de ce que tu me racontes...**


Regardons à quoi ressemble l'architecture 

# Architecture

![Docker architecture](images/architecture.svg)


## Le service Docker

Comme le montre le diagramme ci dessus, le service (deamon) Docker tourne
sur la machine hôte. L'utilisateur n'interagit pas directement avec mais via
le client Docker.


## le client (en ligne de commande de) Docker

Le client Docker, est l'interface utilisateur de docker. Il accepte des
commandes qu'il communique au service pour être exécuté par le service. 

Pour comprendre le fonctionnement de Docker regardons dans le détail ce que sont
les **images**, les **containers** et les **registries**


[^1]: [Alpine](https://hub.docker.com/_/alpine) est une petite distrib Linux 
