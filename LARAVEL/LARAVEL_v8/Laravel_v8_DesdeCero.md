# LARAVEL DESDE CERO
## Versión 8

<a id="topmenu">

## Contenido
* Introducción
* Instalación en Windows 10
* Estructura de Carpetas de Laravel

## Referencias
*Fuente:*
[Laravel desde Cero](https://aprendible.com/series/laravel-desde-cero)

## Instalación en Windows 10

1. Se utilizará la herramienta [Laragon](https://laragon.org/download/)

![Laragon](images/laragon.jpg)

Laragon es una heramienta, moderna e ideal para construir aplicaciones web.

La instalación incluye: NodeJs + Yarm, Apache/Nginx, Memcached, Redis, ngrok, git.

Por defecto se instala Composer, para abrir la terminal Ctrl+Alt+T.

Se puede verificar los componentes instalados

```
node -v
npm -v
composer --version
php -v

```

2. Instalar Laravel desde la terminal

```
composer global require laravel/installer
```
```
laravel --version
```

3. Crear la Aplicacion

```
laravel new nombre_app
```
```
laravel lapazdigital
ls -la
```

4. Acceder a la aplicación desde el navegador web

Antes se debe reiniciar los servicios de Laragon: 
Laragon -> Recargar

```
http://nombre_app.test
```
```
http://lapazdigital.test
```

5. Instalar un editor de código de su preferencia: Ej. [Visual Studio Code](https://code.visualstudio.com/download), 

*Nota:* Los comandos php artisan, deben ejecutarse dentro del directorio de la aplicación.

Extensiones necesarias para Laravel en VSCode
* Laravel Blade Snippets
* Laravel Snippets
* Laravel Blade Spacer
* Laravel Artisan
* Laravel Extra Intellisense
* Laravel goto Controller
* Laravel goto View
* DotENV syntax highlighting

## Rutas

Crear rutas

Editar el archivo /web.php

```php
Route::get('contacto', function () {
    return('La Paz Digital Backend!');
});
```
```
http://lapazdigital.test/contacto
```
renombrar rutas

```php
Route::get('contactanos', function () {
    return('La Paz Digital Backend!');
})->name('contactos');

Route::get('/', function () {
    echo "<a href='" . route('contactos') . "Ir a Contactos</a>";
});


```

## Vistas

Crear un archivo en resources/views/home.blade.php

home.blade.php

```php
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <h1>Bienvenidos a: {{ $nombre ?? "la Web" }}<h1>
</body>
</html>
```

```php
Route::get('/', function () {
    //return view('welcome');
    $nombre = "La Paz Digital";
    return view('home', ['nombre' => $nombre]);
})->name('home');

```

## Motor de plantillas Blade

[Referencia](https://www.cloudways.com/blog/create-laravel-blade-layout/)

**Crear Rutas**

routes/web.php

```php
    Route::get('/', function() {
        return View::make('pages.home');
    });
    Route::get('/about', function() {
        return View::make('pages.contact');
    });
```

**Crear la estructura de Vistas**

```
resources
    views
        layouts
            default.blade.php
        pages
            home.blade.php
            contact.blade.php
        includes
            head.blade.php
            header.blade.php
            footer.blade.php
```

**Crear includes**

head.blade.php

```html
<meta charset="utf-8">
<meta name="description" content="">
<meta name="Saquib" content="Blade">
<title>Checkout our layout</title>
<!-- load bootstrap from a cdn -->
<link rel="stylesheet" href="//netdna.bootstrapcdn.com/twitter-bootstrap/3.0.3/css/bootstrap-combined.min.css">
```

Header.blade.php

```html
<div class="navbar">
   <div class="navbar-inner">
       <a id="logo" href="/">Single Malt</a>
       <ul class="nav">
           <li><a href="/">Home</a></li>
           <li><a href="/contact">Contact</a></li>
       </ul>
   </div>
</div>
```

footer.blade.php

```html
<div id="copyright text-right">© Copyright 2017 Saquib Rizwan </div>
```

**Crear Layouts**

Usar la directiva @include para traer pequeñas partes del código que he creado en la carpeta includes, y usar @yield para traer contenido de las páginas individuales creados en pages.

default.blade.php

```php
<!doctype html>
<html>
<head>
   @include('includes.head')
</head>
<body>
<div class="container">
   <header class="row">
       @include('includes.header')
   </header>
   <div id="main" class="row">
           @yield('content')
   </div>
   <footer class="row">
       @include('includes.footer')
   </footer>
</div>
</body>
</html>
```
**Crear Pages**

pages/home.blade.php

```php
@extends('layouts.default')
@section('content')
   <h1>Home</h1>
@endsection
```
pages/contact.blade.php

```php
@extends('layouts.default')
@section('content')
   <h1>Contact</h1>
@endsection
```

## Estructuras de control Blade

web.php

```php
Route::get('/about', function()
{ 
    $list = [
        ['title'=>'¿Quienes somos?'],
        ['title'=>'Misión'],
        ['title'=>'Visión'],
    ];
    return view('pages.about',['list'=>$list]);
});
```

about.blade.php

```php
@extends('layouts.default')

@section('title')
about
@endsection

@section('content')
   <h1>About</h1>
   <ul>
        <!--
        @foreach($list as $listItem)
            <li>{{ $listItem['title'] }}</li>
        @endforeach
        -->
        @forelse($list as $listItem)
            <li>{{ $listItem['title'] }} <small>{{ $loop->first ? 'Es el primero' : '' }}</small></li> 
        @empty
            No hay elementos disponibles
        @endforelse

    </ul>
@endsection
```
## Controladores

Hacer un listado de rutas

```sh
php artisan route:list
```

Directorio de los controladores: **app/Http/Controllers**

*Crear un controlador*

Ruta: app\Http\Controllers

```sh
php artisan make:controller NameController
```

Ejemplo

```sh
php artisan make:controller CategoryController -i
```
nota: -i genera un metodo __invoke, este tipo de controladores se usa para contar con un solo método. 

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class CategoryController extends Controller
{
    /**
     * Handle the incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return \Illuminate\Http\Response
     */
    public function __invoke(Request $request)
    {
        //
        return view('pages.categories');
    }
}
```

**Errores:**

`CategoryController` is not invokable. 

*Solution:*

Adicionar en el archivo app/Providers/RouteServiceProvider.php la variable global name space: protected $namespace = 'App\\Http\\Controllers'

```php
class RouteServiceProvider extends ServiceProvider
{
    protected $namespace = 'App\\Http\\Controllers';   // -> Adicionar esta linea
    //...
}
```

## Controladores Resource y API

```sh
php artisan make:controller CategoriaController --resource
```
```sh
php artisan make:controller CategoriaController --api
```

File: app\Http\Controllers\CategoriaController.php

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class CategoriaController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //
        $list = [
            ['title' => 'Iglesias de La Paz'],
            ['title' => 'Museos de La Paz'],
            ['title' => 'Vista Aérea de La Paz'],
        ];
        return view('pages.categoria', compact('list'));
    }
    /**
     * Show the form for creating a new resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function create()
    {
        //
    }
    // ...

}
```

File: routes\web.php

```php
Route::get('/categoria', 'CategoriaController@index')->name('categoria');
```

## Identificar Link de Navegación en el menú

Adicionar el estilo del link activo en resources\views\includes\head.blade.php

```php
<style>
    .active a {
        color: olivedrab;
        text-decoration: none;
    }
</style>
```

Crear una función para identificar la página activa
app\helpers.php

```php
function setActive($routeName) {
    return request()->routeIs($routeName) ? 'active' : '';
}
```

Llamar a la funcion en header.blade.php

```php
    <ul class="nav">
        <li class="{{ setActive('home') }}"><a href="/">Home</a></li>
        <li class="{{ setActive('categoria') }}"><a href="/categoria">Categorias</a></li>
        <li class="{{ setActive('contact') }}"><a href="/contact">Contact</a></li>
        <li class="{{ setActive('about') }}"><a href="/about">About</a></li>
    </ul>
```

Indicar a composer para que cargue helpers.php y se habilite la funcion setActive
Editar composer.json y adicionar en la seccion autoload "files": ["app/helpers.php"]

```php
"autoload": {
    "psr-4": {
        "App\\": "app/",
        "Database\\Factories\\": "database/factories/",
        "Database\\Seeders\\": "database/seeders/"
    },
    "files": ["app/helpers.php"]
},
```
Desde consola ejecutar el comando:

```sh
composer dumpautoload
```
es para el cargado automático de archivos

## Formularios y validación

Crear un formulario

resources/views/pages/contact.blade.php

```php
    <h1>Contacto</h1>
    <form method="POST" action="{{ route('contact') }}">
        @csrf
        <input name="name" placeholder="Nombre Completo" value="{{ old('name') }}"><br>
        {!! $errors->first('name','<small>:message</small><br>') !!}
      
        <input name="email" type="email" placeholder="Correo Electrónico" value="{{ old   ('email') }}"><br>
        {!! $errors->first('email','<small>:message</small><br>') !!}

        <input name="subject" placeholder="Asunto" value="{{ old('subject') }}"><br>
        {!! $errors->first('name','<small>:message</small><br>') !!}

        <textarea name="content" placeholder="Mensaje">{{ old('content') }}</textarea><br>
        {!! $errors->first('name','<small>:message</small><br>') !!}

        <button>Enviar</button><br>
    </form>
```

Adjuntar la directiva token de formulario, para evitar la suplantación de identidad
Error: 419

```
@csrf
```

Crear un controlador para gestionar los mensajes enviados

```sh
php artisan make:controller MessagesController 
```

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class MessagesController extends Controller
{
    //
    public function store() {
        request()->validate([
            'name' => 'required',
            'email' => 'required|email',
            'subject'=> 'required',
            'content' => 'required|min:3'
        ]);
        return "Datos Válidos";      
    }
}
```

**Traducir mensajes de validación**

Los archivos de traducción se encuentran en: resources/lang y por defecto esta la carpeta /en y los mensajes de validacion estan en el archivo validation.php

Es recomendable crear una carpeta con el idioma preferido y luego configurar su acceso en app/config/app.php

```php
    'locale' => 'en',
```
* Crear la carpeta /es y crear los mismos archivos de la carpeta /en
* Descargar Laravel Lang de https://github.com/Laravel-Lang/lang o sea las traducciones de los mensajes, entrar a la carpeta /locales, buscar la carpeta /es, abrir el archivo (ej. validation.php), elegir la opcion Raw y descargar el archivo presionando Ctrl+S y guardar en la carpeta del proyecto /resources/lang/es, proceder de la misma manera con el resto de los archivos
* Configurar el cambio de idioma en app/config/app.php, reemplazar 'locale' => 'es'

**Llaves de Traducción**

Editar o Crear el archivo es.json dentro de /resources/lang/es

```json
{
    "Contact": "Contacto"
}
```

LLamar a la traducción en los archivos .blade.php

```php
@lang('Contact')
```
```php
{{ __('Contact') }}
```

## Aplicaciones multilenguaje en Laravel

...

## Enviar emails

Crear un Mailabel es una clase de Php Laravel

```sh
php artisan make:mail MessageReceived
```
se crea el archivo: app/Mail/MessageReceived.php

```php
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;

class MessageReceived extends Mailable
{
    use Queueable, SerializesModels;

    public $subject = 'Mensaje recibido';
    public $msg;

    /**
     * Create a new message instance.
     *
     * @return void
     */
    public function __construct($messageemail)
    {
        //
        $this->msg = $messageemail;
    }

    /**
     * Build the message.
     *
     * @return $this
     */
    public function build()
    {
        return $this->view('emails.message-received');
    }
}
```

Crear la vista en app/resources/views/emails/message-received.blade.php

```php
<!DOCTYPE html>
<html>
<head>
    <title>Mensaje recibido</title>
</head>
<body>
    <p>Recibiste un mensaje de {{ $msg['name']}} - {{ $msg['email']}}</p>
    <p>Asunto:<strong>{{ $msg['subject']}}</strong></p>
    <br>
    <p>{{ $msg['content']}}</p>
</body>
</html>
```
Configurar el email abriendo el archivo .env

```json
MAIL_MAILER=log
MAIL_HOST=mailhog
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS=null
MAIL_FROM_NAME="${APP_NAME}"
```
Los correos en etapa de desarrollo se veran en un archivo log que esta ubicado en: storage/logs/laravel.log

Pasar parametros por el controlador MessagesController.php

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Mail;
use App\Mail\MessageReceived;

class MessagesController extends Controller
{
    //
    public function store() {
        $msgdata = request()->validate([
            'name' => 'required',
            'email' => 'required|email',
            'subject'=> 'required',
            'content' => 'required|min:3'
        ]);
        // Enviar Email

        //Mail::to('lapazdigital2016@gmail.com')->send(new MessageReceived($msgdata)); 
        Mail::to('lapazdigital2016@gmail.com')->queue(new MessageReceived($msgdata)); 

        return "Datos Válidos";      
    }
}
```

**Recibir mensajes enviados por los clientes a nuestra bandeja de entrada**

Para ello se utilizará [SENDGRID](https://sendgrid.com/)

Instalar [driver para Sendgrid](https://github.com/s-ichikawa/laravel-sendgrid-driver)
Ejecutar el comando

```sh
composer require s-ichikawa/laravel-sendgrid-driver
```
```
Si sale el siguiente mensaje
...
Discovered Package: s-ichikawa/laravel-sendgrid-driver
```
significa que se registro automáticamente el paquete el Laravel

Luego copiar las variables de entorno en .env

```json
MAIL_DRIVER=sendgrid
SENDGRID_API_KEY='YOUR_SENDGRID_API_KEY'
```
Para obtener el 'YOUR_SENDGRID_API_KEY' ingresar a la cuenta de SendGrid, Settings, API Keys, Create API Key, Full Access, antes darle un nombre a la llave, luego copiar el API KEY

Por ultimo copiar en el archivo config/services

```php
 'sendgrid' => [
        'api_key' => env('SENDGRID_API_KEY'),
    ],
```

## Variables de Entorno y de Base de Datos

Son valores que cambian segun el entorno como ser: Entorno de Desarrollo o local y Entorno de Produción

Las variables de entorno se encuantran en el archivo .env

el modo actual se encuentra definido en:

```php
    APP_ENV=local
```

**Definir credenciales para conectar a una base de datos**

```json
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=lapazdigitaldb
DB_USERNAME=dev
DB_PASSWORD=12345
```

## Migraciones y Creación de Base de Datos

Crear una base de datos (lapazdigitaldb), crear un usuario (dev) y asignarle todos los privilegios.

```sql

mysql -u root

Show databases;
Create database lapazdigitaldb;
GRANT ALL PRIVILEGES ON lapazdigitaldb.* To 'dev'@'localhost' IDENTIFIED BY '12345';
Flush privileges;
Show grants;
exit

mysql -u dev -p
show databases;

```
Las migraciones se encuentran en: databases/
son como el control de versiones de la base de datos permite crear, modificar las tablas y reconstruir esquemas de la base de datos.

**Crear Migraciónes**

```sh
php artisan make:migration create_categories_table
```

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateCategoriesTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('categories', function (Blueprint $table) {
            $table->increments('id');
            $table->string('title')->unique();
            $table->string('title_en')->unique()->nullable();
            $table->string('comment');
            $table->string('comment_en')->nullable();
            $table->string('keywords')->nullable();
            $table->string('keywords_en')->nullable();
            $table->string('folder')->nullable();
            $table->string('link')->nullable();
            $table->string('icon_image')->nullable();
            $table->string('logo_image')->nullable();
            $table->string('banner_image')->nullable();
            $table->boolean('enabled')->default(true);
            $table->timestamps();
        });
    }
    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('categories');
    }
}
```
```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateItemsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('items', function (Blueprint $table) {
            $table->increments('id');
            $table->string('title');
            $table->string('title_en');
            $table->string('content');
            $table->string('content_en');
            $table->string('link');
            $table->string('icon_image');
            $table->string('logo_image');
            $table->string('background_image');
            $table->boolean('enabled');
            $table->integer('category_id')->unsigned();
            $table->timestamps();
            $table->foreign('category_id')->references('id')->on('categories');
        });
    }
    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('items');
    }
}
```
La migración se almacena en database/migrations y contendrá una marca de tiempo que determina el orden de las migraciones.

Las opciones --table y --create se usan para indicar el nombre de la tabla y si la migración creará una nueva tabla.

```sh

