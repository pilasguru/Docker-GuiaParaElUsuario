# Volume

Los volúmenes son recursos administrador por docker directamente y que pueden ser vistos como un disco montado dentro de los contenedores:

## Creación

La creación de un _volume_ se puede realizar de tres formas diferentes:

### 1. Nuevo volúmen  

Con la opción `volume create` se puede crear un volumen con un nombre dado, para luego utilizar:

```
docker volume create MisDatos
```

Y puede ser visto en el listado de volúmenes disponibles:

```
$ docker volume ls
DRIVER              VOLUME NAME
local               MisDatos
```

### 2. Creación con ejecución   

Esta opción es semejante a _bind mount_ pues se usa con la opción `-v` pero se indica un nombre en lugar de un path del host; esto hará que docker cree ese evolumen:

```
docker run -d -v DataVol:/opt/app/data nginx
```

Que hará que el volumen quede presentado dentro del contenedor en la carpeta `/opt/app/data`.

Podemos analizar su configuración:

```
$ docker volume inspect DataVol
[
    {
        "CreatedAt": "2018-06-04T21:31:46Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/DataVol/_data",
        "Name": "DataVol",
        "Options": null,
        "Scope": "local"
    }
]
```

Y dentro del contenedor lo podemos consultar con mount:

```
/dev/sda1 on /opt/app/data type ext4 (rw,relatime,data=ordered)
```


### 3. Volumen anónimo

El volumen anónimo es un espacio de volumen creado por docker (para evitar que los datos se borren al borrar el contenedor), pero que tiene un nombre aleatorio asignado por docker.

```
docker run -d -v /opt/app/data nginx
```

Y podemos consultar en la lista de volúmenes disponibles:

```
$ docker volume ls
DRIVER              VOLUME NAME
local               9af22968682baefc5c10461d1b3aff226c2a917fe3222ac8f90dd768e1ed5238
```
 
## Re-utilizar un volumen creado



## Limpieza

---

## Ejercicios:

### 1.

### 2.

---

## Referencias:

- [https://docs.docker.com/storage/volumes/](https://docs.docker.com/storage/volumes/)








