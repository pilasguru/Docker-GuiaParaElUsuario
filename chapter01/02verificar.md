# Verificación de la instalación

_No es un objetivo de esta guía abordar la instalación de docker_. Si bien es un proceso sencillo, los requisitos y opciones de configuración varían según dónde se va a utilizar docker.

Docker es nativo de sistemas operativos Linux y los procesos de instalación difieren de acuerdo a la [[distribución y versión de Linux|https://docs.docker.com/engine/installation/linux/ubuntulinux/]] que se use.  Pero en la actualidad, docker se puede instalar en otros sistemas operativos como [[macOS|https://docs.docker.com/engine/installation/mac/]] y [[Windows|https://docs.docker.com/engine/installation/windows/]].

## Verificación de la instalación

Lo primero es consultar la versión instalada de docker:

```
$ docker version
```
que producirá una salida semejante a esta:

```
Client version: 1.6.2
Client API version: 1.18
Go version (client): go1.3.3
Git commit (client): 7c8fca2
OS/Arch (client): linux/amd64
Server version: 1.6.2
Server API version: 1.18
Go version (server): go1.3.3
Git commit (server): 7c8fca2
OS/Arch (server): linux/amd64
```

Y seguidamente con el comando

```
$ docker info
```

saber cómo está docker funcionando en nuestro sistema:

```
Containers: 14
Images: 43
Storage Driver: aufs
 Root Dir: /var/lib/docker/aufs
 Backing Filesystem: extfs
 Dirs: 71
 Dirperm1 Supported: true
Execution Driver: native-0.2
Kernel Version: 3.16.0-4-amd64
Operating System: Debian GNU/Linux 8 (jessie)
CPUs: 4
Total Memory: 7.569 GiB
Name: hostname
ID: CKSU:VCXF:AJB5:6A7Q:AM6D:37TB:IMUJ:G3YA:L7ZU:OGP7:SUSC:OANP
WARNING: No memory limit support
WARNING: No swap limit support
```

