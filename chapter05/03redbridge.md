# Contenedores detrás de bridges

Son los contenedores por defecto que se crean con docker. Cuando se corre Docker Daemon se crea un bridge (`docker0`) y los contenedores que se van creando son automáticamente conectados a ese bridge y se le asigna una IP privada. 

La comunicación entre contenedores conectados al mismo bridge se produce por estar en la misma sub-red. La conexión hacia internet se produce nat utilizando la IP pública del host.

Docker permite la creación de bridges y sub-redes mediante el comando `docker network`

Para crear un contenedor en una detrás de un bridge no se necesita indicar ningún argumento, ya que es el tipo de contenedor que se levanta por defecto. Sin embargo, se puede especificar el argumento `--net bridge` al crear el contenedor:

```
$ docker run -it alpine:latest /bin/sh

/ # ip a s
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
70: eth0@if71: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue state UP
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
```

```
$ docker run --net bridge alpine:latest
```

## Crear una red y bridge 

Es posible crear una propia red con un bridge e indicarle a docker que la use, en lugar de utilizar la que configura por defecto (docker0).

Para crear una nueva red de tipo _bridge_ cualquiera de estos tres comandos es equivalente:

```
docker network create mired

docker network create -d mired

docker network create --driver bridge mired 
```

El argumento `-d` o `--driver` permite indicar el tipo de red a crear, por defecto es _bridge_.

Para crear un _bridge_ con toda la configuración de red necesaria:

```
docker network create \
--driver bridge \
--subnet=192.168.2.0/24 \
--gateway=192.168.2.10 \
nueva_red
```

Para correr un contenedor pegado a nuestra nueva sub-red:

```
docker run --network=nueva_red -itd --name=docker-nginx nginx
```

---

## Referencias:

* [https://docs.docker.com/engine/reference/commandline/network_create/](https://docs.docker.com/engine/reference/commandline/network_create/)


 
