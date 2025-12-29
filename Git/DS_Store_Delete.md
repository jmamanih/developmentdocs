# Evitar que se guarde los archivos .DS_Store en los repositorios

Para evitar que todos los archivos .DS_Store (archivos ocultos generados por macOS) se guarden en el repositorio de Git, se deben seguir los siguientes pasos:


✅ Paso 1: Agrega .DS_Store al archivo .gitignore
Abre (o crea si no existe) el archivo .gitignore en la raíz de tu repositorio y añade esta línea:

```sh
.DS_Store
```

Esto le indica a Git que ignore todos los archivos con ese nombre, sin importar en qué carpeta estén.

✅ Paso 2: Elimina .DS_Store del control de versiones si ya fue añadido
Si el archivo .DS_Store ya fue añadido al repositorio en commits anteriores, debes eliminarlo del historial y del área de staging:

```bash
git rm --cached -r .DS_Store
```

Después haz un commit:

```bash
git commit -m "Remove .DS_Store files from repository"
```

Eliminar los archivos .DS_Store de la carpeta proyecto

Buscar manualmente archivos .DS_Store:

```bash
find . -name .DS_Store
```

Si existen simplemente eliminarlos con:

```bash
find . -name .DS_Store -delete
```

Esto es útil si quieres limpiar tu proyecto completamente de estos archivos, aunque no estén rastreados por Git.

✅ (Opcional) Paso 3: Evita que se creen .DS_Store globalmente (en tu máquina)
Si quieres evitar que se agreguen en todos tus proyectos en tu máquina, puedes configurarlo globalmente con:

```bash
echo .DS_Store >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```



