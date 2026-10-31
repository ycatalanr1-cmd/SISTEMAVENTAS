---
description: Facilita la ubicación de clases en el código.
icon: boxes-stacked
---

# INVENTARIO DE COMPONENTES Y CONTRATOS

## 19

. Inventario de componentes y contratos

Esta sección facilita ubicar clases en el código. La presencia de una clase no implica que todas sus acciones hayan sido ejecutadas en una prueba integral.

### 19.1 Controladores de la API

Ruta del código: `Venta/Controllers/`. La mayoría de estas clases extienden `ControllerBase` y vinculan métodos HTTP con servicios de aplicación. Para conocer parámetros exactos de cada acción, inspeccionar `[HttpGet]`, `[HttpPost]`, `[HttpPut]`, `[HttpDelete]`, `[FromQuery]`, `[FromRoute]` y `[FromBody]`.

| Controlador                         | Área técnica         |
| ----------------------------------- | -------------------- |
| `AdjudicacionControlador.cs`        | Identidad y permisos |
| `ArticuloControlador.cs`            | Identidad y permisos |
| `AuditoriaControlador.cs`           | Identidad y permisos |
| `AuthControlador.cs`                | Identidad y permisos |
| `CategoriaProveedorControlador.cs`  | Identidad y permisos |
| `DepartamentoControlador.cs`        | Identidad y permisos |
| `DetalleAdjudicacionControlador.cs` | Identidad y permisos |
| `DetallePedidoControlador.cs`       | Identidad y permisos |
| `DetalleTelefonoControlador.cs`     | Identidad y permisos |
| `DireccionControlador.cs`           | Identidad y permisos |
| `OfertaProveedorControlador.cs`     | Identidad y permisos |
| `OrdenCompraControlador.cs`         | Identidad y permisos |
| `PedidoInternoControlador.cs`       | Identidad y permisos |
| `PerfilControlador.cs`              | Identidad y permisos |
| `PermisosControlador.cs`            | Identidad y permisos |
| `ProveeArticControlador.cs`         | Identidad y permisos |
| `ProveeRubroControlador.cs`         | Identidad y permisos |
| `ProveedorControlador.cs`           | Identidad y permisos |
| `RelacionControlador.cs`            | Identidad y permisos |
| `ReporteControlador.cs`             | Identidad y permisos |
| `RolPermisoControlador.cs`          | Identidad y permisos |
| `RolesControlador.cs`               | Identidad y permisos |
| `RubroControlador.cs`               | Identidad y permisos |
| `SucursalControlador.cs`            | Identidad y permisos |
| `TelefonoControlador.cs`            | Identidad y permisos |
| `TipoOrdenControlador.cs`           | Identidad y permisos |
| `UnidadMedidaControlador.cs`        | Identidad y permisos |
| `UsuarioControlador.cs`             | Identidad y permisos |
| `UsuariosRolesControlador.cs`       | Identidad y permisos |

### 19.2 Servicios de aplicación

Ubicación: `Aplicacion/Servicios/`. Los servicios coordinan validaciones, reglas y operaciones de persistencia. `ReportePdfService` genera archivos PDF y `AuthService` administra la validación de credenciales y emisión de JWT.

| Servicio                        | Finalidad principal                         |
| ------------------------------- | ------------------------------------------- |
| `AdjudicacionService.cs`        | Operaciones del módulo Adjudicacion         |
| `ArticuloServicio.cs`           | Operaciones del módulo Articulo             |
| `AuditoriaService.cs`           | Consulta de historiales MongoDB             |
| `AuthService.cs`                | Validación de credenciales y emisión de JWT |
| `CategoriaProveedorService.cs`  | Operaciones del módulo CategoriaProveedor   |
| `DepartamentoService.cs`        | Operaciones del módulo Departamento         |
| `DetalleAdjudicacionService.cs` | Operaciones del módulo DetalleAdjudicacion  |
| `DetallePedidoService.cs`       | Operaciones del módulo DetallePedido        |
| `DetalleTelefonoService.cs`     | Operaciones del módulo DetalleTelefono      |
| `DireccionService.cs`           | Operaciones del módulo Direccion            |
| `OfertaProveedorService.cs`     | Operaciones del módulo OfertaProveedor      |
| `OrdenCompraService.cs`         | Operaciones del módulo OrdenCompra          |
| `PedidoInternoService.cs`       | Operaciones del módulo PedidoInterno        |
| `PermisosService.cs`            | Operaciones del módulo Permisos             |
| `ProveeArticService.cs`         | Operaciones del módulo ProveeArtic          |
| `ProveeRubroService.cs`         | Operaciones del módulo ProveeRubro          |
| `ProveedorService.cs`           | Operaciones del módulo Proveedor            |
| `RelacionService.cs`            | Operaciones del módulo Relacion             |
| `ReportePdfService.cs`          | Generación de reportes PDF                  |
| `RolPermisoService.cs`          | Operaciones del módulo RolPermiso           |
| `RolesService.cs`               | Operaciones del módulo Roles                |
| `RubroService.cs`               | Operaciones del módulo Rubro                |
| `SucursalService.cs`            | Operaciones del módulo Sucursal             |
| `TelefonoService.cs`            | Operaciones del módulo Telefono             |
| `TipoOrdeService.cs`            | Operaciones del módulo TipoOrde             |
| `UnidadMedidaService.cs`        | Operaciones del módulo UnidadMedida         |
| `UsuarioService.cs`             | Operaciones del módulo Usuario              |
| `UsuariosRolesService.cs`       | Operaciones del módulo UsuariosRoles        |

### 19.3 Repositorios concretos

Ubicación: `Infraestructura/Repositorio/`. Estas implementaciones encapsulan operaciones de lectura y escritura en la capa de datos. Los contratos correspondientes se encuentran principalmente en `Aplicacion/Repositorio/`.

* `AdRepositorio.cs`
* `ArticuloRepositorio.cs`
* `CatProvRepositorioImpl.cs`
* `DeARepositorio.cs`
* `DeTeRepositorio.cs`
* `DepaRepositorio.cs`
* `DetPedRepositorio.cs`
* `DetaTelRepositorioImpl.cs`
* `DireRepositorio.cs`
* `OfeProRepositorio.cs`
* `OrCoRepositorio.cs`
* `PeInRepositorio.cs`
* `PermRepositorio.cs`
* `ProArRepositorio.cs`
* `ProvRubRepositorio.cs`
* `ProveRepositorio.cs`
* `RelaRepositorio.cs`
* `ReporteRepositorio.cs`
* `RolPeRepositorio.cs`
* `RolRepositorio.cs`
* `RubrRepositorio.cs`
* `SucurRepositorio.cs`
* `TelRepositorio.cs`
* `TiOrRepositorio.cs`
* `UniMedRepositorio.cs`
* `UsRoRepositorio.cs`
* `UsuarRepositorio.cs`

### 19.4 Objetos de transferencia de datos (DTO)

El directorio `Aplicacion/DTO/` contiene clases de recepción, actualización y respuesta. Ejemplos: `AuthDTO.cs`, `PedidoInternoDTO.cs`, `CreateOrdenCompraDTO.cs`, `AdjudicarPedidosDTO.cs`, `CreateOfertaProveedorDTO.cs` y `ActUsuariosDTO.cs`.

Al cambiar propiedades de un DTO deben revisarse el servicio que lo usa, los perfiles de `Aplicacion/Maping/MappingPerfil.cs`, los métodos de controlador correspondientes y las interfaces TypeScript del frontend. Evitar suponer que un DTO equivale exactamente a una tabla física.
