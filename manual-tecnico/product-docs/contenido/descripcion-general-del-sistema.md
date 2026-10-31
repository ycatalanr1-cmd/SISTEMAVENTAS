---
description: >-
  Presenta una visión general de SistemaVentas, sus principales funcionalidades
  y los procesos que permite gestionar dentro de la organización.
icon: bolt
---

# DESCRIPCIÓN GENERAL DEL SISTEMA

## 2. Descripción general del sistema

SistemaVentas centraliza información relacionada con el proceso de compras de una organización. Sus datos se organizan alrededor de sucursales, departamentos, usuarios, artículos, proveedores, rubros, pedidos internos, órdenes de compra, ofertas y adjudicaciones.

### 2.1 Módulos funcionales identificados

| Módulo                   | Responsabilidad técnica y funcional                                                                                                                |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Autenticación            | Valida las credenciales del usuario y genera un token JWT.                                                                                         |
| Usuarios y roles         | Administra usuarios, roles, asignación de roles y permisos.                                                                                        |
| Organización             | Administra sucursales, departamentos, direcciones, teléfonos y sus relaciones.                                                                     |
| Catálogos                | Administra artículos, unidades de medida, rubros, categorías de proveedores y tipos de orden.                                                      |
| Proveedores              | Mantiene información de proveedores y sus relaciones con artículos y rubros.                                                                       |
| Pedidos internos         | Registra solicitudes de artículos realizadas por los departamentos.                                                                                |
| Órdenes de compra        | Agrupa pedidos y permite gestionar estados como borrador, aprobada, publicada, cerrada, cancelada o adjudicada según las operaciones del servicio. |
| Ofertas                  | Permite registrar y consultar propuestas económicas de proveedores.                                                                                |
| Adjudicaciones           | Registra la selección de proveedores para pedidos y sus detalles económicos.                                                                       |
| Informes                 | Consulta información histórica, comparativa y estadística del proceso de compra.                                                                   |
| Informes en fformato PDF | Genera documentos PDF mediante QuestPDF y consultas SQL.                                                                                           |
| Auditoría                | Consulta historiales de operaciones almacenados mediante MongoDB.                                                                                  |

### 2.2 Flujo general de compras

{% stepper %}
{% step %}
## Registrar un pedido interno

Un usuario con perfil habilitado registra un pedido interno y sus artículos.

El pedido queda asociado al departamento correspondiente.
{% endstep %}

{% step %}
## Organizar pedidos en una orden de compra

El personal encargado organiza pedidos dentro de una orden de compra.


{% endstep %}

{% step %}
### Aprobar y publicar la orden

La orden puede aprobarse y publicarse para que los proveedores consulten los pedidos disponibles.
{% endstep %}

{% step %}
## Registrar ofertas de proveedores

Los proveedores registrados envían ofertas para los pedidos que les corresponden.
{% endstep %}

{% step %}
## Registrar la adjudicación

El personal autorizado revisa las ofertas y registra la adjudicación.
{% endstep %}

{% step %}
## Consultar resultados

El sistema permite consultar el resultado mediante los módulos operativos, reportes y registros históricos.
{% endstep %}
{% endstepper %}

El detalle de las validaciones, transiciones de estado y reglas aplicadas se encuentra principalmente en `PedidoInternoService.cs`, `OrdenCompraService.cs`, `OfertaProveedorService.cs` y `AdjudicacionService.cs`.
