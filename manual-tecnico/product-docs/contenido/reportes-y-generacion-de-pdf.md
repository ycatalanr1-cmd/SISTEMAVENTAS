---
description: >-
  Describe los procesos utilizados para consultar información, generar reportes
  y exportarlos en formato PDF.
icon: file
---

# REPORTES Y GENERACIÓN DE PDF

## 11. Reportes y generación de PDF

### 11.1 Reportes de consulta

`Infraestructura/Repositorio/ReporteRepositorio.cs` contiene las consultas para los reportes que devuelve `ReporteControlador`.

| Reporte                           | Información consultada                                               |
| --------------------------------- | -------------------------------------------------------------------- |
| Historial de compras por artículo | Compras asociadas a un artículo, proveedor y precio de adjudicación. |
| Ranking de proveedores            | Montos adjudicados por proveedor dentro de un rango de fechas.       |
| Ofertas por orden                 | Comparación de ofertas recibidas para los pedidos de una orden.      |
| Pedidos pendientes                | Pedidos internos que no tienen orden asignada.                       |
| Órdenes activas                   | Información obtenida desde `Vista_OrdenesActivas`.                   |
| Gasto departamental               | Importes agrupados por departamento y sucursal para el año indicado. |
| Eficiencia del proceso            | Tiempo relacionado con la creación de órdenes y su adjudicación.     |
| Variación de precios              | Evolución de precios de oferta por artículo y proveedor.             |

Las consultas se implementan mediante LINQ/Entity Framework o SQL directo según el método. Para cambios en un reporte se debe revisar tanto el método del repositorio como el DTO que recibe los resultados y el componente Angular que los presenta.

### 11.2 Generación PDF con QuestPDF

La clase `ReportePdfService` se encuentra en `Aplicacion/Servicios/ReportePdfService.cs`.

La clase:

* Configura la licencia Community de QuestPDF.
* Obtiene la cadena `LocalSqlServer` desde la configuración.
* Ejecuta consultas SQL mediante `Microsoft.Data.SqlClient`.
* Convierte los resultados a `DataTable`.
* Construye documentos en tamaño A4 horizontal.
* Agrega encabezados, subtítulos, fecha de generación, tablas y pie de página.
* Devuelve el contenido del documento como un arreglo de bytes.

El método `DocumentoBase` concentra el diseño general de los reportes. Los métodos específicos definen la consulta SQL, el título, el subtítulo y los nombres visibles de las columnas. Las consultas SQL directas deben revisarse de manera independiente de los repositorios EF Core.

### 11.3 Mantenimiento de reportes

{% stepper %}
{% step %}
## Identificar la ruta

Identificar la ruta en `ReporteControlador.cs`.
{% endstep %}

{% step %}
## Localizar la consulta JSON

Localizar el método correspondiente en `ReporteRepositorio.cs` si es una consulta JSON.
{% endstep %}

{% step %}
## Revisar DTO

Revisar el DTO utilizado para transportar el resultado.
{% endstep %}

{% step %}
## Revisar frontend

Revisar el servicio Angular que consume el endpoint.

Revisar el componente de la pantalla que presenta los datos.
{% endstep %}

{% step %}
## Revisar PDF

Si se trata de un PDF, revisar el método correspondiente en `ReportePdfService.cs` y la ruta PDF del controlador.
{% endstep %}

{% step %}
## Probar el reporte

Probar el reporte con datos reales de la base configurada.
{% endstep %}
{% endstepper %}

Para el reporte de órdenes activas, verificar además la existencia y estructura de `Vista_OrdenesActivas` en SQL Server.
