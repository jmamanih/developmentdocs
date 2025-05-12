# POSTMAN

## Instalación en MacOs

Descargar el Intalador de [Postman](https://www.postman.com/downloads/)
Instalar
Crear una cuenta o ingresar con cuenta de correo Gmail

## Instalación en Linux Debian

Descargar la última versión desde su sitio oficial https://www.postman.com/downloads/

Ejecutar los siguientes comandos

    cd Downloads/
    tar -xzf Postman-linux-x64-7.32.0.tar.gz
    sudo mkdir -p /opt/apps/
    sudo mv Postman /opt/apps/
    sudo ln -s /opt/apps/Postman/Postman /usr/local/bin/postman
    postman


Para iniciar la aplicación desde un icono de inicio, debe crear un archivo .desktop (un acceso directo utilizado para iniciar una aplicación en Linux) 

    
    sudo vim /usr/share/applications/postman.desktop


Luego copie y pegue las siguientes configuraciones (asegúrese de que las rutas de los archivos sean correctas dependiendo de dónde extrajo los archivos):

    [Desktop Entry]
    Type=Application
    Name=Postman
    Icon=/opt/apps/Postman/app/resources/app/assets/icon.png
    Exec="/opt/apps/Postman/Postman"
    Comment=Postman Desktop App
    Categories=Development;Code;

Guarde el archivo y ciérrelo.

Si las rutas de archivo son correctas el icono deberia mostrarse en el menú del sistema.

## WORKSPACE

En Postman, un Workspace (espacio de trabajo) es un entorno colaborativo donde se puede organizar y gestionar tus colecciones de peticiones, entornos, scripts, y otros recursos relacionados con APIs. Piensa en un Workspace como un "proyecto" que contiene todo lo necesario para trabajar con una o varias APIs.

Tipos de Workspaces:

    Personal Workspace: Solo tú puedes ver y trabajar en él.
    Team Workspace: Puedes colaborar con otros miembros de tu equipo.
    Public Workspace: Puedes compartirlo públicamente para que otros lo vean y utilicen.

Crear un Workspace en Postman

Desde la aplicación de Postman (escritorio o web):

    Abre Postman.
    En la esquina superior izquierda, haz clic en el selector de Workspace (donde ves el nombre actual del Workspace).
    Haz clic en "Create Workspace" o "Nuevo espacio de trabajo".
    Llena la información:
        Nombre del Workspace.
        Descripción (opcional).
        Tipo de Workspace (Personal, Team, Public).
    Haz clic en "Create Workspace".

¿Para qué usar Workspaces?

    Separar proyectos o entornos de desarrollo.
    Compartir colecciones con un equipo.
    Organizar pruebas automatizadas y documentación de APIs.

## COLLECTIONS

En Postman, una colección es un conjunto organizado de solicitudes HTTP (requests) que se pueden agrupar por proyecto, funcionalidad o flujo de trabajo. Es una forma práctica de estructurar y reutilizar pruebas o llamadas a APIs.

Una colección puede contener:

    Solicitudes HTTP: GET, POST, PUT, DELETE, etc.
    Carpetas: para agrupar solicitudes relacionadas dentro de la misma colección.
    Variables: a nivel de colección para reutilizar valores (como URLs base, tokens).
    Scripts pre-request y tests: automatización antes o después de ejecutar cada solicitud.
    Documentación: puedes documentar cada solicitud para explicar su propósito.

1. Crear una Colección

    En la barra lateral izquierda, haz clic en el botón "Collections".
    Luego haz clic en el botón "+" o "New Collection".
    Asignar un Nombre

    **Nota:** Se puede crear carpetas dentro de la colección para organizar mejor por recursos o módulos, por ejemplo: Usuarios, Productos, Autenticación, etc.

2. Hacer una petición GET

    Dentro de la Coleccion o Collection, hacer un "Add request" o un "Add folder" para organizar

    URL:  127.0.0.1/8000/api
    URL: {{base_url}}/api
    METODO: GET
        
    Headers()

        Key             Value
        --------------------------------------------
        Accept          application/json

    Scripts()

    ```js
    // Verificar el código de estado
    pm.test("El estado de la respuesta es 200", function () {
        pm.response.to.have.status(200);
    });
    ```
    **Nota:** El resultado del script se ve en "Test Results"

3. Hacer una petición POST

    URL:  127.0.0.1/8000/api/auth/login
    URL: {{base_url}}/api/auth/login
    METODO: POST

    Headers()

        Key             Value
        --------------------------------------------
        Content-Type    application/json
        Accept          application/json

    Body() -> raw, JSON
        
        {
            "name": "administrador",
            "password": "12345678",
            "funcionario": false
        }
        
    Script()
    ```js
    // Verificar el estado de la respuesta
    pm.test("Estado de respuesta es 201", function () {
        pm.response.to.have.status(201);
    });

    // Verificar estructura y contenido de la respuesta
    pm.test("La respuesta contiene token de acceso", function () {
        var jsonData = pm.response.json();
        pm.expect(jsonData.estado).to.eql(true);
        pm.expect(jsonData.data).to.have.property('access_token');
        pm.expect(jsonData.data).to.have.property('type_token');
        pm.expect(jsonData.data).to.have.property('user');
    });
    ```
    **Nota:** El Script copia el Token a una variable de entonrno "token"

4. Hacer una petición de una Ruta Protegida con Login

    URL:  127.0.0.1/8000/api/svf-parametricas/tipos-decisiones
    URL: {{base_url}}/api/svf-parametricas/tipos-decisiones
    METODO: GET

    Headers()

    Key             Value
    --------------------------------------------
    Accept          application/json
    Authorization   Bearer {{token}}
    ó
    Authorization   Bearer 2322|0k3ewlB0hn7HSZwFp6pdwtheADweCp7kRRbmJAuP5b7f33e8
    

## ENVIRONMENTES

En Postman, los environments (entornos) son conjuntos de variables que puedes usar para cambiar fácilmente valores como URLs, tokens, claves API, etc., sin tener que editarlos directamente en cada solicitud

Por ejemplo: si se tiene una API que corre en distintos entornos:

    Desarrollo (dev):  https://api-dev.miapi.com
    Pruebas (staging): https://api-staging.miapp.com
    Producción (prod): https://api.miapp.com

En lugar de cambiar manualmente la URL en cada solicitud, se puede usar una variable como {{base_url}}, y asignarle diferentes valores según el environment.

Para ello se pueden crear tres ambientes de trabajo (Environmets) con la definición de las mismas variables con datos diferentes y seleccionar el Environmet a Utilizar solo se puede seleccionar un Environment

1. Crear un Environment

    Ir a la esquina superior derecha y haz clic en el ícono del engranaje ⚙️ → "Manage Environments".
    Haz clic en "Add".
    Asignar un nombre (por ejemplo: Dev Environment).

2. Adicionar Variables

    Agregar variables como:

        base_url → https://api-dev.miapp.com
        token → abc123...
        Haz clic en Save.

    Ej.
        Variable            Type            Initial value       Current value
        -----------------------------------------------------------------------
        base_url            default         127.0.0.1:8000      127.0.0.1:8000
        token               default                             2322|6pdwtheADweCp7kRRbmJAuP5b7f33e8...

    **Nota:** de la misma manera se pueden crear las mismas variables para otros Environmets

3. Seleccionar el environment

    Para que tenga efecto la definición de variables desde el menu desplegable en la parte superior derecha de Postman, elegir el Environment.

