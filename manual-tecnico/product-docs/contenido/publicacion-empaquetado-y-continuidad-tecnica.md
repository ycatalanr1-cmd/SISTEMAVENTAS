---
icon: box-isometric
---

# PUBLICACIÓN, EMPAQUETADO Y CONTINUIDAD TÉCNICA

## 21. Publicación, empaquetado y continuidad técnica

### 21.1 Compilaciones disponibles en el código

La solución .NET y Angular incorporan los archivos necesarios para restauración y compilación con sus herramientas habituales:

```bash
dotnet restore ProyectoVentas.slnx
dotnet build ProyectoVentas.slnx
dotnet publish Venta/Venta.csproj -c Release -o ./publish/backend
```

```bash
cd proyecto-ventas-front
npm ci
npm run build
```

`npm ci` utiliza el archivo `package-lock.json` incluido en el proyecto. El destino de la compilación Angular se determina desde `angular.json` y debe verificarse antes de configurar el servidor que publicará los archivos estáticos.

### 21.2 Orden de publicación y validación

{% stepper %}
{% step %}
## Preparar destino

Guardar una copia y verificar las credenciales y cadenas de conexión de destino.
{% endstep %}

{% step %}
## Aplicar migraciones

Aplicar migraciones de EF Core únicamente tras revisar el impacto en el esquema y disponer de respaldo.
{% endstep %}

{% step %}
## Configurar seguridad

Configurar secretos externos, orígenes CORS y HTTPS.
{% endstep %}

{% step %}
## Publicar componentes

Publicar la API y el frontend en ubicaciones apropiadas para el entorno.
{% endstep %}

{% step %}
## Validar funcionalidad

Confirmar el flujo autenticado, la consulta de catálogos, las operaciones principales y la generación de PDF con datos de prueba autorizados.
{% endstep %}

{% step %}
## Validar eventos

Si están habilitados eventos, confirmar el consumo y la escritura de historiales.
{% endstep %}
{% endstepper %}

Este orden es una recomendación técnica de operación, no una afirmación de que el repositorio incluya un pipeline de despliegue automatizado.

### 21.3 Mantenimiento de la documentación

Cada cambio en `Venta/Controllers/` debe reflejarse en las tablas de endpoints. Las modificaciones en `Aplicacion/DTO/`, `Aplicacion/modelos/` o `Infraestructura/Datos/` exigen comprobar el impacto en modelos TypeScript, DTO, migraciones y consultas. Si cambia el sistema de mensajería, actualizar el inventario de eventos, consumidores y colecciones de auditoría.
