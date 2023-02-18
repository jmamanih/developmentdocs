# LARAVEL 

## Install Laravel in Windows

    1. Download [XAMPP](https://www.apachefriends.org/es/download.html) for Windows laste version
    2. Download [Composer](https://getcomposer.org/download/) for windows
        ```
        composer diagnose
        ```
    3. First install XAMPP
    4. Then install Composer
    5. Install [Git Bash for Windows](https://git-scm.com/download/win)

### Setting up ConEmu with Git Bash on Windows

*Install*
    
    Download [ConEmu](https://sourceforge.net/projects/conemu/)
    Unzip ConEmuPack..zip
    Copy Folder To Windows Directory
    Open ConEmu64.exe

*Setting*
Open Conemu
Show system menu, Settings, StartUp, Task
    
    Select {Bash::Git:bash}
    Check: Default task for new console

    Task parameters: /dir "c:\xampp\htdocs\lapaz" /icon "C:\Program Files\Git\mingw64\share\git\git-for-windows.ico"
    Start console: 
        "C:\Program Files\Git\bin\sh.exe" --login -i

Save settings

![Setting for Git Bash](images/configConEmuGitBash.png "Setting for Git Bash")

### Apache Virtual Host Config XAMPP

Edit File C:\Windows\System32\drivers\etc\hosts

```sh

127.0.0.1 www.lapazdigital.local

```

Edit File C:\xampp\apache\conf\extra\httpd-vhosts.conf

```sh
NameVirtualHost *:80

<VirtualHost *:80>
	DocumentRoot "c:/xampp/htdocs"
	ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "c:/xampp/htdocs/lapazdigital"
    ServerName www.lapazdigital.local
    ServerAlias lapazdigital.local
    <Directory "c:/xampp/htdocs/lapazdigital">
        AllowOverride All
        Require all Granted
        # En versiones anteriores de Apache 2.4 poner estas directivas en lugar de las 2 anteriores.
        # Order allow,deny
        # Allow from all
    </Directory>
</VirtualHost>
```

Restart Apache from XAMPP Control

To check the operation type www.lapazdigital in the browser address bar

### MySQL Add User from phpMyadmin

1. Open in browser:

	http://localhost/phpmyadmin/

2. Select Menu; Base de Datos, Cuentas de Usuario, Agregar cuenta de usuario

	Nombre de Usuario: admin
	Nombre de Host: Cualquier servidor, localhost
	Contraseña: Mysqldb1234
	Privilegios globales: Seleccionar Todo (check)

	Boton: Continuar

## Create Project Laravel 

Open Git Bash Terminal

```sh

cd c:\xampp\htdocs
composer create-project --prefer-dist laravel/laravel test

cd test
php artisan serve

```

* Go to [Laravel](https://laravel.com/) page, documentation.


## Conect proxy cmd in Windows

```sh

netsh winhttp show proxy

netsh winhttp import proxy source=ie

set http_proxy = http://127.0.0.1:3122

netsh winhttp reset proxy

composer diagnose

```
## Laravel version

```sh
php artisan --version
```

## Specifying The Configuration Environment

```sh
php artisan migrate --env=local
```


## RUNNIG PROJECT LARAVEL

Example: 

```sh
git clone https://github.com/karoys/laravel-native-roles-auth.git projectname
cd projectname
composer install
cp .env.example .env
php artisan key:generate
    add your database info in .env
php artisan migrate 
php artisan db:seed 
php artisan serve 
    start the app on http://localhost:8080/
```

