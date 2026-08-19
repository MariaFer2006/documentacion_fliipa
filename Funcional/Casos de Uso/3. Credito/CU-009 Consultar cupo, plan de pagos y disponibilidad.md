### CU-009: Consultar cupo, plan de pagos y disponibilidad de crédito

![Diagrama de caso de uso CU-009](imagenes/diagrama_CU-009.svg)

| Campo | Detalle |
|---|---|
| **Actores** | Cliente empresarial |
| **Descripción** | El cliente accede al portal para consultar su cupo disponible, su plan de pagos y sus movimientos, o para recibir un mensaje claro cuando no tiene ninguna opción de crédito disponible. |
| **Precondiciones** | El cliente cuenta con una línea de crédito registrada en la plataforma. |
| **Flujo principal** | 1. El cliente ingresa al portal de usuarios.<br>2. El sistema valida el estado de la línea de crédito del cliente.<br>3. Si el estado es Aprobado o Activa, el sistema muestra cupo disponible, plan de pagos y movimientos. |
| **Flujos alternativos / excepciones** | A1. La solicitud fue rechazada, no existe oferta disponible o no hay un crédito con el que el cliente pueda continuar: el portal muestra un mensaje claro de que actualmente no hay opciones de crédito disponibles, en lugar de un error o pantalla vacía. |
| **Postcondiciones** | El cliente conoce su situación de crédito actual: su cupo y movimientos, o la razón por la que no puede continuar. |
| **Reglas de negocio** | La consulta de cupo, plan de pagos y movimientos solo se habilita si la línea de crédito está en estado Aprobado o Activa. Estar en blacklist no es, por sí solo, la condición que dispara el mensaje de no disponibilidad en el flujo vigente. |
| **Historias de usuario relacionadas** | HU-010 (Consultar cupo, plan de pagos y movimientos)<br>HU-011 (Ver mensaje de no disponibilidad de crédito) |
| **Estado en plataforma** | Los endpoints de estado de crédito y desembolsos existen y delegan en el core bancario. Se confirmó el mensaje de no disponibilidad; pendiente confirmar línea por línea la restricción exacta de estados en la capa de autenticación de `fliipa-redemption`. |
| **Referencias** | Fuente: fichas HU-010 y HU-011 — *Historias de Usuario — Fliipa*, carpeta "3. Credito" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
