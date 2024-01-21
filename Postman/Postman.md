# POSTMAN

## Instalación en MacOs

Descargar el Intalador de [Postman](https://www.postman.com/downloads/)
Instalar
Crear una cuenta o ingresar con cuenta de correo Gmail

## Instalación en Linux Debian

Descargar la última versión desde su sitio oficial https://www.postman.com/downloads/

Ejecutar los siguientes comandos

    cd Downloads/
    tar -xzf Postman-linux-x64-7.32.0.tar.gz
    sudo mkdir -p /opt/apps/
    sudo mv Postman /opt/apps/
    sudo ln -s /opt/apps/Postman/Postman /usr/local/bin/postman
    postman


Para iniciar la aplicación desde un icono de inicio, debe crear un archivo .desktop (un acceso directo utilizado para iniciar una aplicación en Linux) 

    
    sudo vim /usr/share/applications/postman.desktop


Luego copie y pegue las siguientes configuraciones (asegúrese de que las rutas de los archivos sean correctas dependiendo de dónde extrajo los archivos):

    [Desktop Entry]
    Type=Application
    Name=Postman
    Icon=/opt/apps/Postman/app/resources/app/assets/icon.png
    Exec="/opt/apps/Postman/Postman"
    Comment=Postman Desktop App
    Categories=Development;Code;

Guarde el archivo y ciérrelo.

Si las rutas de archivo son correctas el icono deberia mostrarse en el menú del sistema.

