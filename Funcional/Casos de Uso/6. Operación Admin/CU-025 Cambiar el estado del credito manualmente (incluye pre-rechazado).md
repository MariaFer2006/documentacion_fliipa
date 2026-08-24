### CU-025: Cambiar el estado del crédito manualmente (incluye pre-rechazado)

![Diagrama de caso de uso CU-025](imagenes/diagrama_CU-025.svg)


| Campo | Detalle |
|---|---|
| **Actores** | Administrador / analista de riesgo |
| **Descripción** | El administrador cambia manualmente el estado de la línea de crédito del cliente, incluido el estado pre-rechazado (`pre_rejected`), para gestionar casos en evaluación o decisión manual, de forma distinta a la decisión automática del motor KYC (ver [CU-020](../2.%20KYC/CU-020%20Motor%20KYC%20automatico%20post-solicitud.md)).. |
| **Precondiciones** | El administrador cuenta con el permiso correspondiente sobre la ficha del cliente. |
| **Flujo principal** | 1. El administrador abre la ficha del cliente.<br>2. El administrador selecciona el nuevo estado del crédito, incluyendo la opción `pre_rejected`.<br>3. El sistema aplica el cambio de estado.<br>4. Si el nuevo estado es `pre_rejected`, el sistema envía una alerta operativa al equipo.<br>5. *(Solo si el producto lo garantiza explícitamente por estado de acceso; no se debe asumir un bloqueo adicional no descrito)* El sistema evitaría que el cliente reingrese al flujo de forma inconsistente con el nuevo estado. |
| **Flujos alternativos / excepciones** | A1. El cambio de estado proviene de la decisión automática del motor KYC: corresponde a [HU-044](../../Historias%20De%20Usuario/2.%20KYC/HU-044%20Decidir%20approved%20-%20pre-rejected.md) /  [CU-020](../2.%20KYC/CU-020%20Motor%20KYC%20automatico%20post-solicitud.md)., no a este caso de uso manual. |
| **Postcondiciones** | La línea de crédito queda con el nuevo estado aplicado manualmente y, si corresponde, el equipo fue alertado. |
| **Reglas de negocio** | El cambio manual de estado es independiente de la decisión automática post-KYC  [CU-020](../2.%20KYC/CU-020%20Motor%20KYC%20automatico%20post-solicitud.md); ambos coexisten pero tienen orígenes distintos. |
| **Historias de usuario relacionadas** | [HU-041](../../Historias%20De%20Usuario/5.%20Operaci%C3%B3n%20admin/HU-041%20Cambiar%20el%20estado%20del%20cr%C3%A9dito%20%28incluye%20pre-rechazado%29.md) (Cambiar el estado del crédito, incluye pre-rechazado)<br>*relacionada con:*<br>[HU-008](../../Historias%20De%20Usuario/2.%20KYC/HU-008%20Conocer%20el%20resultado%20en%20m%C3%A1ximo%2024%20horas.md)<br>[HU-044](../../Historias%20De%20Usuario/2.%20KYC/HU-044%20Decidir%20approved%20-%20pre-rejected.md) |
| **Estado en plataforma** | Implementado (cambio manual). El cambio automático post-KYC corresponde a [HU-044](../../Historias%20De%20Usuario/2.%20KYC/HU-044%20Decidir%20approved%20-%20pre-rejected.md) y a [CU-020](../2.%20KYC/CU-020%20Motor%20KYC%20automatico%20post-solicitud.md), cuyo Estado se actualizó: ya opera en lo esencial (no sigue "en desarrollo"; ver la ficha de CU-020 para el detalle). |
| **Referencias** | Fuente: ficha  [HU-041](../../Historias%20De%20Usuario/5.%20Operaci%C3%B3n%20admin/HU-041%20Cambiar%20el%20estado%20del%20cr%C3%A9dito%20%28incluye%20pre-rechazado%29.md)  — *Historias de Usuario — Fliipa*, carpeta "6. Gestión Plataforma del admin" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
