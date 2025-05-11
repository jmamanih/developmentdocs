# Configuración de un símbolo del sistema personalizado para PowerShell o WSL con Oh My Posh

Fuente:  [Oh My Posh](https://learn.microsoft.com/es-es/windows/terminal/tutorials/custom-prompt-setup)
         [Mejorar la Terminal](https://jonathanbucaro.com/blog/mejora-la-experiencia-de-la-terminal-de-windows-con-ohmyposh/)

Oh My Posh proporciona funcionalidades de tema para una experiencia de símbolo del sistema totalmente personalizada que proporciona codificación de colores y avisos de estado de Git.

Instalar Windows Terminal desde la tienda de aplicaciones de Windows

Instalar una fuente con iconos Nerd Fonts (esta seccion se puede omitir)

    descargar los fonts de: https://www.nerdfonts.com/font-downloads
    descomprimir y copiar los archivos .ttf a la carpeta C:\Windows\Fonts

    descargar iconos: https://github.com/microsoft/cascadia-code/releases
    descomprimir y copiar a C:\\Windows\Fonts

Abrir Windows Terminal y ejecutar todos los comandos


Instalación de Oh My Posh para PowerShell

    winget install JanDeDobbeleer.OhMyPosh -s winget
    ó
    winget install JanDeDobbeleer.OhMyPosh

    oh-my-posh --version

Instalar fuentes

Para instalar las fuentes a nivel de sistema, la siguiente instrucción debe ejecutarse en una nueva terminal como administrador.

    oh-my-posh font install


Instalar una fuente con iconos Nerd Fonts

    Descarga la fuentes:

        Cascadia Code 
        Fira Code
        Meslo
    
    Descomprimir y copiar a C:\\Windows\Fonts


Configurar Oh My Posh en PowerShell

    notepad $PROFILE

Si el archivo no existe, Notepad lo creará. Agrega esta línea al final del archivo:

    oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\cascadia.omp.json" | Invoke-Expression

Guardar el archivo y cerrar Notepad

Instalar terminal Icons

    Install-Module -Name Terminal-Icons -Repository PSGallery

En Power Shell elegir la Fuente:  Cascade Code NF

    Abrir Menu Power Shell
    Propiedades, Fuente, Elegir fuente : Cascade Code NF

Cerrar Power Shell y Abrir


Error:

    La ejecución de Scripts está deshabilitada

Sol:

    Abrir Power Shell en modo administrador

    Ejecutar los siguientes comandos:

        Get-ExecutionPolicy -List 
        Set-ExecutionPolicy RemoteSigned -Scope CurrentUser 
            S
        Get-ExecutionPolicy -List
    
    Cerrar y volver abrir Power Shell

Configurar las fuentes en Visual Studio Code

    Instalar el paquete terminal
    F1, escribir json (configuración de usuario settings.json)
    Antes de la ultima llave adicionar: 

        "terminal.integrated.fontFamily": "Cascadia Code NF"

    Guardar, y se veran los cambios



