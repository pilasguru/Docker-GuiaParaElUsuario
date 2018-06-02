# Crear imágenes propias

Existen dos métodos para crear imágenes propias:

1. Hacer cambios en un contenedor y exportarlo como imagen al repositorio local
2. Generar un archivo `Dockerfile` con el script para generación de una imagen. 

## Crear a partir de un contenedor

Correr una contenedor basado en la imagen `debian` e ingresar al shell para hacer cambios:

```
docker container run -ti debian bash
```

Ejecutar estos comandos para instalar `figlet` y salir

```
apt-get update
apt-get install -y fidlet
figlet 'hello docker'
exit
```

El container está detenido y a partir de él se puede crear una imagen, que se guarda en el repositorio local, con el comando `container commit`

```
docker container ls -a
docker container commit <CONTAINER-ID>
docker image ls
```

Le colocamos el nombre a la imagen generada con el comando `image tag` 

```
docker image tag <IMAGE-ID> confidget
docker image ls
```

Ahora que disponemos de una imagen basada en debian que tiene el comando `figlet` instalado la podemos utilizar:

```
docker container run configlet figlet hola
```

## Crear usando Dockerfile

_Give a sysadmin an image and their app will be up-to-date for a day, give a sysadmin a Dockerfile and their app will always be up-to-date_ 

Crear un archivo con el nombre `index.js` con el siguiente contenido:

``` var os = require("os");
var hostname = os.hostname();
console.log("Un saludo desde " + hostname);
```

Crear un archivo con el nombre `Dockerfile` con el siguiente contenido.

``` FROM alpine
RUN apk update && apk add nodejs
COPY . /app
WORKDIR /app
CMD ["node","index.js"]
```

Con el comando `build` construimos la imagen que seguirá el script configurado en el Dockerfile que se busca en el directorio actual con el último punto

```
docker image build -t hello:v0.1 .
```

```
Sending build context to Docker daemon  3.072kB
Step 1/5 : FROM alpine
 ---> 3fd9065eaf02
Step 2/5 : RUN apk update && apk add nodejs
 ---> Running in 867c66ddedd4
fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/community/x86_64/APKINDEX.tar.gz
v3.7.0-190-g3da66f61a4 [http://dl-cdn.alpinelinux.org/alpine/v3.7/main]
v3.7.0-184-ge62f3c3781 [http://dl-cdn.alpinelinux.org/alpine/v3.7/community]
OK: 9054 distinct packages available
(1/10) Installing ca-certificates (20171114-r0)
(2/10) Installing nodejs-npm (8.9.3-r1)
(3/10) Installing c-ares (1.13.0-r0)
(4/10) Installing libcrypto1.0 (1.0.2o-r0)
(5/10) Installing libgcc (6.4.0-r5)
(6/10) Installing http-parser (2.7.1-r1)
(7/10) Installing libssl1.0 (1.0.2o-r0)
(8/10) Installing libstdc++ (6.4.0-r5)
(9/10) Installing libuv (1.17.0-r0)
(10/10) Installing nodejs (8.9.3-r1)
Executing busybox-1.27.2-r7.trigger
Executing ca-certificates-20171114-r0.trigger
OK: 61 MiB in 21 packages
Removing intermediate container 867c66ddedd4
 ---> 9f2675ec7ebd
Step 3/5 : COPY . /app
 ---> 3dfd8536a240
Step 4/5 : WORKDIR /app
Removing intermediate container c56e9d8a8eb2
 ---> 6e9870377075
Step 5/5 : CMD ["node","index.js"]
 ---> Running in 8b80c4c4109d
Removing intermediate container 8b80c4c4109d
 ---> 14ddb4369169
Successfully built 14ddb4369169
Successfully tagged hello:v0.1
```

Con el comando `docker image ls` se puede ver la imagen recién creada:

```
REPOSITORY                      TAG                 IMAGE ID            CREATED              SIZE
hello                           v0.1                14ddb4369169        About a minute ago   50.2MB
```

```
docker container run hello:v0.1
```

## Capas de las imágenes

```
docker image history alpine

echo "console.log(\"version imagen v0.2\");" >> index.js

docker image build -t hello:v0.2 .

docker image ls

docker container run hello:v0.2

docker image history hello:v0.2 
```



```
docker image inspect alpine

docker image inspect --format "{{ json .RootFS.Layers }}" alpine

docker image inspect --format "{{ json .RootFS.Layers }}" hello:v0.2
```

---

## Ejercicios

### 1.

### 2.

---

## Referencias:

* [https://docs.docker.com/engine/getstarted/step_four/](https://docs.docker.com/engine/getstarted/step_four/)
* [https://docs.docker.com/engine/tutorials/dockerimages/](https://docs.docker.com/engine/tutorials/dockerimages/)
* [https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)

