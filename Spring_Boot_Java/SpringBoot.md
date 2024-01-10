# JAVA SPRING BOOT

![SpringBoot](images\springboot.jpg)

Spring Boot es un framework desarrollado para el trabajo con Java como lenguaje de programación. Se trata de un entorno de desarrollo de código abierto y gratuito. Spring Boot cuenta con una serie de características que han incrementado su popularidad y, en consecuencia, su uso por parte de los desarrolladores back-end. 

## IDE Desarrollo

Instalar [IntelliJ Community Edition](https://www.jetbrains.com/es-es/idea/download/?section=mac)

## Iniciar un Proyecto

Paso previo: [Instalar Java](../Java/Install_Java.md)

1. Ingresar al sitio [Spring Initializr](https://start.spring.io/)

2. Ingresar los siguientes datos:

Ejemplo:
![Crear un Proyecto](images/initializr.png)

```sh
Language: Java
Spring Boot: 3.2.1
Project Metadata:
    Group: bo.gob.procuraduria
    Artifact: rope-app
    Name: rope-app
    Description: Registro Obligatorio de Procesos del Estado
    Package Name: bo.gob.procuraduria.rope-app
Packaging: War
Java: 17
```

En dependencias inicialmente adicionar:

```sh
Spring Data JPA (SQL)
Persist data in SQL stores with Java Persistence API using Spring Data and Hibernate.

Spring Web (Web)
Build web, including RESTful, applications using Spring MVC. Uses Apache Tomcat as the default embedded container.

PostgreSQL Driver (SQL)
A JDBC and R2DBC driver that allows Java programs to connect to a PostgreSQL database using standard, database independent Java code.
```

3. Presionar el boton Generar
4. Descomprimir la carpeta y abrir con el IDE

## Configurar IDE IntelliJ CE y Abrir Proyecto

1. Abrir: Open (seleccionar carpeta generada con Spring Initializr)
2. Configurar version de Java en el IDE

    File > Project Structure > Project Settings: Project
        SDK: Add JDK (Select Java Version 17), Button OPEN
        SDK: Java17
3. Configurar Maven para Ejecutar

    Run > Edit Configurations > Maven
        Run: spring-boot:run
        Button Apply, Ok



## Establecer conexión con la Base de Datos Postgres

Paso Previo [Instalar Postgresql](../Postgres/Postgres.md)

1. Abrir el archivo y editar: rope-app/src/main/resources/application.properties

```java
spring.jpa.database=POSTGRESQL
spring.datasource.platform=postgres
spring.datasource.url=jdbc:postgresql://localhost:5432/ropedb
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.show-sql=true
spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
``` 
2. Ejecutar: Run