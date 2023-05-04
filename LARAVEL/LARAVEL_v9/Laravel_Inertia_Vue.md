https://larainfo.com/blogs/laravel-9-inertia-vue-3-crud-tutorial-example


tailwaild

https://dev.to/geowrgetudor/setting-up-laravel-with-inertiajs-vuejs-tailwind-css-21pc


https://www.youtube.com/watch?v=V_OjMBOCW2k

Tutorial Breeze
https://www.youtube.com/watch?v=K_mINArtDoo

## Laravel Breeze

1. Crear un nuevo proyecto
```sh
cd Sites
laravel new laravelbreeze
```
2. Crear la base de datos
```sh
mysql -u root -p
```
```sh
show databases;
create database breezedb;
create user 'dev'@'localhost' identified by '2687126';
select user from mysql.user;
grant all privileges on breezedb.* to 'dev'@'localhost';
flush privileges; 
exit
```
3. Ingresar a la carpeta del proyecto
```sh
cd laravelbreeze
```
4. Establecer conexión con la base de datos editar el archivo *.env* del proyecto
```php
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=breezedb
DB_USERNAME=dev
DB_PASSWORD=2687126
```
5. Instalar Laravel Breeze con Vue
```sh
composer require laravel/breeze --dev
php artisan breeze:install vue
php artisan migrate
npm install
npm run dev
```

*Actualizar nvm y node*
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
```sh
nvm install node
```