# Visual Studio Code

## Install

[Download Visual Studio Code](https://code.visualstudio.com/)

## Essential Plugins

Open Visual Studio Code, Left Menu Extensions, Typing plugins-name in search box, Click button Install

PLUGINS: 

1. Path Intellicense
2. Markdown Github Preview Styling
3. Color Highlight
4. Babel ES6/ES7
5. File Icons

    File > Preferences > File Icon Theme
    
6. TODO Highlight
7. Prettier Now 
   CMD + Shift + P -> Format Document
8. Auto-Open Markdown
   Ctrl + K V  ó  ⌘ + K V

### Install Icon Themes

File > Preferences > Icon Theme > Install Icon Themes, select icons

### Install Color Themes

File > Preferences > Color Theme > Install Color Themes, select theme

### Opening Visual Studio Code from Command Line

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

### Zoom Editor

```
    Cmd +               Zoom In
    Cmd -               Zoom Out
```

## Configurar Font para la terminal con ZSH

- Descargar Font: https://www.nerdfonts.com/ (Descargar, Elegir Hack Nerd Font)
- Descomprimir font, instalar todas las fuentes (doble clic sobre el archivo font)
- Abrir VS Code, F1, escribir json (configuración de usuario settings.json)
- Antes de la ultima llave adicionar:  (anteceder al final de la penultima linea con una coma)
    
    "terminal.integrated.fontFamily": "Hack Nerd Font"

- Guardar, y se veran los cambios

## Extensiones para Temas

- Material Theme
- Material Theme Icons

    Elegir Commmunity Material Theme

## Extensiones por Default
- Material Theme Free
- Material Them Icons
- Markdown Editor
- Markdown Preview
- Path Intellisense
- Path Autocomplete
- PlantUML
- Prettier - Code formatter
- Print

## Extensiones para Perfíl de Python Developer

- Python
- Python Indent
- Python snippets

- Python Debugger
- Python Environment Manager

- Jupyter Keymap
- Jupiter Notebook Renders
- Jupyter
- Jupyter Cell Tags

Ejegir version de python (Crear un archivo .py, clic versión - ventana inferior izquierda, seleccionar interprete python)


## Crear Perfil para Spring Boot Developer Java



https://www.youtube.com/watch?v=cQfBenvXkRw

