### CU-009: Consultar cupo, plan de pagos y disponibilidad de crédito

![Diagrama de caso de uso CU-009](imagenes/diagrama_CU-009.svg)

| Campo | Detalle |
|---|---|
| **Actores** | Cliente empresarial |
| **Descripción** | El cliente accede al portal para consultar su cupo disponible y el código de compra. Si el estado de la línea de crédito no permite el ingreso, el cliente simplemente no entra al portal. |
| **Precondiciones** | El cliente cuenta con una línea de crédito registrada en la plataforma. |
| **Flujo principal** | 1. El cliente ingresa al portal de usuarios.<br>2. El sistema valida el estado de la línea de crédito del cliente.<br>3. Si el estado es Aprobado o Activa, el sistema muestra el cupo disponible y el código de compra. |
| **Flujos alternativos / excepciones** | A1. La solicitud fue rechazada, no existe oferta disponible o no hay un crédito con el que el cliente pueda continuar: el cliente simplemente no entra al portal; el mensaje claro de no disponibilidad de crédito se muestra en el embudo de solicitud (ver [HU-011](../../Historias De Usuario/3. Credito/HU-011 Ver mensaje de no disponibilidad de cr�dito.md)), no como una pantalla del portal. |
| **Postcondiciones** | El cliente conoce su cupo disponible y su código de compra, si su estado le permite entrar al portal. |
| **Reglas de negocio** | El ingreso al portal (y con él, la consulta de cupo y código de compra) solo se habilita si la línea de crédito está en estado Aprobado o Activa. Estar en blacklist no es, por sí solo, la condición que dispara el mensaje de no disponibilidad en el flujo vigente. |
| **Historias de usuario relacionadas** | [HU-010](../../Historias De Usuario/3. Credito/HU-010 Consultar cupo, plan de pagos y movimientos.md) (Consultar cupo, plan de pagos y movimientos)<br>[HU-011](../../Historias De Usuario/3. Credito/HU-011 Ver mensaje de no disponibilidad de cr�dito.md) (Ver mensaje de no disponibilidad de crédito) |
| **Estado en plataforma** | Los endpoints de estado de crédito y desembolsos existen y delegan en el core bancario. Se confirmó el mensaje de no disponibilidad; pendiente confirmar línea por línea la restricción exacta de estados en la capa de autenticación de `fliipa-redemption`. |
| **Referencias** | Fuente: fichas [HU-010](../../Historias De Usuario/3. Credito/HU-010 Consultar cupo, plan de pagos y movimientos.md) y [HU-011](../../Historias De Usuario/3. Credito/HU-011 Ver mensaje de no disponibilidad de cr�dito.md) — *Historias de Usuario — Fliipa*, carpeta "3. Credito" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
