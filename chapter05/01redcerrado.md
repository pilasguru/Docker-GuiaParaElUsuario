# Contenedores cerrados

Los procesos que corren dentro de un mismo contenedor pueden comunicarse entre ellos mediante la interfaz loopback (localhost). Pero en los contenedores cerrados no hay comunicación ni saliente ni entrante al contenedor; es decir el contenedor no se puede comunicar ni con internet ni con otros contenedores.

Para crear un contenedor en una red cerrada utilizamos el argumento `--net none` cuando lo creamos:

```
docker run --net none -it alpine:latest /bin/sh
```

Este ejemplo abre un shell, pero podríamos asignarle comandos o tareas ya automatizadas en la imagen que levantamos.  Por ejemplo se pueden utilizar para realizar respaldos, actualizar bases de datos, obtener y desplegar estadísticas, y cualquier otra tarea que no requiera conexión de red.

