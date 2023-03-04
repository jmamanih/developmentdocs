# HOMEBREW

![Homebrew Logo](images/Homebrew_logo.png)

Homebrew, es el gestor de paquetes para macOS.

El Homebrew Computer Club fue fundado en 1975, y reunía a los más grandes aficionados y profesionales de los ordenadores. Sin duda, los dos miembros más reconocibles son los propios fundadores de Apple, Steve Jobs y Stephen Wozniak.

Un gestor de paquetes es una herramienta que nos permite instalar desde la terminal herramientas o complementos que no vengan de serie en el Mac y está pensado para personas con unos conocimientos del uso de la línea de comandos.

## Instalaciones Previas
* [iTerm](iTerm.md)

## Instalar Homebrew

xcode preinstall

```
xcode-select --install

```
install homebrew

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew -v
```

After installing and as suggested in the command line, to check for any issues with the install run:

```
brew doctor
```

To search for an application:

```
brew search
```

To install
```
brew install <application-name>
```

To list all apps installed by Homebrew

```
brew list
```

To remove an installed application

```
brew remove <application-name>
```

To see what else you can do

```
man brew
```
