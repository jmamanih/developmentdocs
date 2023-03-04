## El Modelo ORM de Laravel ELOQUENT

EL ORM oermipte asociar a cada tabla de la base de datos un modelo de clase se pueden leer, adicionar, modificar y eliminar datos de una forma orientada a objetos.

Los modelos se encuentran en:

```
app\Models
```

## Modelos

*Crear un modelo asociado a una tabla*
```
php artisan make:model NombreTabla
```
*Ubicaciòn de un  modelo*
```
app/Models/
```
*CONVENCION*
Los nombres de las tablas debe estar en plural y en minusculas y los modelos deben escribirse en Singular y empezar con Mayúscula a esa notacion se llama *PascalCase*

Ejemplo:
Para la tabla *procedures* su modelo correspondiente seria
```
php artisan make:model Procedure
```
*Crear tablas y modelos a la vez* 
```
php artisan make:model Procedure -m
```
```php
<?php
namespace App\Models;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Procedure extends Model
{
    use HasFactory;
    //protected $table = 'tramites';
}
```
Si la tabla lleva el mismo nombr en singular no es necesario especificar el nombre de la tabla, Laravel lo detecta automaticamente, de lo contrario mencionar a que tabla hace referencia.
```php
protected $table = 'nombre_tabla';
```
