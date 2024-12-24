# PYTHON

![Python](images/python.png)

Python es un lenguaje de programación ampliamente utilizado en las aplicaciones web, el desarrollo de software, la ciencia de datos y el machine learning (ML). Los desarrolladores utilizan Python porque es eficiente y fácil de aprender, además de que se puede ejecutar en muchas plataformas diferentes. El software Python se puede descargar gratis, se integra bien a todos los tipos de sistemas y aumenta la velocidad del desarrollo.

## Instalar Python en MacOs
Verificar la version de Python

    python3 --version

## Gestionar versiones de python con pyenv

Pyenv en es una herramienta que nos permite instalar diferentes versiones de Python y cambiar entre ellas según los requerimientos del proyecto con el cual necesitamos trabajar.

Instalar pyenv para gestionar las versiones de Python

    brew install pyenv

Añadimos lo siguiente a .bashrc o .zshrc

    # pyenv
    export PATH="$HOME/.pyenv/bin:$PATH"
    eval "$(pyenv init --path)"
    eval "$(pyenv virtualenv-init -)"

Añadir pyenv al Path de Mac:

    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc

Añadir Pyenv Init a tu terminal:

    echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
    echo 'eval "$(pyenv init -)"' >> ~/.zshrc

Reiniciar el shell

    source ~/.zshrc
    ó
    reset

Verificar y validar la instalación

    pyenv --version 
    pyenv -v
    
## Instalar diferentes versiones de Python

Ver un listado de todas las versiones de Python disponibles 

    pyenv install --list

Instalar la versión 3.6.0

    pyenv install -v 3.6.0

Iinstalar Python versión 3.10.2

    pyenv install -v 3.10.2 

Ver las versiones instaladas de python

     pyenv versions

Establecer una versión de Python por defecto de manera global (Bash o ZSH)

    pyenv global 3.10.2

Verificar la versión global de Python

    pyenv versions

Reiniciar la terminal

    reset
    source ~/.zshrc

Para comprobar la versión global ejecutamos el interprete de Python

    python3
    ctrl+Z

## Versiones locales de python

Pyenv es mucho más flexible y nos permite especificar una versión local para un directorio en específico.

Crear un proyecto local con python 3.10.2

    cd ~/CODE/python
    mkdir -p APISearchText
    cd APISearchText
    pyenv local 3.10.2 

Este último comando establece la versión 3.10.2 como la predeterminada en este directorio y todos sus hijos. 
Si listamos el directorio con el comando ls -la podemos ver el archivo .python-version el cual contiene la versión de Python especificada como local.

Ver las versiones de python

    pyenv versions


## Instalación de pip

Verificar si esta instalado pip

    python3 -m pip --version
    pip3 --version

En caso de no estar instalado PIP ejecutar el siguiente comando

    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py

Actualizar la version de pip

    python3 -m pip install --upgrade pip

## Entornos Virtuales para Desarrollo en Python con virtualenv

Actualizar pip

    pip install --upgrade pip 

Verificar librerias instaladas de manera global

    pip list

Si en la lista no aparece *virtualenv*, instalar

    pip install virtualenv  

Crear un entorno Virtual de Python

    cd project_folder
    virtualenv nombre_de_tu_entorno -p python3
    virtualenv venv -p python3
    virtualenv venv

Cambiar version de python del entorno virtual

    cd project_folder
    virtualenv -p python3.12 venv
   
Activar entorno virtual

    source ./venv/bin/activate 

Ver con que version de python se esta trabajando

    cd project_folder
    source ./venv/bin/activate
    python --version

Ver paquetes del entorno virtual

    pip list

Instalar paquetes en el entorno virtual segun lo requerido por el proyecto

    pip install fastapi
    pip install schedule
    ...

Exportar paquetes instalados en el entorno virtual

    pip freeze > requirements.txt  

Instalar paquetes exportados en entorno virtual

    pip install -r requirements.txt
    
Desactivar entorno virtual

    deactivate

Comando para mostrar el entorno virtual activo

    echo $VIRTUAL_ENV 

Ejecutar una app en python desde el entorno virtual

    env/bin/python main.py

Desde la terminal VS Code puede ejecutar 

    python main.py

Eliminar el virtual environment

Si ya no se necesita el virtualenv, se puede eliminar simplemente borrando la carpeta del proyecto

    deactivate
    rm -rf venv

