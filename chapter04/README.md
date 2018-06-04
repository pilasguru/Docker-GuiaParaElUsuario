# 

Los containers tienen un filesystem _esfímero_, es decir: el filesystem va a estar disponible mientras el container exista. Una vez que el container se borre, el filesystem también será eliminado.

Pero evidentemente, la idea es poder iniciar, detener y borrar containers sin perder datos. Es decir, necesitamos persistir los datos fuera del contenedor. 

Existen dos formas de hacerlo: 

- **bind mount** permite usar un carpeta (path) del host y presentarlo dentro del container en un punto de montado, por ejemplo `/app`.   

Es la forma más fácil de conectar el filesystem del host con el contenedor. 

El _bind mount_ se especifica en el momento de lanzar el contenedor y requiere realizar los procesos de respaldo, migración, etc. con herramientas fuera de docker.

- **volume** es un dispositivo de disco externo el contenedor creado por docker y puede ser utilizado por otros contenedores simplemente indicando la ruta (nombre).


