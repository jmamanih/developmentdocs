# FUNDAMENTOS DE LARAVEL 9

[Fuente: Laravel 9 - Fundamentos](https://aprendible.com/series/fundamentos-de-laravel-9/lecciones/introduccion-al-curso-fundamentos-de-laravel-9)

# Instalación

## Windows 10

* Instalar [Laragon](https://laragon.org/download/)
* Abrir la terminal de Laragon y verificar

  composer -v
  git
  php -v

* Descargar la ultima [version de Php (v.8)](https://www.php.net/downloads.php), Windows download, zip
* Descomprimir el archivo zip, y mover a la carpeta \laragon\bin\php
* Seleccionar ultima version de php en Laragon, clic derecho en laragon, php, version, php_v8 y reiniciar Laragon (restart)
* Abrir la terminal de Laragon y verificar

  php -v

* Instalar el instalador de Laravel

  composer global require laravel/installer
  laravel new projectname
  laravel new -h
* Reiniciar los servicios de laravel
* Ejecutar la aplicacion laravel http://projectname.test

## MacOs

* Asegurarse de haber instalado Homebrew

  brew -v
  brew update
* Instalar php

  brew install php
* Verificar la version de php, debe ser superior a la versión 8.0

  php - v
* Actualizar la versión de php

  brew upgrade php
* Instalar base de datos MySql

  brew install mysql
  brew services restart mysql
  mysql -u root
* Instalar [Composer](https://getcomposer.org/download/)

  php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

  php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

  php composer-setup.php

  php -r "unlink('composer-setup.php');"

* Mover composer al path globbal

  sudo mv composer.phar /usr/local/bin/composer

  composer

* Instalar Laravel Valet (Entorno de desarrollo minimalista con PHP para MacOS)

  composer global require laravel/valet

* Verificar si al PATH de composer esta de manera global

  echo $PATH

* Si no aparece el path ~/.composer/vendor/bin ejecutar el siguiente comando

  export PATH=$PATH:~/.composer/vendor/bin

* Instalar Valet

  valet install

* Para almacenar proyectos crear una carpeta en la Raiz /Sites

  mkdir Sites
  cd Sites

* Para que Valet genere los dominios .test ejecutar lo siguiente

  cd Sites
  valet park

* Instalar el instalador de Laravel

  composer global require laravel/installer

* Crear proyectos Laravel

  laravel new appname

  http://appname.test

* Ver opciones de creacion de aplicaciones con Laravel

  laravel new -h

* Ver proyectos enlazados con Valet

  valet links

* Enlazar un proyecto con valet

  cd proyecto
  valet link

  http://proyecto.test

* Eliminar un proyecto de Valet y dejar de servirlo en un dominio .test

  cd proyecto
  valet unlink

* Detener servicio web en el puerto 80

  valet stop

* Iniciar servicio web con Valet 

  valet start

* Reiniciar servicio web con valet 

  valet restart




