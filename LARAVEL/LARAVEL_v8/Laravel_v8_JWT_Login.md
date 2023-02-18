# Autenticación de Usuarios con JWT (Login)

![JWT-Logo](images/jwt_logo_laravel.png)

JSON Web Token (JWT) es un estándar abierto (RFC-7519) basado en JSON para crear un token que sirva para enviar datos entre aplicaciones o servicios y garantizar que sean válidos y seguros.

El caso más común de uso de los JWT es para manejar la autenticación en aplicaciones móviles o web. Para esto cuando el usuario se quiere autenticar manda sus datos de inicio del sesión al servidor, este genera el JWT y se lo manda a la aplicación cliente, luego en cada petición el cliente envía este token que el servidor usa para verificar que el usuario este correctamente autenticado y saber quien es.[Fuente: Introducción a JSON Web Token, Platzi](https://platzi.com/blog/introduccion-json-web-tokens/)

El tutorial se basa en [Laravel 7|8 JWT Authentication Tutorial: User Login & Signup](https://www.positronx.io/laravel-jwt-authentication-tutorial-user-login-signup-api/)


## Crear un proyecto Laravel

**Obtener la Versión de Laravel**

    php artisan --version

**Crear Proyecto Laravel**

    composer create-project --prefer-dist laravel/laravel laravel8jwtapp

## Conexión a la Base de Datos

**Crear Base de Datos para la Aplicacion**

    sudo mysql -u root
        CREATE DATABASE lapazdigital;
        SHOW DATABASES;
        quit

**Crear Usuario y Asignar Privilegios**

    sudo mysql -u root
        CREATE USER 'dev'@'localhost' IDENTIFIED BY '12345';
        GRANT ALL PRIVILEGES ON lapazdigital . * TO 'dev'@'localhost';
        FLUSH PRIVILEGES;
        SHOW GRANTS FOR 'dev'@'localhost';

    mysql -u dev -p
        Select current_user();
        SHOW DATABASES;
        SHOW FULL TABLES FROM lapazdigital;

**Configurando los parámetros de conexión a la base de datos**

Abrir y Editar el archivo .env

        DB_CONNECTION=mysql
        DB_HOST=127.0.0.1
        DB_PORT=3306
        DB_DATABASE=lapazdigital
        DB_USERNAME=dev
        DB_PASSWORD=12345

**Crear o editar la tabla users para usuarios del sistema**

Crear la tabla Users mediante migraciones

    php artisan make:migration create_users_table --create=users

ó editar el archivo: database/migrations/2014_10_12_000000_create_users_table.php

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateUsersTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::defaultStringLength(250);
        Schema::create('users', function (Blueprint $table) {          
            $table->increments('id');
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->rememberToken();
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
        Schema::dropIfExists('users');
    }
}
```

**Crear la Tabla física en la base de datos**

    php artisan migrate

**Verificar la base de datos**

    mysql -u dev -p

        show databases;
        use lapazdigital;
        select * from users;

**Insertar datos del usuario mediante Seeders**

Crear el Seeder

    php artisan make:seeder UserTableSeeder

Editar el archivo seeder: database/seeders/UserTableSeeder.php

```php

<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;

class UserTableSeeder extends Seeder
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
            'name' => 'Juan F. Mamani H.',
            'email' => 'jmamani@lapazdigital.net',
            'password' => bcrypt('jmamani'),
            'created_at' => date("Y-m-d H:i:s")
        ]);
    }
}

```

**Registrar el Seeder**

Editar el archivo: **database/seeders/DatabaseSeeder.php**

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

**Ejecutar el Seeder de Usuarios**

    php artisan db:seed --class=UserTableSeeder

**Verificar en la base de datos el registro creado**

    mysql -u dev -p

        show databases;
        use lapazdigital;
        select * from users;


## Instalando JWT

**Instalando el paquete jwt-auth en el proyecto**

    composer require tymon/jwt-auth
        
Incluir las dependencias en el archivo  **/config/app.php**

```php
'providers' => [
    ....
    ....
    //  JWT auth provider
    Tymon\JWTAuth\Providers\LaravelServiceProvider::class,
],
'aliases' => [
    ....
    // JWT
    'JWTAuth' => Tymon\JWTAuth\Facades\JWTAuth::class,
    'JWTFactory' => Tymon\JWTAuth\Facades\JWTFactory::class,
    ....
],
```
**Publicar la configuración de paquetes JWT desde el proveedor**

    php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider" --force

Como resultado se tiene el archivo **config/jwt.php**


**Generar una nueva clave aleatoria que se utilizará para firmar los tokens**

    php artisan jwt:secret

Esta operación generar una clave JWT y lo almacena al final del archivo .env

    ...
    JWT_SECRET=7bpenlWZ8NVqeqakYTnSXxcReACGlr8q4FfZaHibAkY4dmvz0XLVq3DRFTiksBop


## Configurar el modelo User

Abrir y editar el archivo **app/Model/User.php**

```php
<?php

