# Laravel

![Laravel](images/laravel.png)

Laravel es un framework PHP gratis y de código abierto que brinda un conjunto de herramientas y recursos para crear aplicaciones web modernas. Posee un ecosistema integral que combina funciones integradas y una variedad de paquetes y extensiones compatibles. 

Laravel incluye herramientas que facilitan la construcción de aplicaciones web, haciendo de este proceso algo mucho más rápido y dando como resultado un código bien estructurado y fácil de mantener.

## Entornos de Desarrollo Laravel

* Para Windows se tiene [LARAGON](https://laragon.org/).
* Para entornos Linux es recomendable usar [LARAVEL SAIL](https://laravel.com/docs/10.x/sail).
* Para MACOS el mas recomendable es [LARAVEL HERD](https://herd.laravel.com/)

## Requerimientos para Desarrolar Aplicaciones Laravel

* [PHP](../Php/Php.md)
* NGINX ó APACHE
* [MYSQL](../MySQL/MySql.md) (ò PGSQL, SQLITE, etc)
* Gestor de una Base de Datos ([DBeaver](../DBeaver/DBeaver.md))
* Editor de Código [VSCODE](../Visual_Studio_Code/Visual_Studio_Code.md) (PHPSTORM)
* Terminal de Comandos [iTerm](../iTerm/iTerm.md)

## Instalación 

1. Instalación de Laravel HERD

Herd es un entorno de desarrollo nativo de Laravel y PHP increíblemente rápido para macOS. Incluye todo lo que se necesita para comenzar con el desarrollo de Laravel, incluido PHP y nginx. 

Instalar [Herd Laravel](https://herd.laravel.com/) 

Al instalar HERD tambien se instala: PHP, COMPOSER y LARAVEL

**Nota:** Si se tenia instalado valet es necesario detener el servicio y removerlo de la siguiente manera
```sh
valet stop
composer global remove laravel/valet
```
reiniciar Herd
```sh
herd restart
```
de esta manera se asegura un correcto funcionamiento de Herd

2. Configurar la carpeta de Sitios donde se crearan los proyectos Laravel
```sh
Abrir Herd
Settings
General
Herd Paths (+)
    Adicionar la Carpeta /Sites
``` 

3. Instalación de [MySql](../MySQL/MySql.md)

## Verificar la instalación de los prerequisitos

Ejecutar los siguientes comandos:

```sh
php --version
composer --version
laravel --version
```
**NOTA:** Si ocuure el error "zsh:command not found laravel" al ejecutar "Laravel --version," es porque no esta instaladao Laravel y no está configurado el PATH global. 
```sh

zsh: command not found: laravel

```
Para corregir este error: hacer lo siguiente:

1. Verificar si el archivo de configuraciones zsh no tenga errores
```sh
zsh
```
corregir si existieran errores en zsh

2. Instalar Laravel y todas sus dependencias de manera global
```sh
composer global require "laravel/installer" --update-with-all-dependencies
```

3. Configurar el PATH global de Laravel
```sh
export PATH="$HOME/.config/composer/vendor/bin:$PATH"
source ~/.zshrc
```
O también de forma permanente:

```sh
echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >>  ~/.zshrc
source ~/.zshrc
```
Tambien verificar si esta instalado la Base de Datos

```sh
mysql --version
```









## HTTP Status Codes and the Response Format

We’ve also added the response()->json() call to our endpoints. This lets us explicitly return JSON data as well as send an HTTP code that can be parsed by the client. The most common codes you’ll be returning will be:

|-----------|-----------------------------------------------------
|   Code    |   Descriptive
|-----------|-----------------------------------------------------
|   200     |   OK. The standard success code and default option.
|   201     |   Object created. Useful for the store actions.
|   204     |   No content. When an action was executed successfully, but there is no content to return.
|   206     |   Partial content. Useful when you have to return a paginated list of resources.
|   400     |   Bad request. The standard option for requests that fail to pass validation.
|   401     |   Unauthorized. The user needs to be authenticated.
|   403     |   Forbidden. The user is authenticated, but does not have the permissions to perform an action.
|   404     |   Not found. This will be returned automatically by Laravel when the resource is not found.
|   500     |   Internal server error. Ideally you're not going to be explicitly returning this, but if something unexpected breaks, this is what your user is going to receive.
|   503     |   Service unavailable. Pretty self explanatory, but also another code that is not going to be returned explicitly by the application.



## Ejecutar un Proyecto Laravel

Ejemplo: 

```sh
git clone https://github.com/karoys/laravel-native-roles-auth.git projectname
cd projectname
composer install
cp .env.example .env
php artisan key:generate
    add your database info in .env
php artisan migrate 
php artisan db:seed 
php artisan serve 
    start the app on http://localhost:8080/
```