php artisan make:migration add_votes_to_users_table --table=users

php artisan make:migration create_users_table --create=users

``` 
**Ejecutar todas las Migraciones**

```sh
php artisan migrate
```

Forzar Migraciones en producción

```sh
php artisan migrate --force
```

**Revertir Migraciones**

Revertir la última operación de migración

```sh
php artisan migrate:rollback
```

Revertir todas las migraciones

```sh
php artisan migrate:reset
```

Revertir todas las migraciones y ejecutarlas todas de nuevo

```sh
php artisan migrate:refresh

php artisan migrate:refresh --seed
```

Eliminar tablas y vuelve a ejecutar las migraciones

```sh
php artisan migrate:fresh
```

**Agregar quitar campos a una tabla sin que se elimine la información.**


```sh
php artisan make:migration add_phone_to_users_table --table=users
```

Archivo: 2021_09_01_192827_add_phone_to_users_table
```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class AddPhoneToUsersTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::table('users', function (Blueprint $table) {
            //
            $table->string('phone')->after('email')->nullable();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('users', function (Blueprint $table) {
            //
            $table->dropColumn('phone');
        });
    }
}
```

Para actualizar los cambios ejecutar nuevamente:

```sh
php artisan migrate
```

## Seeders

Los Seeders son sembradores de datos, se ubican el database/seeders

**Crear un Seeder**

```sh
php artisan make:seeder UsersTableSeeder
```

database/seeders/UsersTableSeeder.php

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use DB;    // 

class UsersTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        //
        DB::table('users')->insert([
            'name' => 'Administrador del Sistema',
            'email' => 'admin@lapazdigital.net',
            'password' => bcrypt('admin'),
            'created_at' => date("Y-m-d H:i:s")
        ]);

        DB::table('users')->insert([
            'name' => 'Operador del Sistema',
            'email' => 'operador@lapazdigital.net',
            'password' => bcrypt('operador'),
            'created_at' => date("Y-m-d H:i:s")
        ]);

        DB::table('users')->insert([
            'name' => 'Juan F. Mamani H.',
            'email' => 'jmamani@lapazdigital.net',
            'password' => bcrypt('jmamani'),
            'created_at' => date("Y-m-d H:i:s")
        ]);
    }
}
```

