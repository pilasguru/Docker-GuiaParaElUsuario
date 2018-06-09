# Redes de contenedores

Los contenedores suponen aislación, por lo que para vincularlos tenemos cuatro tipos de opciones o formas de vinculación.

1. Contenedores cerrados (_none_)
2. Contenedores abiertos (_host_)
3. Contenedores detrás de bridges (_bridge_)
4. Containers juntos 

Docker ofrece un sistema muy flexible de red, que permite crear nuestra propia configuración, para atender necesidades específicas.

El comando `network ls` mostrará las redes disponibles

```
$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
67bf7f355a4e        bridge              bridge              local
727420fae124        host                host                local
fa2601d6c7fa        none                null                local
```

