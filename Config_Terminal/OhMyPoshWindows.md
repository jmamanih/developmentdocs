# Configuración de un símbolo del sistema personalizado para PowerShell o WSL con Oh My Posh

Fuente:  [Oh My Posh](https://learn.microsoft.com/es-es/windows/terminal/tutorials/custom-prompt-setup)

Oh My Posh proporciona funcionalidades de tema para una experiencia de símbolo del sistema totalmente personalizada que proporciona codificación de colores y avisos de estado de Git.


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

Creau acceso mediante Powershell en el menú contextual 

    Para añadir PowerShell al menú contextual de carpetas en Windows 10, puedes seguir estos pasos:

    Abrir el Editor del Registro: Presionar Win+R, escribir "regedit" y pulsar Enter.
    Navegar a la siguiente ruta:  HKEY_CLASSES_ROOT\Directory\Background\shell
    Crea una nueva clave dentro de "shell":
    clic derecho en "shell" y selecciona Nuevo > Clave
    Nombra esta clave como "PowerShell" (o "PowerShell Aquí" si prefieres)
    Para la clave que acabas de crear:
    Haz doble clic en el valor "(Predeterminado)" y escribe "Abrir PowerShell aquí"
    (Opcional) Añade un icono: crea un nuevo valor de cadena llamado "Icon" y establécelo como "powershell.exe"

    Ahora crea una subclave "command" dentro de tu clave PowerShell:

    Haz clic derecho en la clave "PowerShell" y selecciona Nuevo > Clave
    Nombra esta subclave como "command"

    Configura el comando:

    Haz doble clic en el valor "(Predeterminado)" de la subclave "command"
    Escribe: powershell.exe -NoExit -Command Set-Location -LiteralPath '%V'

    Cierra el Editor del Registro y reinicia el Explorador de archivos.

Para ver el funcionamiento hacer Shift + Clic derecho sobre la carpeta y elegir Abrir con PowerShell.