**Registrar el Seeder en DatabaseSeeders**

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     *
     * @return void
     */
    public function run()
    {
        // \App\Models\User::factory(10)->create();
        $this->call(UsersTableSeeder::class);
    }
}
```
**Ejecutar Seeder**

Ejecutar de manera general todos a la vez

```sh
php artisan db:seed
```
*NOTA:* Si sale el error de Class 'Database\Seeders\DB' not found, incluir en el seeder:

```php
use DB;
```
Previamente se debe verificar en config/app.php que este definido 'DB':

```php
// ...
'aliases' => [
    //...
    'DB' => Illuminate\Support\Facades\DB::class,
    //...
]
```
Ejecutar solo un seeder

```sh
php artisan db:seed --class=UsersTableSeeder
```

También puede sembrar su base de datos usando el *migrate:fresh* comando en combinación con la opción *--seed*, que eliminará todas las tablas y volverá a ejecutar todas sus migraciones. 

Este comando es útil para reconstruir completamente su base de datos:

```sh
php artisan migrate:fresh --seed
```

**Importar datos desde un archivo JSON**

Archivo origen controles.json

```json
{
	"nombre": [
		{	"texto": "Cerrar",
		 	"traduccion": [
				{"idioma":"en", "texto":"Close"}
			]
		}, 
		{
			"texto": "LEER MAS",
		 	"traduccion": [
				{"idioma":"en", "texto":"READ MORE"}
			]
		}, 
		{
			"texto": "INFORMACION",
		 	"traduccion": [
				{"idioma":"en", "texto":"INFORMATION"}
			]
		},
		{
			"texto": "Información",
		 	"traduccion": [
				{"idioma":"en", "texto":"Information"}
			]
		}, 
		{
			"texto": "Todos",
		 	"traduccion": [
				{"idioma":"en", "texto":"All"}
			]
		}
    ]
}
```

Crear el Seeder

```sh
php artisan make:seeder TranslationsTableSeeder
```
TranslationsTableSeeder.php

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use File;
use DB;

class TranslationsTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        // *********************************************************
        $json = File::get("database/datasources/controles.json");
		$data = json_decode($json);

		if ($error = json_last_error())	{ // Verifica errores de Sintaxis
	        $errorReference = [
	            JSON_ERROR_DEPTH => 'The maximum stack depth has been exceeded.',
	            JSON_ERROR_STATE_MISMATCH => 'Invalid or malformed JSON.',
	            JSON_ERROR_CTRL_CHAR => 'Control character error, possibly incorrectly encoded.',
	            JSON_ERROR_SYNTAX => 'Syntax error.',
	            JSON_ERROR_UTF8 => 'Malformed UTF-8 characters, possibly incorrectly encoded.',
	            JSON_ERROR_RECURSION => 'One or more recursive references in the value to be encoded.',
	            JSON_ERROR_INF_OR_NAN => 'One or more NAN or INF values in the value to be encoded.',
	            JSON_ERROR_UNSUPPORTED_TYPE => 'A value of a type that cannot be encoded was given.',
	        ];
	        $errStr = isset($errorReference[$error]) ? $errorReference[$error] : "Unknown error ($error)";
	        throw new \Exception("=> JSON decode error ($error): $errStr");
	    }

        print_r('Migrando Datos...');

        $translate = $data->nombre;

        DB::table('translations')->delete();

		foreach ($translate as $obj)
		{
			DB::table('translations')->insert([
                'id_table' => 0,
                'table' => '',
                'field' => '',
            	'text' => $obj->texto,
				'iso_lang' => $obj->traduccion[0]->idioma,
				'translated_text' => $obj->traduccion[0]->texto,
				'created_at' => date("Y-m-d H:i:s")
        	]);
		}
		print_r('Proceso concluido!');
        // *********************************************************
    }
}
```
Ejecutar el seeder de migración: 

```sh
php artisan db:seed --class=TranslationsTableSeeder
```
ó 
```sh
php artisan migrate:fresh --seed
```

## Modelos, Obtener Datos con Eloquent (ORM)

Comando para crear un modelo

```php
php artisan make:model MyModel -m
```

-m = parámetro para crear al mismo tiempo la migración
la convención para nombrar modelos en la primera letra en Mayúscula no usar guiones como separador de palabras sino unar una mayúscula y el nombre del modelo debe ir en Singular, esta notación se llama CAMEL CASE.

**ORM**

Object Relational Mapping
Mapeo Relacional de Objetos
Datos => Objetos y Objetos a Datos 

En Laravel el ORM se llama ELOQUENT

Ejemplo:

1. Crear un Seeder para llenar datos a las Categorias

```php
php artisan make:seeder CategoriesTableSeeder
```

CategoriesTableSeeder.php

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use DB;

class CategoriesTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        //
        DB::table('categories')->insert([ 
            'title' => 'IGLESIAS DE LA PAZ',
            'title_en' => 'LA PAZ CHURCHES',
            'comment' => 'Iglesias representativas y concurridas de la ciudad de La Paz',
            'comment_en' => 'Representative and popular churches in La Paz city',
            'keywords' => 'Iglesias, Basílicas, Templos',
            'keywords_en' => 'Churchess, Basilicas, Temples',
            'folder' => 'iglesias',
            'link' => 'iglesias.php',
            'icon_image' => '',
            'logo_image' => '',
            'banner_image' => '',
            'enabled' => true,
            'created_at' => date("Y-m-d H:i:s")
        ]);

        DB::table('categories')->insert([ 
            'title' => 'MUSEOS DE LA PAZ',
            'title_en' => 'MUSEUMS OF LA PAZ',
            'comment' => 'Museos históricos de la ciudad de La Paz',
            'comment_en' => 'Historical museums in the city of La Paz',
            'keywords' => 'Museos, Arte, Arquelogia, Historia',
            'keywords_en' => 'Museums, Art, Arquelogy, History',
            'folder' => 'museos',
            'link' => 'museos.php',
            'icon_image' => '',
            'logo_image' => '',
            'banner_image' => '',
            'enabled' => true,
            'created_at' => date("Y-m-d H:i:s")
        ]);
        
        DB::table('categories')->insert([ 
            'title' => 'PASEOS AEREOS DE LA PAZ',
            'title_en' => 'LA PAZ AIR TOURS',
            'comment' => 'Vistas aereas de la ciudad de La Paz, tomadas desde un dron.',
            'comment_en' => 'Aerial views of the city of La Paz, taken from a drone.',
            'keywords' => 'Vistas, Aéreas, 360 grados, Dron',
            'keywords_en' => 'Views, Aerial, 360 degrees, Drone, Aerial, Drone',
            'folder' => 'aereolapaz',
            'link' => 'aereolapaz.php',
            'icon_image' => '',
            'logo_image' => '',
            'banner_image' => '',
            'enabled' => true,
            'created_at' => date("Y-m-d H:i:s")
        ]);     
    }
}
```
Ejecutar

```sh
php artisan migrate:fresh --seed
```
2. Crear el Modelo para las Categorias

```php
php artisan make:model Category
```
Los modelos se crean en la carpeta app/Models

3. Especificar en el modelo el nombre de la tabla si fuese necesario "protected $table = 'categories';"

app/Models/Category.php

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Category extends Model
{
    use HasFactory;

    protected $table = 'categories';
    
}
```

