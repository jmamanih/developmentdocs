# CREAR UN ENTORNO DE DESARROLLO PARA LARAVEL Y ANGULAR EN WINDOWS 10


Verificar si tienes WSL 2 habilitado

    wsl --list --verbose

Si no está instalado, proceder con la instalación

    wsl --install -d Ubuntu

Iniciar a través de:

    wsl.exe -d Ubuntu

## Configurar la Terminal con Ubuntu

Habilitar el modo desarrollador en Windows

    Windows, Configuración, Actualización y Seguridad, 
    Para programadores, Modo para desarrolladores: Activado, Si
    Reiniciar el equipo

Habilitar Windows Subsysm Linux

    
    Abrir el Panel de control, Programas
    Activar o desactivar las características de Windows
    En la misma ventana buscar la opción de Subsistema de Windows para Linux y seleccionar, Aceptar
    Reiniciar el equipo

Instalar y Configurar Ubuntu

    Abrir Microsoft Ubuntu
    Buscar Ubuntu e Instalar
    Abrir la terminal de Ubunto y ejecutar los siguientes comandos:

        touch $HOME/.hushlogin

# Configurar la terminal Power Shell con Oh My Posh

