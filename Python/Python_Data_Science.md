# PYTHON FOR DATA SCIENCE
![Python](images/python-data-science.jpg)
La ciencia de datos es un área enfocada en la extracción de conocimiento a partir de conjuntos de datos con diversas fuentes y formas. El conocimiento adquirido es generado por diversas técnicas derivadas de estadística, minería de datos, aprendizaje automático. 
Python es un lenguaje de propósito general y es usado para aplicar los métodos de ciencias de datos gracias a la gran cantidad de librerías disponibles y la enorme comunidad que las soporta.

## Google Colab

Colab, también conocido como "Colaboratory", te permite programar y ejecutar Python en tu navegador con las siguientes ventajas:

    No requiere configuración
    Acceso a GPUs sin coste adicional
    Permite compartir contenido fácilmente

### Crear un nuevo archivo Colab

    Abrir Colab
    Iniciar Session con cuenta de correo gmail
    Menu Archivo, Nuevo Cuaderno, asignar nombre de archivo

### Establecer Entorno de Ejecución

    Menu Entorno de Ejecución
    Cambiar tipo de Entorno de Ejecución
    Elegir Tipo de Entorno: Python 2 / Python 3
    Elegir Acelerador por Hardware: CPU / GPU / TPU

**TPU**. Tensor Processing Unit" (TPU), son un hardware diseñado específicamente para resolver cierto tipo de operaciones muy frecuentes en procesos de machine learning, incluyendo el entrenamiento de los modelos o incluso la propia inferencia.

**GPU**. Graphics Processing Unit (GPU),se diseñaron y utilizaron originalmente para gráficos 3D para acelerar cosas como la renderización de video, pero con el tiempo, su capacidad de computación paralela las convirtió en una opción extremadamente popular para su uso en IA.

### Habilitar acceso a carpetas de Google Drive

#### Montar drive
* Opcion Montar Drive
* ¿Permitir que este cuaderno acceda a tus archivos de Google Drive?
  No Gracias
* Ejecutar Codigo (el codigo se copia automaticamente)
```python
from google.colab import drive
drive.mount('/content/drive')
```
* Elegir cuenta google al cual se quiere acceder
* Permitir

#### Desmontar drive
* Desmontar carpeta de Google Drive
```python
from google.colab import drive
drive.flush_and_unmount()
```
* Para Copiar ruta un archivo, clic derecho sobre el archivo y opcion copiar ruta

### Subir archivos temporalmente
* Opcion subir archivo
* Elegir archivo a subir
* Subir

El archivo se subirá temporalmente

### Comandos Linux para Archivos
Listar archivos con permisos y ocultos
```sh
ls -la  							
```
Copiar  archivos
```sh
cp /usr/local/tomcat/*  /home/admin
cp -ru /usr/compartido/fonts/* /usr/share/fonts
```
Los parametros -ru copiar con directorios y sobrescribiendo

Renombrar o mover archivos
```sh
mv archivo.dat nombredat
```
Crear directorio o carpeta
```sh
mkdir directorio
```
Eliminar directorio
```sh
rm -dfr /carpeta
```
Descomprimir un archivo
```sh
unzip flower_data.zip
```
Descomprimir en una carpeta
```sh
mkdir -p /tmp/unziped
unzip tecmint_files.zip -d /tmp/unziped
ls -l /tmp/unziped/
```
Descarga e archivo individual
```sh
wget https://wordpress.org/latest.zip
```
Descargar con otro nombres
```sh
wget -O wordpress-install.zip https://wordpress.org/latest.zip
```
Descargar en carpeta especifica
```sh
wget -P documents/archives/ https://wordpress.org/latest.zip
```

*NOTA*: Para ejecutar como comando linux en Colab se debe anteponer el simbolo ! al comando.

