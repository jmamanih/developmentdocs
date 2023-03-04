# Bases de Datos

## Instalar MySQl en MacOS

```sh
brew install mysql
brew services restart mysql
mysql -u root
```
*Nota:* Se recomienda reiniar el equipo

*Saber el puerto de MySql*
```
mysql - root -p

SHOW GLOBAL VARIABLES LIKE 'PORT';
```
*Configurar MySql*
```
 sudo mysql_secure_installation
```
*Asignar contraseña rrot*
```
sudo mysql -u root -p
```
## Crear perfil de Usuario Desarrollador con todos los privilegios

```
mysql -u root

Show databases;
Create database database_name;
GRANT ALL PRIVILEGES ON nombre_base_de_datos.* To 'nombre_desarrollador'@'localhost' IDENTIFIED BY 'clave';
Flush privileges;
Show grants;
exit

mysql -u dev -p
show databases;
```

## Establecer conexión con la Base de Datos

Establecer la configuración para el tipo de base de datos *config/database.php*
```php
 'default' => env('DB_CONNECTION', 'mysql'),
```
DB_CONNECTION es una variable de entorno que se encuentra en *.env*

Editar el archivo .env y asignar los parámetros de conexión, se recomienda antes probar la conexión con un cliente DB por ejemplo *DBeaver*

```php
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nombre_base_dde_datos
DB_USERNAME=rnombre_desarrollador
DB_PASSWORD=clase
```
Ejecutar las migraciones para comprobar conexion a la base de datos

```sh
php artisan migrate
```
Utilizar un cliente DB como [DBeaver](https://dbeaver.io/) para ver las tablas y relaciones

## Migraciones

Las migraciones crean la estructura fisica de una base de datos

*Crear una Migración*

```sh
php artisan make:migration create_plural_table_name_table
```
donde plural_table name es el nombre de la tabla en plural todo en minusculas

*Ubicaciòn de una migration*
```
database/migrations
```

*Crear una tabla y su modelos*
Tambien se pueden crear tablas y modelos al mismo tiempo

Ej. para la tabla posts de debe ejcutar:
```
php artisan make:model Post -m
```
-m indica que se creará la migración mas:

entonces se tienen dos archivos

```
app/Models/Post.php
```
y
```
database/migrations/2023_02_26_142028_create_posts_table.php
```
*NOTA:* Es recomendable crear primero la estructura de los modelos (ORM) y sus migraciones con el parámetro -m

Ejemplo:  Tablas relacionada de uno a muchos

*branch_offices*

```php
<?php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
return new class extends Migration
{
    public function up(): void
    {
        Schema::create('branch_offices', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name')->unique();
            $table->boolean('enabled')->default(true);        
            $table->timestamps();
        });
    }
    public function down(): void
    {
        Schema::dropIfExists('branch_offices');
    }
};
```
*procedures*
```php
<?php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
return new class extends Migration
{
    public function up(): void
    {
        Schema::create('procedures', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name')->unique();
            $table->string('code')->unique();
            $table->boolean('enabled')->default(true);
            $table->timestamps();
        });
    }
    public function down(): void
    {
        Schema::dropIfExists('procedures');
    }
};
```
*client_procedures*
```php
<?php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;
return new class extends Migration
{
    public function up(): void
    {
        Schema::create('client_procedures', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->bigInteger('user_id', false, true)->unsigned()->index();
            $table->integer('procedure_id')->unsigned();
            $table->integer('branch_office_id')->unsigned();
            $table->string('atention_code');
            $table->string('customer_name')->nullable();
            $table->dateTime('date_time_service');
            $table->string('observations')->nullable();
            $table->boolean('attended')->default(true);
            $table->timestamps();
            $table->foreign('user_id')->references('id')->on('users')->onUpdate('cascade')->onDelete('cascade');
            $table->foreign('procedure_id')->references('id')->on('procedures');
            $table->foreign('branch_office_id')->references('id')->on('branch_offices');
        });
    }
    public function down(): void
    {
        Schema::dropIfExists('client_procedures');
    }
};
```

*Eliminar las ultimas migraciones*

```sh
php artisan migrate:rollback
```

*Eliminar todas la migraciones*

```sh
php artisan migrate:fresh
```

## Seeders

Los Seeders insertan datos en las tablas

*Crear un Seeder*

```sh
php artisan make:seeder UsersTableSeeder
```

*Ubicación de los Seeder*
```
database/seeders
```
```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;
use DB;         // <--- ADD

class UsersTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        //
        DB::table('users')->insert([
            'name' => 'Administrador del Sistema',
            'email' => 'admin@tickets.com',
            'password' => bcrypt('admin'),
            'created_at' => date("Y-m-d H:i:s")
        ]);

        DB::table('users')->insert([
            'name' => 'Operador del Sistema',
            'email' => 'operador@tickets.com',
            'password' => bcrypt('operador'),
            'created_at' => date("Y-m-d H:i:s")
        ]);

        DB::table('users')->insert([
            'name' => 'Juan F. Mamani H.',
            'email' => 'jmamani@tickets.com',
            'password' => bcrypt('2687126'),
            'created_at' => date("Y-m-d H:i:s")
        ]);
    }
}
```
*Registrar el Seeder*

```php
<?php

namespace Database\Seeders;

// use Illuminate\Database\Console\Seeds\WithoutModelEvents;
use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     */
    public function run(): void
    {
        // \App\Models\User::factory(10)->create();
        // \App\Models\User::factory()->create([
        //     'name' => 'Test User',
        //     'email' => 'test@example.com',
        // ]);
        $this->call(UsersTableSeeder::class);
    }
}
```
*Ejecutar el Seeder*

Ejecutar de manera general 

```sh
php artisan db:seed
```
*NOTA:* Si sale el **error** de Class 'Database\Seeders\DB' not found, incluir en el seeder:
  
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
*Ejecutar solo un seeder*

```sh
php artisan db:seed --class=UsersTableSeeder
```

*Recontruir completamente la Base de Datos*

```sh
php artisan migrate:fresh --seed
```



