# Docker como comando

También podemos tomar una imagen cualquiera, aunque tenga una aplicación instalada y ejecutar comandos en ella:

```
$ docker container run busybox echo 'hola mundo!'
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
$ docker container run busybox ps xa
PID   USER     TIME   COMMAND
    1 root       0:00 ps xa
```

Para saber por qué tenemos un único proceso con `PID 1`, ver [Cómo funciona docker](../chapter01/01funciona.md)

**Cada vez que ejecutamos una imagen**, queda guardado el contenedor ejecutado, es decir no se borra:

```
$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS                                                                         NAMES
d223748120dc        busybox             "echo 'hola mundo!'"     17 seconds ago      Exited (0) 16 seconds ago                                                                                 mystifying_heyrovsky
4018dd3cdd71        hello-world         "/hello"                 21 minutes ago      Exited (0) 21 minutes ago                                                                                 vigorous_shannon
```

---

## Ejercicios

### 1.

Ejecute los siguientes comandos con imagen `alpine`:

- `ls -l`
- `cat /etc/alpine-release`
- `ps axu`

### 2.

Compare la salida del comando `mount` ejecutado en el sistema GNU/Linux y dentro de un contenedor (por ej. con la imagen `alpine`). 

Note la diferencia del directorio `/` montado en el contenedor y en el sistema _externo_.

### 3.

Encuentre la diferencia entre ejecutar el comando `man` en las imágenes de `alpine` y `busybox`.

