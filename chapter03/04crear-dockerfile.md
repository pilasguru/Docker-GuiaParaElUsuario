# Crear usando Dockerfile

_Give a sysadmin an image and their app will be up-to-date for a day, give a sysadmin a Dockerfile and their app will always be up-to-date_ 

`Dockerfile` es un archivo de texto que contiene un conjunto de instrucciones o comandos para la creación de una imagen docker. Llamando a la función `docker build` se leen las instrucciones del Dockerfile y se construye una imagen que se guardará en el repositorio local.

## Uso de Dockerfile

Para la construcción de una imagen se utiliza el comando `docker  build ${CONTEXT}`. 

El `${CONTEXT}` son todos los archivos que necesita el Dockerfile para construir la imagen; puede ser una carpeta de nuestra propia máquina o una URL de un repositorio git. 

El proceso de `build` lo ejecuta Docker Daemon y no el utilitario docker. Todo el `${CONTEXT}` es enviado repulsivamente al docker daemon, por lo que no es recomendable utilizar un path con demasiados archivos, ya que todos serán enviados. 

El archivo `Dockerfile` debe estar localizado en el raíz del `${CONTEXT}`

También se puede utilizar un archivo `.dockerignore` para especificar los archivos y carpetas que deben ser excluidos del proceso de construcción de la imagen y que no serán enviados al docker daemon, lo que mejorará la performance del proceso de `build`.

## Build

El `Dockerfile` siempre parte de una imagen creada, mediante la instrucción `FROM`. 

```
FROM node:latest
``` 

Con esta sola instrucción ya podemos crear una imagen, utilizando como `${CONTEXT}` el directorio actual:

```
$ docker build .
Sending build context to Docker daemon 2.048 kB
Step 1 : FROM node:latest
---> 36dc1bb7a52b
Successfully built 36dc1bb7a52b
```

Es posible indicar la ubicación del Dockerfile con el argumento `-f`:

```
docker build -f image/Dockerfile image/
```

También podemos ponerle nombre o etiquetar la imagen a la vez que la construimos utilizando el argumento `-t` y el nombre que le daremos, en el formato `-t ${tag}:${version}`:

```
$ docker build -t pilasguru/nodejs .

$ docker build -t pilasguru/nodejs:0.0.1 .
```

Una vez construída podemos revisar que la imagen esté en nuestro repositorio

```
$ docker images pilasguru/nodejs

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
Pilasguru/nodejs     0.0.1               38dc1bb7a34c        2 weeks ago         655.5 MB
Pilasguru/nodejs     latest              38dc1bb7a34c        2 weeks ago         655.5 MB
```

## Estructura del Dockerfile

El formato del archivo Dockerfile es:

```
# Comentario

INSTRUCCION argument1 argumento2 argumento3 ...
```

La INSTRUCCION no es case-sensitive pero por costumbre se suele usar en mayúscula. 

El **orden de las instrucciones es importante** ya que debe seguir el orden del proceso de construcción de la imagen.

## Estructura del .dockerignore

El archivo `.dockerignore` tiene un formato como el archivo `.gitignore` y es un listado por renglón de los archivos o carpetas que son ignorados:

```
# comentario
*/temp*
*/*/temp*
temp?
testing/
.git/
```

Los asteriscos se utilizan como comodines e incluyen tanto archivos, carpetas y en ese caso las sub-carpetas.

## Instrucciones del Dockerfile

### FROM

Un Dockerfile válido debe tener este instrucción como su primer instrucción e indica la imagen que se utilizará para construir la nueva imagen.  Docker daemon primero verificará si la imagen existe localmente, si no procederá a descargarla de docker hub. 

Se puede utilizar de tres formas:

```
FROM <imagen>
FROM <imagen:tag>
FROM <imagen>@<digest>
```

FROM debe ser la primer línea no comentada en el Dockerfile. Se puede utilizar múltiples veces en el mismo Dockerfile. Tanto el `tag` como `digest` son opcionales y permiten tratar de obtener la imagen exacta, pero de no estar disponible se usará la última (`latest`)

