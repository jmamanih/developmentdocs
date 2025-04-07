# Configuración de un símbolo del sistema personalizado para PowerShell o WSL con Oh My Posh

Fuente:  [Oh My Posh](https://learn.microsoft.com/es-es/windows/terminal/tutorials/custom-prompt-setup)

Oh My Posh proporciona funcionalidades de tema para una experiencia de símbolo del sistema totalmente personalizada que proporciona codificación de colores y avisos de estado de Git.

## Instalación de una fuente Nerd

Instalar una fuente con iconos Nerd Fonts

    descargar los fonts de: https://www.nerdfonts.com/font-downloads
    descomprimir y copiar los archivos .ttf a la carpeta C:\Windows\Fonts

    descargar iconos: https://github.com/microsoft/cascadia-code/releases
    descomprimir y copiar a C:\\Windows\Fonts

Instalación de Oh My Posh para PowerShell

  
    winget install JanDeDobbeleer.OhMyPosh -s winget
    ó
    winget install JanDeDobbeleer.OhMyPosh

    oh-my-posh --version

Instalar una fuente con iconos Nerd Fonts

    Descarga la fuentes:

        Cascadia Code Nerd Font

        Fira Code Nerd Font
    
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

