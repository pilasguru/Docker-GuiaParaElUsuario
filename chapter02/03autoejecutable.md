# Docker autoejecutable

Cuando utilizamos docker para correr una imágen que ya tiene un proceso configurado decimos que ejecutamos un proceso _docketizado_.

```
$ docker run hello-world
```

La primera ejecución bajará la imagen `hello-world` y producirá la siguiente salida:

```
Hello from Docker.
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from
    the Docker Hub.
 3. The Docker daemon created a new container from that 
    image which runs the executable that produces the output 
    you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, 
    which sent it to your terminal.

To try something more ambitious, you can run an Ubuntu container 
with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free 
Docker Hub account:
 https://hub.docker.com

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/

```
Esta imagen ha sido creada con el único fin de correr ese proceso _docketizado_ que __exclusivamente__ muestra ese texto.

---

## Referencias: 

- [https://hub.docker.com/_/hello-world/](https://hub.docker.com/_/hello-world/)


