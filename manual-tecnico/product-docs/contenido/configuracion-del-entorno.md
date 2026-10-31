---
description: >-
  Identifica los parámetros y archivos de configuración necesarios para preparar
  el entorno de ejecución del sistema.
icon: gears
---

# CONFIGURACIÓN DEL ENTORNO

## 13. Configuración del entorno

### 13.1 Requisitos de desarrollo

Los archivos del proyecto declaran .NET 10 para backend y Angular 22 / TypeScript 6 para frontend. Para trabajar con el repositorio se requiere:

* Windows, Linux o macOS con herramientas compatibles con .NET y Node.js.
* .NET SDK 10.
* Node.js compatible con Angular 22.
* npm.
* SQL Server local o una instancia Azure SQL accesible.
* MongoDB si se requiere almacenar y consultar historiales.
* RabbitMQ si se requiere procesar eventos de mensajería.
* Editor de código, por ejemplo Visual Studio o Visual Studio Code.
* SQL Server Management Studio u otra herramienta para administrar SQL Server.

### 13.2 Configuración del backend

Archivo: `Venta/appsettings.json`.

Las claves de configuración utilizadas incluyen:

| Clave                              | Uso                                                                 |
| ---------------------------------- | ------------------------------------------------------------------- |
| `ConnectionStrings:LocalSqlServer` | Conexión a SQL Server local.                                        |
| `ConnectionStrings:AzureSql`       | Conexión a Azure SQL.                                               |
| `ConnectionStrings:MongoDB`        | Dirección de MongoDB.                                               |
| `DatabaseOptions:AzureConfigurado` | Indicador de configuración de Azure declarado en opciones.          |
| `DatabaseOptions:DefaultBd`        | Destino SQL seleccionado cuando la solicitud no indica `X-Tipo-BD`. |
| `Jwt:Key`                          | Clave de firma del token.                                           |
| `Jwt:Issuer`                       | Emisor del token.                                                   |
| `Jwt:Audience`                     | Audiencia del token.                                                |

Ejemplo de estructura de configuración, con valores ilustrativos y no funcionales:

```json
{
  "ConnectionStrings": {
    "LocalSqlServer": "Server=SERVIDOR;Database=SystemVentas;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=true",
    "AzureSql": "",
    "MongoDB": "mongodb://localhost:27017"
  },
  "DatabaseOptions": {
    "AzureConfigurado": false,
    "DefaultBd": "local"
  },
  "Jwt": {
    "Key": "REEMPLAZAR_POR_UN_SECRETO_SEGURO",
    "Issuer": "ProyectoVentas",
    "Audience": "ProyectoVentasUsuarios"
  }
}
```

### 13.3 Configuración del frontend

Los archivos `src/environments/environment.ts` y `src/environments/environment.development.ts` contienen la propiedad `apiUrl`.

Valor observado en el proyecto:

```typescript
export const environment = {
  production: false,
  apiUrl: 'http://localhost:5000/api'
};
```

Si la API se ejecuta en otra dirección o puerto, debe actualizarse la URL utilizada por el frontend y comprobarse que la política CORS permita el origen correspondiente.

### 13.4 Configuración de puertos

El frontend declara el puerto `4200` en el script `start`. Los servicios del frontend apuntan a la API en el puerto `5000`. El backend no fija un puerto mediante una instrucción explícita en `Program.cs`; se debe iniciar con una URL de escucha compatible con la configuración del frontend.

Ejemplo para desarrollo:

```powershell
$env:ASPNETCORE_URLS = "http://localhost:5000"
```
