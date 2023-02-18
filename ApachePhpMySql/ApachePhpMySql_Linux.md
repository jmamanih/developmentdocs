# APACHE WEB SEVER - PHP - MYSQL
## Linux 

![Git](images/apachephpmysql.jpg)

**Contenido**



## Instalación en Linux Debian

# MacOS Mojave Setup: Homebrew + Apache + PHP + MariaDB

## Actualización de git en Mojave MacOs

```
xcode-select --install
brew install git
brew upgrade git
git --version
```

## Homebrew Installation

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew tap homebrew/core
brew doctor
brew -v
```
## Install php

```
brew install php
brew upgrade php
php -v

brew info php72

```

```
==> php
To enable PHP in Apache add the following to httpd.conf and restart Apache:
    LoadModule php7_module /usr/local/opt/php/lib/httpd/modules/libphp7.so

    <FilesMatch \.php$>
        SetHandler application/x-httpd-php
    </FilesMatch>

Finally, check DirectoryIndex includes index.php
    DirectoryIndex index.php index.html

The php.ini and php-fpm.ini file can be found in:
    /usr/local/etc/php/7.2/

To have launchd start php now and restart at login:
  brew services start php
Or, if you don't want/need a background service you can just run:
  php-fpm
```



## Instalar o Actualizar  PHP
Verificar la version de PHP instalado que debe ser mayor o igual a v. 7.1.3

Actualizar PHP con brew

```sh
php -v
brew update
brew upgrade
brew install php     # dependiendo de la version que se necesite  brew install php@7.3 por default se instala la última versionbre
brew info php
brew unlink php && brew link php
php -v

export PATH="$(brew --prefix homebrew/php/php72)/bin:$PATH"

php -v
```
Instalar HTTPD

## Instalar Apache 

```sh
brew update
brew upgrade
brew install httpd
sudo brew services start httpd

```
Test Apache
```
http:\\localhost:8080
```
```
nano /usr/local/var/www/index.html
```
```html
<html>
<body>
Welcome !
</body>
</html>
```
```
http://localhost:8080
```

## CONFIGURAR APACHE

Cambiar de sitio
```
cp /usr/local/etc/httpd/httpd.conf /usr/local/etc/httpd/httpd.backup
```
```
mkdir ~/Sites
```
```
nano /usr/local/etc/httpd/httpd.conf
```
```
#Set Apache Port  
Listen 80

# Change Document Root
DocumentRoot "/Users/juanfer/Sites"

# Change de <Directory>
<Directory /Users/juanfer/Sites
   ...
</Directory>

# Enable Rewrite Module
LoadModule rewrite_module lib/httpd/modules/mod_rewrite.so
```

```
apachectl configtest
sudo apachectl configtest
echo "Welcome" > ~/Sites/index.html
```

Verificar errores de sintaxis
```
apachectl -t
```


```
http://localhost
```

Administración de Servicios Apache

```sh
sudo brew services start httpd
sudo brew services stop httpd
sudo brew services restart httpd

sudo apachectl start
sudo apachectl stop
```

ERROR:
```
httpd: apr_sockaddr_info_get() failed for ...
```
Para solucionar el problema editar el archivo de configuración de apache y descomentar la línea ServerNamer localhost:80

```
nano /usr/local/etc/httpd/httpd.conf
sudo apachectl restart
```

## Instalar MySQL

https://gist.github.com/nrollr/3f57fc15ded7dddddcc4e82fe137b58e

```
brew info mysql
```
```
brew install mysql
```
Configuracion Adicional
```
brew tap homebrew/services
brew services start mysql
brew services list
mysql -V
```

Establecer contraseña de administrador a MySql

```
mysqladmin -u root password 'yourpassword'
```
Conectarse a MySql
```
mysql -u root -p
exit
```
## Instalar PhpMyAdmin

```
brew info phpmyadmin
brew install phpmyadmin

```







# APACHE WEB SERVER

### Apache Virtual Host Config XAMPP

Edit File C:\Windows\System32\drivers\etc\hosts

```sh

127.0.0.1 www.lapazdigital.local

```

Edit File C:\xampp\apache\conf\extra\httpd-vhosts.conf

```sh
NameVirtualHost *:80

<VirtualHost *:80>
	DocumentRoot "c:/xampp/htdocs"
	ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "c:/xampp/htdocs/lapazdigital"
    ServerName www.lapazdigital.local
    ServerAlias lapazdigital.local
    <Directory "c:/xampp/htdocs/lapazdigital">
        AllowOverride All
        Require all Granted
        # En versiones anteriores de Apache 2.4 poner estas directivas en lugar de las 2 anteriores.
        # Order allow,deny
        # Allow from all
    </Directory>
</VirtualHost>
```

Add text to virtual configuration

```sh
<VirtualHost *:80>
	DocumentRoot "D:\DEVELOPMENT\Lapazdigitalweb\lapazdigital_new"
	ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "D:\DEVELOPMENT\Lapazdigitalweb\lapazdigital_new"
    ServerName lapazdigital.local
    ServerAlias lapazdigital
    <Directory "D:\DEVELOPMENT\Lapazdigitalweb\lapazdigital_new">
        AllowOverride All
        Require all Granted
        # En versiones anteriores de Apache 2.4 poner estas directivas en lugar de las 2 anteriores.
        # Order allow,deny
        # Allow from all
    </Directory>
</VirtualHost>
```

Restart Apache from XAMPP Control

To check the operation type www.lapazdigital in the browser address bar


### Configuration virtual host to remote access in XAMPP

Edit File: C:\xampp\apache\conf\extra\httpd-xampp.conf

```sh
<IfModule alias_module>
    ...
    Alias /lapazdigital "D:/DEVELOPMENT/Lapazdigitalweb/lapazdigital_new/"
    <Directory "D:/DEVELOPMENT/Lapazdigitalweb/lapazdigital_new/">
        Require all granted
        ErrorDocument 403 /error/XAMPP_FORBIDDEN.html.var
    </Directory>

</IfModule>
```
Restart xampp control

## Evitar el hotlinking

Bloquear accesos a los archivos con extensiones: jpg, jpeg, gif, png, bmp y zip de sitio.com

.htaccess edit file

```sh
RewriteEngine on
RewriteCond %{HTTP_REFERER} !^http://sitio.com*/.*$ [NC]
RewriteCond %{HTTP_REFERER} !^http://sitio.com*$ [NC]
RewriteRule .*\.(jpg|jpeg|gif|png|bmp|zip)$ - [F,NC] 
``` 
 * NC nocase
(case-insensitive), no importa si los términos aparecen en minúsculas o mayúsculas. 
* F forbidden
devuelve a la petición un mensaje de acceso denegado "403 Forbidden".

## UAC Error

Important! Because an activated User Account Control (UAC) on your system some functions of XAMPP are possibly restricted.

Fixed:
You can press OK and install xampp to C:\xampp and not into program files