4. Llamar al modelo desde el Controlador "$list = Category::get()" e incluir "use App\Models\Category;"

app\Http\Controllers\CategoryController.php

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Category;   // <- incluir

class CategoryController extends Controller
{
    public function index()
    { 
        $list = Category::get();  // <- Obtiene todos los datos de la tabla mediante el modelo>
        return view('pages.categories', compact('list'));
    }
    // ...    
}
```

Listado en forma descendente:

```php
$list = Category::orderBy('title','ASC')->get();
```

Listado desde el ultimo registro adicionado

```php
$list = Category::latest()->get();
```

En la vista se pueden obtener datos como el *tiempo transcurrido desde la ultima adicion*

```php
<br>
{{ $listItem->created_at->diffForHumans() }}
```
**Compaginación del resultado o el listado de datos**

En el controlador especificar la paginación (Ej. 2 elementos por página, por defecto es 15)

```php
$list = Category::latest()->paginate(2);
```
En la vista al final del listado adicionar los links "{{ $list->links() }}"

```php
{{-- ... --}}
</ul>
{{ $list->links() }}
```
Por estética se puede cambiar el pase de parámetros en el Controlador

```php
  public function index()
    {
        //$list = Category::get();                              // Obtiene todos los registros
        //$list = Category::orderBy('title','ASC')->get();      // Ordenar de forma ascendente por el campo 'title'        
        //$list = Category::latest()->get();                    // Ordenar desde el último registro
        //$list = Category::latest()->paginate(2);                // Mostrar solo 2 elementos de la lista
        //return view('pages.categoria', compact('list'));
        return view('pages.categories', [
            'list' => Category::latest()->paginate(2)
        ]);
    }
```

## Obtener registros individuales con Eloquent y registros relacionados

1. Para fines prácticos se creará un Seeder para items que se relaciona con la tabla categories

```php
php artisan make:seeder ItemsTableSeeder
```

2. Crear modelo para Items

```php
php artisan make:model Item
```
3. Crear la funcion items en el modelo Category para obtener registros relacionados del tipo uno a muchos app/Model/Category.php

```php
<?php
namespace App\Models;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use App\Models\Item;
class Category extends Model
{
    use HasFactory;
    protected $table = 'categories';
    public function items()
    {
        return $this->hasMany(Item::class);
    }
}
```
4. Crear el método getitems en el controlador CategoryController.php

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Category;

class CategoryController extends Controller
{
    public function index()
    {
        return view('pages.categories', [
            'list' => Category::latest()->paginate(2),
            'listcat' => Category::get()
        ]);
    }
    public function show($id)
    {
        $category = Category::find($id);
        // $category = Category::findOrFail($id);
        return $category;
    }
    public function getitems($id)
    {
        $category = Category::find($id);        
        return $category->items;
    }
}
```
5. Crear las rutas para llamar a la funcion items en web.php

```php
Route::get('/categories', 'CategoryController@index')->name('categories.index');
Route::get('/categories/{id}', 'CategoryController@show')->name('categories.show');
Route::get('/categories/items/{id}', 'CategoryController@getitems')->name('categories.items');
```
6. Crear los links en la vista para llamar a los metodos que obtienen datos relacionados categories.blade.php

```php
<h1>Items por Categoria</h1>
<ul>
    @foreach($listcat as $listptrcat)
        {{--  <li>{{ $listptrcat['title'] }}</li> --}}
        <li>
            <a href="{{ route('categories.items', $listptrcat) }}">
                {{ $listptrcat['title'] }} 
            </a>
        </li>
    @endforeach
</ul>
```
7. Finalmente actualizar los links de la cabecera menu: app/resources/views/includes/header.blade.php 

```php
<div class="navbar">
    <div class="navbar-inner">
       <a id="logo" href="/">La Paz Digital</a>
       <ul class="nav">
           <li class="{{ setActive('home') }}"><a href="{{ route('home') }}">Inicio</a></li>
           <li class="{{ setActive('categories.index') }}"><a href="{{ route('categories.index') }}">Categorias</a></li>
           <li class="{{ setActive('contact') }}"><a href="{{ route('contact')}}">Contactese</a></li>
           <li class="{{ setActive('about') }}"><a href="{{ route('about') }}">Acerca</a></li>
       </ul>
    </div>
</div>
```

## Insertar datos mediante formularios

Se realizará un caso practico de adicionar un nuevo registro para Categorias

1. Crear la ruta en routes/web.php

```php
Route::get('/categories/create', 'CategoryController@create')->name('categories.create');
```

2. Adicionar el método en el controlador app/Http/Controllers/CategoryController.php

```php
public function create()
{
    return view('pages.categories.category');
}
```
3. Crear la vista category.blade.php en resources/views/pages/categories

```php
@extends('layouts.default')
@section('title')
category
@stop
@section('content')
    <h1>Nueva Categoria</h1>
    <form method="POST" action="{{ route('categories.store') }}">
        @csrf
        <label>
            Título de la Categoria <br>
            <input name="title" placeholder="Título" value="{{ old('title') }}"><br>
        </label>
        <label>
            Descripción de la Categoria <br>
            <textarea name="comment" placeholder="Descripción">{{ old('comment') }}</textarea><br>
        </label>
        <input name="enabled" type="hidden"  value=1>
        <button>Enviar</button><br>
    </form>
@endsection
```

4. Crear la ruta para almacenar datos

```php
Route::post('/categories/store', 'CategoryController@store')->name('categories.store');
```

5. Crear el método store en CategoryController.php

```php
public function store(Request $request)
{
    //
    return Category::create([
        'title' => request('title'),
        'comment' => request('comment'),
        'enabled' => request('enabled')
    ]);
}
```

6. Habilitar asignación masiva con fillable, en el modelo app/Models/Category.php

```php
protected $fillable = ['title', 'comment', 'enabled'];
```
7. Llamar a la ruta de adición de Categorias

app/reources/views/pages/categories.blade.php
```html
<a href="{{ route('categories.create') }}">Crear Nueva Categoria</a>
```

### Asignación Masiva en Laravel

La asignación masiva en Laravel permite solamente actualizar los campos seleccionados por tema de seguridad.
Ejemplo: 

$fillable: Permite llenar solamente los campos citados en el array

```php
protected $fillable = ['title', 'comment', 'enabled'];
```

$guarded: Permite modificar todos los campos excepto los que estan en el array

```php
protected $guarded = ['id', 'created_at', 'updated_at'];
```

Se puede deshabilitar la asignación masiva y controlar de otra forma
Ej.

1. Seleccionando los campos requeridos (CategoryController.php)
```php
// ...
public function store(Request $request)
{
    return Category::create(request()->only('title', 'comment', 'enabled'));
}
```
2. Mediante la validación (CategoryController.php)

Validar campos en el controlador
```php
public function store(Request $request)
{
    $fields = request()->validate([
        'title' => 'required',
        'comment' => 'required',
        'enabled' => 'required',
    ]);
    Category::create($fields);

    return redirect()->route('categories.index');
}
```
Cambiar el modo de protección en el modelo (Category.php)
```php
protected $guarded = [];
```

### Validación en Clase dedicada (Form Request Validation)

Form Request Validation: Estan implementados para validad formularios complejos, son clases dedicadas para encapsular la lógica de validación y autorización.

1. Crear el Request Form para las validaciones

```sh
php artisan make:request CreateCategoryRequest
```
Los request se guardan en app/Http/Request

CreateCategoryRequest.php
```php
<?php

namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class CreateCategoryRequest extends FormRequest
{
    public function authorize()
    {
        //return $this->user()->isAdmin();
        //return false;
        return true;      //  Cualquier usuario puede crear categorias
    }
    public function rules()
    {
        return [
            'title' => 'required',
            'comment' => 'required',
            'enabled' => 'required'
        ];
    }
    public function messages()
    {
        return [
            'title.required' => 'Ingrese el título de Categoria'
        ];
    }
}
```

2. En el modelo establecer el modo de almacenamiento masico $guarded
Category.php
```php
<?php
namespace App\Models;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use App\Models\Item;

class Category extends Model
{
    use HasFactory;

    protected $table = 'categories';
    //protected $fillable = ['title', 'comment', 'enabled'];
    protected $guarded = [];
    // ...    
}
```

3. Modificar la vista para la adicion de Categorias

