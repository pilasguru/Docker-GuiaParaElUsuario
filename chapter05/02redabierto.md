02redabierto.md

# Contenedores abiertos

Los contenedores abiertos se deben evitar en lo posible. Los contenedores abiertos se conectan directamente al sistema de red del host. Para los contenedores abiertos se deben tomar precauciones de aislamiento adicional, ya que se tiene un acceso total a las redes y las interfaces el host.

Para crear un contenedor en una red abierta utilizamos el argumento `--net host` cuando lo creamos:

```
$ docker run --net host -it alpine:latest /bin/sh

/ # ip a s
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
    link/ether 02:e4:ac:f5:39:a9 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::e4:acff:fef5:39a9/64 scope link
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN
    link/ether 02:42:59:1a:e2:84 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:59ff:fe1a:e284/64 scope link
       valid_lft forever preferred_lft forever
```

Este container solamente ejecuta un shell, pero muestra como se tiene acceso a todas las interfaces del host en forma transparente.
