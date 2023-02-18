# MARKDOWN

**Definición**

Markdown es un lenguaje de marcado que facilita la aplicación de formato a un texto empleando una serie de caracteres de una forma especial. En principio, fue pensado para elaborar textos cuyo destino iba a ser la web con más rapidez y sencillez que si estuviésemos empleando directamente HTML. Y si bien ese suele ser el mejor uso que podemos darle, también podemos emplearlo para cualquier tipo de texto, independientemente de cual vaya a ser su destino.

Fuente: "John Gruber":http://daringfireball.net/projects/markdown/, uno de sus creadores.

**Filosofia**

Markdown pretende ser tan fácil de leer y fácil de escribir como sea posible.

La facilidad de lectura, sin embargo, predomina sobre todo lo demás. Un documento con formato Markdown debería ser publicable como es, como texto plano, sin parecer que ha sido mejorado con etiquetas o intrucciones de formato. Aun cuando la sintaxis de Markdown ha sido influenciada por varios filtros conversores de texto a HTML existentes  incluyendo Setext, atx, Textile, reStructuredText, Grutatext, y EtText  la mayor fuente de inspiración para la sintaxis de Markdown es el formato de texto plano de email.

**Enlaces de Interes**

* [Conversor de Markdown a HTML](https://daringfireball.net/projects/markdown/dingus "Conversor")



# ENCABEZADOS

Markdown admite dos estilos de encabezados, Setext y atx.

Los encabezados de estilo de texto están "subrayados" usando signos de igual (para encabezados de primer nivel) y guiones (para encabezados de segundo nivel). Por ejemplo:

This is an H1
=============

This is an H2
-------------

Los encabezados de estilo Atx usan 1-6 caracteres hash al comienzo de la línea, correspondientes a los niveles de encabezado 1-6. Por ejemplo:

# This is an H1

## This is an H2

###### This is an H6

Opcionalmente, puede "cerrar" los encabezados de estilo atx. El número de hashes de apertura determina el nivel del encabezado.

# This is an H1 #

## This is an H2 ##

### This is an H3 ######


# FORMATO

Markdown trata los asteriscos (*) y los guiones bajos () como indicadores de énfasis. 

*cursiva*

_cursiva_

**negrilla**

__negrilla__

~~texto tachado~~ 



# CITAS EN BLOQUE

Markdown utiliza caracteres de estilo de correo electrónico > para comillas en bloque. 

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

Las citas en bloque pueden contener otros elementos de Markdown, incluidos encabezados, listas y bloques de código:

> ## This is a header.
> 
> 1.   This is the first list item.
> 2.   This is the second list item.
> 
> > Here's some example code.
> > Here's some example.
> 
>     return shell_exec("echo $input | $markdown_script");

# LISTAS

Markdown admite listas ordenadas (numeradas) y no ordenadas (con viñetas *, +, -).

Las listas desordenadas utilizan asteriscos, más y guiones - de manera intercambiable - como marcadores de lista:

*   Red
*   Green
*   Blue

1. Uno
2. Dos
3. Tres

# REGLAS HORIZONTALES

Puede producir una etiqueta de regla horizontal (<hr />) colocando tres o más guiones, asteriscos o guiones bajos en una línea por sí mismos. Si lo desea, puede usar espacios entre los guiones o asteriscos. Cada una de las siguientes líneas producirá una regla horizontal:

* * * * * * 

***

*****

- - -

---------------------------------------

# IMÁGENES

Markdown utiliza una sintaxis de imagen que pretende parecerse a la sintaxis de los enlaces, lo que permite dos estilos: en línea y de referencia.

La sintaxis de la imagen en línea se ve así:


![example 1](images/github.png)

**Imágen con mensaje descriptivo**

![example 2](images/markdown.png "Optional title")


**Imágen con vinculo**

[![Imagen que es un vinculo](images/code.png)](https://code.visualstudio.com/)


# TABLAS

* |          separador de celdas
* :--------  alinear a la izquierda
* :--------: centreado
* ---------: alinear a la derecha

*Ejemplo:*

| ID Centreado         |       Descripción del Item    | Costo en Sus |
|:------:|:-------------|---------:| 
| 1    | alineada a la izquierda | $1600 |

# ENLACES

Markdown admite dos estilos de enlaces: en línea y de referencia.

Ejemplo: 

This is [an example](http://example.com/ "Title") inline link.

__Enlaces con mensaje descriptivo__

[Con titulo](http://joedicastro.com "titulo descriptivo")


1. **Menu de Enlaces**

* [Enlace 1][1]
* [Enlace 2][2]
* [Enlace 3][3]

 [1]: https://github.com/
 [2]: https://github.com/ "Título 2"
 [3]: https://github.com/ "Título 3"

2. **Menu de Enlaces Internos**

<a id="top"></a>

**TITULO DEL DOCUMENTO**
 
## Índice de contenidos
* [Contenido 1](#item1 "contenido 1")
* [Contenido 2](#item2 "contenido 2")
* [Contenido 3](#item3 "contenido 3")
 
Lorem ipsum dolor
 
<a id="item1"></a>
### Contenido 1
 
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
 
[Subir](#top)
 
<a id="item2"></a>
### Contenido 2
 
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
 
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
 
[Subir](#top)
 
<a id="item3"></a>
### Contenido 3
 
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
 
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
 
[Subir](#top)
 

3. **Enlaces Automáticos para URL**

Existe una manera adicional de crear enlaces automáticos para direcciones URL, simplemente encerrarla entre los caracteres menor < que y mayor que >

<https://github.com/>

# NOTAS DE PIE

Esto es un texto con nota al pie [^nota1] y esta es otra nota [^nota2]

[^nota1]: Esto es una nota al pie de página.
[^nota2]: Esto es la segunda nota al pie.

# ESCAPE DE BARRA INVERTIDA

Markdown le permite usar escapes de barra invertida para generar caracteres literales que de otro modo tendrían un significado especial en la sintaxis de formato de Markdown. Por ejemplo, si desea rodear una palabra con asteriscos literales (en lugar de una etiqueta HTML <em>), puede usar barras invertidas antes de los asteriscos, de esta manera:

\*literal asterisks\*

Markdown proporciona escapes de barra invertida para los siguientes caracteres:

<pre>
\   barra invertida
`   retroceso
*   asterisco
_   guion bajo
{}  llaves
[]  corchetes
()  paréntesis
#   símbolo de hash
+   signo más
-   signo menos (guión)
.   punto
!   signo de exclamación
</pre>

# BLOQUES DE CODIGO

Los bloques de código (```) formateados previamente se utilizan para escribir sobre código fuente de programación o marcado. En lugar de formar párrafos normales, las líneas de un bloque de código se interpretan literalmente. 

Python
```python
import lifetime

for each_day in lifetime.days():
    carpe_diem()
```

Configuración Apache
```apache

    <VirtualHost *:80>
    DocumentRoot /www/example1
    ServerName www.example1.com

    # Other directives here

    </VirtualHost>
```

Bash y console - Bash y Shell  
```sh
     #!/bin/bash
     echo "Hola mundo"

    bat - Fichero Batch DOS/Windows

    @echo ¡Hola, Mundo!
```

cpp - C++
```cpp
    #include <iostream.h>
    using namespace std;

    int main() {
      cout << "¡Hola, mundo!" << endl;
      return 0;
    }

    csharp - C

    using System;

    class MainClass
    {
        public static void Main()
        {
            System.Console.WriteLine("¡Hola, mundo!");
        }
    }
```

css - Cascade Style Sheet (CSS)
```css
    </pre>
       </td>
       <td class="get">
    <css>
    body {
        font: 75% georgia, sans-serif;
        color: #555753;
        background: #fff;
        margin: 0;
        padding: 5px;
    }
```

diff ó udiff - Diff
```diff
    --- /path/to/original ''timestamp''
    +++ /path/to/new      ''timestamp''
    @@ -1,3 +1,9 @@
    +This is an important
    +notice! It should
    +therefore be located at
    +the beginning of this
    +document!
    +
     This part of the
     document has stayed the
     same from version to

    erlang - Erlang

    -module (hola).
    -export([hola_mundo/0]).

    hola_mundo() -> io:fwrite("Hola mundo!\n").
```

go - Go
```go
package main

    import "fmt"

    func main() {
       fmt.Println("Hello World!")
    }

    haskell - Haskell

    holaMundo :: IO ()
    holaMundo = putStrLn "Hola mundo!"
```

html - HTML
```html
    <html>
      <head>
        <title>Hola Mundo</title>
      </head>
      <body>

    ¡Hola Mundo!
       </body>
    </html>
```

java - Java
```java
    public class HolaMundo {
           public static void main(String[] args) {
              System.out.println("¡Hola, mundo!");
           }
    }
```

js - javascript
```js
    <script type="text/javascript">
      document.write("¡Hola, mundo!");
    </script>
```

latex - LaTeX
```latex
    \documentclass[12pt]{article}
    \usepackage{lingmacros}
    \usepackage{tree-dvips}
    \begin{document}

    \section*{Notes for My Paper}
```

cl - Common Lisp
```cl
    (format t "¡Hola, mundo!")

    lua - Lua

    print("¡Hola, Mundo!\n")
```

mysql - MySQL
```mysql
    SELECT 'HOLA MUNDO';

    pascal y delphi - Pascal y Delphi

    Program HolaMundo;
    Begin
        Write('¡Hola, Mundo!');
    End.
```

perl - Perl
```perl
    print "Hola, mundo\n"
```

php - PHP
```php
    <?php print "Hola Mundo!"; ?>

    python ó py ó pycon ó pytb ó python3 ó cython - Python

    print "¡Hola Mundo!"

    ruby - Ruby

    puts "Hola Mundo"

    scala - Scala

    object HelloWorld extends Application {
      println("Hello world!")
    }
```

scheme - Scheme
```scheme

    (display "Hello World")

    smalltalk - Smalltalk

    Transcript show: '¡Hola, mundo!'
```
    
sql - SQL
```sql
    SELECT 'HOLA MUNDO'
    FROM DUAL;

    sqlite3 - sqlite3

    sqlite> CREATE TABLE tbl2 (
       ...>   f1 varchar(30) primary key,
       ...>   f2 text,
       ...>   f3 real
       ...> );
    sqlite>
```

text - Texto simple monoespaciado
```text
   Hola Mundo
```

vala - Vala
```vala
    class Demo.HelloWorld : GLib.Object {
        public static int main(string[] args) {
            stdout.printf("Hello, World\n");
            return 0;
        }
    }
```

vbnet - Visual Basic .NET
```vbnet
    Private Sub Form_Load()
       Msgbox "Hola Mundo"
     End Sub
```

vim - Vim Script
```vim
    function! ToggleSyntax()
       if exists("g:syntax_on")
          syntax off
       else
          syntax enable
       endif
    endfunction

    nmap <silent>  ;s  :call ToggleSyntax()<CR>
```

xml - XML
```xml
    <?xml version="1.0" encoding="ISO-8859-1"?>
     - <note>
           <to>Tove</to>
           <from>Jani</from>
           <heading>Reminder</heading>
           <body>Don't forget me this weekend!</body>
       </note>
```
