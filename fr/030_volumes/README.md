# Maîtriser les volumes

* Comment gérer les données ? Comme à chaque fois que l'on supprime un container
  on perd la trace de nos données, je ne veux pas les perdre quand je mets à jour
  mon container

* Ai-je besoin de reconstruire (build) mon image à chaque fois quand je
  developpe et teste mon application ? Ça va me prendre trop de temps.

* Comment sont prévus les backups des données?

Nous allons regarder quelsques exemples puis la théorie sur le système de
stockage des données de docker.

Les Exemples sont dans le projet [docker workshop example](https://github.com/
petrus-v/docker-workshop-example/tree/master/02_volumes "Volumes examples")
vous allez apprendre à :

* Déclarer des volumes dans un dockerfile ou au runtime
* Share volumes between containers
* Map host volumes

Then see what is behind the scene [Storage consideration](storage.md)