namespace App\Models;

use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;

use Tymon\JWTAuth\Contracts\JWTSubject; 

class User extends Authenticatable implements JWTSubject
{
    use HasFactory, Notifiable;

    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = [
        'name',
        'email',
        'password',
    ];

    /**
     * The attributes that should be hidden for arrays.
     *
     * @var array
     */
    protected $hidden = [
        'password',
        'remember_token',
    ];

    /**
     * The attributes that should be cast to native types.
     *
     * @var array
     */
    protected $casts = [
        'email_verified_at' => 'datetime',
    ];
    /**
     * Get the identifier that will be stored in the subject claim of the JWT.
     *
     * @return mixed
     */
    public function getJWTIdentifier()
    {
        return $this->getKey();
    }
    /**
     * Return a key value array, containing any custom claims to be added to the JWT.
     *
     * @return array
     */
    public function getJWTCustomClaims()
    {
        return [];
    }
}
```

## Configurar Auth guard

Se tiene que configurar el JWT Auth Guard para asegurar el proceso de autenticación.

Abrir y editar el archivo **config/auth.php**

```php
   /*
    |--------------------------------------------------------------------------
    | Authentication Defaults
    |--------------------------------------------------------------------------
    */
    'defaults' => [
        'guard' => 'api',
        'passwords' => 'users',
    ], 

    /*
    |--------------------------------------------------------------------------
    | Authentication Guards
    |--------------------------------------------------------------------------
    */
    'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],
        'api' => [
            'driver' => 'jwt',
            'provider' => 'users',
            'hash' => false, 
        ], 
    ],
```

## Crear Controlador para la Autenticación

El controlador de autenticación controlará el proceso de autentificación de modo seguro.

Crear controlador

    php artisan make:controller AuthController

Abrir y Editar el archivo del controlador recientemente creado

    nvim app/Http/Controllers/AuthController.php

```php
<?php
<?php

namespace App\Http\Controllers;
use Illuminate\Http\Request;

use Illuminate\Support\Facades\Auth;
use App\Http\Controllers\Controller;
use Validator;

use App\Models\User;
use JWTAuth;

class AuthController extends Controller
{
     /**
     * Create a new AuthController instance.
     *
     * @return void
     */
    public function __construct() {
        //$this->user = new User;
        $this->middleware('auth:api', ['except' => ['login', 'register']]);
    }
        
    /**
     * Get a JWT via given credentials.
     * 
     * The login method is used to provide access to the user, and it is triggered when
     * /api/auth/login API is called. It authenticates email and password entered by the user
     * in an email and password field. In response, it generates an authorization token if it 
     * finds a user inside the database
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function login(Request $request){
    	$validator = Validator::make($request->all(), [
            'email' => 'required|email',
            'password' => 'required|string|min:6',
        ]);

        if ($validator->fails()) {
            return response()->json($validator->errors(), 422);
        }

        if (! $token = auth()->attempt($validator->validated())) {
            return response()->json(['error' => 'Unauthorized'], 401);
        }
        return $this->createNewToken($token);
    }
    
    /*public function login(Request $request) {
        $credentials = $request->only('email', 'password');
        $token = null;
        try {
            if (!$token = JWTAuth::attempt($credentials)) {
                return response()->json([
                    'response' => 'error',
                    'message' => 'Invalid email or password',
                ]);
            }
        } catch (JWTAuthException $e) {
            return response()->json([
                'response' => 'error',
                'message' => 'Failed to create token',
            ]);
        }
        return response()->json([
            'token' => $token,
            'response' => 'successful',
        ]);
    }*/

    /**
     * Register a User.
     * 
     * The register method is used to create a user when /api/auth/register route is called.
     * First, user values such as name, email and password are validated through the validation
     * process, and then the user is registered if the user credentials are valid. Then, it 
     * generates the JSON Web Token to provide valid access to the user.
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function register(Request $request) {
        $validator = Validator::make($request->all(), [
            'name' => 'required|string|between:2,100',
            'email' => 'required|string|email|max:100|unique:users',
            'password' => 'required|string|confirmed|min:6',
        ]);

        if($validator->fails()){
            return response()->json($validator->errors()->toJson(), 400);
        }

        $user = User::create(array_merge(
                    $validator->validated(),
                    ['password' => bcrypt($request->password)]
                ));

        return response()->json([
            'message' => 'User successfully registered',
            'user' => $user
        ], 201);
    }

    /**
     * Log the user out (Invalidate the token).
     * 
     * The logout method is called when /api/auth/logout API is requested, and it clears
     * the passed JWT access token.
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function logout() {
        auth()->logout();

        return response()->json(['message' => 'User successfully signed out']);
    }

    /**
     * Refresh a token.
     * 
     * The refresh method creates a new JSON Web Token in a shorter period, and It is 
     * considered a best practice to generate a new token for the secure user authentication
     * system in Laravel 8|7. It invalidates the currently logged in user if the JWT token is
     * not new.
     *
     * @return \Illuminate\Http\JsonResponse
     */
    public function refresh() {
        return $this->createNewToken(auth()->refresh());
    }

