# Dockerfile

Here a quick table of available commands but I expected the [reference
documentation](https://docs.docker.com/engine/reference/builder/ 
"Dockerfile documentation") is the best one!


|Instructions    |Description                                                  |
|:--------------:|:------------------------------------------------------------|
| FROM           | Sets the base Image                                         |
| MAINTAINER     | *Author* field of the generated images                      |
| RUN            | Execute any commands and commit the result                  |
| CMD            | Provide defaults for an executing container                 |
| LABEL          | Adds metadata to an image                                   |
| EXPOSE         | Informs Docker that the container listens ports at runtime  |
| ENV            | Sets the environment variable                               |
| ADD            | Copies files, directories or remote file urls               |
| COPY           | Copies files or directories                                 |
| ENTRYPOINT     | Configure a container that will run as an executable        |
| VOLUME         | Creates a mount point                                       |
| USER           | Sets the user to use                                        |
| WORKDIR        | Sets the working directory                                  |
| ARG            | A variable that users can pass at build-time to the builder |
| ONBUILD        | Adds to the image a trigger instruction                     |
| STOPSIGNAL     | Sets the system call signal                                 |

