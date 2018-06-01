# Primeros pasos

Estos ejemplos de primeros pasos pretenden mostrar rápidamente acciones básicas que se suelen realizar con docker y, a la vez, dar una primer impresión de su potencia para la ejecución de aplicaciones.	

Puede verificar las opciones disponibles con el comando `docker` sin ningún parámetro ni argumento:

```
Usage:	docker COMMAND

Management Commands:
  config      Manage Docker configs
  container   Manage containers
  image       Manage images
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes
```

El comando `container` es la opción por defecto del comando docker, por lo que generalmente no se escribe, utilizando directamente los sub-comandos.

---

## Ejercicios

### 1. 

Revise con el comando `ps` los procesos _docker_ que están corriendo en su equipo.

### 2. 

Revise los paquetes que están instalados vinculados a docker en su sistema

### 3. 

Liste el _status_ y reinicie el daemon correspondiente a los servicios de Docker Engine.

### 4. 

Localice con el comando `whereis` dónde se encuentra el ejecutable docker 