## Crear un entorno virtual desde la terminal de Visual Studio Code

    # 1. Crear entorno virtual (si no existe)
    python -m venv venv

    # 2. Activar el entorno virtual
    # En Windows:
    # venv\Scripts\activate
    # En macOS/Linux:
    source venv/bin/activate

    # 3. Actualizar pip
    pip install --upgrade pip

    # 4. Instalar librerias por ejemplo: numpy 
    pip install numpy

    # 5. Ejecutar aplicación
    python main.py

## Ejecutar un programa Python en un entorno virtual con Visual Studio Code

    Cmd + Shift + P 
    Escribir "Python: Create Environment" y seleccionar la opción que aparece
    Seleccionar "Venv: Creates a '. venv' 
    Seleccionar la versión de Python a utilizar en el entorno virtual
    VS Code creará el entorno virtual y lo configurará automáticamente para el proyecto

## Elegir un entorno virtual con Visual Studio Code

    Cmd + P
        > Python Select Interpreter
            Select de workspace folder to set the interpreter (seleccionar la carpeta del proyecto)
                Seleccionar interprete ( elegir python del area de trabajo)

## Abrir Terminal Integrado al entorno virtual en Visual Studio Code

    Cmd + P
        > Terminal: Create New Terminal starting in a Custom Working Directory (seleccionar)

**NOTA:** Para trabajar con entornos virtuales activar entorno virtual en el entorno VS Code y en su terminal

## Compilar proyectos python desde Visual Studio Code

    Abrir Visual Studio Code
    Cmd + Shift + P
    Python: Seleccionar Interprete
    -> Elegir la version de python
    ó
    -> Seleccionar en el nivel de área de trabajo

    python --version

## Mostrar estado de virtualenv en el prompt de zsh

Editar el archivo de configuración .zshrc

    nvim ~/.zshrc

Editar las las siguientes lineas

    plugins=(virtualenv)
    POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status command_execution_time root_indicator background_jobs time virtualenv) 

Cerrar y volver a abrir terminal

    source ~/.zshrc

## Instalar Jupyter Notebook (opcional)

Instalar Jupiter Notebook

```sh
pip3 install notebook
```

*Abrir aplicacion Jupyter Notebook*

```sh
jupyter notebook
```

## Instalar Jupyter Lab (opcional)

Para Instalar Jupiter Lab se debe primero instalar PIP

```sh
pip install jupyterlab
```

*Ejecutar Jupyter Lab*

```sh
jupyter lab
```

## Desinstalar Jupyter en MacOs

Desinstala Jupyter utilizando pip: Ejecuta los siguientes comandos para desinstalar Jupyter y sus componentes:

    pip uninstall jupyter
    pip uninstall jupyterlab
    pip uninstall notebook
    pip uninstall nbconvert
    pip uninstall nbformat
    pip uninstall jupyter-console
    pip uninstall ipykernel
    pip uninstall ipywidgets

Verifica que todo se ha desinstalado: Puedes verificar si Jupyter ha sido completamente desinstalado ejecutando:

    jupyter --version

Si muestra un error indicando que jupyter no está instalado, entonces la desinstalación fue exitosa.

* Limpiar Archivos Residuos

Para asegurarte de que no quedan archivos residuales, puedes eliminar las configuraciones y cachés de Jupyter:

Eliminar configuraciones y caché:

    rm -rf ~/.jupyter
    rm -rf ~/Library/Jupyter

Eliminar kernels y extensiones (si tienes configuraciones personalizadas):

    rm -rf ~/Library/Application\ Support/jupyter


* (Opcional) Desinstalar Anaconda o Miniconda

Si instalaste Jupyter a través de Anaconda o Miniconda y deseas eliminar todo el entorno, sigue estos pasos:

Desinstala Anaconda/Miniconda:

    rm -rf ~/anaconda3
    rm -rf ~/miniconda3

Eliminar referencias de Anaconda/Miniconda de tu shell: Edita tu archivo de configuración de shell (~/.bash_profile, ~/.zshrc, etc.) y elimina las líneas relacionadas con Anaconda o Miniconda.

Eliminar caché y archivos residuales de Anaconda:

    rm -rf ~/.conda
    rm -rf ~/.continuum


Estos pasos eliminarán Jupyter, Jupyter Notebook y todos los archivos asociados de tu macOS. Si necesitas ayuda adicional, no dudes en preguntar.


## IDE spyder para python

*Instalar Spyder IDE para python*

https://www.spyder-ide.org/


adicionar terminal al IDE Spyder

    pip install spyder-terminal





  

