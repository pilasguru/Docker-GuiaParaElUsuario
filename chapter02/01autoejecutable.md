# Docker autoejecutable

Cuando utilizamos docker para correr una imagen que ya tiene un proceso configurado decimos que ejecutamos un proceso _docketizado_.

```
$ docker container run hello-world
```

Al ejecutar buscará localmente una imagen llamada `hello-world`, no la encontrará procederá a descargarla y guardarla en el `registry` local:

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
9bb5a5d4561a: Pull complete
Digest: sha256:f5233545e43561214ca4891fd1157e1c3c563316ed8e237750d59bde73361e77
Status: Downloaded newer image for hello-world:latest
```

Seguidamente correrá el proceso que posee la imagen y producirá la siguiente salida:

```
Hello from Docker.
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from
    the Docker Hub.
 3. The Docker daemon created a new container from that 
    image which runs the executable that produces the output 
    you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, 
    which sent it to your terminal.

To try something more ambitious, you can run an Ubuntu container 
with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free 
Docker Hub account:
 https://hub.docker.com

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/

```

Esta imagen ha sido creada con el único fin de correr ese proceso _docketizado_ que __exclusivamente__ muestra ese texto.

---

## Ejercicios

### 1.
Vuelva a ejecutar la imagen `hello-world` y preste atención a que ahora no será descargada, sino que se levantará directamente desde el repositorio local

### 2.
Liste las imágenes con el comando

```
docker image ls
```

Preste atención al tamaño que ocupa en el disco

---

## Referencias: 

- [https://hub.docker.com/_/hello-world/](https://hub.docker.com/_/hello-world/)


