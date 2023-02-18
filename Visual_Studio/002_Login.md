# LOGIN APS.NET MVC PROJECT

Tutoriales:

Usuarios Roles y Permisos

http://anexsoft.com/p/102/roles-y-permisos-personalizados-con-asp-net-mvc?modo=ver

https://code.msdn.microsoft.com/ASPNET-MVC-5-Security-And-44cbdb97

https://www.youtube.com/watch?v=ylmHZwAl9Hc

https://www.youtube.com/watch?v=tAViIIA-7zQ  OK

[Agregando columnas a AspNetUsers](https://www.youtube.com/watch?v=_gbDDrie0gE)
[Create Roles](https://www.youtube.com/watch?v=798wMMCbaTY)
[Creating Defaul Users](https://www.youtube.com/watch?v=dIti9W11tCA)
[Authorize y AllowAnonymous](https://www.youtube.com/watch?v=75HVBfp8ESk)



[Creando Roles para los Users](https://www.youtube.com/watch?v=zZWB6BpHnWo&t=443s)

[Asignando Rol a un Usuario](https://www.youtube.com/watch?v=2v_afsMzuB8&t=126s)

[Manejando Roles](https://www.youtube.com/watch?v=sTSTuHJ476s)



# Crear Aplicacion Web y Base de Datos

* Crear una Base de Datos con Sql Server Management
* Crear una aplicación con Visual Studio, Aplicación Web, MVC, Cuentas de Usuario Individuales

# Establecer conexión del Modelo Entity Framework con la Base de Datos

* Editar Web.config

```xml
  <connectionStrings>
    <add name="DefaultConnection" connectionString="Data Source=(LocalDb)\MSSQLLocalDB;Initial Catalog=GESTIONTH_DB;Integrated Security=True;MultipleActiveResultSets=True"
      providerName="System.Data.SqlClient" />
  </connectionStrings>
```

* Ejecutar la aplicación, Registrar un nuevo usuario y comprobar la creación de tablas

# Cambiar politicas de Contraseña

Editar App_Start\IdentityConfig.cs

```csharp
manager.PasswordValidator = new PasswordValidator
{
    RequiredLength = 5,
    RequireNonLetterOrDigit = false,
    RequireDigit = false,
    RequireLowercase = false,
    RequireUppercase = false,
};
```
# Adicionar campos en la tabla Usuarios

* Editar Models\IdentityModel.cs

```csharp
    public class ApplicationUser : IdentityUser
    {
        [Required]
        [StringLength(250)]
        public string FullName { get; set; }

        public async Task<ClaimsIdentity> GenerateUserIdentityAsync(UserManager<ApplicationUser> manager)
        {
            // Tenga en cuenta que el valor de authenticationType debe coincidir con el definido en CookieAuthenticationOptions.AuthenticationType
            var userIdentity = await manager.CreateIdentityAsync(this, DefaultAuthenticationTypes.ApplicationCookie);
            // Agregar aquí notificaciones personalizadas de usuario
            return userIdentity;
        }
    }
```
* Agregar Migraciones (Menu Herramientas, Administrador de paquetes NuGet, Consola de Admninistración de Paquetes)

```sh

PM> Enable-Migrations
or
PM> Enable-Migrations -EnableAutomaticMigrations

PM> Add-Migration -Name AddFullName

PM> Update-Database -Verbose

```
* Adicionar campo en el Modelo, Editar Models\AccountViewModels.cs

```csharp
public class RegisterViewModel
{
    [Required]
    [Display(Name = "Nombre Completo")]
    public string FullName { get; set; }
}
```

* Adicionar campo en la Vista, Editar Views\Account\Register.cshtml

```csharp
<div class="form-group">
    @Html.LabelFor(m => m.FullName, new { @class = "col-md-2 control-label" })
    <div class="col-md-10">
        @Html.TextBoxFor(m => m.FullName, new { @class = "form-control" })
    </div>
</div>
```
* Pasar parametro desde el controlador (En la vista, clic derecho, Ir al Controlador) ó ir a Controllers\AccountController.cs

```csharp
// POST: /Account/Register
[HttpPost]
[AllowAnonymous]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Register(RegisterViewModel model)
{
    if (ModelState.IsValid)
    {
        var user = new ApplicationUser { UserName = model.Email, Email = model.Email, FullName = model.FullName };
        var result = await UserManager.CreateAsync(user, model.Password);
        if (result.Succeeded)
        {
            await SignInManager.SignInAsync(user, isPersistent:false, rememberBrowser:false);
            return RedirectToAction("Index", "Home");
        }
        AddErrors(result);
    }
    return View(model);
}
```

# Crear Roles por defecto

Editar el archivo App_Start\StartupAuth.cs

```csharp
using System;
using Microsoft.AspNet.Identity;
using Microsoft.AspNet.Identity.Owin;
using Microsoft.Owin;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.Google;
using Owin;
using GestionTaletoHumano.Models;
using Microsoft.AspNet.Identity.EntityFramework;

namespace GestionTaletoHumano
{
    public partial class Startup
    {
        ApplicationDbContext db = new ApplicationDbContext();  // <-- ADD

        public void ConfigureAuth(IAppBuilder app)
        {
            // ...
            CreateDefaultRols();  // <-- ADD
        }

        public void CreateDefaultRols()    // <-- ADD
        {
            var roleManager = new RoleManager<IdentityRole>(new RoleStore<IdentityRole>(db));
            IdentityRole role;

            if (!roleManager.RoleExists("Administrador"))
            {
                role = new IdentityRole();
                role.Name = "Administrador";
                roleManager.Create(role);
            }

            if (!roleManager.RoleExists("Usuario"))
            {
                role = new IdentityRole();
                role.Name = "Usuario";
                roleManager.Create(role);
            }
        }
    }
}
```
Ejecutar la aplicación y ver cambios en la tabla AspNetRoles





