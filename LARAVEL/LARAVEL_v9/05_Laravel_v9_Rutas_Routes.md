# Rutas en Laravel

Las rutas son lo primero que se ejecutan en Laravel

Se encargan de manejar el flujo de solicitudes y respuestas, desde y hacia el cliente

*Ubicación de las Rutas*
```sh
Routes/web.php
```
*Ruta de Inicio*

```php
Route::get('/', function () {
    return view('welcome');
});
```
Lo primero que hace laravel es ejecutar la ruta raiz, en este caso nos lleva a la vista *welcome.blade.php* páfina de bienvenida de Laravel.

*Los cuatro archivos de Rutas en Laravel*
routes/api.php: En este archivo se definen todas las rutas de las APIs que puede llegar a tener nuestra aplicación.

routes/channels.php: Aquí definimos los canales transmisión de eventos. Por ejemplo, cuando realizamos notificaciones en tiempo real.

routes/console.php: En el archivo de rutas console.php definimos comandos de consola que pueden interactuar con el usuario u otro sistema.

routes/web.php: En este archivo de rutas es donde definimos todas las rutas de nuestra aplicación web que pueden ser ingresadas por la barra de direcciones del navegador.

## Tipos de Rutas en Laravel

https://www.laraveltip.com/que-son-los-routes-en-laravel/

Laravelbrinda distintos tipos de routes para atender cada una de las solicitudes HTTP que recibe nuestra aplicación. Solo basta con utilizar la clase Routes con el método que corresponda al verbo HTTP:
```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```
Por ejemplo:
```php
Route::get('/procedures', [ProcedureController::class,'index'])->name('procedures');
```
*Rutas con parámetro*
```php
Route::get('/listado/{idcategoria}', [ProcedureController::class,'index']);
```
En el controlador
```php
...
class PostController extends Controller
{
    public funtion index($idcategoria)
    {
         (...)
    }
}

```
*Rutas con parámetro opcional*
```php
Route::get('/listado/{idcategoria?}', [ProcedureController::class,'index']);
```

## Proteger Rutas

*Proteger Rutas con Middlewares*

```php
Route::group([
    'middleware' => 'admin',
    'prefix' => 'admin',
    'namespace' => 'Admin'
], function () {
    Route::get('/series', 'SeriesController@index');
    Route::get('/series/{id}', 'SeriesController@edit');
});
```

*Rutas que dirigen directo a las vistas*

```php
Route::view("/homepage", "homepage");
```
