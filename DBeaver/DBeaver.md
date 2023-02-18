 
# DBeaver Community
[DBeaver Community Free Universal Database Tool](https://dbeaver.io/)

![DBeaver Logo](images/DBeaver_logo.png)

Herramienta de base de datos multiplataforma gratuita para desarrolladores, administradores de bases de datos, analistas y todas las personas que necesitan trabajar con bases de datos. Admite todas las bases de datos populares: MySQL, PostgreSQL, SQLite, Oracle, DB2, SQL Server, Sybase, MS Access, Teradata, Firebird, Apache Hive, Phoenix, Presto, etc.

<a id="topmenu">

## CONTENIDO

* Instalación en Windows 10
* Instalación en MacOs
* [Instalación en Linux Debian](#idsec30 "Instalación en Linux")



<a id="idsec30">

## Instalación en Linux Debian

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


