# BACKEND

LEVANTAR UN PROYECTO BACKEND DESDE CERO
---------------------------------------
## Instalar git
#### Controador de versiones
------------
Verificar si esta Instalando

    $ git --version

Instalación

    $ sudo apt-get install git

Realizar los siguientes pasos si existe problemas de instalación

    $ sudo nano /etc/apt/source.list
      deb http://ftp.us.debian.org/debian testing main
    $ sudo apt-get update
    $ sudo apt-get install git/testing
    $ git --version

## Instalar nvm
#### Administrador de versiones de node.js

Instalación

    $ sudo apt-get update
    $ sudo apt-get upgrade
    $ sudo apt-get install curl
    $ curl -o-  https://raw.githubusercontent.com/creationix/nvm/v0.31.7/install.sh | bash

    or

    $ wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.7/install.sh | bash
    ...

Al finalizar la instalación reiniciar la terminal

    $ nvm --version

## Instalar node.js
#### Entorno de Ejecución Multiplataforma

Instalación

    $ nvm install 5.6.0
    $ node --version
    $ nvm ls

Usar una version disponible de node.js

    $ nvm use 5.6.0
    $ nvm current

## Instalando dependencias globales via npm
#### sequelize (Framework ORM orientado a SQL)
#### pg-hstore (Módulo para serializar y deserializar datos JSON

    $ npm install -g sequelize sequelize-cli
    $ npm install -g pg pg-hstore

## Instalar postgres
#### Gestor de Bases de Datos

    $ sudo apt-get install postgresql-9.4 postgresql-client-9.4

## Levantar un proyecto Backend

    $ cd /proyecto
    $ npm install
    $ npm run setup
    $ npm start

En caso de existir errores (`babel-node index.js`) se recomienda eliminar la carpeta node_modules y ejecutar npm install tambien se sugiere ejecutar npm install -f

## Error al instalar paquetes npm

write EPROTO 1995436560:error:140770FC:SSL routines:SSL23_GET_SERVER_HELLO:unknown protocol:../deps/openssl/openssl/ssl/s23_clnt.c:794:

Solucion:

    $ npm config set strict-ssl false
    $ npm config set registry="http://registry.npmjs.org/"

# BACKEND EN MODO EJECUCIÓN
-------------------------
Ejecutar aplicacion

    $ nvm use 5.6.0
    $ npm start

Generar Rutas

    $ nvm current
    $ nvm alias default 5.6.0
    // Cerrar terminal
    $ npm run gen-rutas

Hacer persistente la ejecucion del Backend

    $ nodemon
    $ npm install -g nodemon
    $ npm run startdev

Actualizar base de datos para reflejar cambios en el menu

    para actualizar campos en la base de datos editar el archivo lib/config.development.js

    sync: {force: true}

    $ npm start

    luego ejecutar

    $ npm run setup

    volver a editar el archivo lib/config.development
    // sync: {force: true}

    $ npm run  startdev
