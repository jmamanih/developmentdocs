# ANDROID DESDE CERO

* Fuente: [MoureDev, Tutorial Android](https://www.youtube.com/watch?v=BQaxPwZWboA&t=659s)
* Recursos Android: [Android para desarrolladores](https://developer.android.com)

## Iniciar una aplicación Android

1. Instalar entorno de desarrollo [Android Studio](https://developer.android.com/studio)
2. Elegir crear una nueva aplicación (New Project)
3. Elegir el dispositivo (Phone and Tabled)
4. Elegir la plantilla (Empty Activity)
5. Configurar el proyecto
```sh
Name: Titulo de la Aplicación
Ej.   Initial Aplication Android Kotlin

Package name: dominio.empresa.nombre_app
Ej.   com.unisoft.initapp

Save Location: Directorio de la aplicación
Ej.   /Users/juanfer/Development/Aplications/Android/InitApp

Languaje: Lenguaje de programación
Ej.   Kotlin

Minimum SDK: Soporte minimo de version de Android
Ej.  API 21: Android 5.0
```
6. Botón Finish
7. Personalizar Colores en Android Studio.
=> Preferences Menu -> Plugins, buscar Monokai Materialized Color Scheme, Install
=> Preferences Menu -> Editor > Color Scheme, Monokai Materialized
8. Ejecutar la aplicación presionando sobre el boton "RUN App"
```
Error running 'app'
No target device found
```
Este mensaje sale porque no se selecciono el dispositivo de salida

Ir a la opcion [No Devices] -> Device Manager, Create Virtual Device -> Phone, Pixel 3a (Play Store), Next

Seleccionar la versión de Android (Q Android 10), Finish, Next, Startup orientation: Portrait, Finish 

9. Run

## Estructura de Archivos Android 

* En el panel de visualización del Proyecto elegir "Android"
```
> app
  > manifest
    AndroidManifest.xml     (configuración principal de la app, pantallas y nombre de la app)
> java
  > com.unisoft.initapp
    MainActivity            (archivo correspondiente a la primera pantalla de la app)

A todo archivo Activity se le asocia un archivo Layout

> res
  > layout
    activity_main.xml       (vista de la primera pantalla)

En Gradle Scripts se encuentran los archivos de construcción de la app

> Gradle Scripts
  build.gradle (module:)    (esta la version de la app, librerias)
```
## Lenguaje de programación Kotlin

* Fuente: [Tutorial Kotlin](https://www.youtube.com/watch?v=-xRWR_TVa28&list=PL8ie04dqq7_OcBYDpvHrcSFVoggLi3cm_)
* Documentación [Guía de Kotlin](https://www.develou.com/guia-de-kotlin/)
* Recurso: [Compilador Kotlin en Linea](https://play.kotlinlang.org/)
 
*Kotlin es un lenguaje mas moderno que Java y se convertira en un standard a la hora de crear aplicaciones.*

1. Variables

```kt
// NUMERICOS
var tipovariable1: byte = 1      // Byte 
var tipovariable2: short = 25    // Short 
var tipovariable3: int = 8      // Integer  
var tipovariable4: long = 1000000008 // Long 
var tipovariable5: float = 96.00f // Float  
var tipovariable6: double = 36.00 // Double  

// CARACTERES
var primeraLetraPostre: Char = 'T' // Con una letra 
var primerNumeroStock: Char = '3' // Con un dígito 

// CADENA DE CARACTERES
var tipoString: String = "Cadena de Caracteres"  // String 

// BOOLEANOS
var stockagotado: Boolean = true   // Verdadero
var stockagotado: Boolean = false  // Falso

// ARREGLOS
var edades = arrayOf(14, 17, 20, 24, 27)
var postres = arrayOf("Torta de Chocolate", "Gelatina de Fresa", "Pie de Manzana", "Crema Volteada")
var primerNombrePostre = arrayOf('T', 'G', 'P', 'C')
var datos = arrayOfNulls<String>(7)    // Siete elementos nulos
var array = intArrayOf(1, 2, 3, 4, 5)  // elementos de tipo entero
var n = edades.size    // n = 5, cinco elementos
var d = edades.get(3)  // d = 20, tercer elemento
edades.set(1) = 10     // edades = (10, 17, 20, 27), se asigna el valor de 10 al primer elemento

// Se puede definir el tipo de variable asignandole el tipo de dato o valor
var edad = 35
var existe = true
var nombre = "Juan Perez"

```

**Convertir un de Tipo de variable a Otro**

```kt
/*
toByte(): Byte
toShort(): Short
toInt(): Int
toLong(): Long
toFloat(): Float
toDouble(): Double
toChar(): Char
*/
var datodetipobyte: Byte = 1
var datodetipointeger: Int = datodetipobyte.toInt() 
```

2. Constantes
```kt
val pi = 3.1416   // se usa la palabra reservada val
```

3. Comentarios
```kt
//  Para una sola lines
/*
  Para varias
  lineas
*/
```
4. 


