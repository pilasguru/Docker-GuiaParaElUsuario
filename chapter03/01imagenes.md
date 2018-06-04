# Gestión de imágenes

## Buscar

El repositorio de imágenes público Docker Hub se puede buscar mediante web o con el comando `search`:

```
docker search ubuntu | head
```

desplegará la totalidad de las imágenes que posean ubuntu en su nombre o descripción.

Para obtener las imágenes oficiales podemos filtrar solo las imágenes que comienzan con ubuntu:

```
docker search ubuntu | grep ^ubuntu
```

### tags

Podemos contular por el `tag` de la imagen, directamente invocando al api del registry que nos devolverá un JSON que podemos filtrar con el comando `jq`:

```
curl -s -S 'https://registry.hub.docker.com/v2/repositories/library/ubuntu/tags/' | jq '."results"[]["name"]' |sort
```


## Descargar

La forma de descargar una imagen para incorporarla al repositorio local es con el comando `pull`:

```
docker pull ubuntu:bionic
```

Debemos recordar que la opción `run` además de ejecutar una imagen docker, también la descarga y la deja en el repositorio.

## Gestionar

El comando `tag` permite poner el nombre que queremos a una imagen en el formato `repositorio:etiqueta`

```
docker tag ubuntu:bionic pruebas:locales
```

Que generará una nueva entrada en el repositorio local con el nombre que deseamos:

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
pruebas             locales             452a96d81c30        5 weeks ago         79.6MB
ubuntu              bionic              452a96d81c30        5 weeks ago         79.6MB
```

En el repositorio local podemos hacer búsqueda de imágenes con diferentes filtros:

```
docker images ubuntu:*
```

Y el comando `docker images` posee la opción `--filter` que permite buscar imágenes por distintas características

```
-f, --filter valor    Filtrado de la salida basado en condiciones
                        - dangling=(true|false)
                        - label=<key> o label=<key>=<value>
                        - before=(<image-name>[:tag]|<image-id>|<image@digest>)
                        - since=(<image-name>[:tag]|<image-id>|<image@digest>)
                        - reference=(pattern of an image reference)
```
Por ejemplo:

```
docker images --filter "dangling=true" 
```

## Borrar

Para borrar imágenes del repositorio local se utiliza el comando  `rmi`:

```
docker image rmi pruebas:locales
```

Para borrar todas las imágenes que no tienen asignado un nombre se utiliza:

```
docker image prune
``` 

---

## Ejercicios

### 1.
Descargar la imagen de ubuntu correspondiente a `xenial`

---

## Referencias:

- [Docker Hub](https://hub.docker.com)
- [docker image filtering](https://github.com/moby/moby/blob/10c0af083544460a2ddc2218f37dc24a077f7d90/docs/reference/commandline/images.md#filtering)