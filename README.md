# docker_flarum

Información para utilización del Foro de discusión **Flarum**. Se basa principalmente en [el repositorio](https://github.com/mondediefr/docker-flarum) que permite instalar Flarum con **docker-compose**.

## docker-compose
El contenido del **docker-compose.yml** es:
```
version: "3"

services:
  flarum:
    image: mondedie/flarum:stable
    container_name: flarum
    env_file:
      - .flarum.env
    ports:
      - "9003:8888"
    volumes:
      - /mnt/docker/flarum/assets:/flarum/app/public/assets
      - /mnt/docker/flarum/extensions:/flarum/app/extensions
      - /mnt/docker/flarum/nginx:/etc/nginx/conf.d
    depends_on:
      - mariadb

  mariadb:
    image: mariadb:10.4
    container_name: mariadb-flarum
    env_file:
      - .flarum.env
    environment:
      - MYSQL_DATABASE=flarum
      - MYSQL_USER=flarum
    volumes:
      - /mnt/docker/mysql-flarum/db:/var/lib/mysql
```

## Instalación de extensiones

```
# Intalación de la extensión que permite usar Flarum en Español
docker exec -ti flarum extension require darkfoxdeveloper/flarum-ext-spanish

# Instalación de la extensión que permite configurar el acceso mediante LDAP
docker exec -ti flarum extension require tituspijean/flarum-ext-auth-ldap
```

## Personalización literales
```
# Directorio de almacenamiento de literales en el servidor del contenedor (/flarum/app/vendor/darkfoxdeveloper/flarum-ext-spanish/locale )
docker cp ./personalizar/locale/core.yml flarum:/flarum/app/vendor/darkfoxdeveloper/flarum-ext-spanish/locale
´´´
