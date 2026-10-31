---
description: >-
  Incluye situaciones que pueden presentarse durante la instalación o ejecución
  del sistema, junto con orientaciones para identificar sus posibles causas.
icon: user-doctor-message
---

# DIAGNÓSTICO DE PROBLEMAS

## 17. Diagnóstico de problemas

| Síntoma                            | Elementos que se deben revisar                                                                              |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Angular no se conecta a la API     | API iniciada, puerto 5000, `environment.ts`, CORS y consola del navegador.                                  |
| Error de conexión SQL              | Cadena de conexión, servidor, nombre de base, credenciales, firewall y permisos.                            |
| Error al aplicar migraciones       | Proyecto de inicio, proyecto de infraestructura, herramienta `dotnet-ef`, contexto y cadena de conexión.    |
| HTTP 401                           | Credenciales, vigencia del JWT, encabezado `Authorization` y firma.                                         |
| HTTP 403                           | Rol del usuario y atributo `[Authorize(Roles = "...")]` de la acción.                                       |
| No aparecen pedidos para proveedor | Claim `IdProveedor`, relación del usuario con el proveedor, estado de la orden y disponibilidad del pedido. |
| No se genera un PDF                | API activa, conexión `LocalSqlServer`, consulta SQL y disponibilidad de las tablas utilizadas.              |
| Reporte de órdenes activas falla   | Existencia y estructura de `Vista_OrdenesActivas` en la base seleccionada.                                  |
| No se guarda historial             | Conexión RabbitMQ, consumidor registrado, conexión MongoDB y mensajes de advertencia.                       |
| JasperReports no carga             | Disponibilidad del servidor externo, URL configurada, credenciales de acceso y publicación del reporte.     |
| Error de compilación Angular       | Versión de Node/npm, dependencias instaladas y salida de `npm run build`.                                   |
| Error de compilación .NET          | SDK .NET 10, restauración NuGet y errores del proyecto indicado por `dotnet build`.                         |

### 17.1 Registros de diagnóstico

La API imprime información de diagnóstico en consola durante el inicio y cuando ocurren excepciones. Para investigar un error:

{% stepper %}
{% step %}
## Conservar el mensaje completo

Conservar el mensaje completo de la terminal.
{% endstep %}

{% step %}
## Identificar la ruta HTTP

Identificar la ruta HTTP que produjo el error.
{% endstep %}

{% step %}
## Revisar excepción

Revisar el tipo de excepción y su causa interna.
{% endstep %}

{% step %}
## Confirmar dependencias externas

Confirmar la disponibilidad del servicio externo implicado.
{% endstep %}

{% step %}
## Reproducir en desarrollo

Reproducir el problema en un ambiente de desarrollo antes de modificar datos.
{% endstep %}
{% endstepper %}
