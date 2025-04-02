# COMPOSER

![Composer](images/logo.png)

Composer es una herramienta para la gestión de dependencias en PHP. Permite declarar las bibliotecas de las que depende un proyecto y las administrará (instalará/actualizará).

Sitio Oficial de [COMPOSER](https://getcomposer.org/download/)

## Instalación de Composer en MacOs

```sh
mkdir SetupComposer
cd SetupComposer

php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"

ls -l

php composer.phar

```

### Configuracion Global en MacOs

```sh
sudo mv composer.phar /usr/local/bin/composer
```
### Verificar la instalación de Composer

```sh
composer --version
```

## Reinstalar o Actualizar Composer

Crear un directorio de instalacion:

```bash
mkdir setupComposer
cd setupComposer
```

Instalar Composer:

```bash
 php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
 php composer-setup.php
 php -r "unlink('composer-setup.php');"
```

Usar Composer de forma global:

```bash
sudo mv composer.phar /usr/local/bin/composer
```

Verificar que Composer funcionar con un comando global:

```bash
composer --version
```
