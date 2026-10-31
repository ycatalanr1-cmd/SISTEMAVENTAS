---
icon: book-open-cover
---

# MANUAL TÉCNICO

## Introducción

Este manual explica la organización interna de SistemaVentas para que otro estudiante o desarrollador pueda identificar dónde se procesan las solicitudes, cómo se consultan los datos y qué archivos modificar cuando se necesite ampliar el sistema. Aquí se documentan las decisiones y componentes técnicos visibles en el código.

Las entidades y procesos desarrollados se concentran en **adquisiciones**: sucursales, departamentos, artículos, proveedores, pedidos internos, órdenes de compra, ofertas y adjudicaciones.

***

## Control del documento

| Elemento                  | Descripción                                                                                                                                                                                |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Sistema                   | SistemaVentas                                                                                                                                                                              |
| Propósito                 | Gestión del proceso de compras: pedidos internos, órdenes de compra, ofertas de proveedores, adjudicaciones, reportes y auditoría                                                          |
| Fuentes técnicas          | Código fuente del `ProyectoVenta-main` y repositorio GitHub [https://github.com/eduardomorales073-collab/ProyectoVenta.git](https://github.com/eduardomorales073-collab/ProyectoVenta.git) |
| Componentes principales   | API ASP.NET Core, capa de aplicación, infraestructura de datos y frontend Angular                                                                                                          |
| Persistencia              | SQL Server / Azure SQL para datos operativos; MongoDB para historiales                                                                                                                     |
| Mensajería                | RabbitMQ mediante MassTransit                                                                                                                                                              |
| Documentación relacionada | `docs/MANUAL_USUARIO.md` y `docs/MANUAL_INSTALACION.md`                                                                                                                                    |
