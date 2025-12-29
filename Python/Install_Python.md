# PYTHON

![Python](images/python.png)

Python es un lenguaje de programación ampliamente utilizado en las aplicaciones web, el desarrollo de software, la ciencia de datos y el machine learning (ML). Los desarrolladores utilizan Python porque es eficiente y fácil de aprender, además de que se puede ejecutar en muchas plataformas diferentes. El software Python se puede descargar gratis, se integra bien a todos los tipos de sistemas y aumenta la velocidad del desarrollo.

## Instalar Python en MacOs

Verificar si está instalado Python y la versión

```sh
python3 --version
```

## Gestionar las versiones de python con pyenv

Pyenv en es una herramienta que nos permite instalar diferentes versiones de Python y cambiar entre ellas según los requerimientos del proyecto con el cual necesitamos trabajar.

### Instalar pyenv para gestionar las versiones de Python

```sh
brew install pyenv
```

Verificar que Shell se está usando

```sh
echo $SHELL
```

Esto te devolverá una ruta como:

```sh
/bin/zsh → estás usando Zsh
# ó
/bin/bash → estás usando Bash
```

### Configurar pyenv en el shell

Agrega lo siguiente a tu archivo de configuración del shell. Si se usa:

- Zsh (por defecto en macOS): editar ~/.zshrc
- Bash: edita ~/.bash_profile o ~/.bashrc

```sh
# Agrega estas líneas
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
```

Reiniciar el shell o la terminal 

```sh
source ~/.zshrc
# ó
reset
```

Verificar y validar la instalación de pyenv

```sh
pyenv --version 
pyenv -v
```
    
## Instalar diferentes versiones de Python

Instalar versiones de Python

### Instalar versiones especificas

```sh
pyenv install 3.10.14
pyenv install 3.12.3
``` 

Verificar que estén disponibles:

```sh
pyenv versions
```

### Instalar la última versión estable de Python

Ver un listado de todas las versiones disponibles de Python

```sh
pyenv install --list
```

Buscar la última versión estable (sin "dev", "rc", ni "a/b", etc).

Por ejemplo, si se ve:

```sh
  ...
  3.12.3
  3.13.0rc1
```

Entonces 3.12.3 es la version más reciente estable.

Instalar la última versión estable

```sh
pyenv install 3.12.3
```

**Nota:** Si al instalar sale el mensaje:  WARNING: The Python lzma extension was not compiled. Missing the lzma lib?, se debe instalar:

```sh
brew install xz
```

Ver las versiones instaladas de python

```sh
pyenv versions
```

### Establecer la versión de Python

👉 A nivel global (para todo el sistema):

```sh
pyenv global 3.12.3
```

Ver la version global

```sh
pyenv global
python3 --version
```

👉 A nivel local (por proyecto):

En la carpeta de tu proyecto:

```sh
cd /Code/Python/proyecto
pyenv local 3.10.14
```

Esto creará un archivo .python-version en esa carpeta.

Ver la version local de python

```sh
pyenv local
```

Verificar la ruta del Python activo:

```sh
which python
```

Verificar paquetes instalados:

```sh
pip list
```

## Administración de paquetes con pip

### Instalación de pip

Verificar si esta instalado pip

```sh
pip --version
pip3 --version
```

Instalar pip

Al instalar python con "brew install python" se instala python y pip

En caso de no estar instalado pip ejecutar el siguiente comando

```sh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
```

Verificar la instalación de pip

```sh
pip --version
which pip
```

### Actualizar pip en un entorno virtual (venv o virtualenv)

Activa tu entorno virtual:

```sh
source venv/bin/activate
```

Y luego:

```sh
pip install --upgrade pip 
```
ó
```sh
python -m pip install --upgrade pip
```

### Ver paquetes del entorno virtual

Hacer un listado total

```sh
pip list
```
Buscar un paquete especifico instalado 

```sh
pip list | grep -i pandas
```

### Instalar paquetes en el entorno virtual segun lo requerido por el proyecto

Ejemplo

```sh
pip install fastapi
pip install schedule
```

### Exportar paquetes instalados en el entorno virtual

```sh
pip freeze > requirements.txt  
```

### Instalar paquetes exportados en entorno virtual

```sh
pip install -r requirements.txt
```

## Crear entornos virtuales por proyecto con pyenv y virtualenv

Virtualenv permite crear entornos virtuales de Python aislados, donde se puede instalar paquetes sin afectar el sistema.

### Instalar virtualenv

Asegurarse de que esté instalado pip

```sh
pip --version
```

Instalar virtualenv

```sh
pip install virtualenv
```

Actualizar pip

```sh
pip install --upgrade pip
```

### Crear un entorno virtual

Ver versiones disponibles de python

```sh
pyenv versions
```

Asegúrate de tener instalada la versión de python deseada

Por ejemplo:

```sh
pyenv install 3.12.10
```

Crear el entorno virtual con una determinada versión con pyenv

```sh
pyenv shell 3.12.10
python -m venv venvir
```

