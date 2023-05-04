# HERRAMIENTAS DE HARDWARE

## Crear USB Booteable

### Ventoy

[Ventoy](https://www.ventoy.net). 

Ventoy es una herramienta de código abierto para crear una unidad USB de arranque para archivos ISO/WIM/IMG/VHD(x)/EFI.
Con ventoy, no necesita formatear el disco una y otra vez, solo necesita copiar los archivos ISO/WIM/IMG/VHD(x)/EFI a la unidad USB y arrancarlos directamente.
Puede copiar muchos archivos a la vez y ventoy le dará un menú de inicio para seleccionarlos

1. descargar el instalador de ventoy version para windows [ventoy](https://www.ventoy.net/en/download.html)
2. Conectar Dispositivo USB minimo de 16 GB
3. Lanzar el ejecutable Ventoy2Disk.exe
```
    Language: Seleccionar Lenguaje Español
    Opcion: Estilo de partición MBR

    Seleccionar el dispositivo USB
    Boton Instalar
    Boton SI

    La opcion ACTUALIZAR solo mejora la version no afecta a los archivos iso cargados en el USB 
```
4. Copiar los archivos ISO instaladores de Sistemas Operativos al USB

**Personalizar Menu de Arranque de Ventoy**
https://www.youtube.com/watch?v=HdA8aqULN0I
1. Ir al Sitio [Gnome Look](https://www.gnome-look.org/browse?ord=latest)
2. Elegir un tema, Dowload
3. Descomprimir el archivo
4. Copiar la carpeta ventoy a la raiz del USB

En el caso de que el plugin no contenga la carpeta ventoy se debe crear la estructura
* Crear estructura de carpetas y archivos
```
/ventoy
    /themes
    ventoy.json
```
* Copiar dentro de /themes los archivos descargados
* Editar el ventoy.json
```json
{
    "control": [
        { "VTOY_DEFAULT_MENU_MODE": "1" },
        { "VTOY_FILT_DOT_UNDERSCORE_FILE": "1" }
    ],
    
    "theme": {
        "file": "/ventoy/theme/blur/theme.txt",
        "gfxmode": "1920x1080"
    }
}
```
* En File cambiar el nombre del thema y asegurarse de la ruta
5. Se puede personalizar la imagen de fondo background.png con photoshop
6. Se puede personalizar los mensajes editanto el archivo **theme.txt**


## Virtualizadores

### MobaLiveCD

[MobaLiveCD](https://www.mobatek.net/labs.html)

MobaLiveCD es un programa gratuito que ejecutará su Linux LiveCD en Windows gracias al excelente emulador llamado "Qemu". MobaLiveCD le permite probar su LiveCD con un solo clic: después de descargar el archivo de imagen ISO de su LiveCD favorito, solo tiene que iniciarlo en MobaLiveCD y aquí está, sin necesidad de grabar un CD-Rom o reiniciar su computadora

1. Descargar la aplicación [MobaliveCD](https://www.mobatek.net/labs.html)
2. Ejecutar la aplicación
```
    Ejecute el Live USB
```
