---
description: >-
  Documenta los controladores, rutas y operaciones disponibles para la
  comunicación entre el frontend y el backend.
icon: cloud
---

# API REST

## 9. API REST

### 9.1 Convenciones generales

Los controladores se encuentran en `Venta/Controllers/`. La mayoría utiliza:

```csharp
[Route("api/[controller]")]
[ApiController]
```

ASP.NET Core sustituye `[controller]` por el nombre de la clase sin el sufijo literal `Controller`. En este proyecto las clases se denominan, por ejemplo, `AuthControlador` y `ReporteControlador`; por ello, sus rutas son `api/AuthControlador` y `api/ReporteControlador`.

La dirección base configurada en Angular es:

`http://localhost:5000/api`

Por tanto, una ruta relativa `AuthControlador/login` se invoca como:

`http://localhost:5000/api/AuthControlador/login`

Los métodos utilizan los verbos HTTP `GET`, `POST`, `PUT` y `DELETE`.

### 9.2 Autenticación

| Método | Ruta                         | Descripción                                                      |
| ------ | ---------------------------- | ---------------------------------------------------------------- |
| POST   | `/api/AuthControlador/login` | Valida credenciales y devuelve el token JWT y datos del usuario. |

El cuerpo de la solicitud utiliza `LoginDTO`, con correo y contraseña. Si las credenciales son incorrectas, la API responde con HTTP 401.

### 9.3 Recursos organizacionales y catálogos

Los controladores CRUD utilizan, de forma general, `GET` para listar, `GET /{id}` para consultar un registro, `POST` para crear, `PUT` para actualizar y `DELETE /{id}` para eliminar. Los parámetros compuestos se indican expresamente.

| Controlador                     | Prefijo de ruta                      | Operaciones adicionales o identificadores               |
| ------------------------------- | ------------------------------------ | ------------------------------------------------------- |
| `SucursalControlador`           | `/api/SucursalControlador`           | CRUD por identificador.                                 |
| `DepartamentoControlador`       | `/api/DepartamentoControlador`       | CRUD por identificador.                                 |
| `DireccionControlador`          | `/api/DireccionControlador`          | CRUD por identificador.                                 |
| `TelefonoControlador`           | `/api/TelefonoControlador`           | CRUD por identificador.                                 |
| `DetalleTelefonoControlador`    | `/api/DetalleTelefonoControlador`    | Consulta y eliminación por `{idSucursal}/{idTelefono}`. |
| `ArticuloControlador`           | `/api/ArticuloControlador`           | Incluye `GET /por-rubro/{idRubro}`.                     |
| `RubroControlador`              | `/api/RubroControlador`              | CRUD por identificador.                                 |
| `CategoriaProveedorControlador` | `/api/CategoriaProveedorControlador` | CRUD por identificador.                                 |
| `UnidadMedidaControlador`       | `/api/UnidadMedidaControlador`       | CRUD por identificador.                                 |
| `TipoOrdenControlador`          | `/api/TipoOrdenControlador`          | CRUD por identificador.                                 |

### 9.4 Proveedores y asociaciones

| Controlador              | Prefijo de ruta               | Operaciones relevantes                                                               |
| ------------------------ | ----------------------------- | ------------------------------------------------------------------------------------ |
| `ProveedorControlador`   | `/api/ProveedorControlador`   | CRUD; `POST /{idProveedor}/asignar-articulos`.                                       |
| `ProveeArticControlador` | `/api/ProveeArticControlador` | Asociación proveedor-artículo; identificador compuesto `{idProveedor}/{idArticulo}`. |
| `ProveeRubroControlador` | `/api/ProveeRubroControlador` | Asociación proveedor-rubro; incluye `DELETE /por-proveedor/{idProveedor}`.           |
| `RelacionControlador`    | `/api/RelacionControlador`    | Consulta general, creación y eliminación por ID.                                     |

### 9.5 Pedidos internos

Prefijo: `/api/PedidoInternoControlador`

| Método | Ruta                                                              | Descripción                                                |
| ------ | ----------------------------------------------------------------- | ---------------------------------------------------------- |
| GET    | `/api/PedidoInternoControlador`                                   | Lista pedidos.                                             |
| GET    | `/api/PedidoInternoControlador/{id}`                              | Consulta un pedido.                                        |
| POST   | `/api/PedidoInternoControlador`                                   | Crea un pedido.                                            |
| PUT    | `/api/PedidoInternoControlador`                                   | Actualiza un pedido.                                       |
| DELETE | `/api/PedidoInternoControlador/{id}`                              | Elimina un pedido.                                         |
| GET    | `/api/PedidoInternoControlador/por-departamento/{idDepartamento}` | Consulta pedidos de un departamento.                       |
| GET    | `/api/PedidoInternoControlador/disponibles-para-proveedor`        | Obtiene pedidos disponibles para el proveedor autenticado. |

### 9.6 Órdenes de compra

Prefijo: `/api/OrdenCompraControlador`

| Método | Ruta                                         | Descripción                                                  |
| ------ | -------------------------------------------- | ------------------------------------------------------------ |
| GET    | `/api/OrdenCompraControlador`                | Lista órdenes.                                               |
| GET    | `/api/OrdenCompraControlador/{id}`           | Consulta una orden.                                          |
| POST   | `/api/OrdenCompraControlador`                | Crea una orden.                                              |
| PUT    | `/api/OrdenCompraControlador`                | Actualiza una orden.                                         |
| DELETE | `/api/OrdenCompraControlador/{id}`           | Elimina una orden.                                           |
| GET    | `/api/OrdenCompraControlador/con-contadores` | Obtiene órdenes con cantidades de pedidos y datos asociados. |
| GET    | `/api/OrdenCompraControlador/{id}/pedidos`   | Consulta pedidos asociados a una orden.                      |
| PUT    | `/api/OrdenCompraControlador/{id}/aprobar`   | Aprueba una orden.                                           |
| PUT    | `/api/OrdenCompraControlador/{id}/publicar`  | Publica una orden.                                           |
| PUT    | `/api/OrdenCompraControlador/{id}/cerrar`    | Cierra una orden.                                            |
| PUT    | `/api/OrdenCompraControlador/{id}/cancelar`  | Cancela una orden.                                           |