### MAINTAINER

Permite indicar el autor de la imagen y se utiliza asi:

```
MAINTAINER <nombre>
```

### RUN

Permite indicar comandos que serán ejecutados en una nueva capa sobre la imagen (del FROM) en el proceso de construcción y ese resultado será guardado para pasarlo, opcionalmente, a un siguiente RUN que volverá a crear una nueva capa.

RUN tiene dos formatos: **shell** o **exec**:

`RUN <comando>` es el formato shell. El comando se ejecutará en un shell que por defecto es `/bin/sh -c` de Linux o `cmd /S /C` de Windows. 

`RUN [“ejecutable”, “argumento1”, “argumento2”, “argumento3” …]`

Un ejemplo de `Dockerfile` hasta ahora, quedaría construido de la siguiente forma:

```
# Ejemplo
# ----------
FROM node:latest
MAINTAINER pilasguru
RUN /bin/sh -c 'echo "*** hello Dockerfile!! ***"'
RUN ["npm", "--version"]
```

Creando una imagen con este ejemplo, tendremos la siguiente salida:

```
➜  docker build -t pilasguru/nodejs:0.0.3 .
…
Step 3 : RUN /bin/sh -c 'echo "*** hello Dockerfile!! ***"'
 ---> Running in 6ebfa85f7683
*** hello Dockerfile!! ***
…
Step 4 : RUN npm --version
 ---> Running in fc9dab7cf8c2
3.10.10
…
```

### LABEL

Esta instrucción incluye metadatos a la imagen en el formato de pares llave-valor:

```
LABEL <llave>=<valor> <llave>=<valor> <llae>=<valor> ...
```

Y se pueden utilizar múltiples líneas de LABEL:

```
LABEL "com.ejemplo.imagen"="Node JS imagen LABEL ejemplo"
LABEL version="0.0.4"
LABEL descripcion="valores pueden ser \
separados en varias líneas"
```

Y por supuesto que se pueden indicar varios pares de llaves=valor en la misma instrucción LABEL.

Veamos la construcción de una imagen y sus metadatos:

```
$ docker build -t pilasguru/nodejs:0.0.3 . --no-cache=true

$ docker inspect pilasguru/nodejs:0.0.3
…
"Labels": {
                "com.ejemplo.imagen": "Node JS image LABEL ejemplo",
                "descripcion": "valores pueden ser
                Separados en varias líneas",
                "version": "0.0.4"
            }
…
```

### EXPOSE

Esta instrucción informa a Docker que el contenedor escuchará en un determinado puerto cuando esté corriendo. 

```
EXPOSE <port> [<port>...]
```

No significa que el puerto será accesible desde el host. Para construir la red, se debe utilizar el argumento `-p` que publicará el punto al correr docker.

### ENV

Permite configurar variables de entorno en el contenedor cuando esté corriendo.

```
ENV mysql_password passw0rd
ENV src_folder ./src/app
```

Se pueden consultar las declaraciones de ENV con el comando `inspect`:

```
$ docker inspect linoxide/nodejs:0.0.3
…
"Env": [             "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NPM_CONFIG_LOGLEVEL=info",
                "NODE_VERSION=7.2.1",
                "mysql_password=passw0rd",
                "src_folder=./src/app"
            ] …
```

### ADD

La instrucción ADD copia nuevos archivos, directorios o archivos remotos (desde una URL) desde un `<src>` y los agrega a la imagen en el lugar indicado en `<dest>`.

Ejemplos:

```
ADD . /app/

ADD [ "dir con espacios/" "/app/" ]
```

En los dos ejemplos de arriba se copian los archivos de los directorios indicados en la carpeta `/app/` dentro de la imagen.

Si el `<dest>` no finaliza barra al final, se considera un archivo y en el se escribirá el contenido de `<src>`.

Si `<dest>` no existe, será creado.

Se permite el uso de asteriscos en `<src>` como ser `arch*` o `readm?.txt`.

Si el origen `<src>` es un compactado (tar, gzip, bzip2 o xz) la  ejecución de ADD lo descompactará dentro de `<dest>`.

