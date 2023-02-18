# LARAVEL Version 5.5
## JWT Authentication

### Resources
[Signature Verified](https://jwt.io/)

### Install JWT

Get Laravel version

```sh
php artisan --version
```

1. Create Project JWT Authentication

```sh
composer create-project --prefer-dist laravel/laravel jwt_project
```

2. Install [tymon/jwt-auht](https://github.com/tymondesigns/jwt-auth/wiki/installation)

```sh
cd jwt_project
composer require tymon/jwt-auth:dev-develop --prefer-source
```

3. Include the dependency in /config/app.php

```php
	'providers' => [
		// JWT auth provider
        Tymon\JWTAuth\Providers\LaravelServiceProvider::class,
	],

 	'aliases' => [
 	 	// 
		'JWTAuth' => Tymon\JWTAuth\Facades\JWTAuth::class,       
		'JWTFactory' => Tymon\JWTAuth\Facades\JWTFactory::class, 
	],
```

4. Setup the JWT config file

```sh
php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider" --force
```
*Result:* config/jwt.php

Generate a new random key, which will be used to sign your tokens

```sh
php artisan jwt:secret
```

### Setup de Middleware for getting user from token and refreshing token

#### Edit app/User.php

```php
<?php
namespace App;
use Illuminate\Notifications\Notifiable;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Tymon\JWTAuth\Contracts\JWTSubject;

class User extends Authenticatable implements JWTSubject
//class User extends Authenticatable 
{
    use Notifiable;
    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = [
        'name', 'email', 'password',
    ];
    /**
     * The attributes that should be hidden for arrays.
     *
     * @var array
     */
    protected $hidden = [
        'password', 'remember_token',
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

#### Inside the config/auth.php

```php
'defaults' => [
    'guard' => 'api',
    'passwords' => 'users',
],

'guards' => [
    'api' => [
        'driver' => 'jwt',
        'provider' => 'users',
    ],
],
```
#### Create the AuthController

```sh
php artisan make:controller AuthController
```

*Path: app/Http/Controllers/AuthController.php*
```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
use App\Http\Controllers\Controller;
use JWTAuth;
use App\User;

class AuthController extends Controller
{
    public function __construct()
    {
        $this->user = new User;
    }
    
    public function login(Request $request){
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
    }
}
```
#### Add route in routes/api.php 

```php
Route::group(['middleware' => ['api','cors']], function () {
    Route::post('authenticate', 'AuthController@login');
    Route::get(('locations'),['uses'=>'VirtualModelController@locations', 'as'=>'locations']);
    // Protected routes with authentication
    Route::group(['middleware' => 'jwt-auth'], function () {
        Route::get('users', 'UserController@getAuthUser');
    });
});
```
#### Create middleware to filter the request and validate the JWT token.

*Path: /*
```sh
php artisan make:middleware authJWT
```

*Path: app/Http/Middleware/authJWT.php*
```php
<?php
namespace App\Http\Middleware;
use Closure;
use JWTAuth;
use Exception;

class authJWT
{
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle($request, Closure $next)
    {
        try {
            //$user = JWTAuth::toUser($request->input('token'));
            if (!$user = JWTAuth::parseToken()->authenticate()) {
                return response()->json(['error'=>'User not found']);
            }
        } catch (Exception $e) {
            if ($e instanceof \Tymon\JWTAuth\Exceptions\TokenInvalidException) {
                return response()->json(['error'=>'Token is Invalid']);
            } else if ($e instanceof \Tymon\JWTAuth\Exceptions\TokenExpiredException) {
                return response()->json(['error'=>'Token is Expired']);
            } else if ($e instanceof \Tymon\JWTAuth\Exceptions\JWTException) {
                return response()->json(['error'=>'Token Absent']);
            } else {
                return response()->json(['error'=>'Something is wrong']);
            }
        }
        return $next($request);
    }
}
```
#### Register middleware in kernel to run during every HTTP request to your application

*Path: app/Http/Kernel.php*
```php
protected $routeMiddleware = [
    // ...
    'jwt-auth' => \App\Http\Middleware\authJWT::class,
];
```

### Create UserController

```sh
php artisan make:controller UserController
```

```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
use App\Http\Requests;
use App\Http\Controllers\Controller;
use JWTAuth;
use App\User;
use JWTAuthException;

class UserController extends Controller
{
    private $user;
    public function __construct(User $user) {
        $this->user = $user;    
    }

    public function getAuthUser(Request $request){
        $user = JWTAuth::toUser($request->token);
        return response()->json([$user]);
    }
}

```


### Testing Auth JWT

```sh
Open Postman
	POST: lapazdigital.app/api/auth/login
	Body [Raw, JSON(Application/json)]
		{
			"email":"admin@lapazdigital.net",
			"password":"admin"
		}
Send Button
```

Result Post Login JWT:

```sh
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGFwYXpkaWdpdGFsLmFwcC9hcGkvYXV0aGVudGljYXRlIiwiaWF0IjoxNTEzMDg0OTk5LCJleHAiOjE1MTMwODg1OTksIm5iZiI6MTUxMzA4NDk5OSwianRpIjoieWpuMlJjZjlPSXdoS1F6VCIsInN1YiI6MSwicHJ2IjoiODdlMGFmMWVmOWZkMTU4MTJmZGVjOTcxNTNhMTRlMGIwNDc1NDZhYSJ9.ALldHtoMs-veUDOk6PW1rCSlQ__4m6l1f3Up8HAahek",
    "response": "successful"
}
```

![Result Post Login JWT](images/testAuth.png "Result Post Login JWT")

### Testing Filter API JWT

```sh
Open Postman
	GET: lapazdigital.app/api/users
	Headers: 
        Key: Authorization 
        Value: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vbGFwYXpkaWdpdGFsLmFwcC9hcGkvYXV0aGVudGljYXRlIiwiaWF0IjoxNTEzMDg0OTk5LCJleHAiOjE1MTMwODg1OTksIm5iZiI6MTUxMzA4NDk5OSwianRpIjoieWpuMlJjZjlPSXdoS1F6VCIsInN1YiI6MSwicHJ2IjoiODdlMGFmMWVmOWZkMTU4MTJmZGVjOTcxNTNhMTRlMGIwNDc1NDZhYSJ9.ALldHtoMs-veUDOk6PW1rCSlQ__4m6l1f3Up8HAahek
    Send Button
```

Result response:

```sh
[
    {
        "id": 1,
        "name": "Administrador del Sistema",
        "email": "admin@lapazdigital.net",
        "created_at": null,
        "updated_at": null
    }
]
```

![Result Post Login JWT](images/testApiJwt.png "Result Post Login JWT")

## Roles and Permissions

[Laravel Entrust](https://www.uno-de-piera.com/roles-laravel-5-entrust/)

[Spatie / Laravel-Permission](https://styde.net/roles-y-permisos-con-spatie-laravel-permission/)

https://www.youtube.com/watch?v=I6eG8jPKRnU