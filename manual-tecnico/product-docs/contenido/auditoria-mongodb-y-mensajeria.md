---
description: >-
  Explica cómo se gestionan los registros históricos, el almacenamiento de
  información de auditoría y la comunicación mediante mensajería.
icon: magnifying-glass-chart
---

# AUDITORÍA, MONGODB Y MENSAJERÍA

## 12. Auditoría, MongoDB y mensajería

### 12.1 MongoDB

La configuración de MongoDB se realiza en `Venta/Program.cs`. La base de datos utilizada por el código es `LogsDB`.

Se registran colecciones para:

| Colección                           | Clase asociada                 |
| ----------------------------------- | ------------------------------ |
| `compras_historial`                 | `CompraHistorial`              |
| `pedidos_historial`                 | `PedidoHistorial`              |
| `ofertas_historial`                 | `OfertaHistorial`              |
| `ordenes_historial`                 | `OrdenHistorial`               |
| `cancelaciones_historial`           | `CancelacionHistorial`         |
| `adjudicaciones_historial`          | `AdjudicacionHistorial`        |
| `pedidos_actualizaciones_historial` | `PedidoActualizacionHistorial` |
| `ofertas_actualizaciones_historial` | `OfertaActualizacionHistorial` |

`AuditoriaService.cs` implementa la consulta de historiales y transforma los registros a los DTO utilizados por el controlador.

{% hint style="info" %}
La configuración utiliza tiempos de espera breves para la selección de servidor, conexión y socket. El registro del cliente y de las colecciones no equivale por sí solo a comprobar que el servidor MongoDB esté disponible; la disponibilidad debe comprobarse durante la puesta en marcha.
{% endhint %}

### 12.2 Eventos

Los tipos de eventos se encuentran en `Aplicacion/Mensajeria/Eventos/`.

Entre los eventos definidos se incluyen:

* `CompraRegistrada`
* `PedidoCreado`
* `PedidoActualizado`
* `PedidoCancelado`
* `OrdenCreada`
* `OfertaRegistrada`
* `OfertaActualizada`
* `AdjudicacionCreada`

### 12.3 Consumidores

Los consumidores se encuentran en `Aplicacion/Mensajeria/Consumidores/`.

Entre ellos:

* `CompraRegistradaConsumer`
* `PedidoCreadoConsumer`
* `PedidoActualizadoConsumer`
* `PedidoCanceladoConsumer`
* `OrdenCreadaConsumer`
* `OfertaRegistradaConsumer`
* `OfertaActualizadaConsumer`
* `AdjudicacionCreadaConsumer`

Cada consumidor procesa el tipo de evento correspondiente y utiliza el servicio de auditoría o la colección de historial relacionada.

### 12.4 Configuración de RabbitMQ

`Program.cs` registra MassTransit y configura RabbitMQ en `localhost`, con el virtual host `/`. El código utiliza las credenciales de desarrollo `guest` y `guest`, un tiempo de espera de conexión de tres segundos y heartbeat de diez segundos. También configura tres reintentos con intervalos de dos segundos.

{% hint style="warning" %}
Para un ambiente distinto al local, la dirección, usuario y contraseña del broker deben externalizarse y configurarse de acuerdo con la infraestructura disponible.
{% endhint %}

### 12.5 Comportamiento ante fallos de mensajería

En servicios como `OrdenCompraService` y `AdjudicacionService`, la publicación del evento se ejecuta en una tarea independiente y captura excepciones. Esto evita bloquear la operación principal cuando falla la publicación, pero significa que el guardado del registro y la publicación del evento no forman una única transacción garantizada.

Si el historial no aparece, revisar:

{% stepper %}
{% step %}
## Verificar RabbitMQ

Que RabbitMQ esté iniciado y acepte conexiones.
{% endstep %}

{% step %}
## Verificar la conexión de la API

Que la API pueda conectarse al broker.
{% endstep %}

{% step %}
## Verificar consumidores

Que el consumidor correspondiente esté registrado.
{% endstep %}

{% step %}
## Verificar MongoDB

Que MongoDB esté disponible.
{% endstep %}

{% step %}
## Revisar advertencias

Los mensajes de advertencia emitidos por la API.
{% endstep %}
{% endstepper %}
