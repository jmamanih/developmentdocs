# NEOVIM
## LINUX

![Vim](images/neovim.jpg "Neovim")

[Neovim](https://github.com/neovim/neovim) es una refactorización del código de [Vim](https://www.vim.org/), es un fork, no un clon. Trae lo bueno de Vim con una mejor experiencia fuera de caja para el usuario.

¿Entonces qué es Vim? Vim es un editor de texto basado en modos (un lugar para escribir, otro para insertar comandos). Nació como mejora de Vi (1976). Su interfaz no es gráfica, sino basada en texto (aunque existen varias implementaciones con interfaz gráfica, como gVim).

**Referencias**

* [Neovim, Instalación y Configuración Básica](https://stsewd.dev/es/posts/neovim-installation-configuration/)
* [Neovim, Instalación de Plugins](https://stsewd.dev/es/posts/neovim-plugins/)
* [Setting Up Neovim for Web Development in 2020](https://medium.com/better-programming/setting-up-neovim-for-web-development-in-2020-d800de3efacd)
* [Best Neovim Plugins For Software Development in 2019](https://devtechnica.com/vim-neovim/best-neovim-plugins-for-software-development-in-2019)

**Instalaciones Previas**

* [Git](../Git/Git.md)

  ```sh
  sudo apt-get update
  sudo apt-get install git
  git --version
  ```
* Curl
    
  ```sh
  sudo apt-get update && sudo apt-get upgrade
  sudo apt-get install curl
  ```
  
<a id="topmenu">

**Contenido**

* [Instalacion](#idsec10 "Instalación")
* [Administrador de Plugins](#idsec20 "Instalar Administrador")
* [Plugins](#idsec30 "Plugins")

**Enlaces de Interes**

* [Comandos Vim](../Vim/Vim_Commands.md "Comandos Vim")


<a id="idsec10">

## Linux Debian 10 Buster
### Instalar Neovim

```sh
sudo apt-get update
sudo apt-get install neovim
```

Comprobar la instalación
```sh
nvim --version

nvim -v
```

### Instalando dependencias adicionales

**Proveedor de portapapeles**

    sudo apt-get install xclip

**Interfaces de Python**

    sudo apt-get install python-pip

Instalar interfaces de neovim

    sudo python -m pip install neovim

Mantener interface actualizado

    sudo python -m pip install --upgrade neovim

**Comprobando las dependencias adicionales**

    nvim +checkhealth


<a id="idsec20">

### Modos de Edición de nvim

Neovim tiene 3 modos principales:

    Modo normal - Donde todas las teclas son interpretadas como comandos.
    Modo insertar - Donde puedes escribir todo lo que teclees.
    Modo visual - Donde puedes seleccionar bloques de texto.

Para entrar y salir de cada modo:

    Para entrar al modo insertar, presiona i.
    Para salir del modo insertar, presiona Esc
    Para entrar al modo visual, presiona v.
    Para salir del modo visual, presiona Esc

Cuando abres Neovim, el modo por defecto es el normal.

Si se pierde en la aplicación de comandos presionar Esc varias veces hasta volver al modo normal.

Abrir un archivo

    nvim archivo.txt

Moverse por el editor

    h   izquierda
    j   abajo
    k   arriba
    l   derecha

Moverse entre palabras

    w   siguiente palabra
    b   palabra anterior

Comandos escenciales

    :w      guardar archivo
    :q!     salir del editor
    Esc+v   modo visual y seleccionar
    y       copiar texto seleccionado en el modo visual
    yy      copiar una linea
    yiw     copiar palabra
    d       cortar texto seleccionado
    dd      cortar linea actual
    diw     cortar palabra
    p       pegar despues del cursor
    u       deshacer
    ctrl+r  rehacer

Para obtener ayuda ejecutar desde neovim

  :h

Para aprender desde neovim ejecutar

  :Tutor

**Uso del modo visual**

    v       Cambiar a modo Visual y selecionar texto
    ctrl+v  seleccionar bloque

    0       marcar selección al inicio de linea
    $       marcar selección al final de linea

Comandos sobre el texto seleccionado

    u     Cambiar texto a Minusculas
    U     Cambiar texto a Mayusculas
    >     Indentar a la derecha
    <     Indentar a la izquierda

### Instalación del administrador de Plugins (vim-plug)

Instalar el administrador de Plugin *vim-plug*.
Antes se debe tener instalado curl (gestor de tranferencia de archivos).

```sh
curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
ó tambien se puede descargar el archivo [plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim) y guardarlo en ~/.local/share/nvim/site/autoload/plug.vim
```
cd Descargas
wget https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
mv plug.vim ~/.local/share/nvim/site/autoload/
```
Crear el archivo init.vim
```
cd ~
sudo mkdir ~/.config/nvim
sudo nano  ~/.config/nvim/init.vim
```
Agregar lo siguiente en init.vim:

```vim
" Directorio de plugins
call plug#begin('~/.local/share/nvim/plugged')

" Aquí irán los plugins a instalar

call plug#end()

" Luego de esta línea puedes agregar tus configuraciones y mappings
```

Establecer la configuración de init.vim y su ubicación
```
nvim
```
en la linea de comandos escribir
```sh
:so ~/.config/nvim/init.vim
```

### Instalando Plugins

Editar el archivo init.vim
```
sudo nvim ~/.config/nvim/init.vim
```

Copiar lo siguiente

```vim
call plug#begin('~/.local/share/nvim/plugged')

Plug 'tpope/vim-surround'  " Es buena idea agregar una descripción del plugin

call plug#end()
```
Para instalar Plugins ejecutar dentro de nvim los siguiente:
```

:PlugInstall
```
Presionar la tecla **Q**, para cerrar la ventana de administración de plugins

Tambien se puede utilizar desde la terminal
```sh
nvim +PlugInstall
```

### Usar y configurar los plugins

Para deshabilitar el plugin, comentar la linea respectiva al plugin en init.vim y ejecutar desde el editor
```
:PlugInstall
```
Para eliminar el plugin comentarlo y ejecutar
```
:PlugClean
```
Para mantener los plugins actualizados ejecutar
```
:PlugUpdate
```
Para mantener actualizado el administrador del plugin ejecutar
```
:PlugUpgrade
```
### Configuracion Inicial de Neovim

```vim
" -----------------------------
" CONFIGURACION GENERAL DE NVIM
" -----------------------------
" Linenumbers
set number
set ruler

set cursorline
set mouse=a

" Set Proper Tabs
set tabstop=4
set shiftwidth=4
set smarttab
set expandtab
```

### PLUGINS ESCENCIALES
Los nombres de los plugins deben ir entre las funciones de vim-plug (call plug#begin y call plug#end), y las configuraciones deben ir luego de call plug#end().

### Esquema de colores para el editor neovim

**Obtener lista de colores**

    nvim

    :colorscheme [space][tab]

**Instalación:**  Editar el archivo de plugins:

    sudo nvim ~/.config/nvim/init.vim

**Monokai**

```vim
call plug#begin('~/.local/share/nvim/plugged')

  Plug 'sickill/vim-monokai'  

call plug#end()

...

colorscheme monokai
```
**_Otra forma de instalar Monokai_**

[Vim-Monokai](https://github.com/crusoexia/vim-monokai)

Descargar [monokai.vim](https://github.com/sickill/vim-monokai)

Instalar Manualmente
```
sudo mkdir ~/.config/nvim/colors
sudo cp ~/Descargas/monokai.vim ~/.config/nvim/colors
``` 
```
sudo nvim ~/.config/nvim/init.vim


" Scheme Color
syntax enable
colorscheme monokai
```

**Medical Chalk**

```vim
    Plug 'ParamagicDev/vim-medic_chalk' 
    ...
    colorscheme monokai
```
**Instalar otros esquemas de color (Neosolarized)**

* Descargar el tema por ejemplo: [Neosolarized](https://github.com/overcache/NeoSolarized) color schema for neovim

* Descomprimir el archivo zip puede ser en descargas

      cd ~/.config/nvim
      sudo mkdir colors
      sudo cp ~/Descargas/NeoSolarized-master/colors/NeoSolarized.vim ~/.config/nvim/colors

* Editar el archivo  ~/.config/nvim/init.vim
            
      set termguicolors         " Activa true colors en la terminal
      set background=dark       " Fondo del tema: dark/light
      colorscheme NeoSolarized  " Activa tema NeoSolarized

**Identity**

* [Download Identity](https://vimcolors.com/1188/identity/dark)
* Select Schema

      colorscheme Identity

**Temas o Esquemas de Colores para descargar**

* [vim colors](https://vimcolors.com/)


### Barra de Estado (Airline) 
[Airline](https://github.com/vim-airline/vim-airline)
```vim
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'  " Temas para airline
...

let g:airline#extensions#tabline#enabled = 1  " Mostrar buffers abiertos (como pestañas)
let g:airline#extensions#tabline#fnamemod = ':t'  " Mostrar sólo el nombre del archivo

" Cargar fuente Powerline y símbolos (ver nota)
let g:airline_powerline_fonts = 1

set noshowmode  " No mostrar el modo actual (ya lo muestra la barra de estado)

let g:airline_theme='simple'   "Establecer Tema
```
**Temas de Airline**
: simple, dark, light, base16, jellybeans, tomorrow, violet, solarized, papercolor

### Explorador de Archivos (NERDTree) con Iconos
[Nerdtree Documentation](https://github.com/preservim/nerdtree)

Instalacion:
```sh
sudo nvim ~/.config/nvim/init.vim
```
```vim
Plug 'scrooloose/nerdtree'
Plug 'ryanoasis/vim-devicons'
...
" ****************************************
" NERDTREE
" ****************************************
let g:NERDTreeShowHidden = 1
let g:NERDTreeMinimalUI = 1
let g:NERDTreeIgnore = []
let g:NERDTreeStatusline = ''
" Automaticaly close nvim if NERDTree is only thing left open
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif                                                                
" Toggle
nnoremap <silent> <C-q> :NERDTreeToggle<CR>
  
" Tab-Keys Navigate
nnoremap  <C-l> :tabn<CR> 
nnoremap  <C-h> :tabp<CR>
nnoremap  <C-n> :tabnew<CR>

```
Comandos NERDTree

```
:NERDTree               Open tree view
:NERDTreeClose          Close tree view
:NERDTreeToggle         Toggle tree view
:NERDTreeFind           Find tree current file directory

:tabnext     (tabn)     Next Tab             
:tabprevius  (tabp)     Previus Tab     
:tablast     (tabl)     Last Tab
:tabnew                 New Tab
:tabclose               Close Tab

Ctrl+w                  Swap between panels

i                       Open file in horizontal panel
s                       Open file in vertical panel
t                       Open file in new Tab and edit
T                       Open file in new Tab
m                       Show menu NERDTree
                        Esc to exit menu
```
Nota para repetir el ultimo comando en nvim escribir en modo NORMAL
```
@:
```
### Integrar Terminal

Abrir el archivo init.vim
```sh
sudo nvim ~/.config/nvim/init.vim
```
En la sección de configuraciones adicionar lo siguiente:
```vim
" open new split panes to right and below
set splitright
set splitbelow
" turn terminal to normal mode with escape
tnoremap <Esc> <C-\><C-n>
" start terminal in insert mode
au BufEnter * if &buftype == 'terminal' | :startinsert | endif
" open terminal on ctrl+t
function! OpenTerminal()
  split term://zsh           " bash
  resize 15                  " size terminal window
  set nonumber
endfunction
nnoremap <c-t> :call OpenTerminal()<CR>
```
Comandos para la terminal:
```
Ctrl+t          Abrir Terminal
Esc             Salir del modo insertar de la termianl
Ctrl+w+flechas  Moverse entre paneles      
Ctrl+w w        Moverse entre paneles
exit            Para salir
```
### Buscador de Archivos (FZF)
[FZF](https://github.com/junegunn/fzf.vim)

```vim
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }
Plug 'junegunn/fzf.vim'

...

nnoremap <C-p> :FZF<CR>
let g:fzf_action = {
  \ 'ctrl-n': 'tab split',
  \ 'ctrl-h': 'split',
  \ 'ctrl-v': 'vsplit'
  \}
```
Para buscar un archivo presionar *Ctrl+P* ó ejecutar :Files , escribir el nombre de archivo y navegar en el panel para seleccionar el archivo luego presionar:

    ctrl+n    abrir archivo en un nuevo tab.
    ctrl+h    abrir archivo bajo el panel horizontal (split view).
    ctrl+v    abrir archivo al lado del panel vertical (vertical split).
    Enter     abrir archivo en el panel seleccionado.
   
    :Files    abre el panel de busqueda de archivos y vista previa
    :Buffers  abre archivos modificados
    :BLines   buscar una linea en el archivo
    :Colors   abre el panel de selección de colores
    :q        para salir

### Busqueda Mejorada (Incsearch)
[IncSearch](https://github.com/haya14busa/incsearch.vim)

Instalación

```vim
Plug 'haya14busa/incsearch.vim'
...

" Maps requeridos
map /  <Plug>(incsearch-forward)
map ?  <Plug>(incsearch-backward)

" Quitar resaltado luego de buscar
let g:incsearch#auto_nohlsearch = 1
```
Comandos

Para activar el espacio de busqueda, presionar / en el editor en el modo NORMAL

```vim
  /         buscar hacia adelante
            Ej. /function
  ?         buscar hacia atras
  tab       siguiente resultado 
  shift+tab resultado anterior
  enter     seleccionar busqueda
  esc       salir de la busqueda
```


### Guías de Indentacion
[Indentation Guide](https://github.com/Yggdroot/indentLine)
```vim
Plug 'Yggdroot/indentLine'

...

" No mostrar en ciertos tipos de buffers y archivos 
set list lcs=tab:\|\ "(here is a space).
let g:indentLine_fileTypeExclude = ['text', 'sh', 'help', 'terminal']
let g:indentLine_bufNameExclude = ['NERD_tree.*', 'term:.*']
```

### Comentar lineas (NERDCommenter)
[NerdCommenter](https://github.com/preservim/nerdcommenter)

```vim
Plug 'scrooloose/nerdcommenter'

...
let mapleader=","
set timeout timeoutlen=2000     "Dos segundos para presionar el comando Ejemplo ,ci
let g:NERDSpaceDelims = 1  " Agregar un espacio después del delimitador del comentario
let g:NERDTrimTrailingWhitespace = 1  " Quitar espacios al quitar comentario

```
Como utilizar

En modo visual seleccionar el texto a comentar, luego ejecutar el comando requerido.

Lista de Comandos básicos
```
,cc   comentar la linea actual
,ci   comentar por lineas individuales  //
,cs   comentar de forma decorativa  /* *** */
.cm   comentar minimamente solo extremos /*  */
,cu   descomentar lo seleccionado
```
Para mayor información
```
:h NERDCommenter
```

### Resumen de Configuración Básica de Neovim

```vim
" ****************************
" CONFIGURACION DE NEOVIM
" ****************************
"
" DIRECTORIO DE PLUGINS
" ---------------------
call plug#begin('~/.local/share/nvim/plugged')

	" Aquí irán los plugins a instalar

	Plug 'tpope/vim-surround'  " Es buena idea agregar una descripción del plugin
	Plug 'vim-airline/vim-airline'
	Plug 'vim-airline/vim-airline-themes'  	" Temas para airline
	
	" Esquemas de colores
	Plug 'sickill/vim-monokai'    		" Monokai
	Plug 'ParamagicDev/vim-medic_chalk' 	" Medic-Chalk
	
	Plug 'scrooloose/nerdtree'
	Plug 'ryanoasis/vim-devicons'
	Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }
	Plug 'junegunn/fzf.vim'
	Plug 'Yggdroot/indentLine'
	Plug 'haya14busa/incsearch.vim'
	Plug 'preservim/nerdcommenter'

call plug#end()

" -----------------------------
" CONFIGURACION GENERAL DE NVIM
" -----------------------------

" Scheme Color
syntax enable

"colorscheme medic_chalk 
"colorscheme monokai


set termguicolors  	  " Activa true colors en la terminal
set background=dark  	  " Fondo del tema: dark/light

"colorscheme NeoSolarized  " Activa tema NeoSolarized

colorscheme identity

" Enabled linenumbers
set number
set ruler
set cursorline
set mouse=a

" Set Proper Tabs
set tabstop=4
set shiftwidth=4
set smarttab
set expandtab

" Set Copy Paste into Clipboard System
nnoremap <C-c> "+y
vnoremap <C-c> "+y
nnoremap <C-v> "+gP
vnoremap <C-v> "+gP

" ------------------------
" CONFIGURACION DE PLUGINS
" ------------------------

" INDENTATION (Marcas de Indentación tabular)
" -------------------------------------------
"set list lcs=tab:\|\ "(here is a space).
let g:indentLine_char_list = ['|', '¦', '┆', '┊']
let g:indentLine_fileTypeExclude = ['text', 'sh', 'help', 'terminal']
let g:indentLine_bufNameExclude = ['NERD_tree.*', 'term:.*']


" AIRLINES (Barra de Estado)
" --------------------------
let g:airline#extensions#tabline#enabled = 1  " Mostrar buffers abiertos (como pestañas)
let g:airline#extensions#tabline#fnamemod = ':t'  " Mostrar sólo el nombre del archivo
" Cargar fuente Powerline y símbolos
let g:airline_powerline_fonts = 1
let g:airline_theme='simple'

set noshowmode  " No mostrar el modo actual (ya lo muestra la barra de estado)


" NERDTREE (Explorador de Archivos con Iconos)
" --------------------------------------------
let g:NERDTreeShowHidden = 1
let g:NERDTreeMinimalUI = 1
let g:NERDTreeIgnore = []
let g:NERDTreeStatusline = ''
" Automaticaly close nvim if NERDTree is only thing left open
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif
" Toggle Navigation
nnoremap <silent> <C-e> :NERDTreeToggle<CR>
"nnoremap  <c-w>l :tabn<CR>
"nnoremap  <c-w>h :tabp<CR>
"nnoremap  <c-n> :tabnew<CR>
nnoremap  <c-l> :tabn<CR>	
nnoremap  <c-h> :tabp<CR>		
nnoremap  <c-m> :tabnew<CR>

" TERMINAL
" --------
" open new split panes to right and below
set splitright
set splitbelow
" turn terminal to normal mode with escape
tnoremap <Esc> <C-\><C-n>
" start terminal in insert mode
au BufEnter * if &buftype == 'terminal' | :startinsert | endif
" open terminal on ctrl+t
function! OpenTerminal()
  split term://zsh
  resize 15
  set nonumber
endfunction
nnoremap <c-t> :call OpenTerminal()<CR>

" FILE SEARCHING
" --------------
" :Files    command execute for search files
nnoremap <C-f> :FZF<CR>
let g:fzf_action = {
  \ 'ctrl-n': 'tab split',
  \ 'ctrl-h': 'split',
  \ 'ctrl-v': 'vsplit'
  \}

" INCSEARCH
" ---------
" Maps requeridos
map /  <Plug>(incsearch-forward)
map ?  <Plug>(incsearch-backward)
map g/ <Plug>(incsearch-stay)

" Quitar resaltado luego de buscar
let g:incsearch#auto_nohlsearch = 1

" NERDCommenter
" -------------
let mapleader=","
set timeout timeoutlen=2000     "Dos segundos para presionar el comando Ej.  ,ci
let g:NERDSpaceDelims = 1  " Agregar un espacio después del delimitador del comentario
let g:NERDTrimTrailingWhitespace = 1  " Quitar espacios al quitar comentario

```

### Resúmen de configuración de Teclado

    Ctrl + E        Activar panel de NERDTree
                    t   abrir archivo en un nuevo Tab
                    s   abrir archivo en una área vertical al area de edición
                    i   abrir archivo en una área horizontal al área de edición

                    
    Ctrl + L        Moverse hacia la Derecha entre paneles Tab
    Ctrl + H        Moverse hacia la Izquierda entre paneles Tab
    Ctrl + W        Moverse entre sub-paneles 
    Ctrl + W, W     Moverse entre paneles de Edicion y NERDTree

    Ctrl + T        Abrir Terminal en la ventana activa

    Ctrl + C        Copiar lo selecccionado al portapapeles
    Ctrl + V        Pegar del portapapeles

    :Files          Listado de archivos y vista previa
                    Ctrl + N  Abrir archivo en nuevo Tab
                    Ctrl + V  Abrir archivo en subpanel vertical
                    Ctrl + H  Abrir archivo en subpanel horizontal
                    :q        Salir

    /cadena         Buscar cadena
                    TAB         siguiente ocurrencia
                    SHIFT+TAB   ocurrencia anterior
                    ESC         para salir

    ,ci             Comentar lo seleccionado en modo visual
    ,cu             Descomentar
   









