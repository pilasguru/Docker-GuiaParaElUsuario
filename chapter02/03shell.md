# Docker como shell

Podemos ingresar al contenedor docker para ejecutar los comandos que estén disponibles en la imagen que utilizamos para correrlo.

```
$ docker run -it debian bash
```

donde:

- `-i` crea una sesión interactiva
- `-t` ofrece una terminal (tty)

y la _imagen_ que utilizará es un `debian` mínimo y ejecutará el comando `bash`, dando como resultado un shell:

```
root@ce1a1c7bf990:/#
root@ce1a1c7bf990:/# pwd
/
root@ce1a1c7bf990:/# ps ax
  PID TTY      STAT   TIME COMMAND
    1 ?        Ss     0:00 bash
    6 ?        R+     0:00 ps ax
root@ce1a1c7bf990:/# exit
exit
```

## Ejercicios

### 1.

Utilizamos la funcionalidad interactiva para verificar la aislación entre contenedores, ejecute los siguientes comandos:

```
docker container run -it alpine /bin/ash
```

```
echo "hello world" > hello.txt
ls
exit
```

Ejecutamos otro container y listamos su contenido

```
docker container run alpine ls
```

Busque el container que ha ejecutado con `/bin/ash`

```
docker container ls -a | grep ash
```

e inícielo nuevamente

```
docker container start <container ID>
```

en el container que acaba de iniciar ejecute un comando con la opción `exec`

```
docker container exec <container ID> ls
```

### 2.

Del ejercicio anterior entienda bien al diferencia entre las opciones `exec` y `run` 
