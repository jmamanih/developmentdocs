# INSTALL TOOLS - LINUX DEBIAN (jessie ans stretch version)

Get version operating system linux

```
lsb_release -a

```

## Reinstall Grub
Init recovery mode from cd install debian

```
grub-install --boot-directory=/boot/ --recheck /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg
shutdown -r now
```

## Modify timeout on the grub

```
sudo nano /boot/grub/grub.cfg
```

```
terminal_output gfxterm
if [ "${recordfail}" = 1 ] ; then
  set timeout=-1
else
  if [ x$feature_timeout_style = xy ] ; then
    set timeout_style=menu
    set timeout=1
  # Fallback normal timeout code in case the timeout_style feature is
  # unavailable.
  else
    set timeout=1
  fi
fi
```

restart system

```
shutdown -r now
```

## Static IP and Network Configuration

Network configuration

```
sudo cp /etc/network/interfaces /etc/network/interfaces.bak
sudo nano /etc/network/interfaces

```

I will change  the value like this

```
auto lo
iface lo inet loopback

#My IP description
# IPv4 address
iface eth0 inet static
	address	192.168.0.100
	netmask	255.255.255.0
	network	192.168.0.0
	broadcast 192.168.0.255
	gateway	192.168.0.1

```
DNS configuration

```
nano /etc/resolv.conf
```

```
nameserver	8.8.8.8
nameserver	8.8.4.4
```

Restart Networking Service

```
sudo /etc/init.d/networking restart
```

After the service restart you can check the changes

```
ifconfig
```


## Config Wired

```
sudo nano /etc/NetworkManager/NetworkManager.conf
```

```
    [main]
    plugins=ifupdown,keyfile

    [ifupdown]
    managed=true
```

```
sudo sudo /etc/init.d/networking restart
```

```
sudo shutdown -r now
```

## Config Repository

```sh
su
nano /etc/apt/sources.list
```

```sh
# DEBIAN JESSIE ESTABLE
# Repositorio Oficial

deb http://http.us.debian.org/debian/ jessie main contrib non-free
deb-src http://http.us.debian.org/debian/ jessie main contrib non-free

# Repositorio de seguridad
deb http://security.debian.org/ jessie/updates main contrib non-free
deb-src http://security.debian.org/ jessie/updates main contrib non-free

deb http://ftp.debian.org/debian jessie main
deb-src http://ftp.debian.org/debian jessie main
```

To save and exit

```
ctrl+O, intro, ctrl+x
```
## Debian 9 stretch

Path File:  /etc/apt/sources.list 

```sh
deb http://ftp.us.debian.org/debian/ stretch main contrib non-free
deb-src http://ftp.us.debian.org/debian/ stretch main contrib non-free
```

## Install sudo

```
su
apt-get update
apt-get install sudo
nano /etc/sudoers
```


Edit file to enable jmamani

```js
    # User privilege specification
    root    ALL=(ALL:ALL) ALL
    jmamani ALL=(ALL) NOPASSWD: ALL

    # Allow members of group sudo to execute any command
    #%sudo  ALL=(ALL:ALL) ALL
    %sudo   ALL=NOPASSWD: ALL
```
## Update and Upgrade Linux Version

```sh
sudo apt-get update
sudo apt-get upgrade
sudo apt-get --fix-broken install
```

## Install Open VM Tools (VMWare Fusion into iOS MAC)


Add the following line to the /etc/apt/sources.list file.

```
    deb http://ftp.debian.org/debian/ jessie main contrib
```

Run the commands:

```
sudo apt-get update
sudo apt-get install open-vm-tools
sudo apt-get install open-vm-tools-desktop
sudo shutdown -r now
```

## Install Parallels Tools on a Debian Virtual Machine

Open Parallel, Menu Action, Install Parallel Tools

```sh
sudo umount /media/cdrom
sudo mount -o exec /media/cdrom

```
Go to the cdrom folder and run the Parallels Tools install script with the following commands:

```sh
cd /media/cdrom
sudo ./install

```

Unmount the Parallels Tools CD image.

```sh
sudo umount /media/cdrom
```

You need to restart the virtual machine for Parallels Tools to work.

## Install Virtual Box in Debian

In the first step add VirtualBox repository to your local /etc/apt/sources.list file:

```sh

echo "deb http://download.virtualbox.org/virtualbox/debian stretch contrib" >> /etc/apt/sources.list

```

Add VirtualBox repository public key:

```sh

wget -q -O- https://www.virtualbox.org/download/oracle_vbox_2016.asc | apt-key add

```

Update local repository package list:

```sh

apt-get udpate

```

### Install VirtualBox

List all available VirtualBox version:

```sh

$ apt-cache search virtualbox | grep ^virtualbox
virtualbox-5.0 - Oracle VM VirtualBox
virtualbox-5.1 - Oracle VM VirtualBox

```

Install desired VirtualBox version eg.:

```sh

apt-get install virtualbox-5.1

```

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

## dpkg

Install a package

