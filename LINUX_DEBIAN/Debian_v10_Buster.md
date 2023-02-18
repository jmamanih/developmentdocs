# LINUX DEBIAN 10 BUSTER
## Instalación
* Descargar el archivo ISO [Debian 10 Buster](https://cdimage.debian.org/debian-cd/current/amd64/iso-dvd/)
* Proceder con la Instalación con el Asistente en modo Gráfico

## Modos de Arranque

Ingresar al entorno gráfico
```
startx
```
## Configurar la lista del repositorio

```sh
su
nano /etc/apt/sources.list
```

```sh

deb http://deb.debian.org/debian buster main contrib non-free
deb-src http://deb.debian.org/debian buster main contrib non-free

deb http://security.debian.org/debian-security buster/updates main contrib non-free
deb-src http://security.debian.org/debian-security buster/updates main contrib non-free
```
Para guardar cambios: Ctrl+O, Enter, Ctrl+X

## Instalar sudo

```
su
apt-get update
apt-get install sudo
nano /etc/sudoers
```

Habilitar usuario como administrador

file: /etc/sudoers

```sh
    # User privilege specification
    root    ALL=(ALL:ALL) ALL
    jmamani ALL=(ALL) NOPASSWD: ALL

    # Allow members of group sudo to execute any command
    #%sudo  ALL=(ALL:ALL) ALL
    %sudo   ALL=NOPASSWD: ALL
```

Reiniciar Sistema

## Instalar herramientas de red

Obtener informacion de la red con **ifconfig**

    sudo apt-get update
    sudo apt-get install net-tools

    sudo ifconfig

Reiniciar el servicio de red

    sudo /etc/init.d/networking restart


## Install Build-Essential
Build-Essential package contains an informational list of packages which are considered essential for building Debian packages including gcc compiler, make and other required tools.

Installation

```sh
sudo apt-get update
sudo apt-get install build-essential
```

Verify installation

```sh
whereis gcc make
gcc -v
make -v
```

## Instalar Parallels Tools en Máquina Virtual 

Parallel: Menu Acciones, Instalar Parallel Tools

```sh
su
sudo umount /media/cdrom
sudo mount -o exec /media/cdrom

cd /media/cdrom
sudo ./install

sudo umount /media/cdrom
```

Reiniciar Sistema

## Instalar VMTools en VMWare Workstation

1. VMware Workstation: Menu VM, Install VMWare Tools
2. Ejecutar:
```sh
su
sudo umount /media/cdrom
sudo mount -o exec /media/cdrom
cd /media/cdrom
cp /media/cdrom/VMwareTools_<version>_.tar.gz /tmp/
cd /tmp
tar -zxvf VMwareTools-<version>.tar.gz

cd vmware-tools-distrib
./vmware-install.pl
```
3. Desmontar el CDROM
```sh
sudo umount /media/cdrom
```
4. reiniciar maquina virtual


*Otro método de Instalacion de VMWare tools*
```sh
sudo apt-get install open-vm-tools
```

## Cambiar contraseña
```sh
su
passwd
```

## Instalar KDE Plasma en Debian 10

```
sudo apt -y install task-kde-desktop
```
* Cerrar Sesión, e iniciar seleccionando el entorno de escritorio KDE Plasma
* Ir al Menu Inicio, Preferencias de Sistema, Temas de Espacio de Trabajo y personalizar

## Personalizar escritorio KDE
> Inicio, Aplicaciones, Preferencias, Preferencias de Sistema, Tema del espacio de Trabajo


## Instalar paquetes deb con dpkg 

```
dpkg --version                  # Versión
dpkg -i package.deb             # Instalar
dpkg -l                         # Listado de paquetes instalados
dpkg -l | grep 'package_name'   # Verifica si el paquete esta instalado
dpkg -r package.deb             # Desinstalar solo paquete
dpkg -p package.deb             # Desinstalar todo incluido archivos de configuración
dpkg -L package.deb             # Ubicación de archivos del paquete instalado 
```

## Desinstalar firefox-esr entorno GNOME

Ejecutar los siguientes comandos:
```sh
sudo apt-get remove firefox-esr
```
Desinstalar firefox-esr y los paquetes dependientes

Para desinstalar el paquete firefox-esr y todos los paquetes dependientes que ya no sean necesarios en Debian Stretch.
```
sudo apt-get remove --auto-remove firefox-esr
```
Purga firefox-esr

Eliminar la información de configuración del firefox-esr
```
sudo apt-get purge firefox-esr
```
Para eliminar la información de configuración del firefox-esr y todos los paquetes dependientes en Debian Stretch ejecutar:
```
sudo apt-get purge --auto-remove firefox-esr
```

## Desinstalar Firefox ESR desde KDE Plasma
```sr
sudo apt-get remove firefox-esr-dbg
sudo apt-get remove --auto-remove firefox-esr-dbg
sudo apt-get purge firefox-esr-dbg
sudo apt-get purge --auto-remove firefox-esr-dbg
```

## Instalar Firefox
1. Descargar firefox Quantum
2. Ejecutar:
```sh
cd ~
cd Descargas
ls
tar xjf firefox-74.0.tar.bz2
sudo mv firefox /opt
```
3. Crear acceso directo a la Aplicacion
*Para Gnome:*
```sh
sudo apt install alacarte
```
buscar en Aplicaciones, Menu Principal y crear el acceso directo

*Para KDE Plasma:*
```sh
sudo apt install alacarte
su
sudo nano /usr/share/applications/firefox.desktop

[Desktop Entry]
Name=Firefox
Comment=Navegador Firefox
Exec=/opt/firefox/firefox
Icon=/opt/firefox/browser/chrome/icons/default/default128.png
Terminal=false
Type=Application
Categories=Network;WebBrowser;
```
Guardar Archivo: Ctrl+X
Ir al menu inicio, aplicaciones, Internet, Firefox
clic derecho, Añadir al Escritorio

## Instalar Curl

```sh
sudo apt update && sudo apt upgrade
sudo apt-get install curl
```

## Instalar Git

```sh
sudo apt-get update
sudo apt-get install git
git --version
```

Forzar Instalacion
```sh
sudo apt-get install -f      
```

## Instalar Visual Studio Code

Actualizar el índice de paquetes e instalar las dependencias
```sh
sudo apt update && sudo apt install software-properties-common apt-transport-https curl
```

Importar la clave de Microsoft GPG usando el siguiente comando curl:
```sh
curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```

Agrega el repositorio de Visual Studio Code a tu sistema:
```sh
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
```

Instalar la última versión de Visual Studio Code

```sh
sudo apt update
sudo apt install code
sudo apt update && sudo apt upgrade
```
Ejecutar
```sh
code .
```

Actualizar Visual studio Code

```sh
sudo apt updatesudo apt upgrade
```

## Instalar Terminator

```sh
sudo apt-get update
sudo apt-get install terminator
terminator
``` 

## Instalar Zsh (Paquete interprete de comandos)

```sh
sudo apt-get install zsh
zsh --version
```

## Instalar Oh-My-Zsh

```sh
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```
Activar tema por defecto

```sh
zsh
```
Establecer tema por defecto

```sh
cd ~
sudo nano .zshrc

    ZSH="bureau"

source .zshrc
```

Configurar Terminal (En Terminator) para establecer tema por defecto:

>Abrir Terminator, Menu Preferencias, Perfiles (Default), Comando, Ejecutar un comando: zsh


## Instalar tema Powerlevel9k para Oh-My-Zsh

```sh
cd ~
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k

sudo nano .zshrc
    ZSH_THEME="powerlevel9k/powerlevel9k"

source .zshrc
```

## Instalar PowerlineSymbols

```sh
sudo apt-get install fontconfig
sudo wget https://github.com/powerline/powerline/raw/develop/font/PowerlineSymbols.otf
sudo wget https://github.com/powerline/powerline/raw/develop/font/10-powerline-symbols.conf
sudo mkdir -p  ~/.local/share/fonts/
sudo mkdir -p ~/.config/fontconfig/conf.d/
sudo mv PowerlineSymbols.otf ~/.local/share/fonts/
sudo fc-cache -vf ~/.local/share/fonts/
sudo mv 10-powerline-symbols.conf ~/.config/fontconfig/conf.d/
```
## Instalar Powerline Fonts

```sh
sudo git clone https://github.com/powerline/fonts.git --depth=1
cd fonts
sudo ./install.sh
cd ..
sudo rm -rf fonts
```

## Instalar Awesone-Powerline Fonts

```sh
git clone https://github.com/gabrielelana/awesome-terminal-fonts
cp -r ~/awesome-terminal-fonts/build ~/.fonts
fc-cache -fv ~/.fonts
```

## Instalar NerdFonts (Iconos para la terminal)

https://jdelacruz26.github.io/linux/2017/10/18/terminal.html

https://www.triology.de/en/blog-entries/zsh-with-powerlevel9k

1. Primer método
```
git clone https://github.com/ryanoasis/nerd-fonts.git
cd nerd-fonts
sudo ./install.sh
```
En caso de existir errores
```sh
chmod +x install.sh
```

2. Segundo método
Instalar solo las fuentes necesarias, para este caso [Share Tech Mono Nerd Font Complete Mono y Shure Tech Mono Nerd Font Complete](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/ShareTechMono/complete), y tambien es recomendable instalar las fuentes [Hack](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/Hack)

```sh
cd ~
cd Descargas
sudo mv 'Shure Tech Mono Nerd Font Complete.ttf' ~/.local/share/fonts/
sudo mv 'Shure Tech Mono Nerd Font Complete Mono.ttf' ~/.local/share/fonts/
sudo fc-cache -f -v
```
## Estilizar el Prompt

Abrir el archivo ~/.zshrc

```sh
sudo nano ~/.zshrc
```

```sh
export ZSH="/home/juanfer/.oh-my-zsh"
export TERM="xterm-256color"

ZSH_THEME="powerlevel9k/powerlevel9k"

POWERLEVEL9K_MODE="awesome-fontconfig"
POWERLEVEL9K_DISABLE_RPROMPT=false
POWERLEVEL9K_PROMPT_ON_NEWLINE=true
POWERLEVEL9K_MULTILINE_LAST_PROMPT_PREFIX="▶ "
POWERLEVEL9K_MULTILINE_FIRST_PROMPT_PREFIX=""

POWERLEVEL9K_OS_ICON_BACKGROUND="orange1"
POWERLEVEL9K_OS_ICON_FOREGROUND="black"
POWERLEVEL9K_DIR_HOME_FOREGROUND="white"
POWERLEVEL9K_DIR_HOME_SUBFOLDER_FOREGROUND="white"
POWERLEVEL9K_DIR_DEFAULT_FOREGROUND="white"

POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(os_icon dir vcs)
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status time)

```

## Tmux
[Tutorial Tmux](https://www.youtube.com/watch?v=vwRxelWEuFE)

Permite utilizar varias consolas virtuales desde una misma terminal.

Ventajas.
- Restaurar Sesiones
- Organizar Terminales
- Cambiar de Entorno

Conceptos.

*Session*. Consolas virtuales gestionadas por tmux, se pueden dividir en Ventanas.

*Ventana*. Ocupan el espacio total de pantalla y se puede divir en paneles.

*Panel*. Regiones en una ventana, se pueden ejecutar una consola virtual independiente.

Arquitectura.

Cliente/Servidor, al ejecutar tmux se crean dos procesos uno para servidor y otro para cliente, estos procesos se comunican entre si mediante el envio de comandos. El Cliente envia comandos al servidor de tmux para que los ejecute, el Servidor ejecuta los comandos y gestiona sesiones y consolas virtuales, el servidor seguirá ejecutando las sesiones en segundo plano.

### Comandos Tmux

Prefijo: Ctrl+b

#### Comandos de Sesiones

* Crear una nueva sessión
```
tmux
```
Luego cerrar ventana

* Listar sesiones
```
tmux list-sessions
```
```
tmux ls
```
* Conectarnos a la última sesión
```
tmux attach
```
* Conectarnos a una sesión específica
```
tmux attach-session -t 7
```
* Crear nueva sessión desde una session abierta con tmux: Ctrl+b : new -s name-session
* Desconectarnos de una sesión: Ctrl+b d
* Renombrar una sesión: Ctrl+b $
* Navegar entre sesiones: Ctrl+b s
* Matar una sesion: Ctrl+b :  kill-session or
```
exit
```
or
```
tmux kill-session -t name_session
```

#### Comandos de Ventanas
1. Crear nueva ventana: Ctrl+b c
2. Renombrar ventena: Ctrl+b ,
3. Navegar entre ventanas: Ctrl+b 1, Ctrl+b 2, etc.

#### Comandos de Paneles
1. Dividir horizontalmente: Ctrl+b "
2. Dividir verticalmente: Ctrl+b %
3. Navergar entre paneles: Ctrl+b cursor
4. Cerrar panel activo: Ctrl+b x [y/n]  or type command $exit
5. Layouts predefinidos: Ctrl+b spacebar
6. Redimensional panel: Ctrl+b : resize-pane -L 15  (or -D, -L, -R) 
7. Activar Scrooll en el panel: Ctrl+b [  q para desactivar
8. Zoom de panel: Ctrl+b z
9. Mostrar número de panel: Ctrl+b q
10. Mover panel a la izquierda: Ctrl+b {
11. Mover panel a la derecha: Ctrl+b }


### Instalar Tmux

```sh
sudo apt-get update
sudo apt-get install tmux
tmux -V
``` 


### Instalar Oh My Tmux! Pretty & versatil configuracion de tmux
[source:Oh My Tmux](https://github.com/gpakosz/.tmux) 

Requerimientos:

* tmux >= 2.1

```
tmux -V
```

* outside for tmux $TERM must be set to: xterm-256color

```sh
sudo nano ~/.zshrc
```

adicionar la siguiente linea:
```
export TERM="xterm-256color"
```

Instalar Oh My Tmux:

* cambiar de directorio
```
cd ~
```

* sacar una copia de respaldo si existe ~/.tmux.conf
```
cp ~/.tmux.conf ~/.tmux.conf.backup
```

* ejecutar las siguientes lineas
```
cd ~
git clone https://github.com/gpakosz/.tmux.git
ln -s -f .tmux/.tmux.conf
cp .tmux/.tmux.conf.local .
``` 

### Habilitando el aspecto Powerline en tmux

* Instalar PowerlineSymbol
* Editar ~/.tmux.conf.local 
```sh
sudo nano ~/.tmux.conf.local 
```
```
# status left/right sections separators

#tmux_conf_theme_left_separator_main=''
#tmux_conf_theme_left_separator_sub='|'
#tmux_conf_theme_right_separator_main=''
#tmux_conf_theme_right_separator_sub='|'

#tmux_conf_theme_left_separator_main='\uE0B0'  # /!\ you don't need to install Powerline
#tmux_conf_theme_left_separator_sub='\uE0B1'   #   you only need fonts patched with
#tmux_conf_theme_right_separator_main='\uE0B2' #   Powerline symbols or the standalone
#tmux_conf_theme_right_separator_sub='\uE0B3'  #   PowerlineSymbols.otf font, see README.md

tmux_conf_theme_left_separator_main='\uE0B0'
tmux_conf_theme_left_separator_sub='\uE0B1'
tmux_conf_theme_right_separator_main='\uE0B2'
tmux_conf_theme_right_separator_sub='\uE0B3'
```
* Personalizar Colores, editar ~/.tmux.conf.local
```sh
sudo nano ~/.tmux.conf.local
```
```
# status left style
tmux_conf_theme_status_left_fg='#000000,#000000,#e4e4e4'  # black, white , white
tmux_conf_theme_status_left_bg='#ffff00,#00FF00,#00afff'  # yellow, pink, white blue
tmux_conf_theme_status_left_attr='bold,none,none'
```
* Cerrar Terminal
```
exit
```
* Ejecutar tmux
```
tmux
```

### Establecer a ZSH como gestor de comandos por defecto de TMUX

```sh
# set Zsh as your default Tmux shell
set-option -g default-shell /bin/zsh

# use 256 term for pretty colors
set -g default-terminal "screen-256color"
```
```
set-option -g default-shell /bin/zsh
```

## Miscelania para tmux

Instalar Calcurse (Calendario)
```
sudo apt-get install calcurse
calcurse
```

Instalar htop (Administracion de Procesos para el Sistema)
```
sudo apt-get install htop
htop
```
Instalar tty-clock (Reloj)
```
sudo apt-get install tty-clock
tty-clock
```
```
tty-clock -s
```
*Neofetch*

[Fuente](https://tecnonucleous.com/2018/12/25/como-instalar-neofetch-en-windows-10-y-en-linux/)

Neofetch es un programa escrito en lenguaje bash que nos permite ver en la terminal la información básica de nuestro hardware, así como del software. La información se muestra mediante el uso de colores y divertidos logotipos del sistema operativo ascii junto con información sobre tu sistema.

Instalar Neofetch 

```
sudo apt-get update
sudo apt-get install neofetch
neofetch
```
Instalar Ranger ([Filemanager](https://github.com/ranger/ranger))
```sh
sudo apt-get install ranger
ranger
```
Cursores para navegar o h j k l, Enter para abrir archivos y q para salir.

Instalar Cowsay ([Mensajeria](https://github.com/Code-Hex/Neo-cowsay))
```sh
sudo apt-get update
sudo apt-get install cowsay

cowsay "Linux Debian"
```
Otras utilidades
* [i3-gpas](https://github.com/OstOgBajer/i3-gaps) un administrador de ventanas en mosaico para Linux.
* [Rofi](https://github.com/davatorium/rofi) un conmutador de ventanas, iniciador de aplicaciones y reemplazo de menú.
* [Polybar](https://github.com/polybar/polybar) tiene como objetivo ayudar a los usuarios a crear barras de estado hermosas y altamente personalizables para su entorno de escritorio.

## NEOVIM 

* [Instalación y configuracion de NVIM](../NeoVim/Neovim_Linux.md)

