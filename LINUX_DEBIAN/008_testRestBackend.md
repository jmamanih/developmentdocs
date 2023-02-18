TEST REST
=========

Para realizar las pruebas del Backend instalar Google Chrome y posteriormente la Extension POSTMAN

TEST POST
---------
Adicionar Registros
En el URL escribir la ruta rest:
>Ej. 
>localhost:8001/api/v1/agenda/calendario

En el entorno Postman seleccionar
>POST>Body>raw>JSON(application/json)
>escribir los datos a ingresar en formato json

	{
        "fecha": "2016-09-07",
    	"evento": "Test evento 2",
    	"_usuario_creacion": 1
    }

> En PARAMS Seleccionr SEND

Como resultado se muestra:

	{
     "finalizado": true,
     "mensaje": "create",
     "datos": {
        "id_calendario": 3,
        "fecha": "2016-09-07T00:00:00.000Z",
        "evento": "Test evento 2",
        "_usuario_creacion": 1,
        "_fecha_modificacion": "2016-09-07T16:03:28.892Z",
        "_fecha_creacion": "2016-09-07T16:03:28.892Z",
        "_usuario_modificacion": null
     }
    }


TEST PUT
---------
Modificar Registros
>localhost:8001/api/v1/agenda/calendario/1

	{
	"fecha": "2016-09-05",
	"evento": "Test evento actualizado",
	"_usuario_modificacion": 1
    }


TEST GET
---------
Listado de Registros
>localhost:8001/api/v1/agenda/calendario

Resultado:

	{
    "finalizado": true,
    "mensaje": "query",
    "datos": {
    "count": 2,
    "results": [
      {
        "id_calendario": 2,
        "fecha": "2016-09-07T00:00:00.000Z",
        "evento": "Test evento",
        "_usuario_creacion": 1,
        "_usuario_modificacion": null,
        "_fecha_creacion": "2016-09-07T15:34:45.200Z",
        "_fecha_modificacion": "2016-09-07T15:34:45.200Z"
      },
      {
        "id_calendario": 3,
        "fecha": "2016-09-07T00:00:00.000Z",
        "evento": "Test evento 2",
        "_usuario_creacion": 1,
        "_usuario_modificacion": null,
        "_fecha_creacion": "2016-09-07T16:03:28.892Z",
        "_fecha_modificacion": "2016-09-07T16:03:28.892Z"
      }
      ]
     }
    }

TEST DELETE
---------
Eliminar Registros
>localhost:8001/api/v1/agenda/calendario/1



