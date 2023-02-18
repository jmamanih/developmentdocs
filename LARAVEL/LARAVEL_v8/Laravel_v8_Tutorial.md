# Laravel 8

![Laravel](images/logo_laravel.png)

Laravel 8 continua las mejoras introducidas por Laravel 7.x, incorporando Laravel Jetstream, clases para las model factories, consolidación de migraciones, trabajos por lotes, mejoras en el manejo de limitación de peticiones, mejoras en el manejo de las colas, componentes dinámicos en Blade, paginación con Tailwind, helpers para testear casos que involucren tiempo, mejoras al comando artisan serve, mejoras en los event listener, y una variedad de otras correcciones y mejoras de usabilidad.

## CONTENIDO

<a id="topmenu">

* [Instalación de Laravel](Laravel_v8_Install.md "Instalación")
* [Crear un proyecto Laravel](#idsec20 "Crear proyecto")
* [Compilar y ejecutar un proyecto Laravel](#idsec30 "compilar y Ejecutar")
* [Autenticación con JWT](Laravel_v8_JWT_Login.md "JWT Login")
* [Login Jetstream](Laravel_v8_Login.md "Login")
* [Poles y Permisos de Usuarios con Spatie](Laravel_v8_Permission_and_Roles.md "Usuarios Roles y Permisos")

## Referencias

[Curso Tutorial de Laravel v8](https://www.youtube.com/watch?v=A-BL8Ir7puE&list=PLZ2ovOgdI-kWWS9aq8mfUDkJRfYib-SvF)

## Instalaciones previas

* [Git](../Git/Git.md)
* [Servidor Web Nginx](../Nginx/Nginx.md)
* [MySql](../MySQL/MySql.md)

<a id="idsec20">

## Crear un proyecto Laravel

1. Otorgar permisos a la carpeta «html» con el usuario del sistema, (juanfer), a fin de evitar la creación del proyecto laravel como super usuario (evitar usar el comando sudo).

    Obtener usuario del sistema

        whoami

    Otorgar permisos

        cd /var/www
        ls -la
        sudo chown -R juanfer:juanfer html
        ls -la

2. Crear un proyecto laravel via composer (Ej. lapazdigitalint)

        cd html
        composer create-project --prefer-dist laravel/laravel lapazdigitalint
    
3. Asignar permisos adicionales del usuario apache a la carpeta del proyecto (Ej. lapazdigitalint)

        cd lapazdigitalint
        sudo chgrp -R www-data bootstrap/cache storage
        sudo chmod -R ug+rw bootstrap/cache storage

Al ejecutar Laravel generalmetne dan errores por permisos de lectura y escritura en los directorios bootstrap/cache y el storage, con estas dos líneas se evitarán esos errores. 

4. Arrancar el proyecto

        php artisan serve

    ```
    127.0.0.1:8000          dirección donde esta corriendo la aplicación web
    Ctrl+C                  para detener servidor web
    ```
5. Crear el repositorio remoto en GITHUB

6. Subir al repositorio remnoto

    ```sh    
    git init
    git commit -m "first commit"
    git branch -M main
    git remote add origin git@github.com:jmamanih/lapazdigitalint.git
    git push -u origin main
    ```

[Ir al Inicio](#topmenu "Ir al inicio de página")


<a id="idsec30">

# Compilar y Ejecutar un Proyecto Laravel

Example: 

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

