# Subir (compartir) imágenes propias

Para compartir imágenes en [Docker Hub](https://hub.docker.com) se debe poseer una cuenta y primeramente estar logrado:

```
$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: pilasguru
Password:
Login Succeeded
```

Una vez ingresado, la imágenes debe tener un nombre (tag) formado por `usuario/nombre-imagen`, en mi caso:

```
docker tag localtest:latest  pilasguru/test
```

Recién con este nombre y el comando `push` se podrá subir la imagen a Docker Hub, que tomará el nombre de usuario de la primera parte del nombre de la imagen:

```
$ docker push pilasguru/test
The push refers to repository [docker.io/pilasguru/test]
cd7100a72410: Preparing
latest: digest: sha256:8c03bb07a531c53ad7d0f6e7041b64d81f99c6e493cb39abba56d956b40eacbc size: 528
```


---

## Referencias:

- [https://docs.docker.com/engine/reference/commandline/push/](https://docs.docker.com/engine/reference/commandline/push/)
- [https://docs.docker.com/docker-cloud/builds/push-images/](https://docs.docker.com/docker-cloud/builds/push-images/)
