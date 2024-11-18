# LARAVEL 11 CON DOCKER

## Instalar Laravel 11 y MariaDB en Docker

Ingresar a [Docker Hub](https://hub.docker.com/)
Buscar Laravel
Ingresar a bitnami/Laravel

```sh
# Instalar imagen de Laravel 11
docker pull bitnami/laravel
# Instalar imagen de mysql
docker pull mariadb:latest
# Instalar una red privada
docker network create laravel-network

# Ejecutar el contenedor mysql
docker run --name mariadb \
--env MARIADB_ROOT_PASSWORD=2687126 \
--env MARIADB_DATABASE=tramitesdb \
--network laravel-network \
--volume ~/CODE/DOCKER_VOLUMES/mariadb:/var/lib/mysql \
-d -p 3306:3306 mariadb

# Ejecutar el contenedor de Laravel
docker run -d --name laravel \
--env DB_HOST=mariadb \
--env DB_PORT=3306 \
--env DB_USERNAME=root \
--env DB_PASSWORD=2687126 \
--env DB_DATABASE=tramitesdb \
--network laravel-network \
--volume ~/CODE/DOCKER_VOLUMES/laravel/sistram:/app \
-d -p 8000:8000 bitnami/laravel:latest
```
*Ejecutar comandos Laravel*

```sh
docker exec laravel php -v  
docker exec laravel php artisan list    
```


