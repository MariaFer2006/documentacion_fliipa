#### HU-034: Administrar la lista negra (blacklist)

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Administrador del producto |
| **Historia** | Como administrador, quiero agregar o retirar clientes de la lista negra, para bloquear casos de fraude confirmado. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | El administrador agrega o retira clientes de la blacklist, validando que el cliente exista y registrando el motivo por el cual el cliente ingresa a la lista negra. |
| **Relaciones** | Casos de uso: CU-017. Requerimiento: RF-027. Historia relacionada: HU-011  |
| **Referencias** | `backends/b2b/src/controllers/blacklist/add-client-to-blacklist.ts`, `backends/b2b/src/controllers/blacklist/remove-client-client-from-blacklist.ts` |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | **Corrección v1.6**: se agrega al criterio de aceptación el registro del motivo de ingreso a la blacklist, que hacía falta. Pendiente de verificar en código si el modelo actual de blacklist tiene un campo de motivo o si debe agregarse. A diferencia de HU-031/032/033/036, esta historia sí tenía respaldo real desde la v1.3, pero en `backends/b2b` — no en un backend administrativo separado. Se confirma el hallazgo original: no hay enforcement de la blacklist sobre checkout, evaluación de riesgo o desembolso en ningún archivo del repositorio (`blacklists` solo aparece como relación de lectura en `get-client-by-id.service.ts`, sin ninguna validación bloqueante). Este es un riesgo de negocio real y verificado. |