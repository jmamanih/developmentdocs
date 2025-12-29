# RESUMEN DE COMANDOS PYTHON

*Resumen de comandos para administrar un proyecto Python en un entorno MacOs Arm*

## 1. Instalar el administrador de versiones de python con pyenv

```sh
pyenv -v                      # ver la version de pyenv
brew install pyenv            # instalar pyenv si no esta

# Configurar pyenv en el shell
# para Zsh editar ~/.zshrc, y 
# para Bash: editar ~/.bash_profile o ~/.bashrc
# Agrega estas líneas
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
# Reiniciar el shell o la terminal 
source ~/.zshrc
```

## 2. Instalar Python

```sh
pyenv install --list          # listar versiones disponibles de python (no debe tener extensiones como "dev", "rc", etc)
pyenv install 3.12.3          # instala una version especifica de python
pyenv versions                # hace un listado de versiones disponibles en sistema
pyenv global 3.12.3           # establece la version global de python
pyenv local 3.12.3            # establece la version local de python para un proyecto especifico
python --version              # obtiene la version de python ya sea global o local (con entorno virtual activado)
```

## 3. Verificar si esta instalado pip

```sh
python -m pip --version.              # Verificar
python -m ensurepip --upgrade.        # Instalar / actualizar
python -m pip install --upgrade pip
```

## 4. Instalar virtualenv

```sh
pip install --upgrade pip
pip install virtualenv
virtualenv --version          # version de virtualenv
```

## 5. Crear un entorno virtual de python con la version global (virtualenv)

```sh
virtualenv venv               # crear entorno virtual
# estructura del proyecto luego de crear el entorno virtual
mi_proyecto/                 
├── venv/
└── ...
```

## 6. Crear un entorno virtual de python manera local con una version especifica 

```sh
cd proyecto_python
pyenv versions                # obtiene las versiones instaladas de python
pyenv local 3.11.8            # se instala la version de python en .python-version
virtualenv venv
# estructura del proyecto
proyecto_python/
├── venv/
├── .python-version
```

## 7. Activar entorno virtual

```sh
source venv/bin/activate
```

## 8. Desactivar entorno virtual

```sh
deactivate
```

## 9. Ver el entorno virtual activo
  
```sh
echo $VIRTUAL_ENV
```

## 10. Eliminar un entorno virtual

```sh
deactivate
rm -rf venv               
unset VIRTUAL_ENV               # limpia entornos virtuales  
hash -r
```

## 11. Administrar paquetes ya sea de forma global o en entornos virtuales activados

```sh  
pip install --upgrade pip       # actualiza la version de pip                      
pip list                        # obtiene el listado de paquetes instalados
pip list | grep -i pandas       # buscar un paquete instalado
pip install fastapi             # instalar paquete (Ej. fastapi)
pip freeze > requirements.txt   # guardar dependencias 
pip install -r requirements.txt # instalar paquetes desde requirements
```

## 12. Instalar dependencias dentro del entorno virtual

```sh
source venv/bin/activate
pip install numpy pandas flask
```

## 13. Flujo recomendado de trabajo

```sh
cd mi_proyecto
source venv/bin/activate
code .                        # abre visual studio code  
deactivate
```

## 14. Seleccionar el intérprete Python con Visual Studio Code

```sh
Cmd + Shift + P
Buscar → Python: Select Interpreter
Elegir:
    ./venv/bin/python
```
VS Code detectará automáticamente el entorno virtual.

## 15. Estructura recomendada de un proyecto python

Estructa del proyecto

```sh
mi_proyecto/
│── venv/
│── src/
│   └── main.py
│── requirements.txt
│── .gitignore
```
.gitignore:

```sh
venv/
__pycache__/
*.pyc
```
  

