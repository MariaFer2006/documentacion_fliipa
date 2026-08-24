#### HU-034: Administrar la lista negra (blacklist)

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero agregar o retirar clientes de la lista negra |
| **Prioridad** | Media |
| **Criterios de aceptación** | El administrador agrega o retira clientes de la blacklist, validando que el cliente exista y registrando el motivo por el cual el cliente ingresa a la lista negra. |
| **Relaciones** | Casos de uso: [CU-017](../../Casos%20de%20Uso/6.%20Operaci%C3%B3n%20Admin/CU-017%20Administrar%20y%20consultar%20clientes%20en%20blacklist.md). Requerimiento:[RF-027](../../Requerimientos/Requerimientos%20Funcionales.md). Historia relacionada: [HU-011](../3.%20Credito/HU-011%20Ver%20mensaje%20de%20no%20disponibilidad%20de%20cr%C3%A9dito.md)  |
| **Referencias** | `backends/b2b/src/controllers/blacklist/add-client-to-blacklist.ts`, `backends/b2b/src/controllers/blacklist/remove-client-client-from-blacklist.ts` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Corrección v1.6**: se agrega al criterio de aceptación el registro del motivo de ingreso a la blacklist, que hacía falta. Pendiente de verificar en código si el modelo actual de blacklist tiene un campo de motivo o si debe agregarse. A diferencia de HU-031/032/033/036, esta historia sí tenía respaldo real desde la v1.3, pero en `backends/b2b` — no en un backend administrativo separado. Se confirma el hallazgo original: no hay enforcement de la blacklist sobre checkout, evaluación de riesgo o desembolso en ningún archivo del repositorio (`blacklists` solo aparece como relación de lectura en `get-client-by-id.service.ts`, sin ninguna validación bloqueante). Este es un riesgo de negocio real y verificado. |



