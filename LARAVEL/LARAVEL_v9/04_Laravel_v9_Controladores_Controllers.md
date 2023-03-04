# Controladores
Un controlador puede tener un solo método denominado "invoke" o puede tener varios métodos.

*Ubicación de los Controladores*
```sh
app/Http/Controllers
```
*Crear un Controlador*

Los nombres de los controladores deben empezar con una Mayúscula palabra en singular seguido de la palabra reservada *Controller*
```php
php artisan make:controller ProcedureController -i
```
*Procedure* es el nombre del controlador
*-i*: es el parametro para crear un controlador invocable o sea de un solo métodp o una sola acción y se puede invocar mediante una ruta como un solo parametro.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Http\Response;

class ProcedureController extends Controller
{
    /**
     * Handle the incoming request.
     */
    public function __invoke(Request $request): Response
    {
        return response('Testing Invoke Controller', 200)->header('Content-Type', 'text/plain');
    }
}
```
*Invocar al Controlador que lleva un solo método (invoke)*

Crear la siguiente Ruta paraa llamar al controlador tipo *invoke*

Editar el archivo *Routes/web.php*

```php
Route::get('/procedure', ProcedureController::class)->name('procedure');
```
No olvidar incluir el nombre del controlador en la cabecera del archivo de Rutas web.php
```php
use App\Http\Controllers\ProcedureController;
```
Verificar su funcionamiento
```
http://projectname.test/procedure
```

*Crear Controladores con multiples métodos*

```php
php artisan make:controller ProcedureController -r
```
Con el parametro -r de resources, se crean los siete métodos REST: index, create, store, show, edit, update y destroy 

Para crear metodos para un servicio tipo API se usa el parámetro *--api*
```php
php artisan make:controller ProcedureController --api
```
Se crean solamente cinco de los metodos: index, store, show, update y destroy, porque los métodos create y edit se hacen desde el frontend desde las vistas.

*Crear un controlador vacion*
```php
php artisan make:controller ProcedureController
```

*Invocar al Controlador que tiene varios métodos*
```php
Route::get('/procedure', [ProcedureController::class,'index'])->name('procedure');
```
Donde *index* es el nombre del método, generalmente se usar para hacer listados;

