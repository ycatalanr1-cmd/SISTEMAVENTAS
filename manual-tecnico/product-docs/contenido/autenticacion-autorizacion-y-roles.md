---
description: >-
  Explica los mecanismos de inicio de sesión, validación de credenciales,
  generación de tokens y permisos asignados a los diferentes roles.
icon: user-viewfinder
---

# AUTENTICACIÓN, AUTORIZACIÓN Y ROLES

## 10. Autenticación, autorización y roles

### 10.1 Generación del token

El proceso se implementa en `Aplicacion/Servicios/AuthService.cs`.

Después de validar las credenciales, el sistema genera un JWT firmado con HMAC SHA-256. El token contiene claims de identificación, correo, nombre y rol. También puede incluir `IdProveedor` y `IdDepartamento` cuando esos datos están asociados al usuario.

La duración del token generada por el servicio es de ocho horas.

### 10.2 Roles utilizados por el sistema

La asignación de nombre de rol se realiza según `id_Rol`:

| ID de rol | Nombre utilizado en autorización |
| --------: | -------------------------------- |
|         1 | `Administrador`                  |
|         2 | `GestorCompras`                  |
|         3 | `AdministradorProveedor`         |
|         4 | `Auditor`                        |
|         5 | `CreadorPedidos`                 |

{% hint style="warning" %}
Si se encuentra un ID distinto a los contemplados, el código de generación del token asigna el nombre `Auditor`. Por ello, los identificadores de rol almacenados deben mantenerse consistentes con esta correspondencia.
{% endhint %}

### 10.3 Uso del token

Los controladores que requieren autenticación utilizan `[Authorize]`. Las operaciones restringidas utilizan `[Authorize(Roles = "...")]`.

El frontend debe enviar el token en el encabezado:

```http
Authorization: Bearer <token>
```

La API valida firma, emisor, audiencia y vigencia del token antes de permitir el acceso a los endpoints protegidos.

### 10.4 Claims adicionales

Además de los claims estándar, el servicio puede incluir:

* `IdRol`
* `IdProveedor`
* `IdDepartamento`

Estos valores se utilizan en operaciones que necesitan identificar el ámbito del usuario autenticado, como la consulta de pedidos disponibles para un proveedor o el filtrado de órdenes.
