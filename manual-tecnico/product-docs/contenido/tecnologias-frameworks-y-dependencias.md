---
description: >-
  Detalla las herrammientas, lenguajes de programación, frameworks y bibliotecas
  utilizadas para desarrollar y ejecutar el sistema.
icon: user-robot
---

# TECNOLOGÍAS, FRAMEWORKS Y DEPENDENCIAS

## 5. Tecnologías, frameworks y dependencias

Las versiones siguientes corresponden a las referencias declaradas en los archivos de proyecto incluidos en el repositorio.

### 5.1 Backend

| Tecnología / paquete                          |   Versión declarada | Función                                                   |
| --------------------------------------------- | ------------------: | --------------------------------------------------------- |
| C# / .NET                                     | .NET 10 (`net10.0`) | Plataforma de ejecución de los proyectos backend.         |
| ASP.NET Core                                  |             .NET 10 | API REST y ciclo de vida HTTP.                            |
| Entity Framework Core                         |             10.0.12 | ORM para consultas y persistencia relacional.             |
| Microsoft.EntityFrameworkCore.SqlServer       |             10.0.12 | Proveedor SQL Server para EF Core.                        |
| Microsoft.Data.SqlClient                      |               7.1.1 | Conexiones y consultas SQL directas.                      |
| AutoMapper                                    |              16.2.0 | Conversión entre entidades y DTO.                         |
| BCrypt.Net-Next                               |               4.2.0 | Verificación de contraseñas almacenadas como hash BCrypt. |
| Microsoft.AspNetCore.Authentication.JwtBearer |             10.0.12 | Autenticación mediante tokens JWT.                        |
| MassTransit                                   |              8.5.10 | Abstracción de publicación y consumo de mensajes.         |
| MassTransit.RabbitMQ                          |              8.5.10 | Transporte de mensajes RabbitMQ.                          |
| MongoDB.Driver                                |              3.12.0 | Acceso a MongoDB para historiales.                        |
| Swashbuckle.AspNetCore                        |              10.2.3 | Generación de documentación Swagger/OpenAPI.              |

### 5.2 Frontend

| Tecnología          | Versión declarada | Función                                              |
| ------------------- | ----------------: | ---------------------------------------------------- |
| Angular             |              22.x | Framework principal de interfaz.                     |
| Angular Material    |            22.2.0 | Componentes visuales y controles de interfaz.        |
| TypeScript          |             6.0.2 | Lenguaje de desarrollo del frontend.                 |
| RxJS                |             7.8.x | Programación reactiva y manejo de flujos asíncronos. |
| Chart.js            |             4.5.1 | Gráficas del frontend.                               |
| Angular CLI / build |              22.x | Compilación y servidor de desarrollo.                |
| Vitest              |             4.0.8 | Herramienta declarada para pruebas del frontend.     |

### 5.3 Servicios de infraestructura

* **SQL Server:** almacenamiento relacional de la información operativa.
* **Azure SQL:** destino de conexión SQL en la nube.
* **MongoDB:** almacenamiento de historiales de auditoría.
* **RabbitMQ:** intermediario de mensajes.
* **MassTransit:** integración de la API con RabbitMQ.

La selección `local` o `azure` cambia la cadena de conexión SQL utilizada por la aplicación. Ambas opciones usan el proveedor `UseSqlServer`; por tanto, son dos destinos de conexión de la misma familia de motor relacional.

### 5.4 JasperReports

En el frontend existen `jasper.service.ts` y el componente `reporte-jasper/`, que contienen referencias a un servidor JasperReports externo. El servicio utiliza una dirección de servidor independiente de la API. La disponibilidad de esta función requiere que dicho servidor esté instalado, publicado y configurado por separado.

La generación PDF implementada en el backend también utiliza QuestPDF. Son integraciones diferentes: JasperReports es un servicio externo referenciado por el frontend y QuestPDF es una biblioteca utilizada por el backend para construir documentos.
