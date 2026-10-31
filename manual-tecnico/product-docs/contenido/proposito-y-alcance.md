---
description: >-
  Finalidad del manual, su alcance y el tipo de información técnica que
  proporciona al personal encargado del desarrollo, administración y
  mantenimiento del sistema.
icon: github
---

# PROPÓSITO Y ALCANCE

## 1. Propósito y alcance

Este documento está dirigido a desarrolladores, ingenieros de software, administradores de bases de datos y personal técnico que necesite conocer la estructura interna de SistemaVentas para instalarlo, configurarlo, ejecutarlo, diagnosticarlo, mantenerlo o modificarlo.

El manual describe la implementación que se encuentra en el código fuente del proyecto. Explica cómo se distribuyen las responsabilidades entre el frontend, la API, la capa de aplicación, los repositorios y los motores de persistencia; identifica los módulos funcionales; documenta las rutas HTTP; y proporciona procedimientos para preparar el entorno de desarrollo.

El dominio funcional implementado se enfoca en la **gestión de adquisiciones y compras**. El flujo principal comprende solicitudes internas de artículos, agrupación de pedidos en órdenes de compra, recepción de ofertas de proveedores, adjudicación y consulta de reportes.

### 1.1 Fuentes técnicas utilizadas

La información se obtiene de los siguientes elementos del proyecto:

* Solución .NET `ProyectoVentas.slnx`.
* Proyectos `Venta`, `Aplicacion` e `Infraestructura`.
* Controladores, servicios, repositorios, DTO, modelos y configuraciones de Entity Framework Core.
* Migraciones y snapshot del modelo de Entity Framework.
* `Program.cs` y archivos `appsettings`.
* Aplicación Angular, sus rutas, guards, interceptores, modelos y servicios.
* `package.json`, `angular.json` y archivos de configuración del frontend.
* README y documentación ubicados en `docs/` dentro del repositorio.

Cuando una operación depende de un servicio externo o de un objeto de base de datos, se explica la dependencia para que el personal técnico pueda configurarla y comprobarla en su ambiente.