    /**
     * Get the authenticated User.
     *
     * The userProfile method renders the signed-in user’s data. It works when we place the
     * auth token in the headers to authenticate the Auth request made through the 
     * /api/auth/user-profile API.
     * 
     * @return \Illuminate\Http\JsonResponse
     */
    public function userProfile() {
        return response()->json(auth()->user());
    }

    /**
     * Get the token array structure.
     * 
     * The createNewToken function creates the new JWT auth token after a specified period 
     * of time, we have defined token expiry and logged in user data in this function.
     *
     * @param  string $token
     *
     * @return \Illuminate\Http\JsonResponse
     */
    protected function createNewToken($token){
        return response()->json([
            'access_token' => $token,
            'token_type' => 'bearer',
            'expires_in' => auth()->factory()->getTTL() * 60,
            'user' => auth()->user()
        ]);
    }
    
}
```

## Adicionar Rutas de Autenticación

Abrir y editar el archivo **routes/api.php**


```php
<?php

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Route;

/*
|--------------------------------------------------------------------------
| API Routes
|--------------------------------------------------------------------------
|
| Here is where you can register API routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| is assigned the "api" middleware group. Enjoy building your API!
|
*/

// Route::middleware('auth:api')->get('/user', function (Request $request) {
    // return $request->user();
// });

Route::group(['middleware' => ['api','cors']], function () {
    Route::post('authenticate', 'AuthController@login');
    Route::get(('locations'),['uses'=>'VirtualModelController@locations', 'as'=>'locations']);
    // Protected routes with authentication
    Route::group(['middleware' => 'jwt-auth'], function () {
        Route::get('users', 'UserController@getAuthUser');
    });
});
```

# Comprobar los APIs de Autenticación con POSTMAN


* [Instalar Postman](Postman/Postman.md)
* Levantar la aplicación 

    php artisan serve

* Abrir POSTMAN y comprobar los APIs de Autenticación de Usuarios

**Test API User Register**

POST:   http://127.0.0.1:8000/api/auth/register

Boby, form-data:

| KEY                   | DATA                  |
|-----------------------|-----------------------|
| name                  | Juan F. Mamani        |
| email                 | jmamani@gmail.com     |
| password              | juan1234              |
| password_confirmation | juan1234              |

Presionar el boton "SEND"

![API JWT User Register](images/jwt_test_api_register.png)

Ver el registro en la base de datos

    mysql -u dev -p


**Test API Login**

POST:   http://127.0.0.1:8000/api/auth/login

Boby, form-data:

| KEY                   | DATA                  |
|-----------------------|-----------------------|
| email                 | jmamani@gmail.com     |
| password              | juan1234              |

Presionar SEND

![API JWT Login](images/jwt_test_api_login.png)


**Test API User Profile**

GET:   http://127.0.0.1:8000/api/auth/user-profile

Authorization Tab:

| TYPE            | TOKEN                  |
|-----------------|-----------------------|
| Bearer Token    | eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xMjcuMC4wLjE6ODAwMFwvYXBpXC9hdXRoXC9sb2dpbiIsImlhdCI6MTYwOTk0NjEwNywiZXhwIjoxNjA5OTQ5NzA3LCJuYmYiOjE2MDk5NDYxMDcsImp0aSI6IjF2aVZTTHFhWkNmNTJ3amQiLCJzdWIiOjIsInBydiI6IjIzYmQ1Yzg5NDlmNjAwYWRiMzllNzAxYzQwMDg3MmRiN2E1OTc2ZjcifQ.-4XQ1rSNUlLlOIiY3qXxF3Q82MeXs6JbL5Q22cvEa8U |

Presionar SEND

![API JWT Login](images/jwt_test_api_user_profile.png)

**Test API Logout**

POST:   http://127.0.0.1:8000/api/auth/logout

Authorization Tab:

| TYPE            | TOKEN                  |
|-----------------|-----------------------|
| Bearer Token    | eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC8xMjcuMC4wLjE6ODAwMFwvYXBpXC9hdXRoXC9sb2dpbiIsImlhdCI6MTYwOTk0NjEwNywiZXhwIjoxNjA5OTQ5NzA3LCJuYmYiOjE2MDk5NDYxMDcsImp0aSI6IjF2aVZTTHFhWkNmNTJ3amQiLCJzdWIiOjIsInBydiI6IjIzYmQ1Yzg5NDlmNjAwYWRiMzllNzAxYzQwMDg3MmRiN2E1OTc2ZjcifQ.-4XQ1rSNUlLlOIiY3qXxF3Q82MeXs6JbL5Q22cvEa8U |

Presionar SEND

![API JWT Login](images/jwt_test_api_logout.png)