### 9.7 Ofertas

Prefijo: `/api/OfertaProveedorControlador`

| Método | Ruta                                          | Descripción                                                    |
| ------ | --------------------------------------------- | -------------------------------------------------------------- |
| GET    | `/api/OfertaProveedorControlador`             | Consulta ofertas.                                              |
| GET    | `/api/OfertaProveedorControlador/{id}`        | Consulta una oferta.                                           |
| GET    | `/api/OfertaProveedorControlador/mis-ofertas` | Consulta ofertas del proveedor autenticado.                    |
| POST   | `/api/OfertaProveedorControlador/ofertar`     | Registra una oferta desde el flujo de proveedor.               |
| POST   | `/api/OfertaProveedorControlador`             | Crea una oferta mediante la operación general del controlador. |
| PUT    | `/api/OfertaProveedorControlador`             | Actualiza una oferta.                                          |
| DELETE | `/api/OfertaProveedorControlador/{id}`        | Elimina una oferta.                                            |

### 9.8 Adjudicaciones y detalles

| Controlador                      | Prefijo                               | Operaciones                                                                |
| -------------------------------- | ------------------------------------- | -------------------------------------------------------------------------- |
| `AdjudicacionControlador`        | `/api/AdjudicacionControlador`        | CRUD y `POST /adjudicar` para adjudicar pedidos.                           |
| `DetalleAdjudicacionControlador` | `/api/DetalleAdjudicacionControlador` | CRUD; identificador compuesto `{idAdjudicacion}/{idPedido}/{idProveedor}`. |
| `DetallePedidoControlador`       | `/api/DetallePedidoControlador`       | CRUD; identificador compuesto `{idPedido}/{idArticulo}`.                   |

### 9.9 Usuarios, roles y permisos

| Controlador                | Prefijo                         | Operaciones                                                                      |
| -------------------------- | ------------------------------- | -------------------------------------------------------------------------------- |
| `UsuarioControlador`       | `/api/UsuarioControlador`       | CRUD; consulta y actualización de permisos de usuario mediante `/{id}/permisos`. |
| `RolesControlador`         | `/api/RolesControlador`         | CRUD.                                                                            |
| `PermisosControlador`      | `/api/PermisosControlador`      | CRUD.                                                                            |
| `UsuariosRolesControlador` | `/api/UsuariosRolesControlador` | CRUD; identificador `{idUsuario}/{idRol}`.                                       |
| `RolPermisoControlador`    | `/api/RolPermisoControlador`    | CRUD; identificador `{idRol}/{idPermiso}`.                                       |
| `PerfilControlador`        | `/api/PerfilControlador`        | Consulta y actualización del perfil; `POST /cambiar-contrasena`.                 |

### 9.10 Reportes

Prefijo: `/api/ReporteControlador`

| Método | Ruta                                            | Parámetros                                |
| ------ | ----------------------------------------------- | ----------------------------------------- |
| GET    | `/historial-articulo/{idArticulo}`              | Identificador del artículo.               |
| GET    | `/ranking-proveedores`                          | Parámetros de consulta `desde` y `hasta`. |
| GET    | `/ofertas-orden/{idOrdenCompra}`                | Identificador de orden.                   |
| GET    | `/pedidos-pendientes`                           | Sin parámetros de ruta.                   |
| GET    | `/ordenes-activas`                              | Sin parámetros de ruta.                   |
| GET    | `/gasto-departamental/{idSucursal}/{anio}`      | Sucursal y año.                           |
| GET    | `/eficiencia-proceso`                           | Sin parámetros de ruta.                   |
| GET    | `/variacion-precios/{idArticulo}/{idProveedor}` | Artículo y proveedor.                     |

Los métodos de consulta JSON de estos reportes tienen autorización por roles `Administrador`, `Auditor` y `GestorCompras`.

### 9.11 Reportes PDF

El controlador también publica rutas PDF:

* `GET /api/ReporteControlador/pdf/ranking-proveedores`
* `GET /api/ReporteControlador/pdf/gasto-departamental`
* `GET /api/ReporteControlador/pdf/ordenes-activas`
* `GET /api/ReporteControlador/pdf/pedidos-pendientes`
* `GET /api/ReporteControlador/pdf/historial-articulo`
* `GET /api/ReporteControlador/pdf/ofertas-orden`
* `GET /api/ReporteControlador/pdf/eficiencia-proceso`
* `GET /api/ReporteControlador/pdf/variacion-precios`



### 9.12 Auditoría

| Método | Ruta                                  | Descripción                         |
| ------ | ------------------------------------- | ----------------------------------- |
| GET    | `/api/AuditoriaControlador/historial` | Consulta el historial de auditoría. |

La consulta recibe los filtros que define la acción del controlador y devuelve los eventos disponibles para el usuario autorizado.

### 9.13 Documentación interactiva de la API

Swagger se registra en `Program.cs` y se habilita mediante `UseSwagger()` y `UseSwaggerUI()`. La ruta raíz `/` redirige a `/swagger`.

En el ambiente de desarrollo, Swagger permite consultar las operaciones expuestas y probar solicitudes. Para rutas protegidas se debe utilizar un token JWT válido en el esquema Bearer.
