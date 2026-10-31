---
description: >-
  Presenta aspectos relacionados con la protección de credenciales, accesos,
  configuraciones y datos utilizados por el sistema.
icon: shield-quartered
---

# CONSIDERACIONES DE SEGURIDAD

## 8. Consideraciones de seguridad

La configuración de seguridad está distribuida entre `Program.cs`, `AuthService.cs`, los controladores y los guards de Angular.

### 18.1 Contraseñas

El inicio de sesión verifica las contraseñas mediante BCrypt. Las contraseñas no deben almacenarse ni transmitirse en texto plano fuera del proceso de autenticación protegido por HTTPS.

### 18.2 JWT

La API valida emisor, audiencia, vigencia y firma. El token se firma con una clave configurada en `Jwt:Key`; el código también contiene una clave de respaldo para desarrollo. En un despliegue real se debe configurar un secreto fuerte, único y externo al repositorio. Si un secreto real fue publicado en un repositorio compartido, debe rotarse.

### 18.3 CORS

La política `AngularApp` configurada en `Program.cs` permite cualquier origen mediante `SetIsOriginAllowed(origin => true)`, además de cualquier encabezado y método y credenciales. Para un despliegue controlado, se deben definir únicamente los orígenes confiables.

### 18.4 Rutas PDF

Las acciones PDF del controlador de reportes tienen `[AllowAnonymous]` en el código revisado. Si los reportes contienen información interna, se debe evaluar restringirlos mediante autenticación y autorización por rol.

### 18.5 Credenciales y configuración

Los archivos de configuración del repositorio contienen valores que deben tratarse como sensibles. No se deben copiar directamente a documentación pública ni a otros ambientes. Las credenciales deben reemplazarse, externalizarse y rotarse cuando corresponda.

El código de diagnóstico imprime valores de configuración y detalles de excepciones. Para ambientes expuestos se recomienda reducir esos registros y no devolver trazas internas al consumidor.

### 18.6 Comunicación

En ambientes de producción, la API debe publicarse detrás de HTTPS. Las cadenas de conexión remotas deben utilizar cifrado y certificados válidos.
