---
description: >-
  Describe la organización de carpetas, proyectos y archivos del código fuente,
  facilitando la ubicación de los componentes principales.
icon: list-tree
---

# ESTRUCTURA DEL REPOSITORIO

## 4. Estructura del repositorio

La estructura principal del repositorio es la siguiente:

```
ProyectoVenta/
├── Aplicacion/
│   ├── DTO/
│   ├── Interfaz/
│   ├── Maping/
│   ├── Mensajeria/
│   │   ├── Consumidores/
│   │   └── Eventos/
│   ├── modelos/
│   ├── Repositorio/
│   ├── Servicios/
│   └── Aplicacion.csproj
│
├── Infraestructura/
│   ├── Datos/
│   │   ├── Configuraciones/
│   │   ├── AplicacionDBContexto.cs
│   │   └── AplicacionDBContextoFactory.cs
│   ├── Migrations/
│   └── Infraestructura.csproj
│
├── Venta/
│   ├── Controllers/
│   ├── Program.cs
│   ├── appsettings.json
│   ├── appsettings.Development.json
│   └── Venta.csproj
│
├── proyecto-ventas-front/
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/
│   │   │   ├── guards/
│   │   │   ├── interceptors/
│   │   │   ├── models/
│   │   │   ├── pages/
│   │   │   └── services/
│   │   ├── environments/
│   │   └── ...
│   ├── angular.json
│   ├── package.json
│   └── package-lock.json
│
├── docs/
│   ├── MANUAL_INSTALACION.md
│   ├── MANUAL_USUARIO.md
│   └── MANUAL_TECNICO.md
│
├── ProyectoVentas.slnx
└── README.md
```

### 4.1 Directorios de `Aplicacion`

| Directorio                 | Contenido y uso                                                                                                             |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `DTO/`                     | Clases para transportar datos entre frontend, controladores y servicios. Incluye DTO de creación, consulta y actualización. |
| `Interfaz/`                | Contratos que definen operaciones disponibles para los servicios y algunos repositorios.                                    |
| `Maping/`                  | Perfiles y configuraciones de AutoMapper para transformar entidades y DTO.                                                  |
| `modelos/`                 | Entidades del dominio y clases de historial.                                                                                |
| `Repositorio/`             | Contratos de acceso a datos utilizados por los servicios.                                                                   |
| `Servicios/`               | Implementaciones de operaciones y reglas de negocio.                                                                        |
| `Mensajeria/Eventos/`      | Tipos de eventos que representan acciones del sistema.                                                                      |
| `Mensajeria/Consumidores/` | Clases que procesan los eventos recibidos mediante MassTransit.                                                             |

### 4.2 Directorios de `Infraestructura`

| Directorio o archivo                   | Uso                                                                                |
| -------------------------------------- | ---------------------------------------------------------------------------------- |
| `Datos/AplicacionDBContexto.cs`        | Declara los conjuntos de entidades y aplica configuraciones del modelo.            |
| `Datos/Configuraciones/`               | Configura claves, relaciones y otras propiedades de entidades mediante Fluent API. |
| `Datos/AplicacionDBContextoFactory.cs` | Proporciona una forma de crear el contexto para operaciones de diseño.             |
| `Migrations/`                          | Contiene las migraciones y el snapshot del modelo de Entity Framework.             |
| `Repositorio/`                         | Implementa las operaciones de consulta, inserción, actualización y eliminación.    |

### 4.3 Directorios de `Venta`

| Directorio o archivo           | Uso                                                                     |
| ------------------------------ | ----------------------------------------------------------------------- |
| `Controllers/`                 | Controladores que exponen los recursos del sistema mediante HTTP.       |
| `Program.cs`                   | Punto de entrada y configuración de servicios, conexiones y middleware. |
| `appsettings.json`             | Configuración principal de conexiones y parámetros de la aplicación.    |
| `appsettings.Development.json` | Ajustes específicos del entorno de desarrollo.                          |
| `Venta.csproj`                 | Framework objetivo y paquetes NuGet del proyecto API.                   |

### 4.4 Directorios de Angular

| Directorio              | Uso                                                       |
| ----------------------- | --------------------------------------------------------- |
| `src/app/pages/`        | Pantallas organizadas por módulos y perfiles de usuario.  |
| `src/app/components/`   | Componentes compartidos, como encabezados y diálogos.     |
| `src/app/services/`     | Servicios HTTP y servicios compartidos del frontend.      |
| `src/app/models/`       | Interfaces y modelos TypeScript.                          |
| `src/app/guards/`       | Guards que controlan la navegación según sesión y rol.    |
| `src/app/interceptors/` | Interceptores para solicitudes HTTP.                      |
| `src/environments/`     | Configuración de entorno, incluida la URL base de la API. |
| `src/app/app.routes.ts` | Definición de rutas de navegación de Angular.             |
| `src/app/app.config.ts` | Configuración principal de la aplicación Angular.         |
