---
description: >-
  Describe las actividades técnicas necesarias para iniciar, supervisar y
  trabajar con los componentes del sistema
icon: gear-code
---

# OPERACIÓN TÉCNICA DEL SISTEMA

## 15. Operación técnica del sistema

### 15.1 Inicio de los componentes

Para el entorno de desarrollo, iniciar en este orden:

{% stepper %}
{% step %}
## Base de datos relacional

Iniciar SQL Server o confirmar disponibilidad de Azure SQL.
{% endstep %}

{% step %}
## Auditoría

Iniciar MongoDB, si se requiere auditoría.
{% endstep %}

{% step %}
## Mensajería

Iniciar RabbitMQ, si se requiere procesamiento de eventos.
{% endstep %}

{% step %}
## API

Iniciar la API ASP.NET Core.
{% endstep %}

{% step %}
## Frontend

Iniciar el frontend Angular.
{% endstep %}
{% endstepper %}

### 15.2 Selección de base de datos

La pantalla de selección del frontend permite seleccionar el destino. La API utiliza el encabezado `X-Tipo-BD` y las opciones configuradas para escoger la cadena de conexión.

Si se cambia el destino, verificar que la base seleccionada tenga el esquema actualizado y los datos que se esperan consultar.

### 15.3 Operaciones de administración

Los módulos de administración utilizan los endpoints de sucursales, departamentos, artículos, proveedores, usuarios, roles, rubros, unidades de medida, categorías y tipos de orden.

Antes de eliminar o modificar registros que tengan dependencias, revisar las relaciones configuradas en Entity Framework y los efectos en los procesos de pedidos, ofertas y adjudicaciones.

### 15.4 Operación de compras

La operación habitual se apoya en los módulos de pedidos internos, órdenes de compra, ofertas y adjudicaciones. Los cambios de estado se realizan mediante métodos específicos del servicio y endpoints dedicados.

Para investigar una operación, seguir la ruta desde la pantalla Angular hasta el método del servicio C# y el repositorio que persiste los cambios.

### 15.5 Reportes

Los reportes JSON se consumen desde los servicios Angular y se presentan en las páginas de reportes. Los PDF se solicitan a los endpoints `/pdf/...` del controlador de reportes.

Si los datos de un PDF difieren de los reportes JSON, revisar la conexión usada por `ReportePdfService`, ya que utiliza `LocalSqlServer` directamente.
