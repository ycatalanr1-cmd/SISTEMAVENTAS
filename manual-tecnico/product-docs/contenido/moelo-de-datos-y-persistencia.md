---
description: >-
  Explica la estructura de las bases de datos, las entidades principales y
  mecanismos utilizados para almacenar y consultar la información.
icon: folder-heart
---

# MOELO DE DATOS Y PERSISTENCIA

## 6. Modelo de datos y persistencia

### 6.1 Contexto de Entity Framework

El contexto principal se encuentra en:

`Infraestructura/Datos/AplicacionDBContexto.cs`

La clase `AplicacionDBContexto` hereda de `DbContext` y declara los conjuntos `DbSet` que representan las entidades consultables desde Entity Framework Core. En `OnModelCreating` ejecuta `ApplyConfigurationsFromAssembly`, que carga las configuraciones Fluent API del ensamblado.

### 6.2 Entidades registradas en el contexto

| Área                  | Conjuntos de entidades declarados                                                                              |
| --------------------- | -------------------------------------------------------------------------------------------------------------- |
| Organización          | `Sucursal`, `Departamento`, `Direccion`, `Telefono`, `Detalle_Telefono`                                        |
| Artículos y catálogos | `Articulo`, `Unidad_Medida`, `Categoria_Proveedor`, `Rubro`, `Tipo_Orden`                                      |
| Proveedores           | `Proveedor`, `Provee_Artics`, `Provee_Rubro`, `Relacion`                                                       |
| Compras               | `Pedido_Interno`, `Detalle_Pedido`, `Orden_Compra`, `Oferta_Proveedor`, `Adjudicacion`, `Detalle_Adjudicacion` |
| Seguridad             | `Usuarios`, `Roles`, `Permisos`, `Usuarios_Roles`, `Rol_Permiso`                                               |

Los nombres anteriores corresponden a propiedades `DbSet` declaradas en el contexto. Los nombres físicos de tablas y columnas se deben confirmar con las configuraciones de entidades y las migraciones, ya que Entity Framework puede mapear una propiedad a un nombre de tabla diferente.

### 6.3 Relaciones funcionales principales

A partir de las entidades, configuraciones y consultas del repositorio se identifican las siguientes relaciones de dominio:

* Una sucursal agrupa departamentos.
* Los usuarios pueden estar asociados a un departamento y, cuando corresponde, a un proveedor.
* Los pedidos internos pertenecen a un departamento.
* Un pedido puede contener varios detalles de artículos.
* Una orden de compra agrupa pedidos internos mediante la referencia de orden almacenada en el pedido.
* Los proveedores se relacionan con artículos y rubros mediante entidades de asociación.
* Las ofertas se registran para pedidos internos y están asociadas a proveedores.
* Las adjudicaciones contienen detalles de los pedidos adjudicados y el proveedor seleccionado.
* Los usuarios se asocian a roles mediante `Usuarios_Roles`.
* Los roles se relacionan con permisos mediante `Rol_Permiso`.

Estas relaciones describen la estructura lógica que utiliza el código. Para consultar tipos, longitudes, nulabilidad, claves y nombres físicos, revisar las clases de `Aplicacion/modelos/`, las configuraciones de `Infraestructura/Datos/Configuraciones/` y las migraciones.

### 6.4 Migraciones

El proyecto incluye las siguientes migraciones:

* `20260915215548_CleanArchitectureDatabaseCreation`
* `20260918015816_AgregarPKDetalleAdjudicacion`
* `20260921174509_AgregarIdOrdenCompraPedidoInterno`

También incluye `AplicacionDBContextoModelSnapshot.cs`, que representa el estado del modelo utilizado por Entity Framework para comparar cambios y generar nuevas migraciones.

### 6.5 Selección de base de datos

La selección de conexión se realiza en `Venta/Program.cs`.

El contexto revisa el encabezado HTTP `X-Tipo-BD`. Si no se proporciona, utiliza `DatabaseOptions:DefaultBd`; si tampoco existe un valor, el comportamiento predeterminado es `local`.

| Valor de selección | Cadena consultada                  |
| ------------------ | ---------------------------------- |
| `local`            | `ConnectionStrings:LocalSqlServer` |
| `azure`            | `ConnectionStrings:AzureSql`       |

Si la cadena solicitada no está configurada, el código continúa buscando la cadena local. Finalmente existe una cadena local de respaldo definida en el registro del contexto.

El frontend contiene la pantalla `seleccion-bd` y el servicio `bd.service.ts`, relacionados con la selección de destino. El encabezado permite que la API elija una configuración SQL para la solicitud.

{% hint style="warning" %}
`ReportePdfService` obtiene `LocalSqlServer` directamente desde la configuración. Por ello, los PDF generados por este servicio utilizan la conexión local configurada y no necesariamente el destino seleccionado por `X-Tipo-BD`.
{% endhint %}

### 6.6 Vista de órdenes activas

`Infraestructura/Repositorio/ReporteRepositorio.cs` contiene una consulta SQL que lee `Vista_OrdenesActivas` y obtiene los campos `Id`, `Descripcion`, `Fecha_Creacion` y `Fecha_Limite`.

La vista debe existir en la base de datos a la que se conecte el repositorio para que la consulta se ejecute correctamente. Si se modifica la vista, se debe revisar también el DTO utilizado por el reporte.
