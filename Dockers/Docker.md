# Docker

![docker](images/docker.png)

**¿Qué es Docker?**
Docker es una herramienta diseñada para crear, implementar y ejecutar aplicaciones en contenedores. Un contenedor es una unidad de software que contiene todos los componentes necesarios para que una aplicación se ejecute, incluyendo el código, las bibliotecas y las dependencias. Los contenedores son una forma ligera de virtualización que permite a las aplicaciones ejecutarse de manera más rápida y segura que en un sistema operativo tradicional.

## Instalación de Docker

El primer paso para empezar a utilizar Docker es instalarlo en tu sistema operativo. Docker es compatible con Windows, macOS y Linux. 

* Instalación de Windows
* Instalación en Linux
* Instalación en Mac

## Crear un contenedor

Una vez que tienes Docker instalado, puedes empezar a crear contenedores. Para crear un contenedor, necesitas una **imagen de Docker**. Una imagen es un archivo que contiene todas las instrucciones necesarias para crear un contenedor. Puedes buscar imágenes de Docker en **Docker Hub**, el registro público de imágenes de Docker.

Para crear tu primer contenedor, puedes utilizar la imagen de Nginx, un servidor web ligero y rápido. Abre una terminal y escribe el siguiente comando:

```sh
docker run -d -p 80:80 nginx
```

## Crear y gestionar imágenes se Docker

¿Qué es una imagen de Docker?
Una imagen de Docker es un paquete de software que contiene todo lo necesario para ejecutar una aplicación, incluyendo el código, las bibliotecas y las dependencias. Las imágenes de Docker son como plantillas que se utilizan para crear contenedores de Docker. Una vez que se ha creado una imagen de Docker, se puede utilizar para crear múltiples contenedores que ejecuten la misma aplicación.



tutorial
https://www.youtube.com/watch?v=9eTVZwMZJsA


https://www.youtube.com/watch?v=6idFknRIOp4

