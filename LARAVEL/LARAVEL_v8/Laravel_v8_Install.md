# INSTALACION DE LARAVEL 8

<a id="topmenu">

## CONTENIDO
* Instalación en Windows 10
* [Instalacion en MacOs](#idsec20 "Instalación en MacOs")
* [Instalación en Linux Debian](#idsec30 "Instalación en Linux")

## Referencias

* [Tutorial Entorno de Desarrollo de Software para Laravel](https://faustocevallos.com/entorno-de-desarrollo-de-software-para-laravel-en-ubuntu/)
* [Video Tutorial de Instalación de Laravel](https://www.youtube.com/watch?v=m-EjyMPUhhY)

## Crear un Entorno de Desarrollo de Software para Laravel

## Instalaciones previas en general para todos los sistemas operativos

* [Git](../Git/Git.md)
* [MySQL](../MySQL/MySql.md)
* [NGINX](../Nginx/Nginx.md)

## Instalación en Windows 10

<a id="idsec20">

## Instalación en MacOs

### Instalaciones Previas en MacOs

* [Homebrew](../MacOs/homebrew.md)


## Instalar Composer en MacOs

Referncia:

    https://getcomposer.org/download/


```sh

mkdir SetupComposer
cd SetupComposer

php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"

ls -l

php composer.phar

```
Configuracion Global en MacOs

```sh
sudo mv composer.phar /usr/local/bin/composer
cd /
composer
```

<a id="idsec30">

## Instalación en Linux

### Laravel + Nginx + Composer + MariaDB + NPM + PHP-FPM


***Actualizaciones Previas***

    sudo apt-get update
    sudo apt-get upgrade

***Instalación General***

    sudo apt install -y nginx php git mariadb-server

Se instaló en una sola instrucción lo siguiente

* **Nginx**, Servidor Web
* **PHP**, Lenguaje de programación
* **Git**, Herramienta para versionamiento de código
* **MariaDB**, Motor de base de datos

*Instalar Extenciones de Php*

    sudo apt install openssl php-{common,curl,json,mbstring,mysql,xml,zip,opcache,fpm} -y


*Verificar el estado de los servicios instalados*

    systemctl status nginx mariadb php7.3-fpm

*Habilitar servicios al arranque del Sistema*

    sudo systemctl enable nginx
    sudo systemctl enable mariadb
    sudo systemctl enable php7.3-fpm

**COMPOSER**

Instalar composer

    sudo apt-get update

    cd ~

    cd Descargas

    sudo apt-get remove composer    

    curl -sS https://getcomposer.org/installer -o composer-setup.php

    sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

    composer --version

Remover composer

    cd ~
    sudo apt-get remove composer

**NodeJS**

Se debe instalar NPM el gestor de dependencias de NodeJS para gestionar assets de Laravel con VueJS, Angular o React.

**_nvm_**

NVM «Node Version Manager», herramienta que nos permite administrar las versiones de NodeJS y NPM.

*Descargar y Ejecutar Bash de NVM*

    wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash

ó también

    curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh -o install_nvm.sh
    bash install_nvm.sh
    
Verificar la instalación de nvm

    nvm --version

Si no muestra la versión entonces ejecutar las siguientes lineas de comando:

    export NVM_DIR="$HOME/.nvm"  
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
    source ~/.profile 

Comprobar nuevamente haciendo esta vez un listado de versiones disponibles

    nvm ls-remote

Despliega el listado de versiones disponibles de NodeJS que dispone nvm

Seleccionar una version LTS, y proceder con la instalación por ejemplo.

    nvm install v14.15.1

Se instaló la versión 14.15.1 de NodeJS.

Usar dicha version.

    nvm use v14.15.1

Comprobar version en uso de NodeJS y NPM

    node -v
    npm -v


## NGINX

[Instalación de Nginx](../Nginx/Nginx.md)


## MYSQL

[Instalar MySQL](../MySQL/MySql.md)


## Configurar Servidor Web Nginx

Una vez instalada la base de datos, se debe configurar el servidor web con Nginx, para que pueda ejecutarse de manera correcta e interpretar PHP con el servicio PHP-FPM, 

[Configurar Servidor Web](../Nginx/Nginx.md "Servidor Virtual con Nginx")

Para que un proyecto Laravel se ejecute en un virtual host en nginx, se debe agregar al archivo default en la ultima linea, lo siguiente:

    sudo nano /etc/nginx/sites-available/default

```vim
# Virtual Host Configuration

server {
    listen 80;
    listen [::]:80;
    server_name blog.test;
    root /var/www/html/blog/public;
    index index.php;
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock; 
    }
}
```
Para verificar la sintaxis ejecutar

    sudo nginx -t

Reiniciar el servicio Nginx

    sudo systemctl restart nginx


## Sincronizar el navegador y servidor en modo desarrollo

[BrowserSync](https://browsersync.io/)


1. Instalar BrowserSync

Abrir el archivo **webpack.mix.js**, y adicionar:

```php

mix.browserSync('http://127.0.0.1:8000');

```
Nota: la URL debe ser la misma que está en el archivo .env Ej.  APP_URL=http://127.0.0.1

Luego Ejecutar:

```sh

npm run watch

```
En esta primera ocación se instalará BrowserSync

2. Levantar el servidor

```sh
php artisan serve
```

3. Ejecutar BrowserSync

```sh
npm run watch
```