### COPY

COPY es muy similar a ADD: hace lo mismo y tiene el mismo formato. 

La diferencia es que COPY no acepta URLs como `<src>` y en caso de ser un archivo compactado, no lo descompactará al copiarlo dentro de la imagen.

### ENTRYPOINT

Este comando permite especificar un comando que será siempre ejecutado cada vez que se inicie el container.

```
ENTRYPOINT ["/bin/echo", "Hola pilasguru"]
```

```
$ docker build -t pilasguru/nodejs:0.0.3 . --no-cache=true

$ docker run -it --name minodejs pilasguru/nodejs:0.0.3
Hola pilasguru
```

Tenga en cuenta que **solamente un ENTRYPOINT** es permitido en el Dockerfile.

### CMD

Al igual que ENTRYPOINT permite especificar comandos a ejecutar cuando se inicie el container y también, **solamente un CMD** es permitido en el Dockerfile.

La característica de CMD es que será omitido en caso de que el contenedor se inicie especificando otro comando.

Si un Dockerfile especifica:

```
ENTRYPOINT ["/bin/echo", "Hola pilasguru"]
CMD  ["/bin/echo" "Hola Mundo!!"]
```

Y construímos la imagen:

```
$ docker build -t pilasguru/nodejs:0.0.3 . --no-cache=true
```

Y ejecutamos: 

```
$ docker run -it --name minodejs pilasguru/nodejs:0.0.3
Hola pilasguru
Hola Mundo!!  
```

Ahora si creamos un segundo comando, pero indicando un comando:

```
$ docker run -it --name minodejs pilasguru/nodejs:0.0.3 echo "Que onda!"
Hola pilasguru
Que onda!  
```

### VOLUME

La instrucción VOLUME creara un punto de montado con el nombre especificado y tendrá el filesystem externo al contenedor

```
VOLUME /var/log
```

### USER

La instrucción USER seguido del `nombre` o `UID` indica bajo que usuario correrán las instrucciones RUN, CMD o ENTRYPOINT.

### WORKDIR

WORKDIR permite indicar el directorio en el cual los comandos de RUN, CMD, ENTRYPOINT, COPY y ADD serán ejecutados.  Si el directorio WORKDIR no existe, será creado. 

WORKDIR puede ser visto como el `home` del contenedor


## Ejemplos de Dockerfile

Please see the comments in each Dockerfile example.

### Nodejs app Dockerfile example:

```
FROM node:argon
# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install
# Bundle app source
COPY . /usr/src/app
EXPOSE 8080
CMD [ "npm", "start" ]
```

### Nginx Dockerfile example:

```
FROM debian:jessie
MAINTAINER NGINX Docker Maintainers "docker-maint@nginx.com"
ENV NGINX_VERSION 1.11.7-1~jessie
RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
     && echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list \
     && apt-get update \
     && apt-get install --no-install-recommends --no-install-suggests -y \
                               ca-certificates \
                               nginx=${NGINX_VERSION} \
                               nginx-module-xslt \
                               nginx-module-geoip \
                               nginx-module-image-filter \
                               nginx-module-perl \
                               nginx-module-njs \
                               gettext-base \
     && rm -rf /var/lib/apt/lists/*
# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
     && ln -sf /dev/stderr /var/log/nginx/error.log
EXPOSE 80 443
CMD [ "nginx", "-g", "daemon off;" ]
```

---

## Ejercicios:

### 1.

Crear un archivo con el nombre `index.js` con el siguiente contenido:

```
var os = require("os");
var hostname = os.hostname();
console.log("Un saludo desde " + hostname);
```

Crear un archivo con el nombre `Dockerfile` con el siguiente contenido.

```
FROM alpine
RUN apk update && apk adk nodejs
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


---

## Referencias:

* [https://docs.docker.com/engine/getstarted/step_four/](https://docs.docker.com/engine/getstarted/step_four/)
* [https://docs.docker.com/engine/tutorials/dockerimages/](https://docs.docker.com/engine/tutorials/dockerimages/)
* [https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)

