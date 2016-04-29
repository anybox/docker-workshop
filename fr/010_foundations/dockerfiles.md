# Dockerfile

Ci dessous la liste des commandes disponibles dans un dockerfile la 
[documentation de référence](https://docs.docker.com/engine/reference/builder/ 
"Dockerfile documentation") est le meilleur endroit pour comprendre à quoi
elles servent !


|Instructions    |Description                                                    |
|:--------------:|:--------------------------------------------------------------|
| FROM           | Définit l'image de base                                       |
| MAINTAINER     | Champ *Auteur* dans l'image générée                           |
| RUN            | Exécute des commandes et commit le resultat                   |
| CMD            | Commande par défaut lors de l'exécution d'un container        |
| LABEL          | Ajoute des métadonnées à l'image                              |
| EXPOSE         | Informe Docker que le container écoute des ports à l'execution|
| ENV            | Définit une variable d'environnement                          |
| ADD            | Copie des fichiers, répertoires fichiers distant (urls)       |
| COPY           | Copie des fichiers ou répertoires                             |
| ENTRYPOINT     | Configure un container afin qu'il se comporte comme un exec.  |
| VOLUME         | Créé un point de montage                                      |
| USER           | Definit l'utilisateur à utiliser                              |
| WORKDIR        | Definit le répertoire de travail                              |
| ARG            | Une variable que l'utiliseur peut donner lors du build de l'image|
| ONBUILD        | Ajoute à l'image une instruction de trigger                   |
| STOPSIGNAL     | Définit le signal appelé pour arrêter le container            |

