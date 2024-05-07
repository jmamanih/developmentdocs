# Docker

![docker](images/docker.png)

**¿Qué es Docker?**
Docker es una herramienta diseñada para crear, implementar y ejecutar aplicaciones en contenedores. Un contenedor es una unidad de software que contiene todos los componentes necesarios para que una aplicación se ejecute, incluyendo el código, las bibliotecas y las dependencias. Los contenedores son una forma ligera de virtualización que permite a las aplicaciones ejecutarse de manera más rápida y segura que en un sistema operativo tradicional.

## Instalación de Docker

El primer paso para empezar a utilizar Docker es instalarlo en tu sistema operativo. Docker es compatible con Windows, macOS y Linux. 

* Instalación de Windows
* Instalación en Linux
* Instalación en Mac

## Crear un contenedor

Una vez que tienes Docker instalado, puedes empezar a crear contenedores. Para crear un contenedor, necesitas una **imagen de Docker**. Una imagen es un archivo que contiene todas las instrucciones necesarias para crear un contenedor. Puedes buscar imágenes de Docker en **Docker Hub**, el registro público de imágenes de Docker.

Para crear tu primer contenedor, puedes utilizar la imagen de Nginx, un servidor web ligero y rápido. Abre una terminal y escribe el siguiente comando:

```sh
docker run -d -p 80:80 nginx
```

## Crear y gestionar imágenes se Docker

¿Qué es una imagen de Docker?
Una imagen de Docker es un paquete de software que contiene todo lo necesario para ejecutar una aplicación, incluyendo el código, las bibliotecas y las dependencias. Las imágenes de Docker son como plantillas que se utilizan para crear contenedores de Docker. Una vez que se ha creado una imagen de Docker, se puede utilizar para crear múltiples contenedores que ejecuten la misma aplicación.



tutorial
https://www.youtube.com/watch?v=9eTVZwMZJsA


https://www.youtube.com/watch?v=6idFknRIOp4


## Instalar Postgres en Docker

```sh
# Descargar la imagen de postgres ultima version
docker pull postgres

# Crear un contenedor de postgres mediante docker-compose
# Crear un archivo de creacion de contenedor
# docker-compose.yml
services:
  pg-db-agenda:
    container_name: pg-agenda
    image: postgres:11
    restart: always
    hostname: pg-server-agenda
    environment:
      POSTGRES_DB: agendadb
      POSTGRES_USER: developer
      POSTGRES_PASSWORD: developer
    volumes:
      - ~/Documents/Docker/Prac2/pg-agenda-volume:/var/lib/postgresql/data 
      - ~/Documents/Docker/Prac2/MCD_create.sql:/docker-entrypoint-initdb.d/create_tables.sql
      - ~/Documents/Docker/Prac2/data.sql:/docker-entrypoint-initdb.d/data.sql
    ports:
      - "5432:5432"
# Levantar el contenedor
docker-compose up -d
docker-compose up -d --force-recreate
# NOTA: si al conectarse a la base de datos sale el error: FATAL: password authentication failed for user "developer", eliminar o comentar los volumenes

#  
# Crear un contenedor mediante linea de comando
docker run --name pg-agenda -e POSTGRES_USER=developer -e POSTGRES_PASSWORD=developer -p 5432:5432 -d -v ~/Documents/Docker/Volumenes/pg-agenda-volume:/var/lib/postgresql/data postgres

# Mostrar contenedores en ejecución
docker ps

# Ejecutar comandos Bash en el contenedor para crear base de datos
docker exec -it pg-agenda bash

    # Cambiar de usuario (a developer) que se definio al momento de crear el contenedor
    psql -U developer
        # Crear Base de Datos 
        CREATE DATABASE agendadb;
         # Listar las bases de datos
        \l
        quit
    # Salir del usuario postgres
    exit

    # Crear carpeta para copiar archivos desde el host
    cd /home
    mkdir sqlfiles

# Copiar archivos de consulta al contenedor
docker cp ~/Documents/Docker/Prac2/MCD_create.sql pg-agenda:/home/sqlfiles
docker cp ~/Documents/Docker/Prac2/data.sql pg-agenda:/home/sqlfiles 

    # Ingresar nuevamente con el usuario developer
    psql -U developer
    # Seleccionar Base de Datos
    \c agendadb
    # Ejecutar un archivo .sql
    \i /home/sqlfiles/MCD_create.sql
    # Listar Tablas
    \dt
    # Insertar datos a las tablas
    \i /home/sqlfiles/data.sql
    # Consultar datos
    SELECT p.person_id, p.first_name, p.last_name, c.contact_type, c.contact_data     
    FROM person p JOIN contact_info c ON ( p.person_id = c.person_id);
```

