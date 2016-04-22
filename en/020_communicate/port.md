# Port binding

Let's run [port binding pyramid example](https://github.com/petrus-v/
docker-workshop-example/tree/master/00_port_binding_pyramid)

In fact there is different way to run this docker container

```bash
docker run -it --rm -p 0.0.0.0:9080:8080 00_pyramid
```

```bash
docker run -it --rm -p 9080:8080 00_pyramid
```

```bash
docker run -it --rm -P 00_pyramid
```
