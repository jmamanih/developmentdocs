# APACHE WEB SERVER - PHP - MYSQL
## WINDOWS 10

![Git](images/apachephpmysql.jpg)

<a id="topmenu">

**Contenido**

* [Instalación](#idsec10 "Instalación")
* [Configuración](#idsec20 "Configuración")
* [Evitar el Hotlinking](#idsec30 "Hotlinking")
* [Errores](#idsec30 "Gestión de Errores")

<a id="idsec10">

## Instalación

XAMPP es el entorno más popular de desarrollo con PHP.

XAMPP es una distribución de Apache completamente gratuita y fácil de instalar que contiene MariaDB, PHP y Perl. El paquete de instalación de XAMPP ha sido diseñado para ser increíblemente fácil de instalar y usar.

* [Descargar XAMPP](https://www.apachefriends.org/es/download.html)
* Instalar XAMPP

<a id="idsec20">

## Configuración
### Apache Virtual Host Config XAMPP

Edit File C:\Windows\System32\drivers\etc\hosts

```sh
127.0.0.1 localhost

172.19.179.64 lapazdig.lapaz.dev
172.19.179.64 lapazmov.lapaz.dev

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

Add text to virtual configuration

```sh
<VirtualHost *:80>
	DocumentRoot "C:\xampp\htdocs"
	ServerName localhost
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "D:\SITES\lapazdigital"
    ServerName lapazdig.lapaz.dev
    <Directory "D:\SITES\Lapazdigital">
        AllowOverride All
        Require all Granted
        # En versiones anteriores de Apache 2.4 poner estas directivas en lugar de las 2 anteriores.
        # Order allow,deny
        # Allow from all
    </Directory>
</VirtualHost>

<VirtualHost *:80>
    DocumentRoot "D:\SITES\lapazenmov"
    ServerName lapazmov.lapaz.dev
    <Directory "D:\SITES\lapazenmov">
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

### Configuration virtual host to remote access in XAMPP

Edit File: C:\xampp\apache\conf\extra\httpd-xampp.conf

```sh
<IfModule alias_module>
    ...
    Alias /lapazdigital "D:/DEVELOPMENT/Lapazdigitalweb/lapazdigital_new/"
    <Directory "D:/DEVELOPMENT/Lapazdigitalweb/lapazdigital_new/">
        Require all granted
        ErrorDocument 403 /error/XAMPP_FORBIDDEN.html.var
    </Directory>

</IfModule>
```

Restart xampp control


[Ir la Inicio](#topmenu "Ir al inicio de página")


<a id="idsec30">

## Evitar el hotlinking

Bloquear accesos a los archivos con extensiones: jpg, jpeg, gif, png, bmp y zip de sitio.com

.htaccess edit file

```sh
RewriteEngine on
RewriteCond %{HTTP_REFERER} !^http://sitio.com*/.*$ [NC]
RewriteCond %{HTTP_REFERER} !^http://sitio.com*$ [NC]
RewriteRule .*\.(jpg|jpeg|gif|png|bmp|zip)$ - [F,NC] 
``` 
 * NC nocase
(case-insensitive), no importa si los términos aparecen en minúsculas o mayúsculas. 
* F forbidden
devuelve a la petición un mensaje de acceso denegado "403 Forbidden".

[Ir la Inicio](#topmenu "Ir al inicio de página")

<a id="idsec40">

## Gestión de Errores
### UAC Error

Important! Because an activated User Account Control (UAC) on your system some functions of XAMPP are possibly restricted.

Fixed:
You can press OK and install xampp to C:\xampp and not into program files


## Problema de CERTIFICADO SSL  HTTP, HTTPS en navegador Firefox.

Ref: https://support.mozilla.org/en-US/questions/1246548

Solucion:
No es un comportamiento nuevo: si el sitio especifica Strict Transport Security (Seguridad de transporte estricta), no puede agregar una excepción.
Puede ser que en version previas el Firefox ignorara esta advertencia o el nuevo sitio web tenga habilitado dicho control.
Actualmente por razones de seguridad por defecto el Firefox debe comprobarse este control.
De tomas formas, temporalmente, puedes deshabilitar dicha comprobación:
(1) Escriba about: config en la barra de direcciones. Haga clic en el botón de "... aceptar el riesgo".
(2) En el cuadro de búsqueda , escriba  network.stricttransportsecurity.preloadlist
(3) Haga doble clic en la preferencia network.stricttransportsecurity.preloadlist para cambiar el valor de true a false
4) Reinicie el Firefox y pruebe nuevamente
Si no funciona pruebe eliminar el archivo "SiteSecurityServiceState.txt" de la carpeta del perfil del Firefox
(http://mzl.la/1BAQULj).


## Error: La conexión no es privada, Navegador Chrome
### NET::ERR_CERT_AUTHORITY_INVALID


Solución:
Source: https://www.hostinger.es/tutoriales/error-la-conexion-no-es-privada-chrome/
https://www.solvetic.com/tutoriales/article/7692-solucionar-error-chrome-net-err-cert-invalid/

Utilizar los flags de Chrome. 
Esto es especialmente útil si estás probando algo localmente. 
Escribe lo siguiente en la barra de direcciones de Chrome:

chrome://flags/

Desde allí, busca la opción “Allow invalid certificates for resources loaded from localhost” y selecciona Enabled.

Presionar el boton "Relaunch"


