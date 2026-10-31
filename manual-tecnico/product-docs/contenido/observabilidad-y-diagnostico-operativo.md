---
icon: display
---

# OBSERVABILIDAD Y DIAGNÓSTICO OPERATIVO

## 20. Observabilidad y diagnóstico operativo

### 20.1 Instrumentación presente

En `Venta/Program.cs` se encuentran salidas de diagnóstico mediante `Console.WriteLine`, middleware de excepción y configuración de Swagger. Son mecanismos de apoyo durante el desarrollo; no constituyen por sí solos un sistema de métricas persistentes o monitoreo centralizado.

Los pasos siguientes son un **procedimiento de comprobación manual**, no un panel de monitoreo incluido en el proyecto.

### 20.2 Comprobación de disponibilidad

{% stepper %}
{% step %}
## Revisar la API

Revisar el proceso de la API y su salida estándar.
{% endstep %}

{% step %}
## Consultar Swagger

Consultar `http://localhost:5000/swagger` cuando se haya iniciado Kestrel en el puerto 5000.
{% endstep %}

{% step %}
## Abrir Angular

Abrir `http://localhost:4200` cuando se ejecute Angular con `npm start`.
{% endstep %}

{% step %}
## Verificar SQL

Verificar la conectividad de SQL Server o Azure SQL correspondiente a la selección `X-Tipo-BD`.
{% endstep %}

{% step %}
## Verificar auditoría

Para auditoría, comprobar RabbitMQ y MongoDB por separado; un HTTP correcto de la API no garantiza que los eventos hayan sido almacenados.
{% endstep %}

{% step %}
## Inspeccionar errores

Inspeccionar los códigos HTTP, la consola del navegador y los mensajes de la API si hay una diferencia entre la interfaz y el backend.
{% endstep %}
{% endstepper %}

### 20.3 Interpretación de fallos

| Indicio                  | Punto de diagnóstico                              | Acción técnica                                                    |
| ------------------------ | ------------------------------------------------- | ----------------------------------------------------------------- |
| Error HTTP 401           | `AuthService`, JWT y reloj del servidor           | Comprobar token, vigencia, firma y credenciales de configuración. |
| Error HTTP 403           | Atributo `[Authorize]` y claims del JWT           | Revisar permisos y coincidencia de roles.                         |
| SQL no accesible         | `AplicacionDBContexto`, cadenas SQL y `X-Tipo-BD` | Identificar destino activo y verificar red y credenciales.        |
| PDF falla, JSON funciona | `ReportePdfService`                               | Revisar `LocalSqlServer` y SQL directo del PDF.                   |
| Historial no aparece     | Publicador, consumidor, broker y MongoDB          | Seguir el evento y consultar excepciones de mensajería.           |
| Error en órdenes activas | `ReporteRepositorio`                              | Verificar la existencia y esquema real de `Vista_OrdenesActivas`. |

### 20.4 Tratamiento de información en registros

El arranque imprime cadenas de conexión de diagnóstico. Antes de publicar registros, ocultar datos de acceso, direcciones sensibles y tokens. Revisar también las respuestas de excepción de los reportes PDF, ya que algunos controladores devuelven `ex.Message` al cliente.
