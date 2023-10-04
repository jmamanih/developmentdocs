# LARAVEL BREEZE, INERTIA, VUE 3, CRUD
## Laravel Breeze

1. Crear un nuevo proyecto
```sh
cd Sites
export PATH=$PATH:~/.composer/vendor/bin
laravel new breezecrud
```
2. Crear la base de datos
```sh
mysql -u root -p
```
```sh
show databases;
create database breezedb;
```
3. Crear un usuario desarrollador (opcional)
```sh
create user 'dev'@'localhost' identified by '2687126';
select user from mysql.user;
grant all privileges on breezedb.* to 'dev'@'localhost';
flush privileges; 
exit
```
3. Ingresar a la carpeta del proyecto
```sh
cd breezecrud
```
4. Establecer conexión con la base de datos editar el archivo *.env* del proyecto
```php
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=breezedb
DB_USERNAME=root
DB_PASSWORD=2687126
```
5. Actualizar nvm y node
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
```sh
nvm install node
```
6. Instalar Laravel Breeze con Vue
```sh
composer require laravel/breeze --dev
php artisan breeze:install
    vue                 2
    inertia             yes
php artisan migrate
npm install
npm run dev
```
7. Ejecutar la aplicacion Web
Ejecutar de forma nativa
```sh
php artisan serve
```
*http:127.0.0.1:8000*

En el caso de usar Laravel Valet
```sh
cd breezecrud
valet link
```
*http://breezecrud.test*


https://larainfo.com/blogs/laravel-9-inertia-vue-3-crud-tutorial-example

juego:

https://www.youtube.com/watch?v=zfSk7AiMldk&list=PLfSVB4Wge3DIBIbK8YKR_BVTQadlaq3ZT

meteorito
https://www.youtube.com/watch?v=jrUJ8EsnctI&list=PLuB3bC9rWQAuzlz932pjjFLE1q8caF21N