 
# NGINX

![Mginx](images/nginx_logo.png) 

Nginx, pronunciado como “engine-ex”, es un servidor web de código abierto que, desde su éxito inicial como servidor web, ahora también es usado como proxy inverso, cache de HTTP, y balanceador de carga. [Fuente](https://kinsta.com/es/base-de-conocimiento/que-es-nginx/)

<a id="topmenu">

## CONTENIDO

* Instalación en Windows
* Instalación en MacOs
* [Instalación en Linux Debian](#idsec30 "Instalación en linux")
* [Servicios de Nginx](#idsec40 "Servicios de Nginx")
* [Configurar servidor web Nginx](#idsec50 "configurar servidor virtual")

## Referencias

[Guía de Instalación de Nginx](https://chachocool.com/como-instalar-nginx-en-debian-10-buster/)

<a id="idsec30">

## Instalación en Linux Debian

*Instalar nginx*

    sudo apt-get update
    sudo apt-get -y install 
    sudo nginx -v
    sudo nginx -V

*Mostrar archivos de configuración y verificar sintaxis*

    sudo nginx -t

*Ver configuración*

    sudo nginx -T

*Ver el estado del servicio*

    sudo service nginx status
    sudo systemctl status nginx 

*Verificar su funcionamiento*

    curl -I 127.0.0.1 

resultado:

    HTTP/1.1 200 OK
    Server: nginx/1.14.2
    Date: Thu, 03 Dec 2020 19:09:32 GMT
    Content-Type: text/html
    Content-Length: 612
    Last-Modified: Thu, 03 Dec 2020 18:25:14 GMT
    Connection: keep-alive
    ETag: "5fc92d8a-264"
    Accept-Ranges: bytes

Otra forma de verificar es abrir el navegador web y en la barra de direcciones escribir:


    http://localhost

[Ir al Inicio](#topmenu "Ir al inicio de la página")

<a id="idsec40">

## Servicios de Nginx

*Iniciar el servicio Nginx*

    sudo service nginx start   
    sudo systemctl start nginx 

*Habilitar el servicio Nginx*

    sudo service nginx enable 
    sudo systemctl enable nginx

*Reiniciar el servicio Nginx*

    sudo service nginx restart
    sudo systemctl restart nginx 

*Servicio de recarga Nginx*

Para indicarle a nginx que vuelva a cargar su configuración.

    sudo service nginx reload   
    sudo systemctl reload nginx 

*Detener el servicio de Nginx*

    sudo service nginx stop
    sudo systemctl stop nginx

*Mostrar ayuda del comando Nginx*

    systemctl -h nginx


[Ir al Inicio](#topmenu "Ir al inicio de la página")

<a id="idsec50">

## Configurar Servidor Web Nginx

Una vez instalada la base de datos, se debe configurar el servidor web con Nginx, para que pueda ejecutarse de manera correcta e interpretar PHP con el servicio PHP-FPM, 


1. Directorio principal de instalación de nginx

        /etc/nginx/

2. Ruta del archivo de configuración de nginx

        /etc/nginx/nginx.conf

3. Directorio donde se encuentran los hosts virtuales

        /etc/nginx/sites-available

4. Archivo de configuración por defecto del host virtual predeterminado

        /etc/nginx/sites-available/default 

5. Archivo de configuracion de hosts del sistema

        /etc/hosts

**Configurar un virtual host**

Para que un proyecto Laravel se ejecute en un virtual host en nginx, se debe agregar al archivo default en la ultima linea, lo siguiente:

    sudo nano /etc/nginx/sites-available/default

```vim
# Virtual Host Configuration

server {
    listen 80;
    listen [::]:80;
    server_name blog.test;
    root /var/www/html/blog/public;
    index index.php;
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock; 
    }
}
```
Para verificar la sintaxis ejecutar

    sudo nginx -t

Reiniciar el servicio Nginx

    sudo systemctl restart nginx

**Configurar el host**

Editar el archivo:

    sudo nvim /etc/hosts

Adicionar lo siguiente

    127.0.0.1       blog.test

Comprobar configuración

    ping blog.test


[Ir al Inicio](#topmenu "Ir al inicio de la página")