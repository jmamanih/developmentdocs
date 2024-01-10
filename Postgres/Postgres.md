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
NOTA: Error ...bootstrap /gui/501...
Sol. Ejecutar los siguientes comandos

```sh
# Remove postgresql 14 with brew 
brew remove postgresql@14

# Reinstall postgresql 14 with brew
brew install postgresql@14

# Remove all the files in the db folder
rm -rf /usr/local/var/postgresql@14/*

# Kill all process that run any db of the postgresql 14 folder 
pkill -f /usr/local/var/postgresql@14   
   
# Initialize the db folder for postgresql 14 
initdb --locale=C -E UTF-8 /usr/local/var/postgresql@14

# Restart postgresql with brew (should say that it's already running) 
brew services start postgresql@14
```
Error: psql: FATAL: role "postgres" does not exist
Sol.

```sh
createuser -s postgres
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
Reiniciar el servicio.
```sh
brew services start postgresql
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