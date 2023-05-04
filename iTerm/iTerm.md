# iTerm

iTerm es un potente shell que te permite ampliar tu flujo de trabajo en sistemas de desarrollo Mac osx. Una interfaz sencilla y amigable.

## Instalaciones Complementarias
* [Homebrew](Homebrew.md)
* [Git](../Git/InstalacionGit.md)

## Instalar iTerm

Se puede descargar la aplicacion de la siguiente dirección: https://www.iterm2.com/downloads.html, o tambien se puede instalar desde la consola ejecutando el siguiente comando:


```sh
brew cask install iterm2
```
Para ejecutar el comando brew debe instalar previamente [Homebrew](Homebrew.md)

## Personalizar la Terminal
[Install Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh)

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

```sh
brew doctor
```

```sh
echo 'export PATH="/usr/local/sbin:$PATH"' >> ~/.zrc
```

```sh
brew doctor
```

```sh
brew prune
```
Para ver los cambios cierre la terminal y vuelva a abrirla.

## Recomendaciones
[Personalizacion de la Terminal en MacOS](../Config_Terminal_MacOS/configTerminal.md), es una guía completa para personalizar la terminal en MacOS cambiando su apariencia y la facilidad para ejecutar comandos mediante los hotkeys.

