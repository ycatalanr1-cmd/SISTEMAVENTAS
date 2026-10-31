---
description: >-
  Describe las reglas de negocio y los procedimientos que controlan las
  operaciones principales del sistema.
icon: handshake
---

# LÓGICA DE NEGOCIO Y PROCESOS PRINCIPALES

## 7. Lógica de negocio y procesos principales

Los servicios se encuentran en `Aplicacion/Servicios/`. Cada servicio coordina operaciones de una entidad o módulo y utiliza repositorios para acceder a los datos.

### 7.1 Autenticación

Archivo: `AuthService.cs`.

{% stepper %}
{% step %}
## Validar contenido de credenciales

Comprueba que el correo y la contraseña tengan contenido.
{% endstep %}

{% step %}
## Buscar usuario activo

Busca un usuario cuyo correo coincida y que se encuentre activo.
{% endstep %}

{% step %}
## Verificar contraseña

Verifica la contraseña con `BCrypt.Net.BCrypt.Verify`.
{% endstep %}

{% step %}
## Generar token

Genera un token JWT.
{% endstep %}

{% step %}
## Devolver respuesta de autenticación

Devuelve un objeto `AuthResponseDTO` con el token y los datos básicos del usuario.

Si las credenciales no coinciden o el usuario no está activo, devuelve un resultado nulo que el controlador transforma en respuesta HTTP 401.
{% endstep %}
{% endstepper %}

### 7.2 Pedidos internos

Archivos principales:

* `PedidoInternoControlador.cs`
* `PedidoInternoService.cs`
* `PedIntRepositorio.cs`
* `Pedido_Interno.cs`
* DTO de pedidos y detalles.

El servicio permite crear, consultar, actualizar y eliminar pedidos. También obtiene pedidos por departamento y los disponibles para un proveedor.

En la consulta general se reúnen datos relacionados con departamentos, sucursales, ofertas, adjudicaciones, proveedores, detalles de pedido y artículos. El resultado incluye información complementaria para presentar el pedido en el frontend, como el total de ofertas y si existe adjudicación.

El método de consulta de pedidos disponibles recibe el identificador de proveedor obtenido desde el claim `IdProveedor` del token.

### 7.3 Órdenes de compra

Archivos principales:

* `OrdenCompraControlador.cs`
* `OrdenCompraService.cs`
* `OrdComRepositorio.cs`
* `Orden_Compra.cs`

El servicio permite registrar y consultar órdenes, obtener los pedidos asociados y consultar contadores para la pantalla de gestión.

Al crear una orden, el servicio:

* Convierte el DTO a la entidad mediante AutoMapper.
* Obtiene el identificador siguiente a partir del mayor identificador existente.
* Completa `fecha_limite_ofertas` con `Fecha_Limite` cuando no se proporciona.
* Asigna el usuario creador.
* Establece el estado inicial `Borrador`.
* Guarda la orden mediante el repositorio.
* Intenta publicar el evento `OrdenCreada`.

El servicio incluye operaciones para aprobar, publicar, cerrar y cancelar órdenes. Las acciones de estado tienen rutas específicas en el controlador.

En la consulta `GetConContadoresAsync`, el resultado se filtra según el rol: los creadores consultan órdenes creadas por ellos; los gestores pueden ver las órdenes vinculadas a su ámbito departamental/sucursal; y el administrador de proveedor consulta órdenes publicadas o adjudicadas.

### 7.4 Ofertas de proveedores

Archivos principales:

* `OfertaProveedorControlador.cs`
* `OfertaProveedorService.cs`
* `OferProvRepositorio.cs`
* `Oferta_Proveedor.cs`

El módulo administra el registro y consulta de ofertas. Incluye operaciones para consultar ofertas, consultar ofertas propias y registrar una oferta mediante la ruta `ofertar`.

El controlador aplica restricciones de rol: el registro de ofertas está destinado al rol `AdministradorProveedor`; la consulta de ofertas propias también está asociada a ese rol, con acceso adicional del administrador.

### 7.5 Adjudicaciones

Archivos principales:

* `AdjudicacionControlador.cs`
* `AdjudicacionService.cs`
* `AdjuRepositorio.cs`
* `DetaAdjRepositorio.cs`
* `Adjudicacion.cs`
* `Detalle_Adjudicacion.cs`

El servicio valida que la orden indicada exista y que la fecha de resolución no sea anterior a la fecha de creación de la orden.

El método `AdjudicarPedidosAsync` requiere que se seleccione al menos un pedido, comprueba que la orden exista y revisa que el pedido no tenga una adjudicación previa. También consulta las ofertas disponibles para realizar las validaciones correspondientes antes de registrar los detalles de adjudicación.

La adjudicación se representa mediante una entidad principal y detalles asociados a pedidos y proveedores.

### 7.6 Proveedores y catálogos

Los servicios de proveedores, artículos, rubros, categorías, unidades de medida y tipos de orden permiten mantener los datos que utilizan los procesos de compra.

También existen servicios para las relaciones entre proveedores y artículos, y entre proveedores y rubros. Estas asociaciones permiten determinar qué artículos o categorías corresponden a cada proveedor.

### 7.7 Mapeo de datos

El proyecto registra AutoMapper desde `Program.cs` utilizando el ensamblado que contiene los perfiles. Los perfiles se encuentran en `Aplicacion/Maping/MappingPerfil.cs`.

El propósito es convertir objetos recibidos o devueltos por la API en entidades y DTO, evitando realizar todas las asignaciones de propiedades manualmente en cada controlador.