*Nota:* El comando "pyenv shell 3.12.10" establece la versión de Python 3.12.10 como la versión activa de Python para la sesión actual de terminal. Esto significa que cualquier comando python que ejecutes en esta terminal usará la versión 3.12.10 (si está instalada), sin afectar otras terminales o la configuración global de pyenv.

Crear un entorno virtual con la version por defecto de python o la versión global

```sh
python -m venv venv-dev
```

Crear entorno virtual con virtualenv con una version especifica python 

```sh
pyenv versions
virtualenv -p ~/.pyenv/versions/3.12.10/bin/python venv-dev
```

Tambien se puede crear un entorno virtual con la version global de python

```sh
virtualenv venv-dev
```

*Nota:* Igual usará el python de la versión global de pyenv.

*Nota:* Antes de crear entornos virtuales en Apple Silicon (ARM64) instalar lo siguiente:
Instalar herramientas de desarrollo

```sh
xcode-select --install
```

### Activar entorno virtual

Activar el entorno virtual

Asumiendo que el entorno se llama venv-dev y está en el directorio actual:

```sh
source venv-dev/bin/activate
python --version
```

### Desactivar entorno virtual

Desactivar un entorno virtual

```sh
deactivate
```

### Eliminar entorno virtual

Eliminar la carpeta del entorno virtual

```sh
deactivate
rm -rf venv
```

## Limpiar entornos virtuales

Limpiar el cache de entornos virtuales

```sh
unset VIRTUAL_ENV
hash -r
```

### Ver el entorno virtual activo

```sh
echo $VIRTUAL_ENV
```

## Mostrar el nombre del entorno virtual en el prompt de zsh (powerlevel10k)

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

Cerrar y volver a abrir terminal ó ejecutar los siguientes comandos

```sh
source ~/.p10k.zsh
source ~/.zshrc
reset
```

## Cuando usar python, pip y python3, pip3

Usa python3 y pip3 si:

* Estás trabajando con el Python 3 del sistema o de Homebrew.
* No tienes pyenv y quieres asegurarte de que estás ejecutando Python 3.

Ejemplo:

```sh
python3 -m venv venv
source venv/bin/activate
pip3 install numpy
```

Usa python y pip si:

* Estás en un entorno virtual (venv, virtualenv, Conda): ahí python y pip ya están correctamente redirigidos.

Resumen de uso de python, python3

| Comando |	Uso típico |
|---------|-------------------------------------------------------------|
| python  | Puede ser Python 2 o 3 (depende del sistema/configuración)  |
| python3 | Asegura que usas Python 3                                   |
| pip	  | Instala paquetes para python                                |
| pip3	  | Instala paquetes para python3                               |


## Ejecutar una aplicación Python de forma normal

```sh
python nombre_de_archivo.py
```
```sh
python main.py
```
Esto ejecuta el código una sola vez.

### Ejecutar una app Python con autoreload

Para autorecarga al guardar cambios, se tiene las siguientes opciones:

**⚙️ Opción A: Usar watchdog (universal y flexible)**

Instalar:
```sh
pip install watchdog
```
Ejecutar con:
```sh
watchmedo auto-restart --directory=. --pattern="*.py" --recursive -- python main.py
```
Esto observará todos los .py en el directorio y subdirectorios, y reiniciará la app cuando detecte cambios.

**⚙️ Opción B: Usar flask o fastapi con modo desarrollo (si es una app web)**

Flask:
```sh
export FLASK_APP=app.py
export FLASK_ENV=development
flask run
```
Esto activa el modo debug, que incluye auto-reload.

FastAPI (usando uvicorn):
```sh
pip install uvicorn
uvicorn app:app --reload
```
La opción --reload hace exactamente eso: reinicia la app al detectar cambios en los archivos.


## Instalar Jupyter Notebook y Jupyter Lab

### ✅ 1. Instalar Jupyter

🔸 Instalar dentro de un entorno virtual (recomendado)

Crea y activa un entorno virtual:

```sh
python -m venv venv
source venv/bin/activate  # en Mac/Linux
```

Instala jupyter y jupyterlab:

```sh
pip install jupyterlab notebook ipykernel
```

### 🚀 2. Ejecutar Jupyter Notebook

```sh
jupyter notebook
```
Esto abrirá automáticamente el navegador web en http://localhost:8888, con una interfaz clásica para crear y editar notebooks .ipynb.

### 🚀 3. Ejecutar JupyterLab

```sh
jupyter lab
```
Esto abrirá la nueva interfaz moderna y más potente de Jupyter en el navegador (también en http://localhost:8888 por defecto, pero con otra interfaz).

### 🛑 4. Detener Jupyter

Presiona Ctrl + C en la terminal donde se ejecuta. Confirmar con y si.

### 🔍 Verifica instalación
Para comprobar qué versión tienes instalada:

```sh
jupyter --version
```
*Nota:* Se recomienda usar extensiones de jupyter en visual studio para una mayor performance 



