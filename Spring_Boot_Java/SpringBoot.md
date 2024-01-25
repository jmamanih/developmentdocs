# JAVA SPRING BOOT

![SpringBoot](images/springboot.jpg)

Spring Boot es un framework desarrollado para el trabajo con Java como lenguaje de programación. Se trata de un entorno de desarrollo de código abierto y gratuito. Spring Boot cuenta con una serie de características que han incrementado su popularidad y, en consecuencia, su uso por parte de los desarrolladores back-end. 

## IDE Desarrollo

Instalar [IntelliJ Community Edition](https://www.jetbrains.com/es-es/idea/download/?section=mac)

*Personalizar IntelliJ*

Cambiar Thema de Colores
    
    IntelliJ Menu > Preferences > Appearance & Behavior > Appearance
        Get more themes
        Material Theme UI
    
    Restart IntelliJ IDEA CE
        IntelleJ Menu > Preferences > Appearance & Behavior > Appearance
        Theme: Material Oceanic
        Apply
        Ok

Instalar Plugins
    
    IntelleJ Menu > Preferences > Plugins
        Search: Rainbow Brackets
        Install
        Restart IDE

Plugins

    Atom Material           # Thema de Colores de Material
    Raidbow Brackets        # Pone los llaves en colores
    SonarLint               # Revisa código y detecta Bugs
    Atom Material Icons     # Iconos de Material
    Spring Boot Assistant 

Key Maps

    Cmd + Alt + L           Reformatea el código
    Ctrl + Espacio          Información del código 



## Iniciar un Proyecto

Paso previo: [Instalar Java](../Java/Install_Java.md)

1. Ingresar al sitio [Spring Initializr](https://start.spring.io/)

2. Ingresar los siguientes datos:

Ejemplo:
![Crear un Proyecto](images/initializr.png)

Referencia [Iniciar Proyecto Spring Boot](https://www.arteco-consulting.com/post/tu-primera-aplicacion-con-spring-boot)

```sh
Project: Maven Project
Language: Java
Spring Boot: 3.2.1
Project Metadata:
    Group: bo.gob.pge
    Artifact: rope
    Name: rope
    Description: Registro Obligatorio de Procesos del Estado
    Package Name: bo.gob.pge.rope
Packaging: War
Java: 17
```

En dependencias inicialmente adicionar:

```sh
Spring Data JPA (SQL)
Spring Web (Web)
PostgreSQL Driver (SQL)
```

3. Presionar el boton Generar
4. Descomprimir la carpeta y abrir con el IDE

## Configurar IDE IntelliJ CE y Abrir Proyecto

1. Abrir: Open (seleccionar carpeta generada con Spring Initializr)
2. Configurar version de Java en el IDE

    File > Project Structure > Project Settings: Project
        SDK: Add JDK (Select Java Version 17), Button OPEN
        SDK: Eclipse Temurin Java17
        Button Ok
3. Configurar Maven para Ejecutar

    Run > Edit Configurations > Maven (Add Maven si no existiera) 
        Run: spring-boot:run
        Button Apply, Ok


## Establecer conexión con la Base de Datos Postgres

Paso Previo [Instalar Postgresql](../Postgres/Postgres.md)

*Parámetros de conexión a una Base de Datos Postgres*

```sh
spring.datasource.url=jdbc:postgresql://localhost:5432/your_database
spring.datasource.username=your_user
spring.datasource.password=your_password
```
*Delegar a Spring Boot la creacion de tablas*

```sh
spring.jpa.hibernate.ddl-auto=create
```
Parámetros de esta propiedad
```sh
create: se borrarán las tablas y se volveran a crear
none: no se realizará ninguna acción.
drop: se crearán las tablas a partir de las entidades y al final se borrarán.
update: realiza una actualización del esquema a partir de las entidades.
validate: sólo realiza una validación entre las entidades y el esquema de la base de datos.
```

Abrir el archivo de propiedades y editar:

Ruta: proyecto/src/main/resources/
Archivo: application.properties

```java
server.port=9090
spring.jpa.database=POSTGRESQL
spring.datasource.platform=postgres
spring.datasource.url=jdbc:postgresql://localhost:5432/ropedb
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.show-sql=true
spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
``` 
Ejecutar aplicacion: Run

## Crear una página de Presentación de Backend

*Adicionar la dependencias Thymeleaf*

Editar el archivo de dependencias y plugins

Ruta: /
Archivo: pom.xml
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

Nota: también se pueden buscar las dependencias en [Maven Repository](https://mvnrepository.com/) con el nombre "Spring Boot Thymeleaf"

*Crear un archivo Html de Presentación*

Crear un archivo
Ruta: src/main/resources/templates
Archivo: intro.html
```html
<head>
    <meta charset="UTF-8">
    <title>Backend-ROPE</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
    <link rel="stylesheet" href="https://code.getmdl.io/1.3.0/material.indigo-pink.min.css">
    <script defer src="https://code.getmdl.io/1.3.0/material.min.js"></script>
    <style>
        <!-- Square card Style-->
        .demo-card-square.mdl-card {
        }
        .demo-card-square > .mdl-card__title {
          color: #fff;
          background: bottom right 15% no-repeat #46B6AC;
        }
        .cont {
          width: 100vw;
          height: 100vh;
          position: relative;
        }
        .sub {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
        }
    </style>
</head>
<body>
<!-- Square card -->
<div class="cont">
    <div class="sub">
        <div class="demo-card-square mdl-card mdl-shadow--2dp">
            <div class="mdl-card__title mdl-card--expand">
                <h1 class="mdl-card__title-text">BACKEND TECHNOLOGY</h1>
            </div>
            <div class="mdl-card__supporting-text">
                <b>RUNNING BACKEND</b></br></br>
                Procuraduria General del Estado</br></br>
                Sistema de Registro de Procesos del Estado</br>
                ROPE version 2.0
            </div>
            <div class="mdl-card__actions mdl-card--border">
               <p style="text-align:center">© Copyright PGE - 2024</p>
            </div>
        </div>
    </div>
</div>
</body>
</html>
```

*Crear el Controlador*

Crear un nuevo paquete
Ruta: src/main/java/bo.gob.pge.rope
Paquete: intro

Crear un Controlador
Ruta: src/main/java/bo.gob.pge.rope/intro
Archivo: IntroController
```java
package bo.gob.pge.rope.intro;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class IntroController {
    @RequestMapping ("/")
    public String intro() {
        return "intro";
    }
}
```
Nota: Las extensiones de los archivos creados son .java

## Arquitectura Multicapa de Spring Boot

![Arquitectura Spring Boot](images/arqcapas.png)

## Reducir código con la libreria (Lombok)

Es una librería que nos ayuda a reducir líneas de código típicas de getters y settter en clases.

Adicionar la dependencia Lombok
Ruta: /
Archivo: pom.xml
```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <optional>true</optional>
</dependency>
```

Nota: para que el ID detecte las funciones de Lombok se debe instalar tambien el Plugin de Lombok en IntelliJ IDEA CE

    IntelliJ IDE Menu > Preferences > Plugins
        Install: Lombok

Anotaciones:

    @Data
    @Getter
    @Setter
    @NoArgsConstructor
    @AllArgsConstructor
    @Builder
    @Log

## Crear un API REST CRUD para una tabla

*Como ejemplo se creara una tabla paramétrica Deptos (Departamentos)*

Crear Paquete Entity
Ruta: src/main/java/bo.gob.pge.rope/
Paquete: entity

Crear archivo de Clase para el Entity
Archivo: Depto (Class)

```java
package bo.gob.pge.rope.model;
import jakarta.persistence.*;
import lombok.Data;

@Entity
@Table (name = "deptos")
@Data                    // Getters, Setters y Constructor
public class Depto {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    @Basic               // Campos basicos para el resto de atributos
    private String descrip;
    private String cod;
}
```

Crear Paquete Repository
Ruta: src/main/java/bo.gob.pge.rope/
Paquete: repository

Crear archivo de Interface 
Archivo: DeptoRepository (Class Interface)

```java
package bo.gob.pge.rope.repository;

import bo.gob.pge.rope.entity.Depto;
import org.springframework.data.jpa.repository.JpaRepository;

public interface DeptoRepository extends JpaRepository<Depto, Long> {
}
```

Crear Paquete Service
Ruta: src/main/java/bo.gob.pge.rope/
Paquete: service

Crear archivo de Clase
Archivo: DeptoService (Class)

```java
package bo.gob.pge.rope.service;

import bo.gob.pge.rope.model.Depto;
import bo.gob.pge.rope.repository.DeptoRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Optional;

@Service
public class DeptoService {
    private final DeptoRepository deptoRepository;

    @Autowired
    public DeptoService(DeptoRepository deptoRepository) {
        this.deptoRepository = deptoRepository;
    }

    public List<Depto> getDeptos() {
        return deptoRepository.findAll();
    }

    public Optional<Depto> getDeptoById(Long id) {
        return deptoRepository.findById(id);
    }

    public Depto createDepto(Depto depto) {
        return deptoRepository.save(depto);
    }

    public void deleteDepto(Long id) {
        deptoRepository.deleteById(id);
    }
}
```

Crear Paquete Controller
Ruta: src/main/java/bo.gob.pge.rope/
Paquete: controller

Crear archivo de Clase 
Archivo: DeptoController (Class)

```java
package bo.gob.pge.rope.controller;

import bo.gob.pge.rope.model.Depto;
import bo.gob.pge.rope.service.DeptoService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/depto")
public class DeptoController {
    private final DeptoService deptoService;

    @Autowired
    public DeptoController(DeptoService deptoService) {
        this.deptoService = deptoService;
    }

    @GetMapping
    public List<Depto> getDeptos() {
        return deptoService.getDeptos();
    }

    @GetMapping("/{id}")
    public Depto getDeptoById(@PathVariable Long id) {
        return deptoService.getDeptoById(id).orElse(null);
    }

    @PostMapping
    public Depto createDepto(@RequestBody Depto depto) {
        return deptoService.createDepto(depto);
    }

    @PutMapping
    public Depto updateDepto(@RequestBody Depto updatedDepto) {
        return deptoService.createDepto(updatedDepto);
    }

    @DeleteMapping("/{id}")
    public void deleteDepto(@PathVariable Long id) {
        deptoService.deleteDepto(id);
    }

}
```
## Comprobar las APIS

Instalar Postman 

    Descargar el Intalador de [Postman](https://www.postman.com/downloads/)
    Instalar
    Crear una cuenta o ingresar con cuenta de correo Gmail  

Abrir Postman

Listado General

    GET: localhost:9090/api/depto

Listado por id

    GET: localhost:9090/api/depto/1

Crear un registro

    POST: localhost:9090/api/depto

        Boby > raw : JSON

        {
            "descrip" : "LA PAZ",
            "cod" : "LPZ"
        }

Modificar un registro

    PUT: localhost:9090/api/depto

        Boby > raw : JSON

        {
            "id" : 1, 
            "descrip" : "LA PAZ",
            "cod" : "LP"
        }

Eliminar registro

    DELETE: localhost:9090/api/depto/1

## Documentar las API REST

Referencias:
* [Springdoc Openapi](https://springdoc.org/)
* [Documenting a Spring Rest](https://www.baeldung.com/spring-rest-openapi-documentation)
* [Swagger 2.x Annotation](https://github.com/swagger-api/swagger-core/wiki/Swagger-2.X---Annotations)

Adicionar la dependencia
Ruta: /
Archivo: pom.xml

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.3.0</version>
</dependency>
```

Configurar swagger en el archivo de propiedades
Ruta: src/main/resources
Archivo: application.Properties

```sh
# swagger documentation
springdoc.swagger-ui.enabled=true
springdoc.api-docs.enabled=true
springdoc.swagger-ui.path=/swagger-ui.html
```

Probar funcionamiento abriendo la dirección:

    http://localhost:9090/swagger-ui.html

Documentar Información General de la API 

Ruta: src/main/java/bo.gob.pge.rope/controller
Archivo: DeptoController

```java
@OpenAPIDefinition (info =
    @Info(
        title = "API DEPTO",
        version = "1.0",
        description = "Servicios API REST para la tabla 'Depto'\nTabla paramétrica donde se almacenan los datos de los departamentos del país"
        license = @License(name = "PGE - ROPE Versión 2.0", url = "http://foo.bar"),
        contact = @Contact(url = "http://gigantic-server.com", name = "Fred", email = "Fred@gigagantic-server.com")
    )
)
public class DeptoController {
    ...
}
```

Documentar Información de la API especifico

Ruta: src/main/java/bo.gob.pge.rope/controller
Archivo: DeptoController

```java
@Operation(summary = "Obtiene datos de la tabla 'Deptos'", description = "Obtiene Listado General de la Tabla 'Deptos'")
@ApiResponse(responseCode = "200", description = "Departamentos Encontrados")
@ApiResponse(responseCode = "400", description = "Parámetros Proporcionados no validos")
@ApiResponse(responseCode = "404", description = "Departamentos no encontrados")
@GetMapping
public List<Depto> getDeptos() {
    return deptoService.getDeptos();
}
```
## Validación de campos

Para la validación agregar la dependencia: 

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

*Anotaciones:*

|Anotación  	|Tipos 	          |Explicación|
|---------------|-----------------|-----------|
|@AssertFalse 	|Boolean, boolean 	|El booleano deberá ser false
|@AssertTrue 	|Boolean, boolean 	|El booleano deberá ser true
|@Digits(integer=n, fraction=m) 	|Cualquier tipo numérico 	|Especifica el nº máximo de cifras enteras y decimales
|@Future 	    |java.util.Date y java.util.Calendar 	|La fecha debe ser mayor que ahora
|@Past 	        |java.util.Date y java.util.Calendar 	|La fecha debe ser menor que ahora
|@Max(n) 	    |Cualquier tipo numérico 	|El valor deberá ser menor o igual a n
|@Min(n) 	    |Cualquier tipo numérico 	|El valor deberá ser mayor o igual a n
|@NotNull 	    |Object 	|El objeto no puede ser null
|@Null          |Object 	|El objeto debe ser null
|@Pattern(regexp=“r”) 	|String 	|Comprueba que el valor se ajusta a la expresión regular r
|@Size(min=n, max=m) 	|String o colecciones 	|El tamaño del String o la colección debe estar entre n y m.
|@Email 	    |String 	|El valor tiene el formato de una dirección de correo electrónico
|@NotBlank 	    |String 	|Comprueba que el String no sea null y que al hacer un trim() aún haya algún caracter
|@Valid 	    |Object 	|Si el campo es otro objeto que tiene sus propias validaciones, con esta anotación indicaremos que también debe validarse ese otro objeto 

*Anotar la validación antes del un campo*

Ruta: Ruta: src/main/java/bo.gob.pge.rope/entity
Archivo: Depto (Class)

```java
package bo.gob.pge.rope.model;
import jakarta.persistence.*;
import jakarta.validation.constraints.NotBlank;
import jakarta.validation.constraints.NotNull;
import lombok.Data;

@Entity
@Table (name = "deptos")
@Data                    // Getters, Setters y Constructor
public class Depto {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    @Column(nullable = false, unique = true)
    @NotBlank(message = "El nombre del departamento, es requerido")
    private String descrip;
    @Column(nullable = false, unique = true)
    @NotBlank(message = "Asigne un código de departamento")
    private String cod;
}
```

*Asignar la anotaciión @Valid en el controlador*

Ruta: Ruta: src/main/java/bo.gob.pge.rope/controller
Archivo: DeptoController

```java
// ...

@PostMapping
@Operation(summary = "Adiciona datos en la tabla 'Deptos'", description = "Adiciona un registro en la Tabla 'Deptos'")
public Depto createDepto(@Valid @RequestBody Depto depto) {
    return deptoService.createDepto(depto);

@PutMapping
@Operation(summary = "Modifica datos de la tabla 'Deptos'", description = "Modifica un registro de la Tabla 'Deptos'")
public Depto updateDepto(@Valid @RequestBody Depto updatedDepto) {
    return deptoService.createDepto(updatedDepto);
}

// ...
```

## Manejo de Errores o Excepciones

*Crear el paquete manejador de Errores y archivos de clase*

Ruta: src/main/java/bo.gob.pge.rope/
Paquete: error

*Crear archivo de clase EntityError, la estructura de un mensaje de error*

Ruta: src/main/java/bo.gob.pge.rope/error
Archivo: ErrorResponse (Class)

```java
package bo.gob.pge.rope.error;

import lombok.*;

import java.util.Date;
import java.util.List;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class ErrorResponse {

    private int status;
    private String message;
    private Date timestamp;
    List<String> errors;
    ErrorResponse(String message) {
        this.message = message;
    }
}
```
*Crear el archivo InvalidDataException*

Ruta: src/main/java/bo.gob.pge.rope/error
Archivo: InvalidDataException (Class)

```java
package bo.gob.pge.rope.error;

import lombok.Getter;
import org.springframework.validation.BindingResult;
@Getter
public class InvalidDataException extends RuntimeException {
    private static final long serialVersionUID = 1L;
    private final transient BindingResult result;
    public InvalidDataException(BindingResult result) {
        super();
        this.result = result;
    }
    public InvalidDataException(String message, BindingResult result) {
        super(message);
        this.result = result;
    }
}
```

*Crear el archivo manejador de errorees RestExceptionHandler*

Ruta: src/main/java/bo.gob.pge.rope/error
Archivo: RestExceptionHandler (Class)

```java
package bo.gob.pge.rope.error;

import org.springframework.dao.DuplicateKeyException;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.validation.FieldError;
import org.springframework.web.method.annotation.MethodArgumentTypeMismatchException;
import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;

import java.util.Date;
import java.util.List;
import java.util.NoSuchElementException;
import java.util.stream.Collectors;

@ControllerAdvice
public class RestExceptionHandler extends ResponseEntityExceptionHandler {
    @ExceptionHandler
    protected ResponseEntity<ErrorResponse> handleException(NoSuchElementException exc) {
        HttpStatus httpStatus = HttpStatus.BAD_REQUEST;
        return buildResponseEntity(httpStatus, exc);
    }
    @ExceptionHandler
    protected ResponseEntity<ErrorResponse> handleException(DuplicateKeyException exc) {
        HttpStatus httpStatus = HttpStatus.BAD_REQUEST;
        return buildResponseEntity(httpStatus, exc);
    }
    @ExceptionHandler
    protected ResponseEntity<ErrorResponse> handleException(IllegalArgumentException exc) {
        HttpStatus httpStatus = HttpStatus.BAD_REQUEST;
        return buildResponseEntity(httpStatus, exc);
    }
    @ExceptionHandler
    protected ResponseEntity<ErrorResponse> handleException(InvalidDataException exc) {
        HttpStatus httpStatus = HttpStatus.BAD_REQUEST;
        List<String> errors = exc.getResult().getFieldErrors().stream().map(FieldError::getDefaultMessage)
                .collect(Collectors.toList());
        return buildResponseEntity(httpStatus, new RuntimeException("Dato enviado, inválido"), errors);
    }
    @ExceptionHandler
    protected ResponseEntity<ErrorResponse> handleException(MethodArgumentTypeMismatchException exc) {
        HttpStatus httpStatus = HttpStatus.BAD_REQUEST;
        // Aplica cuando en el URL se envia un argumento invalido, por ejemplo String
        // por Integer
        return buildResponseEntity(httpStatus, new RuntimeException("Tipo de Argumento, inválido"));
    }
    @ExceptionHandler
    protected ResponseEntity<ErrorResponse> handleException(Exception exc) {
        HttpStatus httpStatus = HttpStatus.INTERNAL_SERVER_ERROR;
        return buildResponseEntity(httpStatus, new RuntimeException("Se presentó un problema"));
    }
    private ResponseEntity<ErrorResponse> buildResponseEntity(HttpStatus httpStatus, Exception exc) {
        return buildResponseEntity(httpStatus, exc, null);
    }
    private ResponseEntity<ErrorResponse> buildResponseEntity(HttpStatus httpStatus, Exception exc, List<String> errors) {
        ErrorResponse error = new ErrorResponse(null);
        error.setMessage(exc.getMessage());
        error.setStatus(httpStatus.value());
        error.setTimestamp(new Date());
        error.setErrors(errors);
        return new ResponseEntity<>(error, httpStatus);
    }
}
```

*En el controlador llamar al manejador de Excepciones*

En el método (REST) se debe incluir como parámetro BindingResult y preguntar si hay errores

Ruta: src/main/java/bo.gob.pge.rope/controller
Archivo: DeptoController

```java

// ...
@PostMapping
@Operation(summary = "Adiciona datos en la tabla 'Deptos'", description = "Adiciona un registro en la Tabla 'Deptos'")
public Depto createDepto(@Valid @RequestBody Depto depto, BindingResult result) {
    if(result.hasErrors()) {
        throw new InvalidDataException(result);
    }
    return deptoService.createDepto(depto);
}
// ...

```

## Métodos de Consulta JPA (Query Method)




## Objeto de Transferencia de Datos (DTO)

