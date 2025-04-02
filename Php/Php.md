# PHP

![Php Logo](images/php_logo.png)

Es un lenguaje de programación de uso general que se adapta especialmente al desarrollo web.

Fue creado inicialmente por el programador danés-canadiense Rasmus Lerdorf en 1994.

En la actualidad, la implementación de referencia de PHP es producida por The PHP Group.

PHP originalmente significaba Personal Home Page (Página personal), pero ahora significa el inicialismon recursivo PHP: Hypertext Preprocessor.

## Instalaciones previas

Instalar Homebrew, y si no está instalado ejecutar:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verificar que este correctamente configurado

```bash
brew --version
```

## Instalación de php en MacOs

* Asegurarse de haber instalado Homebrew y Actualizar
```sh
brew -v
brew update
```
* Instalar php

Instala la última versión estable de PHP con:

```sh
brew install php
```
Si se necesita una versión específica de php (por ejemplo, PHP 8.1 o 7.4):

```bash
brew install php@8.1
brew install php@7.4
```
* Configurar PHP:

Añadir PHP al PATH. 

```bash
echo 'export PATH="/usr/local/opt/php/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

* Verificar la instalación y la version de php
```sh
php - v
```

* Actualizar la versión de php a la ultima versión estable
```sh
brew upgrade php
```

## Configurar un servidor PHP (opcional)

Si se desea ejecutar un servidor PHP embebido para desarrollo, se puede iniciar con:

```bash
php -S localhost:8000
```

## Desinstalación de php en MacOs

Ver servicios activos

    brew services info --all


* Detener y Deshabilitar Servicios PHP

Antes de eliminar PHP, asegúrate de que ningún servicio relacionado esté en ejecución:

Detén cualquier servicio de PHP: Si PHP se ejecuta como parte de otros servicios (como Nginx o Apache), asegúrate de detener esos servicios primero.

Verificar versiones de PHP instaladas con Homebrew: Si has instalado PHP a través de Homebrew, puedes listar todas las versiones instaladas con:

    brew list | grep php

* Desinstalar PHP Instalado con Homebrew

Si has instalado PHP usando Homebrew, puedes desinstalar todas las versiones con los siguientes comandos:

Eliminar todas las versiones de PHP:

    brew uninstall --force php@7.4
    brew uninstall --force php@8.0

Eliminar paquetes relacionados: Asegúrate de eliminar todos los paquetes relacionados con PHP, como extensiones o herramientas adicionales:

    brew uninstall --force $(brew list | grep php)

Eliminar Archivos y Directorios Restantes de PHP

Para asegurarte de que no queden restos de PHP en el sistema, elimina manualmente los archivos y directorios asociados:

Eliminar directorios comunes de PHP:

    sudo rm -rf /usr/local/etc/php
    sudo rm -rf /usr/local/Cellar/php

Eliminar configuraciones y extensiones:

    sudo rm -rf /usr/local/lib/php
    sudo rm -rf /usr/local/include/php
    sudo rm -rf /Library/Server/Web/Config/php

Verificar la existencia de binarios: Verifica y elimina binarios adicionales de PHP que puedan estar en tu $PATH:

bash

    which php
    sudo rm -rf $(which php)

* Limpiar Caches y Preferencias

Si PHP ha creado archivos de caché o preferencias, puedes eliminarlos también:

    sudo rm -rf ~/Library/Caches/Homebrew/php

* Verificación Final

Para asegurarte de que todas las versiones de PHP han sido completamente eliminadas, puedes verificar nuevamente con:

    which php
    php -v

Si los comandos anteriores no devuelven ninguna versión de PHP, la desinstalación ha sido exitosa.
