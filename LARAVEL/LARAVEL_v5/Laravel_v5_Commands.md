# LARAVEL Version 5.5

## Resources

* Go to [Laravel](https://laravel.com/) page, documentation.
* [Errors Http request](https://forge.laravel.com/api-documentation#introduction)

## CREATE PROJECT 

Open Terminal

```sh
cd c:\xampp\htdocs
composer create-project --prefer-dist laravel/laravel test

cd test
php artisan serve
```

Laravel version

```sh
php artisan --version
```

Specifying The Configuration Environment

```sh
php artisan migrate --env=local
```

## CREATE TABLES WITH MIGRATIONS

### Create database MySQL

Open console MySql: (Windows)
```sh
cd c:\xampp\mysql\bin
mysql -u admin -p
```

```sh
mysql> create database lapazdigitaldb;
```

### Config Environment for database
Open project Laravel
Edit file .env

```sh

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=lapazdigitaldb
DB_USERNAME=admin
DB_PASSWORD=mysqldb1234

```

### See full list of commands

```sh

php artisan list

php artisan make:migration --help

```

### Create Table

```sh
php artisan make:migration create_table_migration
```

Example:
```sh
php artisan make:migration create_languages_table --create=languages
```

On Error:

```sh
  [Illuminate\Database\QueryException]
  SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes (SQL: alter table `users` add
   unique `users_email_unique`(`email`))

  [PDOException]
  SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes
```

Solution:

Edit file \database\migrations\2014_10_12_000000_create_users_table.php

```php
 ...
 public function up()
    {
        Schema::defaultStringLength(191);    // <--- ADD 
        Schema::create('users', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name');
            $table->string('email')->unique();
            $table->string('password');
            $table->rememberToken();
            $table->timestamps();
        });
    }
 ...
```

#### Running migrates

Create Tables
```sh
php artisan migrate
```

Delete And Create Tables
```sh
php artisan migrate:refresh
```

Delete Tables
```sh
php artisan migrate:reset
```

Undo the last migration
```sh
php artisan migrate:rollback
```

State of Migrations
```sh
php artisan migrate:status
```

Para crear una migración:

## SEEDERS

### Runnig Seeders

Run all seeders

```sh
php artisan db:seed
```

```sh
php artisan db:seed --class=LanguageTableSeeder

php artisan db:seed --class=VirtualModelsTableSeeder

```

### Create Seeeders

```sh
php artisan make:seeder LanguageTableSeeder
```

Edit File LanguageTableSeeder.php

```php
...
public function run()
{
        DB::table('languages')->insert([
            'language_name' => 'Español',
            'iso' => 'es',
            'icon_path' => 'images/icon-flags/spain.png',
            'enabled' => true,
            'created_at' => date("Y-m-d H:i:s")
        ]);

        DB::table('languages')->insert([
            'language_name' => 'English',
            'iso' => 'en',
            'icon_path' => 'images/icon-flags/united-kingdom.png',
            'enabled' => true,
            'created_at' => date("Y-m-d H:i:s")
        ]);
}
...
```

Edit File \database\seeds\DatabaseSeeder.php

```php
...
public function run()
{
    // $this->call(UsersTableSeeder::class);
    $this->call(LanguageTableSeeder::class);
}
...
```
### Infor Seeders

```php

    $this->command->info('They are terrorizing picnics!');
    
```

## MODEL FACTORIES

Create Model and Migrate
```sh
php artisan make:model User -m
```

Create Model and Factory
```sh
php artisan make:model User --factory
```

Create Factory with refence to Model
```sh
php artisan make:factory UserFactory --model User
```

*Path: UserFactory*

```php
$factory->define(App\User::class, function (Faker $faker) {
    static $password;
    return [
        'name' => $faker->name,
        'email' => $faker->unique()->safeEmail,
        'password' => $password ?: $password = bcrypt('secret'),
        'remember_token' => str_random(10),
    ];
});
```

```php
// Creamos un model factory para poblar usuarios de tipo encargado
$factory->defineAs(App\User::class, 'encargado', function ($faker) {
    return [
        'name' => $faker->name,
        'email' => $faker->email,
        'password' => str_random(10),
        'type' => 'encargado',
        'remember_token' => str_random(10),
    ];
});
```

*Path: database/seeds/DatabaseSeeder.php*
```php
//...
public function run()
{
    $this->call(UsersTableSeeder::class);
    
    factory('App\User', 50)->create();
    factory('App\User','encargado',1)->create();   
}
```
Run seeder

```sh
php artisan db:seed
```

## MODELS

Models Directory
```
\app
```
## Define Models

```sh
php artisan make:model ModelName
```

Example:
```sh
php artisan make:model Language
```

Edit file app\Language.php

```php
<?php
namespace App;
use Illuminate\Database\Eloquent\Model;

class Language extends Model
{
    protected $table = "languages";                     // Set model with table
    protected $fillable = [                             // Return data in Json format
        'language_name', 'iso', 'icon_path', 'enabled'
    ];

    public function translations()  // Relationship One to Many
    {
        return $this->hasMany('App\Translation');  // Class model name
    }
}
```

Example: app\Translation.php

```php
<?php
namespace App;
use Illuminate\Database\Eloquent\Model;

class Translation extends Model
{
    protected $table = "translations";
    protected $fillable = [
        'translated_text', 'language_id', 'descriptive_text_id', 'user_id'
    ];

    public function language()
    {
        return $this->belongsTo('App\Language');
    }
}
```

## Generate a database migration when you generate the model

```sh

php artisan make:model User --migration

php artisan make:model User -m

```


### Create Models in custom Folder

```sh
cd app
mkdir Models
php artisan make:model Models/NewModel
``` 

## ROUTES

routes\web.php

```php
Route::get('test', function() {
    echo "Hellow world routings";
});
```

route list

```sh
php artisan route:list
```

## CONTROLLERS

PATH: app\Http\Controllers

### Create Controller

```sh
php artisan make:controller NameController
```

Example

```sh
$ php artisan make:controller LanguageController
```

# VIEWS

Views Directory

```sh
resources\views
```

Create view

```sh
cd resources\view
mkdir test
cd test
nano index.blade.php
```

index.blade.php
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Index Page</title>
</head>
<body>
    <h1>Test View, Hello world</h1>
</body>
</html>
```

controller
```php
<?php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
class TestController extends Controller
{
    public function view()
    {
        return view('test.index'); // <-----
    }
}

```

iclude files in views

```html
<link rel="stylesheet" type="text/css" href="{{ asset('css/styles.css') }}">
```

Asset redirect to folder public the Laravel Project

## INSTALL PROJECTS LARAVEL


[Guide](https://styde.net/como-instalar-proyectos-existentes-de-laravel/)

* Install Web Server xampp
* Create virtual host
* Clone project or download
* Grant writing permission

```sh
sudo chmod -R 755 storage
sudo chmod -R 755 bootstrap/cache
```

* Install dependencies
```sh
composer install
```

## INSTALL PACKAGE IN LARAVEL

### Install Bower and Gulp (Frontend packet manager)

#### Install in windows

[Download & Install Node.js](https://nodejs.org/en/)

* Install Bower Global

```sh
npm install -g bower
```

    *NOTE:*
    proxy configuration:

    ```sh
    npm help config
    npm config list
    npm config set proxy http://127.0.0.1:3122/
    npm config edit
    ```

    Error: bower not found
    ```sh
    npm config get prefix
    ```

    Open the Windows Control Panel, System environment Variables, find 'Path', copy path Step 1, here ; delimited
    Close Terminal

    Testing Bower
    ```sh
    bower -v
    ```

* [Download & Install Git](https://git-scm.com/downloads)

* Create your Project

    ```sh
    composer create-project --prefer-dist laravel/laravel nameProject
    cd nameProject
    git init
    cd public
    npm init
    bower init
    ```


### Install Material Design Lite

```sh
bower install material-design-lite --save
```

    NOTE:
    Bower proxy configuration
    Project root folder, create a file .bowerrc

    ```sh
    {
      "proxy": "http://<url>:<port>",
      "https-proxy": "http://<url>:<port>"
    }
    ```
Install MDL Icons

```sh
bower install material-design-icons --save
bower list
```

### Install Bootstrap

```sh
bower install bootstrap --save
```


## BUG FIX

No application encryption key has been specified.

.env

```sh
php artisan key:generate
```



## CRUD API REST

### Resource:

https://www.toptal.com/laravel/restful-laravel-api-tutorial

http://georgehk.blogspot.com/2015/04/crud-operations-in-laravel-5-with-mysql.html

https://platzi.com/blog/como-crear-apis/


### HTTP Status Codes and the Response Format

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
|   500     |   Internal server error. Ideally you're not going to be explicitly returning this, but if something unexpected 
breaks, this is what your user is going to receive.
|   503     |   Service unavailable. Pretty self explanatory, but also another code that is not going to be returned explicitly by the application.


Create Model and Migration

```sh
php artisan make:model Article -m
```

Create Model
Example: Menu Model
```sh
php artisan make:model Models/Menu
```

## Declare Global Variables

```sh
ng g cl app.globals
```

*Path: app.globals.ts*
```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class Globals {
    apiUrl: string = 'http://lapazdigital.app/api/';
}
```

*Path: app.module.ts*
```typescript
//...
import { Globals } from './app.globals';
//...
providers: [
    Globals
],
```
Usage global variables

*Component file*
```typescript
//...
import { Globals } from '../../app.globals';
//...
constructor(private globals: Globals) {}
//...
return this.globals.apiUrl;
```