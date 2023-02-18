# MYSQL

![MySql](images/mysql_logo.png)

MySQL es un sistema de gestión de bases de datos relacional desarrollado bajo licencia dual: Licencia pública general/Licencia comercial por Oracle Corporation y está considerada como la base de datos de código abierto más popular del mundo,1​2​ y una de las más populares en general junto a Oracle y Microsoft SQL Server, todo para entornos de desarrollo web.
[Fuente: Wikipedia](https://es.wikipedia.org/wiki/MySQL)

<a id="topmenu">

## CONTENIDO

* Instalación en Windows 10
* [Instalación en MacOs](#idsec20 "Instalación en MacOs")
* [Instalación en Linux Debian](#idsec30 "Instalación en Linux")
* [Configuración de MySQL](#idsec40 "Configuración")
* [Crear una base de datos](#idsec50 "Crear Base de Datos")
* [Comandos de uso frecuente en MySQL](#idsec60 "Comandos Importantes")


<a id="idsec20">

## Instalación en MacOs

        brew install mysql
        brew services restart mysql
        mysql -u root

<a id="idsec30">

## Instalación en Linux

*Instalar MySQL*

    sudo apt-get install mariadb-server


<a id="idsec40">

## Configuración de MySQL

    sudo mysql_secure_installation

Ej.
    password root: 2687126

Se recomienda responder todos con [Y]

<a id="idsec50">

## Crear una base de datos

1. Ingresar al modo cli de MariaDB, ingresamos la contraseña y se podrá administrar la base de datos desde la consola.

        sudo mysql -u root

        sudo mysql -u root -p

2. Crear una base de datos para probar la ejecución, recuerde que esto es en modo consola. (Ej. blog)

            create database blog;

3. Este comando permite crear un usuario (Ej. dev) y a la vez darle los permisos a la base de datos correspondiente (blog)

            GRANT ALL PRIVILEGES ON blog.* To 'dev'@'localhost' IDENTIFIED BY 'abcde';

donde:

    blog        es la base de datos
    dev         es el usuario
    localhost   nombre del dominio del servidor
    abcde       contraseña

4. Refrescar los privilegios asignados.

            flush privileges;

5. Para salir de la consola presionamos **ctrl+c** o escribir el comando **exit** ó **quit**


6. Ingresar a la consola con el usuario creado (dev) y verificar que todo está correcto.

    mysql -u dev -p

        show databases;

[Ir al Inicio](#topmenu "Ir al inicio de la página")

<a id="#idsec60">

## Comandos importantes de MySql

*Ingresar al modo consola como usuario administrador (root)*

        sudo mysql -u root

*Obtener la lista de Usuarios*

        select User from mysql.user;

*Usuario actual*

        Select current_user();

*Cambiar contraseña de usuario*

        set password for 'dev'@'localhost' = password('12345');
        
        flush privileges;

*Crear una Base de Datos*

        CREATE DATABSE nombre_base_de_datos;

        Ej.

        CREATE DATABASE lapazdigital;

*Obtener el Listado de las Bases de Datos*

        SHOW DATABASES;

*Eliminar una base de datos*

        DROP DATABASE database_name;

*Obtener el listado de las tablas*

        SHOW FULL TABLES FROM mi_base_de_datos;

*Mostrar estructura de una tabla o las columnas de una tabla*
        
        SHOW COLUMNS FROM TABLE_NAME

        DESCRIBE TABLE_NAME;

*Crear un nuevo usuario de base de datos*

        CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';

        Ej.

        CREATE USER 'dev'@'localhost' IDENTIFIED BY '12345';

*Eliminar un usuario por completo*

        DROP USER 'username'@'localhost';

*Asignar todos los privilegios a un usuario*

        GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
        
        Ej.

        GRANT ALL PRIVILEGES ON * . * TO 'dev'@'localhost';

*Asignar todos los privilegios a un usuario y una base de datos*

        GRANT ALL PRIVILEGES ON database.tables TO 'user'@'localhost';
        
        Ej.

        GRANT ALL PRIVILEGES ON lapazdigitaldb.* TO 'dev'@'localhost';

*Refrescar Privilegios*

        FLUSH PRIVILEGES;

*Otorgar permisos especificos a un usuarios*

        GRANT type_of_permission ON database_name.table_name TO 'username'@'localhost';

        Ej.

        GRANT SELECT ON lapazdigital.* TO 'dev'@'localhost';

*Lista de permisos*


    ALL PRIVILEGES      Otorgar acceso completo a una base de datos
                        si no se selecciona ninguna base de datos, acceso global a todo el sistema).
    CREATE              Permite crear tablas o bases de datos.
    DROP                Permite eliminar tablas o bases de datos.
    DELETE              Permite eliminar filas de las tablas.
    INSERT              Permite insertar filas en las tablas.
    SELECT              Permite leer las bases de datos.
    UPDATE              Permite actualizar las filas de las tablas.
    GRANT OPTION        Permite otorgar o eliminar privilegios de otros usuarios.

*Revocar Permisos*

        REVOKE type_of_permission ON database_name.table_name FROM 'username'@'localhost';

*Revisar permisos actuales de un usuario*

        SHOW GRANTS FOR 'username'@'localhost';

*Cerrar sesión*

        quit

*Iniciar sesion con un usuario*

        mysql -u [newuser] -p

        Ej.

        mysql -u dev -p

*Seleccionar una base de datos y consultar datos*

        USE database_name;

        Ej.

        USE lapazdigital;
        Select * from users;

*Mostrar todas las tablas*

        show tables; 

*Mostrar columnas de una tabla*

        show columns from table_name;

[Ir al Inicio](#topmenu "Ir al inicio de la página")