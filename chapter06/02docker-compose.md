# docker-compose

El utilitario `docker-compose` primate definir y correr ambientes de multiples contenedores con Docker.

Creamos un directorio para nuestro entorno:

```
$ mkdir wpdc; cd wpdc
```


Se basa en el archivo `docker-compose.yml`

```
version: '2'

services:

  wordpressdb:
    image: mariadb:latest
    volumes:
      - ../wp/database:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: wordpress

  wordpress:
    depends_on:
      - wordpressdb
    image: wordpress
    ports:
      - "8082:80"
    volumes:
      - ../wp/html:/var/www/html
    environment:
      WORDPRESS_DB_HOST: wordpressdb:3306
      WORDPRESS_DB_PASSWORD: rootpass
    links:
      - wordpressdb:mysql
```

Y levantamos nuestro entorno con up:

```
$ docker-compose up -d
Creating network "wpdc_default" with the default driver
Creating wpdc_wordpressdb_1
Creating wpdc_wordpress_1
```

```
$ docker-compose ps
       Name                     Command               State          Ports
----------------------------------------------------------------------------------
wpdc_wordpress_1     docker-entrypoint.sh apach ...   Up      0.0.0.0:8082->80/tcp
wpdc_wordpressdb_1   docker-entrypoint.sh mysqld      Up      3306/tcp
```

## Ejercicios

### 1.

Cree un `docker-compose.yml` para levantar una aplicación tomcat de ejemplo [Sample Application](https://tomcat.apache.org/tomcat-8.0-doc/appdev/sample/)

Basados en la imagen [tomcat](https://hub.docker.com/_/tomcat/) que escucha en el puerto 8080


---

Referencias:

* [https://docs.docker.com/compose/overview/](https://docs.docker.com/compose/overview/)
* [https://docs.docker.com/compose/compose-file/compose-file-v2/](https://docs.docker.com/compose/compose-file/compose-file-v2/)