app/resources/views/pages/categories/category.blade.php
```php
@extends('layouts.default')
@section('title')
category
@stop
@section('content')
   <h1>Nueva Categoria</h1>
   <!-- Espacio para los errores -->
   @if($errors->any())
   <ul>
      @foreach ($errors->all() as $error)
        <li> {{ $error }}</li>
      @endforeach
   </ul>
   @endif
   <!-- Formulario de adición -->
   <form method="POST" action="{{ route('categories.store') }}">
      @csrf
      <label>
         Título de la Categoria <br>
         <input name="title" placeholder="Título" value="{{ old('title') }}"><br>
      </label>
      <label>
         Descripción de la Categoria <br>
         <textarea name="comment" placeholder="Descripción">{{ old('comment') }}</textarea><br>
      </label>
      <input name="enabled" type="hidden"  value=1>
      <button>Enviar</button><br>
   </form>
@endsection
```
4. Modificar el pase de parametros para la validación en el controlador

app/Http/Controllers/CategoryController.php
```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
use App\Models\Category;
use App\Http\Requests\CreateCategoryRequest;   //<-- Add

class CategoryController extends Controller
{   // ...
    public function store(CreateCategoryRequest $request)
    {
        Category::create($request->validated());   // <--   validated()
        return redirect()->route('categories.index');
    }
    // ...
}
```
## Editar o actualizar registros

Como ejemplo se tomará la edicion de una Categoría en sus campos titulo y descripcion o comentario

1. Crear la vista formulario de edición:

resources/views/pages/categories/editcategory.blade.php

```php
@extends('layouts.default')
@section('title')
category edit
@stop
@section('content')
   <h1>Editar Categoría</h1>
   <!-- Espacio para los errores -->
   @if($errors->any())
   <ul>
      @foreach ($errors->all() as $error)
          <li> {{ $error }}</li>
      @endforeach
   </ul>
   @endif
   <!-- Formulario de edición-->
   <form method="POST" action="{{ route('categories.update', $category) }}">
      @csrf @method('PATCH')      
      <label>
         Título de la Categoría <br>
         <input name="title" placeholder="Título" value="{{ old('title', $category['title']) }}"><br>
      </label>
      <label>
         Descripción de la Categoría <br>
         <textarea name="comment" placeholder="Descripción">{{ old('comment', $category['comment']) }}</textarea><br>
      </label>      
      <button>Actualizar</button><br>
   </form>
@endsection
```

2. Agregar rutas para la la vista de edicion y actualización de datos

```php
Route::get('/categories/{category}/edit', 'CategoryController@edit')->name('categories.edit');
Route::patch('/categories/{category}', 'CategoryController@update')->name('categories.update');
```

3. Crear los métodos para la edicion en el controlador

app/Http/Controller/CategoryController.php

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Models\Category;
use App\Http\Requests\SaveCategoryRequest;

class CategoryController extends Controller
{
    public function index()
    {
        return view('pages.categories', [
            'list' => Category::latest()->paginate(2),
            'listcat' => Category::get()
        ]);
    }
    public function show($id)
    {
        $category = Category::find($id);
        return view('pages.categories.showcategory', [
            'category'=>$category
        ]);
    }
    public function create()
    {
        return view('pages.categories.addcategory');
    }
    public function store(SaveCategoryRequest $request)
    {
        Category::create($request->validated());
        return redirect()->route('categories.index');
    }
    public function edit(Category $category)
    {
        return view('pages.categories.editcategory', [
            'category' => $category
        ]);
    }
    public function update(Category $category, SaveCategoryRequest $request)
    {
        $category->update( $request->validated());
        return redirect()->route('categories.show', $category);
    }
}
```

4. Renombrar el CreateController por SaveController a fin de usar el método de validacion en ambos casos

app/Http/Requests/SaveCategoryRequest.php

```php
<?php

namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class SaveCategoryRequest extends FormRequest
{
    public function authorize()
    {
        return true;      //  Cualquier usuario puede crear categorias
    }
    public function rules()
    {
        return [
            'title' => 'required',
            'comment' => 'required'            
        ];
    }
    public function messages()
    {
        return [
            'title.required' => 'Ingrese el título de Categoria'
        ];
    }
}
```

## Reutilizar Formularios para Crear y Editar datos

Reutilizar porciones de código extrayendo las partes que se repiten en ambos formularios

Ejemplo:

1. Crear el archivo resources/views/pages/categories/errorsform.blade.php

```php
@if($errors->any())
<ul>
   @foreach ($errors->all() as $error)
       <li> {{ $error }}</li>
   @endforeach
</ul>
@endif
```
2. Llamar a la porcion de código en addcategory.blade.php y editcategory.blade.php

```php
@include('pages.categories.errorsformcat')
```
3. En los campos de título (title) y descripcion (comment) se deben normalizar los parámetros para poderlos extraer en una sola porción de código

addcategory.blade.php

```php
// ...
<label>
    Título de la Categoría <br>
    {{-- <input name="title" placeholder="Título" value="{{ old('title') }}"><br> --}}
    <input name="title" placeholder="Título" value="{{ old('title', $category['title']) }}"><br>
</label>
<label>
    Descripción de la Categoría <br>
    {{--  <textarea name="comment" placeholder="Descripción">{{ old('comment') }}</textarea><br> --}}
    <textarea name="comment" placeholder="Descripción">{{ old('comment', $category['comment']) }}</textarea><br>
</label>
// ...
```
4. En el CategoryController.php, modificar el método create para estandarizar los parámetros

```php
// ...
public function create()
{   //
    return view('pages.categories.addcategory', [
        'category' => new Category
    ]);
}
// ...
```
5. La porcion de código similar sobre los campos del formulario se almacenan en:

fieldsformcat.blade.php
```php
@csrf
<label>
    Título de la Categoría <br>
    <input name="title" placeholder="Título" value="{{ old('title', $category['title']) }}"><br>
 </label>
 <label>
    Descripción de la Categoría <br>
    <textarea name="comment" placeholder="Descripción">{{ old('comment', $category['comment']) }}</textarea><br>
 </label>
 <button>{{ $btnText }}</button>
```

6. Los formularios de adición y modificacion quedaria de la siguiente manera:

addcategory.blade.php
```php
@extends('layouts.default')
@section('title')
new category
@stop
@section('content')
   <h1>Nueva Categoria</h1>
   @include('pages.categories.errorsformcat')
   <form method="POST" action="{{ route('categories.store') }}">      
      @include('pages.categories.fieldsformcat', ['btnText' => 'Adicionar'])      
   </form>
@endsection
```
editcategory.blade.php
```php
@extends('layouts.default')
@section('title')
category edit
@stop
@section('content')
   <h1>Editar Categoría</h1>
   @include('pages.categories.errorsformcat')
   <form method="POST" action="{{ route('categories.update', $category) }}">
      @method('PATCH')
      @include('pages.categories.fieldsformcat', ['btnText' => 'Actualizar'])
   </form>
@endsection
```

## Eliminar Registros

1. Crear el metodo destroy en CategoryController.php

```php
//...
public function destroy(Category $category)
{
    $category->delete();
    return redirect()->route('categories.index');
}
// ...
```

2. Adicionar la ruta para eliminar en web.php

```php
Route::delete('/categories/{category}', 'CategoryController@destroy')->name('categories.destroy');
```

3. Crear el formulario para eliminar el registro en showcategory.blade.php

```php
// ...
<form method="POST" action="{{ route('categories.destroy', $category) }}">
      @csrf
      @method('DELETE')
      <button>Eliminar</button>
