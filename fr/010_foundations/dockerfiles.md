# Dockerfile

Ci dessous la liste des commandes disponible dans un dockerfile la 
[documentation de référence](https://docs.docker.com/engine/reference/builder/ 
"Dockerfile documentation") est le meilleurs en droit pour comprendre à quoi
elles servent!


|Instructions    |Description                                                  |
|:--------------:|:------------------------------------------------------------|
| FROM           | Défini l'image de base                                      |
| MAINTAINER     | Champ *Auteur* dans l'image générée                         |
| RUN            | Execute des commandes et commit le resultat                 |
| CMD            | Commande par défaut lors de l'execution d'un container      |
| LABEL          | Ajoute des métadonnées à l'image                            |
| EXPOSE         | Informe Docker que le container écoute des port à l'execution|
| ENV            | Défini une variable d'environnement                         |
| ADD            | Copies des fichiers, répertoires fichiers distant (urls)    |
| COPY           | Copies des fichiers ou répertoires                          |
| ENTRYPOINT     | Configure un container afin qu'il se comporte comme un exec.|
| VOLUME         | Créé un point de montage                                    |
| USER           | Defini l'utilisateur à utiliser                             |
| WORKDIR        | Defini le repertoire de travail                             |
| ARG            | Une variable que l'utiliseur peut donner lors du build de l'image|
| ONBUILD        | Ajoute à l'image une instruction de trigger                 |
| STOPSIGNAL     | Defini le signal applé pour arrêter le container            |

