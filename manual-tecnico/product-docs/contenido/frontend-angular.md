---
description: >-
  Presenta la estructura de la interfaz gráfica, sus componentes, módulos, rutas
  y servicios encargados de la interacción con el usuario.
icon: code
---

# FRONTEND ANGULAR

## 8. Frontend Angular

### 8.1 Inicio y configuración

El frontend se encuentra en `proyecto-ventas-front/`. El archivo `package.json` define los comandos:

| Comando         | Acción                                                    |
| --------------- | --------------------------------------------------------- |
| `npm start`     | Inicia Angular en el puerto 4200.                         |
| `npm run build` | Compila la aplicación para producción.                    |
| `npm run watch` | Compila en modo de desarrollo con observación de cambios. |
| `npm test`      | Ejecuta la configuración de pruebas del proyecto.         |

La URL base de la API se encuentra en:

* `src/environments/environment.ts`
* `src/environments/environment.development.ts`

Ambos archivos declaran `http://localhost:5000/api`.

### 8.2 Rutas de navegación

Las rutas se definen en `src/app/app.routes.ts`.

| Ruta Angular                     | Módulo o pantalla                       |
| -------------------------------- | --------------------------------------- |
| `/seleccion-bd`                  | Selección del destino de base de datos. |
| `/login`                         | Inicio de sesión.                       |
| `/admin/dashboard`               | Panel de administración.                |
| `/admin/articulos`               | Catálogo de artículos.                  |
| `/admin/usuarios`                | Administración de usuarios.             |
| `/admin/sucursales`              | Administración de sucursales.           |
| `/admin/departamentos`           | Administración de departamentos.        |
| `/admin/rubros`                  | Catálogo de rubros.                     |
| `/admin/proveedores`             | Administración de proveedores.          |
| `/admin/roles`                   | Administración de roles.                |
| `/admin/tipos-orden`             | Tipos de orden.                         |
| `/admin/unidades-medida`         | Unidades de medida.                     |
| `/admin/categorias-proveedor`    | Categorías de proveedores.              |
| `/admin/ordenes-compra`          | Órdenes de compra.                      |
| `/admin/reportes`                | Reportes administrativos.               |
| `/admin/adjudicaciones`          | Adjudicaciones.                         |
| `/admin/pedidos-internos`        | Pedidos internos.                       |
| `/admin/auditoria`               | Consulta de auditoría.                  |
| `/creador/pedidos`               | Pedidos del creador.                    |
| `/creador/ordenes-compra`        | Órdenes visibles para el creador.       |
| `/auditor/reportes`              | Reportes para auditoría.                |
| `/auditor/auditoria`             | Consulta de historial.                  |
| `/empleado/pedidos`              | Pedidos para gestor de compras.         |
| `/empleado/ordenes-compra`       | Órdenes para gestor de compras.         |
| `/empleado/adjudicaciones`       | Gestión de adjudicaciones.              |
| `/proveedor/ofertas`             | Ofertas del proveedor.                  |
| `/proveedor/pedidos-disponibles` | Pedidos disponibles para ofertar.       |
| `/perfil`                        | Perfil del usuario autenticado.         |

### 8.3 Guards

Los guards están en `src/app/guards/`. Entre los identificados se encuentran:

* `authGuard`
* `adminGuard`
* `empleadoGuard`
* `proveedorGuard`
* `auditorGuard`
* `creadorGuard`

Su función es controlar el acceso a las rutas de Angular según la sesión y el perfil del usuario. La autorización real de las operaciones también se valida en la API mediante los atributos de autorización de ASP.NET Core.

### 8.4 Servicios frontend

Los servicios de `src/app/services/` concentran la comunicación con la API. Entre ellos:

* `auth.service.ts`
* `bd.service.ts`
* `articulo.service.ts`
* `sucursal.service.ts`
* `departamento.service.ts`
* `proveedor.service.ts`
* `pedido-interno.service.ts`
* `orden-compra.service.ts`
* `oferta-proveedor.service.ts`
* `adjudicacion.service.ts`
* `reporte.service.ts`
* `reporte-pdf.service.ts`
* `auditoria.service.ts`
* `jasper.service.ts`
* `usuario.service.ts`
* `rol.service.ts`
* `rubro.service.ts`
* `unidad-medida.service.ts`

Cuando se agregue una operación en el backend, debe revisarse si requiere un método equivalente en el servicio Angular y su integración en el componente correspondiente.
