# Link Docker containers

Lets improve previous example! This time we will use a *TODOs* REST API
developed with [Anyblok](http://docs.anyblok.org/default
"Anyblok documentation") and [Anyblok pyramid](
http://docs.pyramid.anyblok.org/default "Anyblok pyramid documentation").

This service allow to create / delete / update / get *TODOs* stored in a
database.

[link containers example](https://github.com/anybox/
docker-workshop-example/tree/master/01_link_containers_anyblok)

As you could see in this exercise we linked the postgres Docker container
with the todo service Docker container, then docker automatically set
``/etc/hosts`` for you.