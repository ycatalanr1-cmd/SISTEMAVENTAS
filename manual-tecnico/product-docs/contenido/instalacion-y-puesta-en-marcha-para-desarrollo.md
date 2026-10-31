---
description: >-
  Presenta los pasos para instalar las dependencias, configurar los componentes
  y ejecutar el sistema en un entorno de desarrollo
icon: circle-play
---

# INSTALACIÓN Y PUESTA EN MARCHA PARA DESARROLLO

## 14. Instalación y puesta en marcha para desarrollo

Esta sección describe la puesta en marcha desde el código fuente incluido. El ZIP contiene las migraciones de Entity Framework Core; no contiene un archivo `docs/script.sql` independiente, por lo que la creación del esquema puede realizarse mediante las migraciones.

### 14.1 Obtener el proyecto

Desde una terminal:

```bash
git clone https://github.com/eduardomorales073-collab/ProyectoVenta.git
cd ProyectoVenta
```

También se puede descomprimir el archivo ZIP recibido y abrir la carpeta raíz `ProyectoVenta-main`.

### 14.2 Restaurar y compilar el backend

Desde la carpeta raíz:

```bash
dotnet restore ProyectoVentas.slnx
dotnet build ProyectoVentas.slnx
```

Si se desea iniciar directamente la API:

```bash
cd Venta
dotnet restore
dotnet build
```

### 14.3 Preparar SQL Server

{% stepper %}
{% step %}
## Disponer de SQL Server o Azure SQL

Instalar y ejecutar SQL Server o disponer de una instancia Azure SQL.
{% endstep %}

{% step %}
## Crear o seleccionar la base de datos

Crear o seleccionar la base de datos `SystemVentas`.
{% endstep %}

{% step %}
## Configurar la conexión

Configurar la cadena de conexión correspondiente en `Venta/appsettings.json` o mediante configuración externa.
{% endstep %}

{% step %}
## Verificar permisos

Comprobar que el usuario de conexión tenga permisos para crear y modificar el esquema durante la instalación.
{% endstep %}
{% endstepper %}

### 14.4 Aplicar migraciones de Entity Framework Core

El proyecto incluye migraciones y referencia `Microsoft.EntityFrameworkCore.Tools`. Para ejecutar las migraciones desde la raíz de la solución se puede instalar la herramienta CLI si aún no está disponible:

```bash
dotnet tool install --global dotnet-ef
```

Si ya está instalada:

```bash
dotnet tool update --global dotnet-ef
```

Aplicar las migraciones:

```bash
dotnet ef database update --project Infraestructura/Infraestructura.csproj --startup-project Venta/Venta.csproj
```

Si la herramienta no logra crear el contexto, revisar `Infraestructura/Datos/AplicacionDBContextoFactory.cs` y que la configuración de conexión esté disponible para el proyecto de inicio.

### 14.5 Iniciar la API

En PowerShell:

```powershell
cd Venta
$env:ASPNETCORE_URLS = "http://localhost:5000"
dotnet run
```

Al iniciar, la API registra los servicios y middleware configurados en `Program.cs`. La ruta raíz redirige a Swagger. Abrir:

`http://localhost:5000/swagger`

### 14.6 Instalar e iniciar Angular

Abrir otra terminal:

```bash
cd proyecto-ventas-front
npm install
npm start
```

Angular inicia en el puerto `4200` según el script del `package.json`. Abrir:

`http://localhost:4200`

Verificar que la API se encuentre activa en el puerto `5000` y que la URL de `environment.ts` coincida con la dirección real.

### 14.7 Configurar MongoDB

Si se utilizará auditoría:

{% stepper %}
{% step %}
## Iniciar MongoDB

Instalar y arrancar MongoDB.
{% endstep %}

{% step %}
## Configurar la conexión

Configurar `ConnectionStrings:MongoDB`.
{% endstep %}

{% step %}
## Verificar conectividad

Verificar que la API pueda conectarse al servidor.
{% endstep %}

{% step %}
## Comprobar historial

Realizar una operación que publique un evento y comprobar que el consumidor registre el historial correspondiente.
{% endstep %}
{% endstepper %}

La base de datos utilizada por el código es `LogsDB`; las colecciones se registran desde `Program.cs`.

### 14.8 Configurar RabbitMQ

Si se utilizará mensajería:

{% stepper %}
{% step %}
## Iniciar RabbitMQ

Instalar y arrancar RabbitMQ.
{% endstep %}

{% step %}
## Configurar broker y credenciales

Configurar el host y las credenciales que utiliza MassTransit en `Program.cs` o externalizarlas para el ambiente.
{% endstep %}

{% step %}
## Iniciar API

Iniciar la API.
{% endstep %}

{% step %}
## Revisar conexión

Revisar los mensajes de inicio y conexión.
{% endstep %}

{% step %}
## Comprobar procesamiento

Ejecutar una operación que publique un evento y comprobar el procesamiento del consumidor.
{% endstep %}
{% endstepper %}

### 14.9 Verificación inicial

Una vez iniciados los componentes:

* Abrir Swagger y comprobar que la API responde.
* Abrir Angular y comprobar que carga la pantalla de selección de base de datos.
* Seleccionar el destino SQL configurado.
* Probar el inicio de sesión con una cuenta válida del ambiente.
* Consultar un catálogo.
* Crear o consultar un pedido de prueba con un usuario autorizado.
* Comprobar los logs de la API si falla una solicitud.
* Verificar MongoDB y RabbitMQ si se está probando auditoría.

Las cuentas de prueba deben obtenerse del responsable de la base de datos del ambiente. No se deben asumir credenciales de ejemplo ni reutilizar contraseñas publicadas en documentación.

### 14.10 Publicación del backend

Para generar una publicación del backend:

```bash
dotnet publish Venta/Venta.csproj -c Release -o ./publish/backend
```

El resultado se genera en `publish/backend`. La publicación del backend no incluye por sí sola el proceso de empaquetado de escritorio.

### 14.11 Compilación del frontend

```bash
cd proyecto-ventas-front
npm run build
```

El resultado de compilación se genera en el directorio de salida configurado en `angular.json`.
