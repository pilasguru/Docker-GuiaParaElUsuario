# Espacio de host 

Montar una carpeta desde del host directamente dentro de un contenedor se hace utilizando la opción 

`-v path-host:path-container`

Y se configura al lanzar el contenedor:

```
docker container run --name web-nginx -v /opt/website:/usr/share/nginx/html:ro -d nginx
```

Esto hará que la carpeta del host `/opt/website` quede presentada como la carpeta `/usr/share/nginx/html` en el contenedor.

El atributo `:ro` hará que para el contenedor sea un espacio de solo lectura.

---

## Referencias:

- bind mount