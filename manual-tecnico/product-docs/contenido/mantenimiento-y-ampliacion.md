---
description: >-
  Explica las connsideraciones para realizar modificaciones, incorporar nuevas
  funcionalidades y mantener el funcionamiento del software.
icon: screwdriver-wrench
---

# MANTENIMIENTO Y AMPLIACIÓN

## 16. Mantenimiento y ampliación

### 16.1 Agregar una entidad o modificar el modelo

{% stepper %}
{% step %}
## Modificar el modelo

Crear o modificar la clase en `Aplicacion/modelos/`.

Registrar el `DbSet` en `AplicacionDBContexto.cs` cuando corresponda.

Crear o actualizar la configuración Fluent API en `Infraestructura/Datos/Configuraciones/`.
{% endstep %}

{% step %}
## Crear y revisar la migración

Generar una migración.

Revisar el código generado por la migración.
{% endstep %}

{% step %}
## Aplicar cambios de esquema

Aplicar la migración en una base de desarrollo.
{% endstep %}

{% step %}
## Actualizar capas backend

Actualizar repositorio, DTO, servicio y controlador.
{% endstep %}

{% step %}
## Actualizar frontend

Incorporar o modificar el servicio Angular y los componentes que consumen la operación.
{% endstep %}

{% step %}
## Probar operaciones

Ejecutar pruebas de consulta y modificación.
{% endstep %}
{% endstepper %}

Ejemplo para crear una migración:

```bash
dotnet ef migrations add NombreDelCambio --project Infraestructura/Infraestructura.csproj --startup-project Venta/Venta.csproj
```

Aplicar los cambios:

```bash
dotnet ef database update --project Infraestructura/Infraestructura.csproj --startup-project Venta/Venta.csproj
```

### 16.2 Agregar un endpoint

{% stepper %}
{% step %}
## Definir DTO

Definir el DTO de entrada o salida en `Aplicacion/DTO/`.
{% endstep %}

{% step %}
## Definir operación de servicio

Definir la operación en la interfaz correspondiente.

Implementar la operación en el servicio.
{% endstep %}

{% step %}
## Implementar acceso a datos

Implementar o reutilizar el método del repositorio.
{% endstep %}

{% step %}
## Registrar dependencias

Registrar dependencias en `Venta/Program.cs` si se agrega una nueva clase.
{% endstep %}

{% step %}
## Exponer controlador

Exponer la acción en el controlador correspondiente.

Aplicar atributos `[Authorize]` o `[AllowAnonymous]` de acuerdo con el acceso requerido.
{% endstep %}

{% step %}
## Integrar frontend

Agregar el método de consumo en el servicio Angular.

Actualizar la pantalla que lo utiliza.
{% endstep %}

{% step %}
## Probar endpoint

Probar respuestas correctas, errores y permisos.
{% endstep %}
{% endstepper %}

### 16.3 Modificar reglas de negocio

Las reglas se deben modificar en los servicios de `Aplicacion/Servicios/`, no directamente en los componentes visuales. Revisar también las validaciones del controlador y los DTO relacionados.

Servicios centrales:

* `PedidoInternoService`
* `OrdenCompraService`
* `OfertaProveedorService`
* `AdjudicacionService`
* `ProveedorService`
* `ArticuloServicio`
* `AuthService`
* `AuditoriaService`

### 16.4 Modificar reportes

Para reportes JSON, revisar `ReporteRepositorio`, `ReporteControlador`, DTO y componentes Angular. Para PDF, revisar `ReportePdfService` y el endpoint PDF correspondiente.

Cuando la consulta utilice SQL directo, comprobar nombres de tablas, columnas, tipos y compatibilidad con el esquema instalado.

### 16.5 Modificar permisos

Revisar:

* `AuthService.cs`, para los claims y nombres de rol.
* Atributos `[Authorize]` de los controladores.
* Guards de `src/app/guards/`.
* `app.routes.ts`.
* Servicios y componentes que muestran opciones según el rol.

La protección del frontend mejora la navegación, pero no reemplaza la autorización del backend.

### 16.6 Recomendaciones de control de cambios

* Crear una rama antes de modificar componentes centrales.
* Generar migraciones pequeñas y con nombres descriptivos.
* Revisar el SQL generado antes de aplicarlo a una base compartida.
* No modificar manualmente una base productiva sin respaldo.
* Mantener sincronizados los DTO del backend y los modelos TypeScript.
* Actualizar la documentación técnica cuando cambien rutas, configuración, entidades o procesos.
