# Postgresql

## Instalar Postgres en MacOsX

Actualizar brew

```sh
brew update
brew doctor
```

Instalar postgresql

```sh
brew install postgresql
```

Verificar la instalación

```sh
postgres --version
```

Iniciar Gestor de Base de Datos

```sh
brew services stop postgresql
brew services start postgresql
```

Listar los servicios activos

```sh
brew services list
```

NOTA.
Error: psql: FATAL: role "postgres" does not exist
Sol.

```sh
createuser -s postgres
brew services restart postgresql
```

Error: No ingresa a psql
Sol.

```sh
rm /usr/local/var/postgresql@14/postmaster.pid
brew services restart postgresql
```

## Crear una base de datos

Acceso a la linea de comandos postgres

```sh
psql postgres
```
```sh
psql -U postgres
password: postgres
```
Cambio de contraseña.

```sh
    =# ALTER ROLE postgres PASSWORD 'postgres';
```
Otra forma de cambiar contraseña

```sh
psql postgres
    \password postgres
```

Reiniciar el servicio de postgres

```sh
brew services restart postgresql@14
```

Creando la base de datos.

```sh
=# CREATE DATABASE nombre_db;
```

Lista las bases de datos existentes.

```sh
=# \l
```

Para salir
```sh
=# \q
```

## Restaurar una base de datos

1. Crear la base de datos
```sh
psql -U postgres

    =# CREATE DATABASE nombre_db;
    
```
2. Restaurar base de datos
```sh
pg_restore -U postgres -d easba -1 ~/backup.sql
```

## Comandos Postgres

```sh
# -- Comandos PostgreSQL


# Iniciar session 
psql postgres

# Cerrar session
Ctrl+D

# Listar base de datos
\l

# Seleccionar una base de datos o cambiar de base
\c nombre_base_datos

# Listar todas las tablas
\dt

# Listar campos de una tabla
# Si la lista es muy larga veremos que podemos movernos hacia abajo y luego para salir solo digitamos la letra “q”

\d nombre_tabla

# Vaciar una tabla en especifico o el famoso TRUNCATE que conocemos
# Con este comando borramos el contenido de una tabla y reiniciamos su indice sino agregamos RESTART IDENTITY nuestros indices no seran reiniciados y seguiran según el ultimo registro.
TRUNCATE TABLE nombre_table RESTART IDENTITY

# Crear una base de datos
CREATE DATABASE nombre_db;

# Borrar o eliminar una base de datos
DROP DATABASE nombre_db;

# Borrar o eliminar una tabla en especifico
DROP TABLE nombre_tabla;

# Enviar resultados de una consulta a un archivo delimitado por |
# Cabe mencionar que el archivo necesita permisos de escritura.
COPY (SELECT * FROM tablename) TO '/home/tablename.csv' WITH DELIMITER '|';

# Uso de LIMIT y OFFSET
  # Donde:
  # limit: es nuestro limite de registros a mostrar
  # offset: indica desde donde comenzaran a mostrarce los registros

SELECT * FROM nombre_tabla LIMIT limit OFFSET offset;

# Uso de comillas
SELECT “column” FROM “nombre_tabla” WHERE “column” = 'value';

# Generalmente podemos utilizar comillas dobles para nuestras columnas y comillas simples para nuestros valores, esto no es una regla pero a veces es necesario en casos especiales, tales como cuando ocupamos nombres reservados, por ejemplo:
SELECT to FROM table;

# En este caso tenemos un campo llamado “to”, esto nos dará un error de sintaxis, por lo tanto tendremos que usar comillas dobles:
SELECT “to” FROM table;
  
# Salir del cliente psql
\q
```

## Esquemas en Postgres

En PostgreSQL, una base de datos es un contenedor lógico que almacena todos los objetos relacionados, como tablas, vistas, funciones, índices, etc. 

En PostgreSQL, los esquemas son espacios de nombres que permiten organizar y agrupar lógicamente los objetos de base de datos.

Dentro de una base de datos, se pueden crear múltiples esquemas.

¿Para qué se usan los esquemas?

Los esquemas se utilizan para:

    Organizar objetos dentro de una base de datos (por ejemplo, por módulo o área funcional).

    Evitar conflictos de nombres entre objetos (pueden existir tablas con el mismo nombre en diferentes esquemas).

    Controlar el acceso mediante permisos específicos por esquema.

    Separar ambientes dentro de la misma base de datos (por ejemplo, pruebas vs producción).

### Ejemplo práctico de uso de esquemas

Crear una base de datos

    CREATE DATABASE empresa_db;

Conectarse a la base de datos

    \c empresa_db

Crear un esquema

    CREATE SCHEMA rrhh;

Crear una tabla dentro del esquema

    CREATE TABLE rrhh.empleados (
        id SERIAL PRIMARY KEY,
        nombre TEXT NOT NULL,
        puesto TEXT NOT NULL,
        fecha_ingreso DATE
    );

Insertar datos en la tabla del esquema

    Opción 1: Referenciar el esquema explícitamente

        INSERT INTO rrhh.empleados (nombre, puesto, fecha_ingreso)
        VALUES ('Ana López', 'Analista', '2022-03-15');

    Opción 2: Cambiar el esquema por defecto usando SET search_path

        SET search_path TO rrhh;

        INSERT INTO empleados (nombre, puesto, fecha_ingreso)
        VALUES ('Carlos Pérez', 'Gerente', '2021-11-01');


## Desinstalar postgres

```sh
brew uninstall postgres
rm -rf /usr/local/var/postgres
rm /usr/local/var/log/postgres.log
rm -f ~/.psqlrc ~/.psql_history

brew remove postgresql
brew list --formula | grep -e postgres -e psql

```

Or

```sh
# check version
postgres --version
    postgres (PostgreSQL) 13.3

# locate where it is installed
which psql
    /Library/PostgreSQL/13/bin/psql

# change directory$ cd /Library/PostgreSQL/13
open uninstall-postgres.app

#remove Postgres related files
# change to home directory
cd ~
sudo rm -rf /Library/PostgreSQL
sudo rm /etc/postgres-reg.ini
# or
sudo rm -rf /usr/local/opt/postgresql@14
sudo rm /etc/postgres-reg.ini
brew remove postgresql
brew list --formula | grep -e postgres -e psql

# some people also suggested to remove sysctl.conf
# but I don't seem to have this file in my environment
# so I ignored it. You can try if you'd like
sudo rm /etc/sysctl.confrm
    /etc/sysctl.conf: No such file or directory
```

