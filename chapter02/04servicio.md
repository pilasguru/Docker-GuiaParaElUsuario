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
$ docker ps
CONTAINER ID        IMAGE 
01a420094251        andygrunwald/simple-webserver:latest 
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
$ docker stop 01a420094251
```

---

## Referencias:  

- [https://hub.docker.com/r/andygrunwald/simple-webserver/](https://hub.docker.com/r/andygrunwald/simple-webserver/)
 

