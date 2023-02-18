# FRONTEND

## LEVANTAR UN PROYECTO FRONTEND DESDE CERO

Se recomienda levantar primero un proyecto Backend

Instalar paquetes

    $ npm install -g bower
    $ npm install -g grunt-cli
    $ npm install -g grunt
    $ npm install -g yo
    $ npm install –g gulp
    $ npm install -g generator-gulp-angular
    $ npm install -g generator-gulp-angular-sub

Instalar dependencias

    $ bower install
    $ npm install
    $ gulp serve

Ejecutar aplicacion

    $ nvm use 5.6.0
    $ gulp serve

Instalar gulp angular sub

    $ npm install -g generator-gulp-angular-sub

Generar vistas para el CRUD

    $ yo gulp-angular-sub:view

    Ej:
    ? the view name tipoDocumentoIdentidad
    ? the view url tipo_documento_identidad
    ? the parent folder in which the the view folder will be created
      modules/parametros

## Error al instalar paquetes npm
      Error ssl.....

      Solucion:

          $ npm config set strict-ssl false
          $ npm config set registry="http://registry.npmjs.org/"
