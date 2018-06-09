# Multiple contenedores

Ejecutar dos containers vinculados

```
$ docker image pull mariadb:latest

$ docker container run -p 3306:3306 \
--name mysql \
-e MYSQL_ROOT_PASSWORD=pass123 \
-d mariadb:latest

$ docker image pull nimmis/apache-php5

$ docker container run -d \
-p 80:80 \
--name apache2 \
--link mysql \
nimmis/apache-php5

$ docker exec -it apache2 bash -c \
"echo '<?php phpinfo() ?>' > /var/www/html/test.php"

$ curl http://localhost/test.php

$ docker exec -it apache2 /bin/bash
/# apt-get update && apt-get install -y mysql-client
/# mysql -u root -ppass123 -h mysql 
```


```
mkdir -p wp/database wp/html; cd wp

docker run \
-e MYSQL_ROOT_PASSWORD=rootpass \
-e MYSQL_DATABASE=wordpress \
--name wordpressdb \
-v "$PWD/database":/var/lib/mysql \
-d mariadb:latest

docker run \
-e WORDPRESS_DB_PASSWORD=rootpass \
--name wordpress \
--link wordpressdb:mysql \
-p 8082:80 \
-v "$PWD/html":/var/www/html \
-d wordpress
```




