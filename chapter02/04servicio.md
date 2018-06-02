# Docker como servicio

Poner a correr una imagen docker cuyo proceso es un servicio supone __dejar corriendo__ algo en forma permanente para utilizar el servicio.

Al poner algo a correr en forma permanente debemos, además de saber cómo ejecutarlo, saber si está funcionando, utilizar el servicio y cómo apagarlo, así que este paso involucra algunos conceptos más del uso de docker.

## Ejecución

Entonces, ejecutando:

```
$ docker run -d -p 8082:8082 andygrunwald/simple-webserver
```

donde:

- `-d` pondrá a correr el docker en //background//
- `-p 8082:8082` abrirá el puerto 8082 en el equipo local conectará con el puerto 8082 del contenedor.

y descargará la imagen y nos devolverá el _prompt_, pero ha dejado corriendo el docker.

## Saber si está funcionando

Podemos interrogar con docker si el contenedor está corriendo:

```
$ docker container ls
CONTAINER ID        IMAGE                           COMMAND             CREATED              STATUS              PORTS                    NAMES
8d5297a02f2c        andygrunwald/simple-webserver   "app"               About a minute ago   Up About a minute   0.0.0.0:8082->8082/tcp   stupefied_bohr
```

## Utilizar el servicio

El servicio es un servidor web simple que lo podemos ver con el navegador conectando al puerto local, que configuramos con `-p`, mediante el comando [curl](https://curl.haxx.se/):

```
$ curl http://localhost:8082/version
simple webserver v1.0.0
```

## Apagar el contenedor

Como al contenedor lo creamos sin nombre, nos referimos a él por el _Container ID_ y lo apagamos con:

```
$ docker container stop 01a420094251
$ docker container ls
CONTAINER ID        IMAGE               COMMAND
$
```

## Encender el contenedor

```
$ docker container start 01a420094251
```

## Acceder a un contenedor en ejecución

Es posible acceder a un contenedor, para modificar contenido, revisar logs, verificar distintas configuraciones, obteniendo shell:

```
docker container exec -it eager_hopper sh
```

donde:

- `-i` entrará en modo interactivo
- `-t` asignara una consola `tty` al proceso ejecutado (sh)

## Ejercicios

### 1.

Borrar todos los container apagados utilizando los comandos:

```
docker container ps -a
docker container rm <CONTAINER-ID> 
```

### 2.

Volver a ejecutar el container (_Ejecución_)como se muestra a principio esta sección verificando que esté activo y tratar de borrarlo con los comandos, verificando las diferencias entre ellos:

```
docker container rm <CONTAINER-ID>
docker container rm -f <CONTAINER-ID> 
```

### 3.

Volver a ejecutar el container (_Ejecución_) pero esta vez **sin** el parámetro `-d` dejando el servicio en primer plano.

Desde otra consola hacer conexiones con `curl http://localhost:8082`

Salir con `Ctrl-C` y verificar qué sucede con el contenedor utilizando el comando `docker container ls`

---

## Referencias:  

- [https://hub.docker.com/r/andygrunwald/simple-webserver/](https://hub.docker.com/r/andygrunwald/simple-webserver/)
 

