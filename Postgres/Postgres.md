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
brew services start postgresql
```
Listar los servicios activos
```sh
brew services list
```

## Crear una base de datos

Acceso a la linea de comandos postgres
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

