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

## Cambiar Fuente y tamaño de letra en Docker Desktop

    Settings, General, Enable Docker Terminal
        Fuente: Cascadia Code NF
        Font Size: 12

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

## Instalar postgres 9.6 y restaurar base de datos
```sh
# Instalar imagen
docker pull postgres:9.6
# Crear volumen para administrar bases de datos postgres
mkdir pg-easba-volume
# Crear el contenedor con definición de usuarios
docker run --name pg-easba -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:9.6
# Verificar la versión de la base de datos
docker exec -it pg-easba bash
postgres --version
# Conectar remotamente desde un cliente
Abrir DBEaver:
    Conected by: Host
    Host: localhost
    Database: postgres
    Usuario: dev
    Contraseña: dev
# Restaurar Base de Datos
    # Crear una carpeta de archivos SQL
    docker exec -it pg-easba bash
    cd /home
    mkdir sqlfiles
    exit
    # Copiar archivos de consulta al contenedor
    docker cp ~/Documents/MAESTRIA_CIENCIA_DE_DATOS/Mineria_de_Datos_2/Database_Easba_2016/easbadb.sql pg-easba:/home/sqlfiles
    # Ingresar con el usuario de postgres
    docker exec -it pg-easba bash
    psql -U postgres
    # Crear base de datos
    create database easbadb;
    # Seleccionar Base de Datos
    \c easbadb;
    # Ejecutar el archivo .sql
    \i /home/sqlfiles/easbadb.sql
    # Listar Tablas
    \dt
```

## Instalar Postgres en ARMx64

1. Instalar la imagen de postgres ultima version estable

```sh
docker pull postgres:latest
```

Verificar 

```sh
docker images
```

2. Crear un directorio para el volumen de postgres

```sh
mkdir  ~/Docker_Volumes/postgres
```

3. Crear el contenedor para postgres

Ejecutar el comando:

```sh
docker run --name postgres \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_PASSWORD=postgres \
  -v ~/Docker_Volumes/postgres:/var/lib/postgresql/data \
  -p 5432:5432 \
  -d postgres:latest
```

## Conectar un cliente SQL (DBeaver) a Postgres

Crear una nueva conexión: Menu > Nueva conexion, PostgresSQL

    General:
        Server Host:  localhost
        Database: (dejar en blanco para ver todas la dbs y elegir un nombre en caso de usar un db especifico) 
        Port: 5432
        Nombre de usuario: postgres
        Contraseña: postgres

## Contenedor Postgres en Windows

*Instalar Docker Desktop*