Nota: cuando no se usa el parametro -d se puede usar
      Ctrl+C para detener la ejecución de un contenedor

## Instalar MongoDB en Docker

```sh

# Instalar Mongo DB
docker pull mongo

# Ejecutar Mongo en un Contenedor
docker run -d --name mongo-agenda -e MONGO_INITDB_ROOT_USERNAME=developer -e MONGO_INITDB_ROOT_PASSWORD=developer -p 27017:27017 -v ~/Documents/Docker/Volumenes/mongo-agenda-volume:/data/db mongo

# Ingresar al contenedor de mongo
docker exec -it mongo-agenda bash
    # Ver variables de entorno
    env
    # Ejecutar el Shell de Mongo
    mongosh
    # Cambiar a usuario Administrador
    use admin
    # Autenticarse
    db.auth("developer","developer")
    # Mostrar todas las bases de datos
    show dbs
    # Crear una base de datos ej: agenda
    use agenda
    # Ver base de datos en uso
    db
    # Insertar un registro
    db.agenda.insertOne({
        "first_name": "JUAN",
        "last_name": "PEREZ",
        "contact_info": [
            {
                "contact_data": "72023456",
                "contact_type": "PHONE",
            },
            {
                "contact_data": "jperez@gmail.com",
                "contact_type": "EMAIL",
            }
        ]
    });
    # HAcer un listado general
    db.agenda.find({});
    # Mostrar Colecciones
    show collections

```
Conectarse a mongo mediante un cliente
* Instalar MongoDB Compass descargar el instalador de: (https://www.mongodb.com/try/download/compass)
* En New Connection, URI escribir:
    mongodb://developer:developer@localhost:27017
* Presionar el Boton Connect

## Instalar NEO4J en docker

```sh
# Descargar imagen de NEO4J
docker pull neo4j
# Crear una carpeta para el volumen de neo4j
mk dir ~/Documents/Docker/Prac2/neo4j-data
# Ejecutar el Contenedor
docker run --name neo4j-mcd -p 7474:7474 -p 7687:7687 -v ~/Documents/Docker/Prac2/neo4j-data:/data -d neo4j
# Ingresar a
http://localhost:7474
# Configurar Usuario y Contraseña
Connect URL: neo4j://localhost:7687
Database:
Authentication type: Username/Password
Username: neo4j
Password: neo4j
Connect
# Cambiar contraseña
New password:  Neo4j2687126
Repeat new password: Neo4j2687126
# Iniciar
: play start
# Otros comandos
:help commands
:help keys
:help MATCH
:sysinfo
:history
:help server
:clear
# Crear Nodos con propiedades
CREATE (Paco:Person {name:'Paco', born:1964})
CREATE (Juan:Person {name:'Juan', born:1967})
CREATE (Andres:Person {name:'Andres', born:1961})
CREATE (Hugo:Person {name:'Hugo', born:1960})
CREATE (Natalia:Person {name:'Natalia', born:1967})
CREATE (Miriam:Person {name:'Miriam', born:1965})
CREATE (Rosa:Person {name:'Rosa', born:1952})

# Crear sus relaciones
CREATE
   (Paco)-[:FRIEND_OF {role:['Amigo de Trabajo']}]->(Juan),
   (Paco)-[:FRIEND_OF {role:['Amigo de Trabajo']}]->(Andres),
   (Juan)-[:FRIEND_OF {role:['Amigo de la infancia']}]->(Hugo),
   (Andres)-[:FRIEND_OF {role:['Amigo de la infancia']}]->(Natalia),
   (Miriam)-[:FRIEND_OF {role:['Amigo de Trabajo']}]->(Rosa)

# Ver grafo
:MATCH (n) RETURN (n)
# Eliminar todo el grafo
:MATCH (n) OPTIONAL MATCH (n)-[r]-() DELETE n,r

# Mostrar Bases de Datos
SHOW DATABASES;
# Mostrar el nombre y el estado de la base de datos predeterminada actual
SHOW DEFAULT DATABASE;
```

## Instalar MySQL ó MariaDB en Docker

```sh
# Descargar contenedor tanto para mariadb o mysqñ
docker pull mariadb:latest
docker pull mysql

# Levantar contenedor de MariaDB
docker run --name mariadb --env MARIADB_ROOT_PASSWORD=2687126 -v ~/Documents/Docker/Volumenes/mariadb-volume:/var/lib/mysql -p 3306:3306 -d mariadb:latest
# Levantar contenedor en MySQL
docker run --name mysqldb --env MYSQL_ROOT_PASSWORD=2687126 -e MYSQL_USER=developer -e MYSQL_PASSWORD=developer -e MYSQL_DATABASE=mcd_db -v ~/Documents/Docker/Volumenes/mysql-volume:/var/lib/mysql -p 3306:3306 -d mysql
# En el caso de mysql no es necesario crear usuario, contraseña y base de datos porque se esta declarando en las variables de entorno

# Ingresar al command line
docker exec -it mariadb bash
docker exec -it mysqldb bash
    # Ingresar al usuario root
    mariadb -u root -p
    mysql -u root -p
    # password: 2687126
    # Mostrar bases de datos;
    show databases;
    # Crear una base de datos;
    create database mcd_db;
    # Crear usuario y dar privilegios a una base de datos
    # Crear usuario de base de datos
    create user 'developer'@'localhost' identified by 'developer';
    # Eliminar usuarios
    drop user 'username'@'localhost';
    # Mostrar usuarios
    select user FROM mysql. user;
    # Asignar todos los privilegios a un usuario y una base de datos
    grant all privileges on mcd_db.* to 'developer'@'localhost';
    flush privileges;
    # Cambiar de Usuarios (cambiar a developer)
    quit
    mariadb -u developer -p
    mysql -u developer -p
    # Ver usuario actual
    select current_user();
    # Seleccionar base de datos
    use mcd_db;
    # Listar todas la tablas;
    show tables;
    # Mostrar columnas de una tabla
    show columns from table_name; 
    # salir 
    exit
```

Conectar un cliente DBeaver:

Crear una nueva conexión:

    General:
        Server Host:  localhost
        Database:
        Nombre de usuario: root
        Contraseña: 2687126

    Driver properties:
        allowPublicKeyRetrieval      true


## COMANDOS DOCKER

```sh
# Construye una imagen a partir de un Dockerfile en el directorio actual
docker build

# Construye una imagen desde un repositorio GIT remoto
docker build https://github.com/docker/rootfs.git#contenedor:docker

# Información de docker
docker info

# Lista de Contenedores solo en ejecución
docker ps

# Lista de todos los contenedores 
docker ps -a

# Detener la Ejecucion de un Contenedor
docker stop ID_or_Name_Container

# Eliminar un contenedor
docker rm ID_or_Name_Container

# Ejecutar linea de comandos dentro de un contenedor
docker exec -it ID_or_Name_Container Command 
docker exec -it postgres bash

# Eliminar todo ya sea cualquier recurso (imágenes, contenedores, volúmenes y redes) que estén pendientes
docker system prune -a

# Eliminar una o varias imagenes
docker rmi Image Image
docker Image prune

# Eliminar todas las imagenes
docker images purge

# Muestra el Historial de una imagen
docker history image

# Muestra información de bajo nivel sobre una imagen
docker inspect image

# Iniciar un contenedor detenido
docker start container

# Detener un contenedor
docker stop container

# Reiniciar un contenedor
docker restart container

# Pausar un contenedor
docker pause container

# Despausar un contenedor
docker unpause container

# Muestra los procesos en ejecución de un contenedor
docker top container

# Muestra información de bajo nivel sobre un contenedor
docker inspect container

# Muestra los lods de un contenedor
docker logs container

# Muestra las estadísticas de uso de los recursos del contenedor
docker stats container

# Crear un volumen
docker volume create nombre-volumen

# Ver volumenes
docker volume ls

# Binding mounth volume
docker run -v path-host:path-contenedor nombre-imagen

# Usar el volumen en un contenedor
docker run -v nombre-volumen:/var/lib/mysql mysql

# Asociar el volumen con una direccion de carpeta
docker run -v ~/Documents/Docker/Almacen:/var/lib/postgresql/data postgres

# Comandos de ejecución
docker run (options) image (command) (arg...)   
    –detach , -d	Ejecuta un contenedor en segundo plano e imprime el ID del contenedor
    –env , -e	    Establece variables de entorno
    –hostname , -h	Establece un nombre de host a un contenedor
    –name	        Asigna un nombre a un contenedor
    –network	    Conecta un contenedor a una red
    -p              Establece el puerto de ejecucíon (8081:8080)

# Inspeccionar un volumen
docker volume inspect nombre_volumen

# Eliminar Volumenes
docker volume rm volume_name volume_name

# Eliminar todos los volumenes
docker volume prune

# Crear una red
docker network create mi_red_docker

# Listar redes
docker network ls

# Eliminar una red
docker network rm mi_red_docker

# Conectar un contenedor a una red
docker network connect mi_red_docker mi_contenedor

# Desconectar un contenedor de una red
docker network disconnect mi_red_docker mi_contenedor

# Inspeccionar una red
docker network inspect Nombre_Contenedor bash
```

La ubicación de almacenamiento de imágenes y contenedores de Docker

    Ubuntu: /var/lib/docker/
    Fedora: /var/lib/docker/
    Debian: /var/lib/docker/
    Windows: C:\ProgramData\DockerDesktop
    MacOS: ~/Library/Containers/com.docker.docker/Data/vms/0/


# Practica.
# Implementar un servidor de alta disponibilidad con apache que tenga un balanceador de carga

```sh
# Crear un directorio para compartir archivos con los contenedores
mkdir Documents/Docker/Prac1
cd Documents/Docker/Prac1

# Crear el archivo index1.html, index2.html y el archivo index3.html con el siguiente contenido 
# solamente cambiará en numero de servidor de acuerdo al nombre de archivo

nvim index1.html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>MCD</title>
  </head>
  <body>
    <h1>Maestría en Ciencia de Datos</h1>
    <h2>Servidor: 1</h2>
  </body>
</html>

# Descargar la imagen httpd del repositorio Docker Hub
docker pull httpd

# Ver imagenes disponibles
docker images

# Crear un contenedor para el primer servidor web
docker run -v ~/Documents/Docker/Prac1/index1.html:/usr/local/apache2/htdocs/index.html -d -p 8081:80 --name webserver1 httpd

docker run -v ~/Documents/Docker/Prac1/index2.html:/usr/local/apache2/htdocs/index.html -d -p 8082:80 --name webserver2 httpd

docker run -v ~/Documents/Docker/Prac1/index3.html:/usr/local/apache2/htdocs/index.html -d -p 8083:80 --name webserver3 httpd

# Obtener la direccion IP del Contenedor
docker inspect webserver1
    "IPAddress": "172.17.0.2",

docker inspect webserver2
    "IPAddress": "172.17.0.3",

docker inspect webserver3
    "IPAddress": "172.17.0.4",

# Descargar la imagen de nginx
docker pull nginx

# Crear el archivo de configuracion de nginx para que funcione como balanceador de carga
nvim nginx.conf

    events {}

    http {

        upstream my_servers {
            #least_conn;        --->  Enviar al servidor con menos trafico
            server 172.17.0.2;
            server 172.17.0.3;
            server 172.17.0.4;
        }

        server {
            listen 80;
            location / {
                proxy_pass http://my_servers;
            }
        }

    }

# Crear el contenedor balanceador de carga
docker run -v ~/Documents/Docker/Prac1/nginx.conf:/etc/nginx/nginx.conf -d -p 8084:80 --name balancer nginx

# hacer el testeo con:
localhost:8084
```