# ENTITY FRAMEWORK CODE FIRST

Tutoriales:

Entity Framework:  https://www.youtube.com/watch?v=IKlmroHxDNc

Relationship EF 6: http://www.entityframeworktutorial.net/code-first/configure-one-to-many-relationship-in-code-first.aspx


## Instalación

Abrir Administrador de Paquetes NuGet, Examinar, Buscar EntityFramework

## Creación de Modelos

* Crear Nuevo Proyecto

  Web Application MVC ASP.NET Framework, 
  Ej. WebAppCompetencias

* Crear un Nuevo Modelo

  En la Carpeta Models/ Agregar, Clase, Ej. Item.cs

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
using System.Linq;
using System.Web;

namespace WebAppCompetencias.Models
{
    public class Item
    {
        public int Id { get; set; }

        [Required]
        public int Nro { get; set; }

        [Required]
        [StringLength(1000)]
        public string Descrip { get; set; }
    }
}
```

* Crear un DB Context

  En Models/ agregar clase Ejemplo: DBCompContext.cs  
  
```csharp
using System;
using System.Collections.Generic;
using System.Data.Entity;
using System.Linq;
using System.Web;

namespace WebAppCompetencias.Models
{
    public class DBCompContext : DbContext
    {
        public DbSet <Item> Items { get; set; }

    }
}
```

* Crear un Connection String

  Abrir Web.config, y debajo de <configSections> adicionar

```xml
<connectionStrings>
    <add name="DefaultConnection" connectionString="Data Source=(LocalDb)\SQLSERVERDB;Initial Catalog=DBCOMP;AttachDBFilename=|DataDirectory|\DBComp.mdf;Integrated Security=True;" providerName="System.Data.SqlClient" />
</connectionStrings>
```

* Configurar el proyecto para habilitar Entity Framework

  Abrir Herramientas, Administrador de paquetes NuGet, Consola Administrador de Paquetes y escribir: enable-migrations

```sh

PM> enable-migrations


Checking if the context targets an existing database...
Code First Migrations enabled for project WebAppCompetencias.

```  
* Configurar para que se realicen cambios en la estructura de la Base de Datos: Abrir Migrations/Configuration.cs, y asignar a la variable AutomaticMigrationsEnabled = true;

```csharp

public Configuration()
{
    AutomaticMigrationsEnabled = true;
}
```
* Crear la Base de Datos o Actualizarlo, ejecutando el comando update-database

```sh

PM> update-database


Specify the '-Verbose' flag to view the SQL statements being applied to the target database.
No pending explicit migrations.
Running Seed method.
```

```sh
PM> update-database -force
```


## Creación de Contexto de Base de Datos

