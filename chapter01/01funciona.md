# Cómo funciona docker

Generalmente docker (o contenedores) se explican a través de las diferencias entre virtualización y contenedores y destacando los pro y contras de cada uno de ellos.

Los contenedores es un método de encapsular o aislar, a nivel de kernel, procesos y recursos en el sistema operativo de forma que no tengan contacto o posibilidad de conocer otros contenedores que están corriendo sobre el mismo sistema operativo.

Contenedores se construyen a través de métodos de aislamiento (chroot, labels, virtual networks, etc) que hacen que los comandos que se ejecuten en el contenedor (ps, top, ip, free, ls, etc.) solo tengan acceso a los recursos asignados al contenedor y no llegan a ver los del sistema operativo principal ni los de otros contenedores.

Docker es una implementación de las funcionalidades de contenedores para sistemas GNU/Linux que tiene como objetivo facilitar la creación, uso y la posibilidad de compartir los contenedores creados, de forma que no solo se pueden levantar en un sistema, sino que pueden ejecutarse en multiples equipos e, inclusive, distribuciones de Linux.

Las imágenes de docker es la forma en que se comparten los contenedores, mediante repositorios de imágenes llamados `Registry` a los que se accede para obtener imágenes con distinto grado de personalización que se utilizan para correr aplicaciones en distintos sistemas. 

Los docker en cuanto contenedores representan un estándar que permite compartir aplicaciones para poner a correr en distintos sistemas con un mínimo de esfuerzo de instalación y ocupando los recursos que requiera la aplicación, con un mínimo de sobrecarga de construcción o mantenimiento. 

De esta forma docker ha evolucionado a conceptos de máxima aislación entre procesos (Microservicios) y ejecución paralela de varias instancias 


 