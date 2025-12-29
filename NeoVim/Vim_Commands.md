# Comandos Vim

## **_Diferentes modos de Vim_**

**Modo Normal**. Éste es el modo central, desde el que se cambia a los otros modos, Se activa pulsando la tecla ESC. 

**Modo insertar**. Es el modo en el que podemos introducir texto. Se puede entrar a este modo desde el modo normal pulsando la tecla i. 

**Modo de comandos**. Se accede pulsando :  Permite introducir diferentes comandos, como buscar y reemplazar con expresiones regulares. También podremos personalizar aspectos de Vim.

**Modo visual**. Se entra pulsando la tecla v. Es como seleccionar texto con el cursor, solo que podremos escribir comandos para manipularlo.

**Modo selección**. Se entra desde el modo visual pulsando Ctrl-G. Tiene un comportamiento similar al modo visual solo que al escribir no realizaremos comandos sino que reemplazaremos el texto, como en un editor de texto normal,

**Modo Ex**. Este modo se asemeja al modo de comandos, con la diferencia de que tras la ejecución de una orden no se vuelve al modo normal. Se entra pulsando Q y se sale con vi.

# Vi Commands

Text Entry Commands

```
a       Append text following current cursor position
A       Append text to the end of current line
i       Insert text before the current cursor position
I       Insert text at the beginning of the cursor line
o       Open up a new line following the current line and add text there
O       Open up a new line in front of the current line and add text there
```

Cursor Movement Commands

```
h       Moves the cursor one character to the left
l       Moves the cursor one character to the right
k       Moves the cursor up one line
j       Moves the cursor down one line

nG or :n    Cursor goes to the specified (n) line 
            (ex. 10G goes to line 10) or 
            (:5 goes to line 5)

CTRl F       Forward screenful
CTRl B       Backward screenful
CTRl f       One page forward
CTRl b       One page backward

CTRl u      Up half screenful
CTRl d      Down half screenful

$   Move cursor to the end of current line
0   (zero) Move cursor to the beginning of current line

w   Forward one word
b   Backward one word
```

Text Deletion Commands

```
x       Delete character
dw      Delete word from cursor on
db      Delete word backward
dd      Delete line

d$      Delete to end of line
d0      Delete to beginning of line
```

Copy/Paste Commands

Yank (has most of the options of delete)--VI's copy commmand
```
yy      yank current line
y$      yank to end of current line from cursor
yw      yank from cursor to end of current word
5yy     yank, for example, 5 lines
```
Paste (used after delete or yank to recover lines.)
```
p       paste below cursor
P       paste above cursor
"2p     paste from buffer 2 (there are 9)
````

```
v       mode VISUAL, select text
y       to copy
d       to cut
p       to paste after cursor
P       to paste befor cursor  
```

Undo commands

```
u       Undo last change
U       Restore line
```

Search and Substitution Commands

```
:/      pattern Search forward for the pattern
:?      pattern Search backward for the pattern
n       used after either of the 2 search commands above to
        continue to find next occurrence of the pattern.

:/search-text   

:%s/source-text/target-text/gc   

        %               Will be searched from the first to the last line of the document.
        source-text     It is the term we will replace.
        target-text     It is the term we will apply instead.
        g               The substitution will be made with every search match.(Indica que la sustitución se realizará con toda coincidencia de búsqueda.)
        c               It will request confirmation of substitution every time the word to be found is found.

        Opciones de Confirmación de sustitución:

        y   Confirmamos la acción 
        n   Saltamos esta coincidencia con la búsqueda sin sustituirla y pasamos a la siguiente 
        a   Confirmamos la acción para esta y todas las siguientes coincidencias 
        q   Dejamos de sustituir en la búsqueda 
        l   Confirmamos la sustitución y paramos la búsqueda saliendo de nuevo al modo editor 
        Ctrl+e  Avanzamos un poco hacia abajo en el documento para localizar el contexto de la coincidencia 
        Ctrl+y  Retrocedemos un poco en el texto para localizar el contexto de la coincidencia.
```

Exit Commands

```
:wq     Write file to disk and quit the editor
:q!     Quit (no warning)
:q      Quit (a warning is printed if a modified file has not been saved)

:qa!    Quit force all tabs
:wqa!   Quit and Save all tabs

ZZ      Save workspace and quit the editor (same as :wq)

: 10,25 w temp.txt  Write lines 10 through 25 into file
                    named temp. Of course, other line
                    numbers can be used. (Use :f to find
                    out the line numbers you want.
```

File Manipulation Commands

```
:w              Write workspace to original file
:w file-name    Write workspace to named file
:e              file Start editing a new file
:r              file Read contents of a file to the workspace

:tabnew file-name       Open file in new tab

```

Other Useful Commands

```
J       Join next line down to the end of the current line
@:      Repeat last command
cw      Change current word to a new word
r       Replace one character at the cursor position
R       Begin overstrike or replace mode ? use ESC key to exit
```

**Uso del modo visual**


    v       Cambiar a modo Visual y selecionar texto
    ctrl+v  seleccionar bloque

    0       marcar selección al inicio de linea
    $       marcar selección al final de linea

Comandos sobre el texto seleccionado

    u     Cambiar texto a Minusculas
    U     Cambiar texto a Mayusculas
    >     Indentar a la derecha
    <     Indentar a la izquierda