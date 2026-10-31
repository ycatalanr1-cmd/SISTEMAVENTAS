---
icon: compass
---

# Flujo Completo de Compra

Una compra en SistemaVentas pasa por varias personas, y cada una hace su parte con su propia cuenta. Esta sección sigue el recorrido de un pedido, desde que alguien lo solicita hasta que se elige al proveedor que lo atenderá.

#### Paso 1: Se registra el pedido

**Quién lo hace:** el Creador de Pedidos.

Todo empieza cuando alguien necesita algo, el Creador de Pedidos inicia sesión, (test.creador@test.com) y su contraseña, entra a "Mis Órdenes de Compra" y crea una nueva orden con los artículos que se necesitan.

<figure><img src="../.gitbook/assets/imagen (74).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Captura de pantalla 2026-10-29 200801.png" alt=""><figcaption></figcaption></figure>

&#x20;Al guardarla, la orden queda en estado "Borrador"

<figure><img src="../.gitbook/assets/imagen (63).png" alt=""><figcaption></figcaption></figure>

&#x20;El sistema genera automáticamente el pedido correspondiente, que se puede consultar en "Mis Pedidos" con el estado "Creado".

<figure><img src="../.gitbook/assets/imagen (54).png" alt=""><figcaption></figcaption></figure>

#### Paso 2: Aprobar la orden

**Quién lo hace:** el Gestor de Compras.

1. Se "Inicia sesión con la cuenta de Gestor de Compras, (maria.garcia@gmail.com) y su contraseña.
2. Entrar a "Órdenes de Compra" y ubicar la orden en estado "Borrador".

<figure><img src="../.gitbook/assets/imagen (55).png" alt=""><figcaption></figcaption></figure>

3. Hacer clic en el ícono del sello con check, en la columna "Acciones".

<figure><img src="../.gitbook/assets/imagen (56).png" alt=""><figcaption></figcaption></figure>

4. En la ventana "Aprobar orden", hacer clic en "Aceptar" para confirmar. Si se prefiere no aprobarla, se usa "Cancelar".

<figure><img src="../.gitbook/assets/imagen (57).png" alt=""><figcaption></figcaption></figure>

Resultado: la orden pasa al estado "Aprobada".

<figure><img src="../.gitbook/assets/imagen (58).png" alt=""><figcaption></figcaption></figure>

5. Se publica la orden
6. En "Órdenes de Compra", hacer clic en el ícono del ojo de la orden aprobada y se abre la ventana "Pedidos de la Orden".
7. Hacer clic en "+ Agregar Pedido" y completar los datos solicitados.
8. Guardar el pedido y cerrar la ventana con "Cerrar".
9. La orden pasa al estado "Publicada" y queda disponible para los proveedores.

<figure><img src="../.gitbook/assets/imagen (70).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/imagen (66).png" alt=""><figcaption></figcaption></figure>

#### Paso 3: Los proveedores ven el pedido y envian ofertas

**Quién:** Administrador de Proveedor

1. Se inicia sesión con el usuario de proveedor, (jose.hernandez@gmail.com) y su contraseña.
2. Abre **Pedidos Disponibles**. Solo verás los pedidos de tu rubro que pertenezcan a órdenes **Publicadas**.
3. Selecciona el pedido y registra tu oferta (precio y datos solicitados).
4. Confirma el envío. Tu oferta aparecerá en **Mis Ofertas**.

**Resultado:** el pedido pasa a estado   **Con Ofertas**.

> El buscador de Pedidos Disponibles filtra por **código o departamento** (por ejemplo, "Administración"). Si escribes otra cosa, la lista saldrá vacía.

**Paso 4: El Gestor de Compras adjudica al mejor precio**

**Quién:** Gestor de Compras

1. Se inicia sesión como Gestor de Compras.
2. Abre **Adjudicaciones** en el menú superior.
3. Selecciona el pedido que ya tiene ofertas.
4. Compara las ofertas recibidas y elige la de mejor precio.
5. Confirma la adjudicación.

**Resultado:**

* Se crea la adjudicación y el pedido pasa a  **Adjudicado**.
* Cuando todos los pedidos de la orden están adjudicados, la orden pasa automáticamente a **Adjudicada**.

<figure><img src="../.gitbook/assets/imagen (68).png" alt=""><figcaption></figcaption></figure>

**Paso 5: El Auditor genera reportes**

**Quién:** Auditor

1. Inicia sesión como Auditor, (juan.perez@gmail.com) y su contraseña.&#x20;
2. Abre **Reportes** en el menú superior.

<figure><img src="../.gitbook/assets/imagen (75).png" alt=""><figcaption></figcaption></figure>

Selecciona el reporte que necesitas (por ejemplo, Ranking de Proveedores u Órdenes Activas).

<figure><img src="../.gitbook/assets/imagen (76).png" alt=""><figcaption></figcaption></figure>

4. El PDF se genera en 1 o 2 segundos.
5. Usa **Recargar** para regenerarlo o **Descargar** para guardarlo.

**Resultado:** el Auditor obtiene el análisis del proceso, en modo solo lectura.

<figure><img src="../.gitbook/assets/imagen (67).png" alt=""><figcaption></figcaption></figure>

