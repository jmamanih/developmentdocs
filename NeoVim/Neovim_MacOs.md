# NEOVIM
## MacOS

![Vim](images/neovim.jpg "Neovim")

[Neovim](https://github.com/neovim/neovim) es una refactorización del código de [Vim](https://www.vim.org/), es un fork, no un clon. Trae lo bueno de Vim con una mejor experiencia.

Vim es un editor de texto basado en modos.  Nació como mejora de Vi (1976). Su interfaz no es gráfica, sino basada en texto (aunque existen varias implementaciones con interfaz gráfica, como gVim).

<a id="topmenu">

**Contenido**

* [Instalacion en MacOs](#idsec10 "Instalación en MacOs")
* [Configuración](#idsec20 "Configuración")
* [Plugins](#idsec30 "Plugins")

**Enlaces de Interes**

* [Comandos Vim](../Vim/Vim_Commands.md "Comandos Vim")

<a id="idsec10">

## Instalación en MACOS

Instalaciones previas

```
cd ~
brew install curl
```
```
curl -LO https://github.com/neovim/neovim/releases/download/nightly/nvim-macos.tar.gz
tar xzf nvim-macos.tar.gz
./nvim-osx64/bin/nvim
```
```
brew install neovim
```
ó instale la version de desaroollo de Neovim
```
brew install --HEAD neovim
```

[Ir la Inicio](#topmenu "Ir al inicio de página")

<a id="idsec20">

## Configuración de Neovim

Instalación de Administrador de Complementos

Instalación de vim-plug

```
curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

Habilitar la compatibilidad con Python

```
brew install python
```
ó
```
brew upgrade python@3.8
```
```
python --version
```

[Ir la Inicio](#topmenu "Ir al inicio de página")

<a id="idsec30">

## Plugins
