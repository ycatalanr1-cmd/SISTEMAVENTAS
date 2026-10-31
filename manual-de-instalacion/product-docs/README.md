# MANUAL\_INSTALACION

Guía para instalar y configurar el sistema.

## 🖥️ Requisitos

### Hardware mínimo

* **CPU:** 2 núcleos
* **RAM:** 4 GB
* **Disco:** 1 GB libre
* **SO:** Windows 10/11 (x64)

### Software

* **SQL Server** (local) o **Azure SQL** (nube)
* **MongoDB** (para auditoría)
* **RabbitMQ** (opcional, para eventos)

## 🗄️ Instalación de SQL Server

### Opción A: SQL Server Express (Local)

{% stepper %}
{% step %}
## Descargar SQL Server Express 2022

Descarga **SQL Server Express 2022**:

https://www.microsoft.com/es-es/sql-server/sql-server-downloads
{% endstep %}

{% step %}
## Ejecutar el instalador

Ejecuta el instalador.
{% endstep %}

{% step %}
## Seleccionar la instalación básica

Selecciona **"Básica"**.
{% endstep %}

{% step %}
## Aceptar los términos

Acepta los términos.
{% endstep %}

{% step %}
## Instalar

Instala.
{% endstep %}

{% step %}
## Instalar SQL Server Management Studio

Instala **SQL Server Management Studio (SSMS)**:

https://learn.microsoft.com/es-es/sql/ssms/download-sql-server-management-studio-ssms
{% endstep %}
{% endstepper %}

### Crear la base de datos

{% stepper %}
{% step %}
## Abrir SSMS

Abre **SSMS**.
{% endstep %}

{% step %}
## Conectarse al servidor

Conéctate a `localhost`.
{% endstep %}

{% step %}
## Crear una base de datos

**Clic derecho en "Bases de datos"** → **"Nueva base de datos"**.
{% endstep %}

{% step %}
## Asignar el nombre

Nombre: `SystemVentas`
{% endstep %}

{% step %}
## Confirmar

Clic en **"Aceptar"**.
{% endstep %}
{% endstepper %}

### Ejecutar el script de migración

{% stepper %}
{% step %}
## Abrir el script

Abre el archivo `docs/script.sql` en SSMS.
{% endstep %}

{% step %}
## Seleccionar la base de datos

Selecciona la BD `SystemVentas` en el dropdown.
{% endstep %}

{% step %}
## Ejecutar

Presiona **F5**.
{% endstep %}
{% endstepper %}

## 🍃 Instalación de MongoDB

### Windows

{% stepper %}
{% step %}
## Descargar MongoDB Community

Descarga **MongoDB Community**:

https://www.mongodb.com/try/download/community
{% endstep %}

{% step %}
## Ejecutar el instalador

Ejecuta el instalador.
{% endstep %}

{% step %}
## Seleccionar la instalación completa

Selecciona **"Complete"**.
{% endstep %}

{% step %}
## Instalar como servicio

Instala como **servicio** con "Install MongoDB as a Service".
{% endstep %}

{% step %}
## Instalar MongoDB Compass

Instala **MongoDB Compass** (GUI):

https://www.mongodb.com/try/download/compass
{% endstep %}
{% endstepper %}

### Verificar

```powershell
# Verificar el servicio
Get-Service MongoDB

# Verificar el puerto
Test-NetConnection -ComputerName localhost -Port 27017
```

## Instalación de RabbitMQ (Opcional)

### Windows

{% stepper %}
{% step %}
## Instalar Erlang

Instala Erlang:

https://www.erlang.org/downloads
{% endstep %}

{% step %}
## Instalar RabbitMQ

Instala RabbitMQ:

https://www.rabbitmq.com/download.html
{% endstep %}

{% step %}
## Habilitar el plugin de gestión

```powershell
rabbitmq-plugins enable rabbitmq_management
```
{% endstep %}

{% step %}
## Acceder a la consola

http://localhost:15672

Usuario: `guest`

Contraseña: `guest`
{% endstep %}
{% endstepper %}

```powershell
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
```

## Configuración de Azure SQL (Opcional)

{% stepper %}
{% step %}
## Crear cuenta de Azure

https://azure.microsoft.com/free/
{% endstep %}

{% step %}
## Crear Azure SQL Database

Portal de Azure → "Crear un recurso".

Busca "SQL Database".

Configura:

* Grupo de recursos: `rg-sistemaventas`
* Nombre BD: `SystemVentas`
* Servidor: `srv-sistemaventas`
* Ubicación: `Mexico Central`
* Nivel de servicio: `Uso general`
* Nivel de proceso: `Sin servidor`
* Máx vCores: `2`
* Pausa automática: `20 min`
* Datos: `32 GB`
* Firewall: `Permitir Azure + IP cliente`