</form>
// ...
```

## Simplificar Rutas con Route Resource

Obtener el listado de rutas

Ej. Categorias

```sh
php artisan route:list --name=categories
```
```
+--------+----------+----------------------------+--------------------+--------------------------------------------------+------------+
| Domain | Method   | URI                        | Name               | Action                                           | Middleware |
+--------+----------+----------------------------+--------------------+--------------------------------------------------+------------+
|        | GET|HEAD | categories                 | categories.index   | App\Http\Controllers\CategoryController@index    | web        |
|        | GET|HEAD | categories/create          | categories.create  | App\Http\Controllers\CategoryController@create   | web        |
|        | GET|HEAD | categories/items/{id}      | categories.items   | App\Http\Controllers\CategoryController@getitems | web        |
|        | POST     | categories/store           | categories.store   | App\Http\Controllers\CategoryController@store    | web        |
|        | PATCH    | categories/{category}      | categories.update  | App\Http\Controllers\CategoryController@update   | web        |
|        | DELETE   | categories/{category}      | categories.destroy | App\Http\Controllers\CategoryController@destroy  | web        |
|        | GET|HEAD | categories/{category}/edit | categories.edit    | App\Http\Controllers\CategoryController@edit     | web        |
|        | GET|HEAD | categories/{id}            | categories.show    | App\Http\Controllers\CategoryController@show     | web        |
+--------+----------+----------------------------+--------------------+--------------------------------------------------+------------+
```
web.php
```php
// ...
Route::get('/categories', 'CategoryController@index')->name('categories.index');
Route::get('/categories/create', 'CategoryController@create')->name('categories.create');
Route::post('/categories/store', 'CategoryController@store')->name('categories.store');
Route::get('/categories/{category}/edit', 'CategoryController@edit')->name('categories.edit');
Route::patch('/categories/{category}', 'CategoryController@update')->name('categories.update');
Route::delete('/categories/{category}', 'CategoryController@destroy')->name('categories.destroy');
Route::get('/categories/{id}', 'CategoryController@show')->name('categories.show');
// ...
```
Se puede simplicar las 7 rutas utilizando Route Resource:

```php
Route::resource('categories', 'CategoryController');
```
En el caso de que la URI y los paramteros tengan otro nombre se los debe mencionar como sigue Ej.

```php
Route::resources('categorias','CategoryController')->names('categories')->parameters(['categoria'=>'category'])
```

## Mensajes de Sesión o Mensajes Flash

Los mensajes de sesión son los que se muestran por única vez como resultado de las operaciones realizadas

La sesión es un tipo de almacenamiento temporal donde se guardan información del usuario que esta utilizando la aplicación.

Laravel soporta varios drivers para almacenar estas sesiones

*config/session.php*

```php
    /*
    | Supported: "file", "cookie", "database", "apc",
    |            "memcached", "redis", "dynamodb", "array"
    */
    'driver' => env('SESSION_DRIVER', 'file'),
```

Por defecto las sesiones se almacenen en archivos en la carpeta: **storage/frameworks/sessions**

En modo producción es recomendable cambiar a "memcached" o "redis"


1. Implementar mensajes flash, se definiran los mensajes en el controlador CategoryController.php

app/Http/Controllers/CategoryController.php

```php
// ...
 public function store(SaveCategoryRequest $request)
{
    Category::create($request->validated());
    return redirect()->route('categories.index')->with('status','La Categoria fue adicionada correctamente.');
}
public function update(Category $category, SaveCategoryRequest $request)
{
    $category->update( $request->validated());
    return redirect()->route('categories.show', $category)->with('status','La Categoria fue actualizada correctamente.');
}
public function destroy(Category $category)
{
    $category->delete();
    return redirect()->route('categories.index')->with('status','La Categoria fue eliminada correctamente.');
}
// ...
```
2. Crear un parcial-code para personalizarlo posteriormente

resources/views/includes/sessionmessages.blade.php

```php
@if(session('status'))
    <p>
        {{ session('status') }}
    </p>
@endif()
```
3. Mostrar estos mensajes, incluyendo el parcial en layout

app/resources/views/includes/layouts/default.blade.php

```php
<div>
    @include('includes.sessionmessages')
</div>
```

## Login y Registro

[Técnicas de Autenticación con Laravel](https://aprendible.com/series/autenticacion)

**Se utilizará el paquete Laravel Breeze**

Instalar Laravel Breeze

```php
composer require laravel/breeze --dev
php artisan breeze:install
npm install && npm run dev
```

Luego de la Instalación se crean los siguientes archivos:

rutas:  routes/auth.php
controladores: app/Http/Controllers/Auth
requests: app/Http/Requests/Auth/LoginRequest.php
vistas: app/resources/views/auth

Cambiar la ruta de HOME en:
app/Providers/RouteServiceProvider.php

```php
public const HOME = '/dashboard';
```

**Llamar al Login y Logout**, desde la vista

resources/views/includes/header.blade.php

```php
<div class="navbar">
    <div class="navbar-inner">
       <a id="logo" href="/">La Paz Digital</a>
       <pre>
           {{-- dump(request()); --}}
       </pre>
       <ul class="nav">
           <li class="{{ setActive('home') }}"><a href="{{ route('home') }}">Inicio</a></li>
           <li class="{{ setActive('categories.index') }}"><a href="{{ route('categories.index') }}">Categorias</a></li>
           <li class="{{ setActive('contact') }}"><a href="{{ route('contact')}}">Contactese</a></li>
           <li class="{{ setActive('about') }}"><a href="{{ route('about') }}">Acerca</a></li>
           {{-- ************************************* --}}
           @auth
                <li>
                    <a href="#" onclick="event.preventDefault(); document.getElementById('logout-form').submit();">
                    Logout 
                    </a>
                </li>                     
           @else
                <li> 
                    <a href="{{ route('login') }}">
                    Login
                    </a>
                </li>                        
           @endauth
           {{-- ************************************* --}}
       </ul>
    </div>
</div>
<form id="logout-form" action="{{ route('logout') }}" method="POST" style="display: none;">
    @csrf
</form>
```

## Proteger Rutas mediante autenticación

Para ello se utilizará MIDDLEWARES, que filtra las peticiones HTTP

Los Middlewares de Laravel estan en: app/Http/Middleware

Las protecciones se pueden realizar de distintas maneras:

1. En el archivo de rutas web.php al final redireccionar "->middleware('auth);"

routes/web.php

```php
Route::get('/categories/items/{id}', 'CategoryController@getitems')->name('categories.items')->middleware('auth');
```
2. La otra manera es restringir el acceso desde el controlador desde el método constructor "__construct()".

Ej. Si se quiere proteger el método 'create' y 'edit' del controlador Category aplicar la función "only"

app/Http/Controllers/CategoryController.php

```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
use App\Models\Category;
use App\Http\Requests\SaveCategoryRequest;
class CategoryController extends Controller
{
    public function __construct()
    {
        $this->middleware('auth')->only('create', 'edit');
    }
    // ...
}
```

Ej. Si se quiere proteger todos los métodos exceptuando 'index' y 'show' se debe aplicar la función "except"

app/Http/Controllers/CategoryController.php

```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
use App\Models\Category;
use App\Http\Requests\SaveCategoryRequest;
class CategoryController extends Controller
{
    public function __construct()
    {
        $this->middleware('auth')->except('index', 'show');
    }
    // ...
}
```
3. Escondiendo los links que funcionen mediante autenticación, para ello se debe encerrar en la directiva "@auth", y "@endauth".

Ej.

resources/views/pages/categories.blade.php

```php
@auth
    <a href="{{ route('categories.create') }}">Crear Nueva Categoria</a>
@endauth
```

## Laravel Mix (Frontend)

Se utilizara la libreria mas popular en componentes para front-end denominado [Bootstrap](https://getbootstrap.com/)

Se pueden usar los archivos css y javascript que estan en public/css y public/js, pero no es buena idea porque estos archivos son compilaciones de las fuentes que se encuentran en resources/css, sas, js.

Para adicionar una hoja de estilo, se debe hacer en el archivo resources/css/app.css

resources/css/app.css

```css
/* Fonts */
@import url('https://fonts.googleapis.com/css?family=Nunito');

/* Variables */
@import 'variables';

/* Bootstrap */
@import '~bootstrap/scss/bootstrap';

