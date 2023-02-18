# Autenticación de Usuarios (Login)
## Paquete JetStream

**Contenido**



**Referencias**

* [Tutorial Login](https://www.youtube.com/watch?v=2XeVVHdUWMg)
* [Tutorial Laravel 8](https://www.youtube.com/watch?v=2XeVVHdUWMg)

## Crear un proyecto Laravel

**Obtener la Versión de Laravel**

    php artisan --version

**Crear Proyecto Laravel**

    composer create-project --prefer-dist laravel/laravel laravellogin

## Conexión a la Base de Datos

**Crear Base de Datos para la Aplicacion**

    sudo mysql -u root
        CREATE DATABASE lapazdigitaldb;
        SHOW DATABASES;
        quit

**Crear Usuario y Asignar Privilegios**

    sudo mysql -u root
        CREATE USER 'dev'@'localhost' IDENTIFIED BY '12345';
        GRANT ALL PRIVILEGES ON lapazdigitaldb . * TO 'dev'@'localhost';
        FLUSH PRIVILEGES;
        SHOW GRANTS FOR 'dev'@'localhost';

**Asiganr privilegios a un usuario existente**

    sudo mysql -u root
        GRANT ALL PRIVILEGES ON lapazdigitaldb.* TO 'dev'@'localhost';
        FLUSH PRIVILEGES;
        SHOW GRANTS FOR 'dev'@'localhost';

**Verificar privilegios del usuario sobre una base de datos**

    mysql -u dev -p
        Select current_user();
        SHOW DATABASES;
        SHOW FULL TABLES FROM lapazdigitaldb;

**Configurando los parámetros de conexión a la base de datos**

Abrir y Editar el archivo **.env** en el proyecto laravel

        DB_CONNECTION=mysql
        DB_HOST=127.0.0.1
        DB_PORT=3306
        DB_DATABASE=lapazdigitaldb
        DB_USERNAME=dev
        DB_PASSWORD=12345

## Utilizar el paquete jetstream para el Login

Pasos previos

Verificar la instalación de composer tiene que ser superior a la version 2

    composer --version

Descargar el paquete jetstream

    composer require laravel/jetstream
    
Instalar el paquete jetstream, crear migraciones

    php artisan jetstream:install livewire --teams

Ejecutar npm para completar la instalación de las vistas de jetstream

    npm install
    npm run dev

**Ejecutar las migraciones para crear las tablas en la base de datos**

    php artisan migrate

**Verificar la base de datos**

    mysql -u dev -p

        show databases;
        use lapazdigitaldb;
        show tables;
        describe users;

**Iniciar la aplicación**

    php artisan serve

**Configuración de características de Jetstream**

    Todas las funciones relacionadas con la autentificación se pueden activar o desactivar en: config/fortify.php

```php
     'features' => [
        Features::registration(),
        Features::resetPasswords(),
        // Features::emailVerification(),
        Features::updateProfileInformation(),
        Features::updatePasswords(),
        Features::twoFactorAuthentication([
            'confirmPassword' => true,
        ]),
    ],
```
    Las funciones de Jetstream se encuentran en: config/jetstream.php

```php
    'features' => [
        // Features::termsAndPrivacyPolicy(),
        // Features::profilePhotos(),
        // Features::api(),
        Features::teams(['invitations' => true]),
        Features::accountDeletion(),
    ],
```

**Habilitar Fotografia en el Perfil de Usuarios**

Editar el archivo config/jetstream.php

```php
...
'features' => [
        // Features::termsAndPrivacyPolicy(),
        Features::profilePhotos(),
        // Features::api(),
        Features::teams(['invitations' => true]),
        Features::accountDeletion(),
    ],
...
```
```sh
php artisan serve
```
**NOTA**

En el caso de que no se muestre al foto del perfil hacer lo siguiente:

1. Editar el archivo .env y dejar en blanco APP_URL=

```php
APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:/QkIocW0cBpnqsf4Dd1cBNiTpTVX6m+o1oeO3zuAnNQ=
APP_DEBUG=true
APP_URL=
```

2. Ejecutar el comando

```sh
php artisan storage:link
```

Las fotografias se almacenan en: **public/storage/profile-photos/**   


