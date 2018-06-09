# Contenedores juntos
 
En una red de contenedores juntos, multiple contenedores comparten la misma interfaz de red y loopback; como resultado podemos crear redes cerradas y levantar otros container en la misma red que se pueden comunicar unos con otros. De esta forma se pueden crear containers aislados de internet pero vinculados por red entre ellos redes.

Para crear un contenedor unido a otro utilizamos el argumento `--net container: nombre`, como este ejemplo:

Creamos un primer contenedor en una cerrado:

```
$ docker run --name contenedor_cerrado --net none -it alpine /bin/sh
```

Creamos un segundo contenedor pegándolo al creado en el paso anterior:

```
$ docker run --net container:contenedor_cerrado -it alpine /bin/sh
```