Clic en "Crear".
{% endstep %}

{% step %}
## Migrar los datos

Abre SSMS y conéctate a Azure SQL.

Ejecuta el script `docs/script.sql`.

Verifica las tablas.
{% endstep %}
{% endstepper %}

### Configurar la app

```json
{
  "ConnectionStrings": {
    "AzureSql": "Server=tcp:srv-sistemaventas.database.windows.net,1433;Initial Catalog=SystemVentas;User ID=adminventas;Password=TU_PASSWORD;Encrypt=True;TrustServerCertificate=False;"
  },
  "DatabaseOptions": {
    "AzureConfigurado": true
  }
}
```

## 🚀 Instalación de la Aplicación

### Opción A: Usar el .exe portable

{% stepper %}
{% step %}
## Copiar el ejecutable

Copia `SistemaVentas.exe` a tu PC.
{% endstep %}

{% step %}
## Ejecutar

Doble clic para ejecutar.
{% endstep %}

{% step %}
## Finalizar

Listo.
{% endstep %}
{% endstepper %}

### Opción B: Compilar desde el código

```bash
# 1. Clonar
git clone https://github.com/tu-usuario/ProyectoVentas.git
cd ProyectoVentas

# 2. Backend
cd Venta
dotnet restore
dotnet build -c Release
dotnet publish -c Release -r win-x64 --self-contained true -o bin\Release\net10.0\publish

# 3. Frontend
cd ..\proyecto-ventas-front
npm install
npm run build

# 4. Electron
cd ..\electron
npm install
Remove-Item -Recurse -Force "temp_asar\browser" -ErrorAction SilentlyContinue
Copy-Item "browser" "temp_asar\browser" -Recurse -Force
npx asar pack temp_asar "dist\win-unpacked\resources\app.asar"
npx electron-builder --win portable --prepackaged dist/win-unpacked
```

## Configuración Inicial

{% stepper %}
{% step %}
## Verificar servicios

```powershell
# SQL Server
Get-Service MSSQLSERVER

# MongoDB
Get-Service MongoDB

# RabbitMQ
Get-Service RabbitMQ
```
{% endstep %}

{% step %}
## Configurar appsettings.json

Abre `Venta\appsettings.json` y edita:

```json
{
  "ConnectionStrings": {
    "LocalSqlServer": "Server=localhost;Database=SystemVentas;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=true",
    "AzureSql": "",
    "MongoDB": "mongodb://localhost:27017"
  },
  "DatabaseOptions": {
    "AzureConfigurado": false,
    "DefaultBd": "local"
  },
  "Jwt": {
    "Key": "una-clave-secreta-muy-larga-de-al-menos-32-caracteres",
    "Issuer": "ProyectoVentas",
    "Audience": "ProyectoVentasUsuarios"
  }
}
```
{% endstep %}

{% step %}
## Ejecutar la app

1. Abre `SistemaVentas.exe`.
2. Selecciona la BD.
3. Login.
{% endstep %}
{% endstepper %}

## 🔧 Solución de Problemas

<details>

<summary>El .exe no arranca</summary>

**Síntoma:** Doble clic no hace nada.

**Solución:**

1. Verifica que SQL Server esté corriendo.
2. Ejecuta como administrador.
3. Revisa el Event Viewer de Windows.

</details>

<details>

<summary>Error "Login failed for user 'adminventas'"</summary>

**Causa:** La contraseña es incorrecta.

**Solución:**

1. En el Portal de Azure, ve al servidor SQL.
2. Clic en "Restablecer contraseña".
3. Nueva contraseña: `Sistemas2026` (sin caracteres especiales).

</details>

<details>

<summary>Error de conexión a Azure SQL</summary>

**Causa:** El firewall bloquea tu IP.

**Solución:**

1. Portal de Azure → Servidor SQL → "Redes".
2. Marca "Agregar dirección IP del cliente actual".
3. Guarda.

</details>

<details>

<summary>El PDF no se genera</summary>

**Causa:** El backend no está corriendo.

**Solución:**

1. Abre DevTools (F12) en la app.
2. Ve a la pestaña Console.
3. Busca el error.

</details>

<details>

<summary>La app se queda en blanco al recargar (F5)</summary>

**Causa:** El servidor HTTP local no está sirviendo el SPA fallback.

**Solución:**

1. Verifica que `main.js` tenga el servidor HTTP.
2. Recompila y reempaqueta.

</details>

📌 Última actualización: 07/10/2026
