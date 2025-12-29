# Instalaciòn de Paquetes Importantes en MacOs arquitectura ARM Apple Silicom
# M1, M2, M3, M4

## Instalaciòn de Brew

Verifica el chip de tu Mac

Ve a:  > Acerca de este Mac

```sh
"Chip: Apple M4"
```

Abrir la terminal
```sh
Presionar Cmd + Espacio, escribe Terminal y presiona Enter
```

*Nota:* Se recomienda usar la Terminal [Warp](https://www.warp.dev)

Instalar Xcode Command Line Tools

```sh
xcode-select --install
```

Instalar Homebrew (brew)

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Añadir Homebrew al PATH

```sh
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verificar instalación

```sh
brew doctor
brew --version
```

Actualizar y revizar brew

```sh
brew update
brew upgrade
```

## Instalacion de Git

Instalar Git, la versión mas reciente

```sh
brew install git
```

Verificar la instalación de Git

```sh
git --version
```

## Instalar iTerm2

Instalar iTerm2 con Homebrew

Ejecuta este comando en tu Terminal:

```sh
brew install --cask iterm2
```

*Nota:* 🧠 --cask se usa para instalar aplicaciones gráficas (GUI).

Abrir iTerm2

Una vez instalado, se puede abrir iTerm2 desde:

Launchpad (búscalo como iTerm)

O directamente desde la Terminal con:

```sh
open -a iTerm
```

Configuración básica recomendada de iTerm2 (opcional)

Aquí algunas sugerencias rápidas para dejarlo listo:

🎨 Tema y colores

```sh
Abre iTerm2 → iTerm2 > Settings > Profiles > Colors
Cambia el color scheme o importa uno bonito como Dracula, Solarized, etc.
```

Para importar temas:

    brew install --cask iterm2-shell-integration

Y descarga esquemas desde: https://iterm2colorschemes.com/

🔠 Fuente con soporte para íconos (recomendado)

Instala una fuente como MesloLGS NF para usarla con oh-my-zsh y plugins con íconos:

```sh
brew tap homebrew/cask-fonts
brew install --cask font-meslo-lg-nerd-font
```

Luego en iTerm2 → Settings → Profiles → Text → Cambia la fuente a MesloLGS NF.

*Nota:* En VSCode editar el archivo settings.json y al final de la estructura adicionar: "terminal.integrated.fontFamily": "MesloLGS NF"

## Instalar Oh My Zsh

Instalar Oh My Zsh

Ejecuta este comando en tu terminal (usa iTerm2 para seguir desde ahora):

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Este comando:

Instala oh-my-zsh
Cambia tu shell por defecto a zsh
Crea un archivo de configuración ~/.zshrc
Cuando termine, reinicia iTerm2 o ejecuta:

```sh
source ~/.zshrc
```

## Instalar Powerlevel10k (reemplazo moderno y más rápido que Powerlevel9k)

Clonar el repositorio:

```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Cambia el tema en .zshrc:

Edita tu archivo:

```sh
nano ~/.zshrc
```

Busca la línea:

```sh
ZSH_THEME="robbyrussell"
```

Y cámbiala por:

```sh
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Guarda (Ctrl + O, Enter) y sal (Ctrl + X).

Recargar:

```sh
source ~/.zshrc
```

### Configurar Powerlevel10k

Al cerrar y abrir iTerm2, La primera vez te aparecerá una pantalla de configuración guiada (p10k configure).

Si no aparece, ejecutar:

```sh
p10k configure
```

Instalar fuente compatible (Nerd Font)

Powerlevel10k necesita una fuente compatible con íconos:

```sh
brew tap homebrew/cask-fonts
brew install --cask font-meslo-lg-nerd-font
```

Luego:

```sh
Abre iTerm2 > Preferences > Profiles > Text
Cambia la fuente a MesloLGS NF
```

## Instalar plugins útiles para Zsh

Autosuggestions y Syntax highlighting:

**Autosuggestions**

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

**syntax highlighting**

```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Luego editar el .zshrc:

```sh
nano ~/.zshrc

    plugins=(git zsh-autosuggestions zsh-syntax-highlighting)

```
Y recarga:

```sh
source ~/.zshrc
```

## Personalizar colores del prompt Powerlevel10k

Editar manualmente ~/.p10k.zsh

Abre el archivo:

```sh
nano ~/.p10k.zsh
```
Busca las secciones como:

```sh
typeset -g POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(
  os_icon
  dir
  vcs
  ...
)

typeset -g POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(
  status
  command_execution_time
  ...
  virtualenv
  node_version
  php_version
  laravel_version
  ...
)
```

Luego buscar las variables de color como:

```sh
POWERLEVEL9K_DIR_FOREGROUND=33
POWERLEVEL9K_DIR_BACKGROUND=236
```

Se puedes cambiar los números a otros colores ANSI. Por ejemplo:

```sh
Red: 160
Green: 34
Yellow: 220
Blue: 33
Magenta: 201
Cyan: 45
Gray: 245
Black: 0
White: 15
```
*Nota:* Para el tema de los colores para obtener toda la gama se puede ejecutar 
`for i in {0..255}; do print -P "%K{$i}  %k %F{$i}Color $i%f"; done`

Se puede usar esta tabla: https://upload.wikimedia.org/wikipedia/commons/1/15/Xterm_256color_chart.svg

Luego de editar guardar (Ctrl + O, Enter) y cerrar (Ctrl + X), luego recargar:

```sh
source ~/.zshrc
```

## Activar el segmento virtualenv (zsh) en el prompt para Python

Abre el archivo de configuración de Powerlevel10k:
```sh
nano ~/.p10k.zsh
```

Editar el archivo de configuración .p10k.zsh

```sh
nano ~/.p10k.zsh
# ó
code ~/.p10k.zsh
```

Editar las siguientes lineas

```sh
  typeset -g POWERLEVEL9K_VIRTUALENV_SHOW_PYTHON_VERSION=false
  typeset -g POWERLEVEL9K_VIRTUALENV_FOREGROUND='046'  # Verde brillante
  typeset -g POWERLEVEL9K_VIRTUALENV_BACKGROUND='234'  # Gris oscuro
  typeset -g POWERLEVEL9K_VIRTUALENV_PREFIX='🐍 '
  typeset -g POWERLEVEL9K_VIRTUALENV_SHOW_WITH_PYENV=true
  typeset -g POWERLEVEL9K_VIRTUALENV_GENERIC_NAMES=(virtualenv venv .venv)
  
  function prompt_my_virtualenv() {
    if [[ -n $VIRTUAL_ENV ]]; then
      local venv_name=$(basename "$VIRTUAL_ENV")
      p10k segment -f 2 -b 0 -t "🐍 $venv_name"
    fi
  }

  # The list of segments shown on the left. Fill it with the most important segments.
  typeset -g POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(
    # =========================[ Line #1 ]=========================
    os_icon                 # os identifier
    dir                     # current directory
    my_virtualenv           # nuestro segmento personalizado
    virtualenv              # python virtual environment
    vcs                     # git status
    # =========================[ Line #2 ]=========================
    newline                 # \n
    prompt_char             # prompt symbol
  )
```    

Activa un entorno virtual:

```sh
python3 -m venv venv
source venv/bin/activate
```

Y deberia ver algo como:

    🐍 venv-dev

Recargar configuración

```sh
source ~/.p10k.zsh
source ~/.zshrc
reset
```

Mostrar en el prompt la Ultima carpeta de la ruta de directorios

Abre el archivo de configuración de Powerlevel10k:

```sh
nano ~/.p10k.zsh
```

Busca esta variable:

```sh
typeset -g POWERLEVEL9K_SHORTEN_DIR_LENGTH=1
```

Si no existe, agrégala.

También asegúrarse de tener las siguientes lineas:

```sh
typeset -g POWERLEVEL9K_DIR_SHORTEN_STR='…'
typeset -g POWERLEVEL9K_SHORTEN_DIR_SHOW_LAST=always
typeset -g POWERLEVEL9K_SHORTEN_STRATEGY=truncate_to_last
```

Recargar configuración

```sh
source ~/.zshrc
```



