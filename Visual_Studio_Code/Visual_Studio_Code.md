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
