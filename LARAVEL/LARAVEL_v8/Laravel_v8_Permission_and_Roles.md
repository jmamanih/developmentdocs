 
# Roles y permisos en Laravel con spatie/laravel-permission

Referencia: [Tutorial spatie/laravel-permission](https://rimorsoft.com/roles-y-permisos-en-laravel-con-spatie-laravel-permission)

https://medium.com/@dozieogbo/jwt-authentication-and-role-based-authorization-on-laravel-5-6-and-jwt-auth-6b36e11ed0b0

## Definición

En el marco de la seguridad, la administración de usuarios en relación a permisos y roles nos proporciona un medio de control de acceso a la información.

Spatie es una empresa de Bélgica que desarrolla y diseña sitios web, ellos crean sus propias soluciones y las suben a GitHub para que otros programadores y empresas aprovechen su código y componentes, laravel-permission es uno de esos componentes.

**Lista de control de acceso o ACL (access control list))**

Es un término famoso en informática, se refiere a la seguridad que permite dar o quitar permisos a un usuario sobre nuestro sistema a eso se denomina ACL.

Un Middleware es la implementación de ACL, se crean políticas de acceso para el usuario.

**Listado de métodos**

* Con **givePermissionTo** conseguimos dar permisos, ejemplo:

    ```php
    $user->givePermissionTo('posts.index');
    ```
* Con **assignRole** asignamos un rol al usuario, ejemplo:

    ```php
    $user->assignRole('admin');
    ```
* givePermissionTo también relacionaría permisos con un rol, ejemplo:
    
    ```php
    $role->givePermissionTo('posts.index');
    ```
* Si deseamos ver todos los permisos asignados a un usuario podemos usar

    ```php
    $user->permissions;
    ```
* Si necesitamos saber el listado de permisos asignados a un usuario a través de un rol podemos usar:
    
    ```php
    // get all permissions inherited by the user via roles
    $permissions = $user->getAllPermissions();
    ```

Este componente cubre multiples guards y cada guard puede tener su propio conjunto de roles y permisos. ¿Esto que quiere decir?, que podemos tener permisos para el acceso web y diferentes para el acceso a una API.

    * Web es el acceso clásico y tradicional a un sistema
    * Un guard de API basa su seguridad en tokens

Esto significa que si vamos a crear un API en Laravel y queremos que esté incluido en nuestro gran sistema de roles y permisos con spatie/laravel-permission lo podemos lograr.

Por último, podemos ver que la forma de comprobar si el usuario logueado tiene o no permisos sobre una ruta es a través del método can, ejemplo:

```php
    $user->can('posts.index');
```

## Implementación de spatie/laravel-permission

## Configuración

**Crear proyecto**

    composer create-project --prefer-dist laravel/laravel tutorial-spatie

**Cofigurar la base de datos**

Editar archivo .env

    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=lapazdigital
    DB_USERNAME=dev
    DB_PASSWORD=12345

**Configurar el Service Porvider**

Editar el archivo: config/app.php (llave de providers)

```php
<?php

return [

    'providers' => [
        // Spatie
        Spatie\Permission\PermissionServiceProvider::class,
    ],

];
```

**Configurar el Miidleware**

Editar el archivo: app/Http/kernel.php

```php

<?php

namespace App\Http;

use Illuminate\Foundation\Http\Kernel as HttpKernel;

class Kernel extends HttpKernel
{

    protected $routeMiddleware = [
        // ...
        'role' => \Spatie\Permission\Middlewares\RoleMiddleware::class,
        'permission' => \Spatie\Permission\Middlewares\PermissionMiddleware::class,
    ];

}
```

# Instalación del componente

Ejecutar el comando 

    composer require spatie/laravel-permission

Terminando la configuración y publicaciones

    php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider" --tag="migrations"
    php artisan migrate
    php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider" --tag="config"