```
dpkg -i package.deb
```

List all the installed Packages

```
dpkg -l
```

Verify if a package is installed

```
dpkg -l | grep 'package'
```

Uninstall a package

```
dpkg -r package.deb
```

Remove all package tracks

```
dpkg -p package.deb
```

Check the location of Packages installed

```
dpkg -L package.deb
```

## Enable maximize and minimize buttons into gnome

```
sudo apt-get install gnome-tweak-tool
```
Abrir el buscador de Debian: Actividades, buscar: Retoques, luego ir a Ventanas y Habilitar Maximizar y Minimizar.

## Cambiar XFCE por KDE Plasma

```
sudo apt -y install task-kde-desktop
```
* Cerrar Sesión, e iniciar seleccionando el entorno de escritorio KDE Plasma
* Ir al Menu Inicio, Preferencias de Sistema, Temas de Espacio de Trabajo y personalizar

## Install Visual Studio Code

* [Descargar VSCode ](https://code.visualstudio.com/): code_xxx_amd64.deb
* Install VScode
```
dpkg -i code_xxx_amd64.deb
code .
```



## To Install ATOM
Donwload file [atom-amd64.deb](https://atom.io/) download .deb

```sh
sudo apt-get update
sudo apt-get -f install
sudo dpkg -i atom-amd64.deb
atom
```

Uninstall Atom

```sh
sudo dpkg -r atom
```

## To Install Dropbox
Donwload file [dropbox..amd64.deb](https://www.dropbox.com/es/install-linux)

```sh
sudo apt-get update
sudo dpkg -i dropbox...-amd64.deb
```

```
Menu ACTIVITIES from Linux
Typing dropbox
Continue with the installation and configure the user and password and ready
```

## To Install Git

Installation

```sh
sudo apt-get update
sudo apt-get install git
sudo apt-get install -f
git --version
```


## To Install Docky

```sh
sudo apt-get update
sudo apt-get install docky
docky
```

## Install Google Chrome

Add Google Chrome Repository on Debian

```sh
sudo nano /etc/apt/sources.list
```

```sh
deb http://dl.google.com/linux/deb/ stable main
```

Installation

```sh
sudo apt-get update
sudo apt-get install google-chrome-stable
```

## To Install Terminator

Installation

```sh
sudo apt-get install terminator
terminator
```

To Configuration Terminal

```
Right-click in terminator
Preferences
Profiles
```
## To install Tmux






## Install Zip Unzip Files


    $ sudo apt-get install zip unzip

    $ unzip pics.zip
    $ unzip -tq pics.zip

    $ unzip pics.zip  -d /tmp
    $ unzip -l pics.zip




## Install PostgresSQL EnterpriseDB

Download postgres from:
http://www.enterprisedb.com/products-services-training/pgdownload

    $ sudo chmod +x postgresql-9.5.4-1-linux-x64.run
    $ ls -l
    $ sudo ./postgresql-9.5.4-1-linux-x64.run


## CouchDB

## Ver espacio en disco duro

```
$ df -h
$ df . -h

```
## Install Supervisor
Verify installed supervisor
```
apt-cache show supervisor
```

To install Supervisord
```
sudo apt-get install -y supervisor

```
Installing it as a package gives us the ability to treat it as a service:
```
sudo /etc/init.d/supervisor start
```

Configuration supervisor

```
sudo nano /etc/supervisor/supervisord.conf
```

Edit

```
[unix_http_server]
file=/var/run/supervisor.sock   ; (the path to the socket file)
chmod=0777                      ; sockef file mode (default 0700)

[include]
files=/etc/supervisor/conf.d/*.conf

[inet_http_server]
port=9001
username=admin
password=admin
```

Create configuration to run and monitor node script for notificaciones

```
sudo nano /etc/supervisor/conf.d/notificaciones.conf

```

Get path node

```
ps aux | grep node
```

notificaciones.conf

```
[program:notificaciones]
command=/opt/.nvm/versions/node/v5.6.0/bin/node /home/jmamani/Notificaciones_V1.0/asamblea-legislativa-backend/node_modules/babel-cli/lib/_babel-node index.js
directory=/home/jmamani/Notificaciones_V1.0/asamblea-legislativa-backend
autostart=true
autostart=true
autorestart=true
startretries=3
environment=NODE_ENV=development
stderr_logfile=/var/log/notificaciones/notificaciones.err.log
stdout_logfile=/var/log/notificaciones/notificaciones.out.log
user=jmamani
```

Create directoy logs

```
sudo mkdir /var/log/notificaciones
```

Restart service supervisor
```
sudo /etc/init.d/supervisor restart
```

Controlling Processes
```
supervisorctl reread
supervisorctl update
supervisorctl reload

```
```
supervisorctl
supervisor> stop notificaciones
notificaciones: stopped
supervisor> start notificaciones
notificaciones: started
supervisor> help
supervisor> exit

```
testing supervisor web
```
http://localhost:9001
user: admin
password: admin
```

## Install Postgres