Si no está instalado Docker, descargar desde (Docker Desktop)[https://www.docker.com/products/docker-desktop/] y asegúrarse de que esté en modo WSL 2 o Hyper-V.

Verificar el modo de ejecución:
    
    Verificar en Docker Desktop
        Abre Docker Desktop.
        Ve a Settings > General.
        Si ves la opción "Use the WSL 2 based engine" activada, entonces estás en WSL 2.
        Si no está activada, Docker está corriendo con Hyper-V.

*Ejecutar el contenedor con volumen*

Abrir CMD

```sh
    docker pull postgres

    docker run --name pg_senasag -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -v F:\DOCKER_VOLUME\postgres_senasag:/var/lib/postgresql/data -d postgres:latest
```
Conectar con una base de datos especifica

```sh
    docker run --name pg_senasag -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=senasagdb -p 5432:5432 -v F:\DOCKER_VOLUME\postgres_senasag:/var/lib/postgresql/data -d postgres:latest
```

Verificar que el contenedor está corriendo

```sh
    docker ps
```

Inngresar al shell de postgres

```sh
    docker exec -it pg_senasag psql -U postgres
    docker exec -it pg_senasag psql -U postgres -d senasagdb
```

Conectarse a un cliente PostgreSQL

Desde cualquier cliente, usa los siguientes datos:

    Host: localhost
    Puerto: 5432
    Usuario: admin
    Contraseña: admin
    Base de datos: midb

Errores de conexión de cliente DBEaver:

    Maven artifact 'org.postgresql:postgresql:RELEASE' cannot be resolved in external repositoresMaven artifact 'org.postgresql:postgresql:RELEASE' cannot be resolved in external repositores DBEAVER

Solución:

    In my case I had to add the Maven index site url in DBeaver as follows:

        Go to DbBeaver "Preferences" menu
        Locate "Connections" -> "Drivers" -> "Maven"
        Click "Add" and paste this link: https://mvnrepository.com
        Click "Apply" and "Close"
        On the driver settings menu that will appear, click "Download"

    After the download has finished, I was able to connect to the database.


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
docker run --name mysqldb --env MYSQL_ROOT_PASSWORD=2687126 -v ~/Documents/Docker/Volumenes/mysql-volume:/var/lib/mysql -d -p 3306:3306 mysql 

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
    # Crear una tabla
    CREATE TABLE juan_innodb (
      id  INT4 AUTO_INCREMENT PRIMARY KEY,
      data VARCHAR(100)
    ) ENGINE = INNODB;
    # Insertar Datos
    INSERT INTO foo_innodb (data) VALUES ('bmw');
    INSERT INTO foo_innodb (data) VALUES ('toyota');
    INSERT INTO foo_innodb (data) VALUES ('ford');
    # Listar todas la tablas;
    show tables;
    # Mostrar columnas de una tabla
    show columns from table_name; 
    describe table_name;
    # Bloqueo a nivel de fila
    # Inicial transacción
    star transactions;
    select * from foo_innodb;
    update foo_innodb set data = 'nissan' where id = 1;
    # Cerrar transacción
    commit; 
    #rollback;

    # limpiar pantalla
    Ctrl + l
    # salir 
    exit
```

## Instalar paquetes en el contenedor de MySQL

```sh
# copiar la base de datos al contenedor
docker cp ~/Downloads/employees_db.zip mysqlsdb:/home

# ingresar al contenedor
docker exec -it mysqldb bash

# instalar paquetes
microdnf install -y vim
microdnf install -y yum
yum update
yum install unzip

# descomprimir la base de datos
cd /home
unzip employees_db.zip
cd employees_db

# cargar la base de datos
mysql -u root -p < employees.sql

# ingresar como usuario root a mysql
mysql -u root -p

# hacer un listado de las bases de datos
show databases;

```
## Conectar un cliente SQL (DBeaver) a Mysql

Crear una nueva conexión:

    General:
        Server Host:  localhost
        Database:
        Nombre de usuario: root
        Contraseña: 2687126

    Driver properties:
        allowPublicKeyRetrieval      true

## Instalar Laravel 11 en Docker

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
--volume ~/Documents/Docker/Volumenes/mariadb:/var/lib/mysql \
-d -p 3306:3306 mariadb
# Ejecutar el contenedor de Laravel
docker run -d --name laravel \
--env DB_HOST=mariadb \
--env DB_PORT=3306 \
--env DB_USERNAME=root \
--env DB_PASSWORD=2687126 \
--env DB_DATABASE=tramitesdb \
--network laravel-network \
--volume ~/Documents/Docker/Volumenes/laravel/sistram:/app \
-d -p 8000:8000 bitnami/laravel:latest
```
*Ejecutar comandos Laravel*

```sh
docker exec laravel php -v  
docker exec laravel php artisan list    
```

## Instalar SQL Server 2019 en aquitectura ARMx64 Macos

Verificar si esta instalado docker

```sh
docker --version
```

1. Descargar la imagen oficial de SQL Server 2022

```sh
docker pull mcr.microsoft.com/mssql/server:2019-latest
```

Esto descarga la versión más reciente y estable de SQL Server 2022.

2. Crear un volumen apuntando a una carpeta local (~/Docker_Volumes/sqlserver)

Primero, crea una carpeta en tu sistema local para almacenar los backups:

```sh
mkdir -p ~/Docker_Volumes/sqlserver
```

Docker no puede usar directamente volúmenes con ruta absoluta en docker volume create, pero puedes hacer bind-mount directamente en el docker run:

3. Crear el contenedor y montar la carpeta como volumen

```sh
docker run -d \
  --platform linux/amd64 \
  --name sqlserver \
  -e "ACCEPT_EULA=Y" \
  -e "MSSQL_SA_PASSWORD=Juanfer2687." \
  -e "MSSQL_PID=Developer" \
  -e "MSSQL_MEMORY_LIMIT_MB=2048" \
  -p 1433:1433 \
  -v ~/Docker_Volumes/sqlserver:/var/opt/mssql \
  --cap-add SYS_PTRACE \
  mcr.microsoft.com/mssql/server:2019-latest
```


4. Verificar que todo esté funcionando

Verifica que el contenedor está en ejecución:

```sh
docker ps
```

Verifica que el volumen esté montado correctamente:

```sh
docker exec -it ls /var/opt/mssql
```

Se debe ver el contenido de ~/Docker_Volumes/sqlserver



5. Conectar a Sql Server desde un cliente como AZURE DATA STUDIO

Para eso debe ingresar los siguiwentes parámetros: ir a > Connections

| Campo                | Valor                                     |
| -------------------- | ----------------------------------------- |
| **Connection type**  | `Microsoft SQL Server`                    |
| **Input type**       | `Parameters`                              |
| **Server**           | `localhost,1433`                          |
| **Authentication**   | `SQL Login`                               |
| **User name**        | `sa`                                      |
| **Password**         | `Juanfer2687.`                            |
| **Database**         | (dejar en blanco o usar `master`)         |
| **Encrypt**          | `Mandatory`                               |
| **Trust server cert**| **Truee** (muy importante en Linux o Mac) |
| **Server group**     | (dejar en blanco o `Default`)             |
| **Name**             | (dejar en blanco)                         |



6. Sacar un backup de una base de datos dentro del contenedor

Abrir una nueva consulta en Azure Data Studio

Hacer clic en New Query (nueva consulta), y ejecutar:

```sql
BACKUP DATABASE [master] 
TO DISK = N'/var/opt/mssql/backup/master_backup.bak' 
WITH FORMAT, INIT, SKIP, COMPRESSION, STATS = 10;
```
**Nota:** reemplazar 'master' por la base de datos a respaldar, mantener los corchetes

Verificar si se respaldo la base de datos correctamente

```sh
ls -lh ~/Docker_Volumes/sqlserver
```

Mostrará la base de datos respaldad en .bak dentre del directorio ~/Docker_Volumes

Si no aparece nada después del backup?

Asegúrarse de que el backup SQL no falló.

Verifica que el contenedor esté en ejecución (docker ps).

Asegúrate de estar mirando la carpeta correcta en el host (~/Docker_Volumes/sqlserver).

Probar en el contnedor escribiendo un archivo de texto en esa ruta, y viendo si aparece en tu host:

```bash
docker exec -it sqlserver bash
echo "prueba" > /var/opt/mssql/backup/archivo.txt
```
Luego, en tu host:

```bash
cat ~/Docker_Volumes/sqlserver/archivo.txt
# → debería mostrar: prueba
```

7. Restaurar una base de datos

Al igual que en el paso anterior ejecutar en Azure Data Studio:

```sql
RESTORE DATABASE [MiBaseDeDatosRestaurada]
FROM DISK = N'/var/opt/mssql/backup/MiBaseDeDatos.bak'
WITH MOVE 'MiBaseDeDatos' TO '/var/opt/mssql/data/MiBaseDeDatos.mdf',
     MOVE 'MiBaseDeDatos_log' TO '/var/opt/mssql/data/MiBaseDeDatos_log.ldf',
     REPLACE;
```

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
docker start -a container

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


# Ejemplos:
## Implementar un servidor de alta disponibilidad con apache que tenga un balanceador de carga

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
