# Estados de un Pedido

Durante el proceso de compra, los pedidos pueden pasar por diferentes estados, estos permiten identificar en qué etapa se encuentra cada solicitud.

| Estado          | Descripción                                                         |
| --------------- | ------------------------------------------------------------------- |
| **Creado**      | El pedido acaba de registrarse en el sistema.                       |
| **Sin Orden**   | El pedido todavía no tiene una orden de compra asignada.            |
| **Con Ofertas** | Uno o varios proveedores han registrado sus ofertas para el pedido. |
| **Adjudicado**  | El pedido ya fue asignado al proveedor seleccionado.                |

### 2. Estados de una Orden

Las órdenes de compra también cuentan con estados que permiten conocer el avance del proceso de adquisición.

| Estado         | Descripción                                                                                          |
| -------------- | ---------------------------------------------------------------------------------------------------- |
| **Borrador**   | La orden acaba de crearse y todavía no ha sido aprobada.                                             |
| **Aprobada**   | El Gestor de Compras ha aprobado la orden.                                                           |
| **Publicada**  | La orden está disponible para que los proveedores consulten los pedidos correspondientes a su rubro. |
| **Adjudicada** | Todos los pedidos asociados a la orden ya fueron adjudicados.                                        |
|  **Cancelada** | La orden fue cancelada por un administrador.                                                         |
