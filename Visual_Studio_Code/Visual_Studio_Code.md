# Visual Studio Code

## Install

[Download Visual Studio Code](https://code.visualstudio.com/)


## Opening Visual Studio Code from Command Line

```sh
touch ~/.bash_profile
open ~/.bash_profile 
```
or

```sh
open ~/.zshrc
```

Edit File:

```sh
code () { VSCODE_CWD="$PWD" open -n -b "com.microsoft.VSCode" --args $* ;}
```

Testing

```sh
code .
```


## Configurar Font para la terminal con ZSH

- Descargar Font: https://www.nerdfonts.com/ (Descargar, Elegir Hack Nerd Font)
- Descomprimir font, instalar todas las fuentes (doble clic sobre el archivo font)
- Abrir VS Code, F1, escribir json (configuración de usuario settings.json)
- Antes de la ultima llave adicionar:  (anteceder al final de la penultima linea con una coma)
    
    "terminal.integrated.fontFamily": "Hack Nerd Font"

    ó

    "terminal.integrated.fontFamily": "Cascadia Code NF"

- Guardar, y se veran los cambios

## Instalar Idioma Español y Alternar entre Idiomas

* Instalar el paquete "Spanish Language Pack" o "Paquete de idioma español"
* Presione "Ctrl+Mayús+P" o "Cmd+Shift+P" elegir "Configure Display Language", seleccionar el idioma deseado
* Reiniciar VS Code

## Extensiones por Default
- Material Theme Free
- Material Them Icons
- Markdown Editor
- Markdown Preview
    Ctrl + K V  ó  ⌘ + K V
- Path Intellisense
- Path Autocomplete
- PlantUML
- Prettier - Code formatter
    CMD + Shift + P -> Format Document
- Print
- Highlight CSV and TSV files, Run SQL-like queries
- TODO Highlight
- Terminal

## Select Icon Themes

File > Preferences > Icon Theme > Install Icon Themes, select icons

## Select Color Themes

File > Preferences > Color Theme > Install Color Themes, select theme

## Zoom Editor

```
    Cmd +               Zoom In
    Cmd -               Zoom Out
```
## Compartir Extensión con todos los Perfiles

        Clic derecho sobre la extensión, ó clic sobre icono Adminstrar de la extensión y elegir "Aplicar extensión a todos los perfiles"

## Crear perfiles de desarrollo

        Clic sobre icono Administrar, Perfil, Perfiles, Nuevo Perfil

## Extensiones para Perfíl de Python Developer

- Python
- Python Indent
- Python snippets

- Python Debugger

- Jupyter Keymap
- Jupiter Notebook Renderers
- Jupyter
- Jupyter Cell Tags

Ejegir version de python (Crear un archivo .py, clic versión - ventana inferior izquierda, seleccionar interprete python)

## Extensiones para Perfíl de React JS developer

- ES7 + React/Redux/React-Native snippets

## Extensiones para Perfil de Laravel

- Alpine.js IntelliSense
- GitHub Copilot - Your AI peer programmer
- Official Laravel VS Code Extension
- Laravel goto view
- Laravel Snippets
- Php Intelephense

## Extensiones para perfil de Angular

- Angular Language Service
- Angular Snippets (Version ..) 

Esenciales para Angular

    Angular Language Service – Ofrece autocompletado, sugerencias de código y detección de errores en archivos .ts, .html y .json de Angular.
    Angular Snippets (Version 15) – Proporciona fragmentos de código predefinidos para Angular 15.

Para TypeScript y JavaScript

    ESLint – Ayuda a detectar errores y mejorar la calidad del código.
    Prettier - Code formatter – Formateador de código compatible con Angular.

Para HTML, CSS y SCSS

    HTML CSS Support – Mejora el soporte de HTML y CSS en Angular templates.
    Tailwind CSS IntelliSense (Si usas Tailwind CSS en tu proyecto) – Ofrece autocompletado y validación de clases de Tailwind.

Para trabajar con archivos y terminal

    Path Intellisense – Autocompletado de rutas en archivos.
    Auto Rename Tag – Cambia automáticamente la etiqueta de cierre cuando editas una etiqueta de apertura en HTML.
    Rainbow Brackets – Resalta y colorea pares de llaves {}, [], ().
    GitLens – Mejora la integración con Git y muestra el historial de cambios en línea.

## Extensiones para IA

    - Cline (prev. Claude Dev) – #1 on OpenRouter

## Crear Perfil para Spring Boot Developer Java


https://www.youtube.com/watch?v=cQfBenvXkRw


## Crear un entorno virtual de Python desde la terminal de Visual Studio Code

    # 1. Crear entorno virtual (si no existe)
    python -m venv venv

    # 2. Activar el entorno virtual
    # En Windows:
    # venv\Scripts\activate
    # En macOS/Linux:
    source venv/bin/activate

    # 3. Actualizar pip
    pip install --upgrade pip

    # 4. Instalar librerias por ejemplo: numpy 
    pip install numpy

    # 5. Ejecutar aplicación
    python main.py

## Ejecutar un programa Python en un entorno virtual con Visual Studio Code

    Cmd + Shift + P 
    Escribir "Python: Create Environment" y seleccionar la opción que aparece
    Seleccionar "Venv: Creates a '. venv' 
    Seleccionar la versión de Python a utilizar en el entorno virtual
    VS Code creará el entorno virtual y lo configurará automáticamente para el proyecto

## Elegir un entorno virtual con Visual Studio Code

    Cmd + P
        > Python Select Interpreter
            Select de workspace folder to set the interpreter (seleccionar la carpeta del proyecto)
                Seleccionar interprete ( elegir python del area de trabajo)