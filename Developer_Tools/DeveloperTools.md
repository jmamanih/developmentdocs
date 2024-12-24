# Herramientas de Desarrollo

## dbdiagram.io

Dibuja diagramas entidad-relación 😎.

Una herramienta sencilla y gratuita para dibujar diagramas ER con solo escribir código.
Diseñado para desarrolladores y analistas de datos.

Aplicación Online: [dbdiagram.io](https://dbdiagram.io)

    
## drawio.com

Draw.io es una herramienta de diagramación, de diagrama de flujo, de proceso, entre otras muchas funciones. Es una herramienta gratuita con la que se puede dibujar cualquier tipo de mapas mentales, mapas conceptuales, esquemas o diferentes representaciones gráficas, como diagrama de jerarquía o conjuntos.

Aplicación Online:  [drawio.com](https://www.drawio.com/)

Se puede también descargar la aplicación [Drawio](https://github.com/jgraph/drawio-desktop/releases/tag/v25.0.2)

## Visual Paradigm Community Edition

Visual Paradigm es una herramienta de software que ayuda a los equipos de desarrollo de software a modelar sistemas de información empresarial y administrar procesos de desarrollo.

Descargar la aplicación [Visual Paradigm Community Edition](https://www.visual-paradigm.com/download/community.jsp), proceder con la instalación


    REALIZAR UN PROYECTO DE SOFTWARE CON VISUAL PARADIGM

    1. Crear un Diagrama de Casos de Uso
        * Crear Especificacion de Requisitos para cada caso
    2. Crear las Historias de Usuario (Storyboard) Muckups
    3. Crear el Modelo ORM Diagrama de clases
        * Crear un model ER a partir de un diagrama de clases
        * Crear la Base de Datos

## DBeaver Community

[DBeaver Community Free Universal Database Tool](https://dbeaver.io/)

![DBeaver Logo](images/DBeaver_logo.png)

Herramienta de base de datos multiplataforma gratuita para desarrolladores, administradores de bases de datos, analistas y todas las personas que necesitan trabajar con bases de datos. Admite todas las bases de datos populares: MySQL, PostgreSQL, SQLite, Oracle, DB2, SQL Server, Sybase, MS Access, Teradata, Firebird, Apache Hive, Phoenix, Presto, etc.

* Instalación en Windows 10

    Descargar el instalador de [DBeaver](https://dbeaver.io/download/), y proceder con la instalación

* Instalación en MacOs

    Descargar el instalador de [DBeaver](https://dbeaver.io/download/), versión para MacOs y proceder con la instalación

* Instalación en Linux Debian

        Instalación en Linux Debian

        1. Primera forma de instalación

        Decargar el paquete .dev de su sitio oficial: https://dbeaver.io/

        Instalar con dpkg

            cd Downloads
            sudo dpkg -i dbeaver-ce_7.3.2_amd64.deb
            dbeaver

        2. Segunda forma de instalación

            wget -O - https://dbeaver.io/debs/dbeaver.gpg.key | sudo apt-key add -
            echo "deb https://dbeaver.io/debs/dbeaver-ce /" | sudo tee /etc/apt/sources.list.d/dbeaver.list
            sudo apt-get update && sudo apt-get install dbeaver-ce
            dbeavaer