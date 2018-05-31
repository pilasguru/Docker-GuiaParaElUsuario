# Docker como comando

Una de las primeras acciones que podemos hacer con docker es ejecutar comandos:

```
$ docker run busybox echo 'hola mundo!'
```

La primera vez que lo ejecutamos, descargará la _imagen_ `busybox` e inmediatamente ejecutará el comando `echo 'hola mundo!'` produciendo la salida correspondiente:

```
Unable to find image 'busybox:latest' locally
latest: Pulling from busybox
920777304d1d: Pull complete 
437595becdeb: Pull complete 
Digest: sha256:4a731fb46adc5cefe3ae374a8b6020fce9
Status: Downloaded newer image for busybox:latest
hola mundo!
```

A partir de tener la imagen `busybox` local, podemos ejecutar otros comandos con ella:

```
$ docker run busybox ps xa
PID   USER     TIME   COMMAND
    1 root       0:00 ps xa
```

Para saber por qué tenemos un único proceso con `PID 1`, ver [Cómo funciona docker](../chapter01/01funciona.md)
