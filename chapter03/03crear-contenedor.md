# Crear a partir de un contenedor

Correr una contenedor basado en la imagen `debian` e ingresar al shell para hacer cambios:

```
docker container run -ti debian bash
```

Ejecutar estos comandos para instalar `figlet` y salir

```
apt-get update
apt-get install -y fidlet
figlet 'hello docker'
exit
```

El container está detenido y a partir de él se puede crear una imagen, que se guarda en el repositorio local, con el comando `container commit`

```
docker container ls -a
docker container commit <CONTAINER-ID>
docker image ls
```

Le colocamos el nombre a la imagen generada con el comando `image tag` pues no lo hicimos junto con el `container commit`

```
docker image tag <IMAGE-ID> confidget
docker image ls
```

Ahora que disponemos de una imagen basada en _debian_ que tiene el comando `figlet` instalado la podemos utilizar:

```
docker container run configlet figlet hola
```

---

## Ejercicios

### 1.

### 2.