/* Estilos propios */
.active a {
    color: olivedrab;
    text-decoration: none;
}
```
en este archivo se cargan las fuentes, las variables y los estilos de bootstrap y los estilos definidos para el proyecto

Al ejecutar la aplicacion web no se reflejan los cambios, porque requieren la respectiva compilación de las fuentes (resources/) al destino (public/).

Para compilarlo se debe usar Laravel Mix.

Laravel Mix, proporciona una API fluida para definir los pasos de compilación de Webpack de nuestra aplicación Laravel utilizando varios procesadores de CSS y JavaScript.

En el archivo webpack.mix.js, esta la configuración de la compilación con laravel mix.

webpack.min.js

```js
const mix = require('laravel-mix');
mix.js('resources/js/app.js', 'public/js').postCss('resources/css/app.css', 'public/css', [
    require('postcss-import'),
    require('tailwindcss'),
    require('autoprefixer'),
]);
```
En este caso las fuentes estan en resources/css/app.css y public/js/app.js, y el destino en public/css/app.css y public/js/app.js

**Compilar las fuentes**

Para compilar las fuentes verificar si esta instalado node.js

```sh
node -v
npm -v
```

Otra opcion a usar es yarn se instala con npm

```sh
npm install --global yarn
```
*Pasos para compilar:*

1. Primero se debe instalar los paquetes de dependencia de uso de Laravel que estan en el archivo package.json

```sh
npm install
```
ó
```sh
yarn
```

luego de la instalación aparece la carpeta node_modules donde se guardan todas las dependencias

2. Segundo compilar las fuentes ejecutando el comando "npm run dev"

```sh
npm run dev
```
ó 
```sh
yarn dev
```
Incluir en el layout o archivo de cabecera del proyecto lo sigueinte

resources/views/includes/header.blade.php

```php
{{-- <link rel="stylesheet" type="text/css" href="{{ asset('/css/app.css') }}"> --}}
<link href="{{ mix('/css/app.css') }}" rel="stylesheet">
<script src="{{ mix('/js/app.js') }}"></script>
```
3. Refrescar la vista en el navegador Ctrl+F5, para ver los cambios

**Comando watch**

Para evitar la compilación cada vez que se hagan cambios en los archivos fuente (css, js) es necesario ejecutar el comando watch

```sh
npm run watch
```
ó
```sh
yarn watch
```
Cada vez que se hagan cambios en las fuentes se compilara automaticamente.

Y para terminar el proceso presionar Ctrl+C en la terminal

 Otra forma de refrescar los cambios es usar browser.sync

webpack.mix.js

```js
mix.browserSync('http://lapazdigital.test');
```
Ejecutar el comando wach nuevamente

```sh
npm run watch
```

**Minificar Archivos para puesta en Producción**

```sh
npm run prod
```

ó

```sh
yarn prod
```
Con estos comando los archivos destino son minificados para su rapida carga en ejecucón y optimizados en espcacio de almacenamiento.

**Hard Reload en el Navegador**

A veces es necesario refrescar el navegar con Ctrl+F5 para ver los cambios realizados porque los archivos cache no se actualizan debido al nombre de archivo que no cambia pero si cambia su contenido, para que cada cambio se refleje en el navegador se debe renombrar estos archivos con un ID de versión para que lo vuelva a cargar esto es necesario solo en producción y no en desarrollo.

Adicionar en webpach el siguiente código:

webpack.mix.js

```js
if(mix.inProduction())
{
    mix.version();
}
```
Ejecutar 

```sh
npm run prod
```

Y en las vistas utilizar la funcion "mix" que mantiene al archivo siempre actualizado en el navegador.

resources/views/includes/head.blade.php

```php
<link href="{{ mix('/css/app.css') }}" rel="stylesheet">
```

## Diseño Frontend con Bootstrap

Quitar la version actual de bootstrap

```sh
yarn remove bootstrap
```
**Instalar Bootstrap**

Para instalar bootstrap ejecutar los sigueintes comandos:

```sh
composer require laravel/ui
php artisan ui bootstrap
php artisan ui bootstrap --auth
npm install && npm run dev
```
Luego de la instalación se configura automaticamente SASS como lenguaje de extension de estilos mediante Laravel Mix, esta configuración se puede ver en el archivo webpack.min.js

```js
const mix = require('laravel-mix');
/*
 |--------------------------------------------------------------------------
 | Mix Asset Management
 |--------------------------------------------------------------------------
 |
 | Mix provides a clean, fluent API for defining some Webpack build steps
 | for your Laravel application. By default, we are compiling the Sass
 | file for the application as well as bundling up all the JS files.
 |
 */
mix.js('resources/js/app.js', 'public/js')
    .sass('resources/sass/app.scss', 'public/css')
    .sourceMaps();
```
Las definiciones de estilos se deben hacer en: resources/sass/app.scss

```css
// Fonts
@import url('https://fonts.googleapis.com/css?family=Nunito');
// Variables
@import 'variables';
// Bootstrap
@import '~bootstrap/scss/bootstrap';

// Definciones propias Css
// Layouts
.h-screen {
    height: 100vh;
}
```
La directiva *"@import '~bootstrap/scss/bootstrap';"* hace referencia a "node_modules/bootstrap/scss/bootstrap.scss".

Luego se debe compilar las fuentes mediante laravel mix y que se reflejen los cambios en la carpeta public/css

```sh
npm run dev
```
Para que la compilación sea automática ejecutar "Watch"

```sh
npm run watch
```
En el archivo cabecera (resources/views/includes/head.blade.php) incluir el siguiente código:

```php
{{-- Styles --}}
<link href="{{ mix('/css/app.css') }}" rel="stylesheet">

{{-- Scripts --}}
<script src="{{ mix('/js/app.js') }}" defer></script>
```

El atributo "defer" hace que se ejecute al final de la carga.


**Diseñar las vistas con bootstrap**

* Usar la clase "navbar" para la barra de menú
* Cambiar el layout de Login resources/views/auth/login.blade.php
```php
{{-- @extends('layouts.app') --}}
@extends('layouts.default')
```
* Personalizar el Lauout principal o por defecto: resources/views/layouts/default.blade.php
```php
<!doctype html>
<html>
<head>    
   @include('includes.head')
   <title>@yield('title')</title>   
</head>
<body>
<div id="app" class="d-flex flex-column h-screen justify-content-between">
   <header>
        @include('includes.header')
        @include('includes.sessionmessages')
   </header>
   <main id="main">
        @yield('content')
   </main>
   <footer class="bg-white text-center text-black-50 py-3 shadow">
        @include('includes.footer')
   </footer>
</div>
</body>
</html>
```
* Personalizar la vista contacto: resources/views/pages/contact.blade.php

```php
@extends('layouts.default')
@section('title')
contact
@stop
@section('content')
   <div class="container">
      <div class="row">
         <div class="col-12 col-sm-8 col-lg-6 mx-auto">            
            <form class="bg-white shadow rounded py-3 px-4" method="POST" action="{{ route('contact') }}">
               @csrf
               <div class="display-4">Contactese con Nosotros</div>
               <hr>
               <div class="form-group">
                  <label for="name">Nombre Completo</label>
                  <input class="form-control bg-light shadow-sm @error('name') is-invalid @else border-0 @enderror"
                        id="name" 
                        name="name" 
                        placeholder="Nombre ..." 
                        value="{{ old('name') }}">
                  @error('name')
                     <span class="invalid-feedback" role="alert">
                        <strong>{{ $message  }}</strong>
                     </span>
                  @enderror
               </div>
               
               <div class="form-group">
                  <label for="email">Correo Electrónico</label>
                  <input class="form-control bg-light shadow-sm @error('email') is-invalid @else border-0 @enderror"
                        id="email"       
                        name="email" 
                        type="email" 
                        placeholder="Correo electrónico ..." 
                        value="{{ old('email') }}">
                  @error('email')
                     <span class="invalid-feedback" role="alert">
                        <strong>{{ $message }}</strong>
                     </span>
                  @enderror
               </div>

               <div class="form-group">
                  <label for="subject">Asunto</label>
                  <input class="form-control bg-light shadow-sm @error('subject') is-invalid @else border-0 @enderror"
                        id="subject"
                        name="subject" 
                        placeholder="Asunto ..." 
                        value="{{ old('subject') }}">
                  @error('subject')
                     <span class="invalid-feedback" role="alert">
                        <strong>{{ $message }}</strong>
                     </span>
                  @enderror
               </div>         

               <div class="form-group">
                  <label for="content">Mensaje</label>
                  <textarea class="form-control bg-light shadow-sm @error('content') is-invalid @else border-0 @enderror"
                           id="content"
                           name="content" 
                           placeholder="Mensaje ...">
                     {{ old('content') }}
                  </textarea><br>
                  @error('content')
                     <span class="invalid-feedback" role="alert">
                        <strong>{{ $message }}</strong>
                     </span>
                  @enderror
               </div>
               
               <button class="btn btn-primary btn-lg btn-block">
                  @lang('Enviar')
               </button>

            </form>
         </div>
      </div>
   </div>
@endsection
```
Para que los titulos sean responsive añadir en: resources/sass/_variables.scss

```css
// Enable Titles Responsive
$enable-responsive-font-sizes: true;
```
* Personalizar listados, vista categorias: resources/views/pages/categories.blade.php

```php
@extends('layouts.default')
@section('title')
categorias
@endsection

@section('content')
<div class="container">
    <div class="d-flex justify-content-between align-items-center mb-3">
        <h1 class="display-4 mb-0">Categorías de La Paz Digital</h1>
        @auth
            <a  class="btn btn-primary"
                href="{{ route('categories.create') }}">
                Crear Nueva Categoria
            </a>
        @endauth
    </div>
    <hr>
    <p class="lead text-secondary">
        Listado de categorias de La Paz Digital
    </p>
    <hr>
    <ul class="list-group">      
        @forelse($list as $listItem)
            <li class="list-group-item border-0 mb-3 shadow-sm">
                <a class="d-flex text-secondary justify-content-between align-item-center"
                    href="{{ route('categories.show', $listItem) }}">
                    <span class="font-weight-bold">
                        {{ $listItem['title'] }} {{-- <small>{{ $loop->first ? 'Es el primero' : '' }}</small> --}}
                    </span>
                    <span class="text-black-50">
                        {{ $listItem->created_at->format('d/m/Y') }}
                    </span>
                    <span class="text-black-50">
                        {{ $listItem->created_at->diffForHumans() }}
                    </span>
                </a>
            </li>
            
        @empty
            <li class="list-group-item border-0 mb-3 shadow-sm">
                No hay elementos disponibles
            </li>
        @endforelse           
    </ul>
    <div class="d-flex justify-content-end">
        {{ $list->links('pagination::bootstrap-4') }}
    </div>
    <hr>
    <h1>Items por Categoria</h1>
    <ul class="list-group">
        @foreach($listcat as $listptrcat)
            <li class="list-group-item border-0 mb-3">
                <a href="{{ route('categories.items', $listptrcat) }}">
                    {{ $listptrcat['title'] }} 
                </a>
            </li>
        @endforeach
    </ul>
</div>
@endsection
```

*Alineacion horizontal de elementos*

```html
<div class="d-flex justify-content-start">...</div>
<div class="d-flex justify-content-end">...</div>
<div class="d-flex justify-content-center">...</div>
<div class="d-flex justify-content-between">...</div>
<div class="d-flex justify-content-around">...</div>
```
*Alineacion vertical de elemnetos*

```html
<div class="d-flex align-items-start">...</div>
<div class="d-flex align-items-end">...</div>
<div class="d-flex align-items-center">...</div>
<div class="d-flex align-items-baseline">...</div>
<div class="d-flex align-items-stretch">...</div>
```
* Personalizar formulario con mensajes de error en un solo bloque.

resources/views/pages/categories/addcategory.blade.php
```php
@extends('layouts.default')
@section('title')
new category
@stop
@section('content')
<div class="container">
   <div class="row">
      <div class="col-12 col-sm-8 col-lg-6 mx-auto">
         <h1>Nueva Categoría</h1>
         <hr>
         @include('pages.categories.errorsformcat')
         <form class="bg-white shadow rounded py-3 px-4"
               method="POST" 
               action="{{ route('categories.store') }}">      
            @include('pages.categories.fieldsformcat', ['btnText' => 'Adicionar'])      
         </form>
      </div>
   </div>
</div>
@endsection
```
Formulario de Adición:
resources/views/pages/categories/editcategory.blade.php
```php
@extends('layouts.default')
@section('title')
category edit
@stop
@section('content')
<div class="container">
   <div class="row">
      <div class="col-12 col-sm-8 col-lg-6 mx-auto">
         <h1>Editar Categoría</h1>
            @include('pages.categories.errorsformcat')
            <form class="bg-white shadow rounded py-3 px-4"
                  method="POST" 
                  action="{{ route('categories.update', $category) }}">
               @method('PATCH')
               @include('pages.categories.fieldsformcat', ['btnText' => 'Actualizar'])
            </form>
      </div>
   </div>
</div>
@endsection
```

Formulario de Modificación:
resources/views/pages/categories/editcategory.blade.php
```php
@extends('layouts.default')
@section('title')
category edit
@stop
@section('content')
<div class="container">
   <div class="row">
      <div class="col-12 col-sm-8 col-lg-6 mx-auto">
         <h1>Editar Categoría</h1>
            @include('pages.categories.errorsformcat')
            <form class="bg-white shadow rounded py-3 px-4"
                  method="POST" 
                  action="{{ route('categories.update', $category) }}">
               @method('PATCH')
               @include('pages.categories.fieldsformcat', ['btnText' => 'Actualizar'])
            </form>
      </div>
   </div>
</div>
@endsection
```
Campos compartidos de los formularios de Adición y Modificación:
resources/views/pages/categories/fieldformcat.blade.php
```php
@csrf
<div class="form-group">
   <label for="title">Título de la Categoría</label>
   <input class="form-control border-0 bg-light shadow-sm"
          id="title" 
          name="title" 
          type="text"
          placeholder="Título ..." 
          value="{{ old('title', $category['title']) }}">   
</div>
<div class="form-group">
   <label for="comment">Descripción de la Categoría</label>
   <textarea class="form-control border-0 bg-light shadow-sm"
             name="comment" 
             placeholder="Descripción ...">
             {{ old('comment', $category['comment']) }}
   </textarea>
</div>
<button class="btn btn-primary btn-lg btn-block">
   {{ $btnText }}
</button>
<a class="btn btn-outline-secondary btn-block"
   href="{{ route('categories.index') }}">
   Cancelar
</a>
```
Mensajes de error:
resources/views/pages/categories/errorsformcat.blade.php
```php
@if($errors->any())
<div class="alert alert-danger alert-dismissible fade show" role="alert">
   @foreach ($errors->all() as $error)
       <li> {{ $error }}</li>
   @endforeach
   <button type="button"
           class="close"
           data-dismiss="alert"
           aria-label="Close">
           <span aria-label="true">&times;</span>
   </button>
</div>
@endif
```
Mostrar Categoria:
resources/views/pages/categories/showcategory.blade.php
```php
@extends('layouts.default')
@section('title')
category
@stop
@section('content')
<div class="container">
   <div class="row">
      <div class="col-12 col-sm-8 col-lg-6 mx-auto">
         <div class="bg-white p-5 shadow rounded">
            <h1>Datos de la Categoría</h1>      
            <hr>
            <p class="text-primary">
               {{ $category->title }}
            </p>
            <p class="text-secondary">
               {{ $category->comment }}
            </p>
            <hr>
            <div class="d-flex justify-content-between align-items-center">
               <a class="btn btn-outline-secondary" 
                  href="{{ route('categories.index') }}">
                  Regresar
               </a>
               @auth
                  <div class="d-flex justify-content-end">
                     <a class="btn btn-primary m-1" 
                        href="{{ route('categories.edit', $category) }}">
                        Editar
                     </a>                   
                     <a class="btn btn-danger m-1"
                        href="#" onclick="document.getElementById('id-delete-cat').submit()">
                        Eliminar
                     </a>
                     <form id="id-delete-cat" 
                           method="POST" 
                           action="{{ route('categories.destroy', $category) }}"
                           class="d-none">
                        @csrf
                        @method('DELETE')
                     </form>
                  </div>
               @endauth
            </div>
         </div>
      </div>
   </div>
</div>
@endsection
```
* Personalización de Otras Vistas

En esta sección se incluiran imáganes o diseños tomadas de: [undraw](https://undraw.co/illustrations)

Copiar las imagenes descargadas en .svg a la carpeta public/images

*Página de Inicio:*
resources/views/pages/home.blade.php
```php
@extends('layouts.default')
@section('title')
La Paz Digital
@stop
@section('content')
<div class="container">
   <div class="row">
      <div class="col-12 col-lg-6">
         <h1 class="text-primary mb-4">Bienvenidos a La Paz Digital</h1>
         <p class="lead text-secondary">
            La Paz Digital, es un portal de información web interactivo de la Ciudad de La Paz, que contiene datos sobre las Iglesias de La Paz, Museos de La Paz, Edificios más representativos, Monumentos, está también la representación virtual en modelos 3D de la ciudad de La Paz del siglo XVIII, gran parte de la esta información contiene una galería de fotografías, fotografías históricas, modelos tridimensionales, videos render, catálogos y un resumen informativo.
         </p>
         <div class="d-flex justify-content-end">
            <a class="btn btn-primary m-3"
               href="{{ route('categories.index') }}">
               Categorias
            </a>
            <a class="btn btn-outline-primary m-3"
               href="{{ route('contact') }}">
               Contactame
            </a>
         </div>
      </div>
      <div class="col-12 col-lg-6">
         <img class="img-fluid m-5" src="/images/home.svg" alt="La Paz Digital">
      </div>
   </div>
</div>
@endsection
```

*Habilitar los gradientes en bootstrap*
resources/sass/_variables.scss
```scss
// Enable gradients
$enable-gradients: true;
```

# Componentes

Lo habitual es trabajar con layouts y secciones de Blade en las vistas, pero hay una forma diferente de trabajar usando componentes de Blade que nos ayudan a crear elementos que podemos reutilizar en las vistas, sin necesidad de repetir código a través de toda la aplicación.

**Crear un componente**

```sh
php artisan make: component Nombrecomponente
```

Ejemplo:

```sh
php artisan make: component Alert
```

Luego de ejecutar el comando se crean dos archivos:

* Vista (resources/views/componentes/alert.blade.php)
* Clase (app/View/Components/Alert.php)

Personalizar la vista:




## Desactivar y personalizar las rutas de Auth::route()

[Referencia](https://styde.net/desactivar-y-personalizar-la-url-de-registro-en-laravel/)


## Middlewars

[Referencia](https://programacionymas.com/blog/restringir-acceso-solo-administradores-laravel-usando-middlewares)

