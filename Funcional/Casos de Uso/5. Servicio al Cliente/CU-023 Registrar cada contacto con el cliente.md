### CU-023: Registrar cada contacto con el cliente

![Diagrama de caso de uso CU-023](imagenes/diagrama_CU-023.svg)

> **Nota:** HU-030 no traía un número de CU asignado; se asigna el consecutivo **CU-023**.

| Campo | Detalle |
|---|---|
| **Actores** | Agente de servicio al cliente; Sistema (Fliipa) |
| **Descripción** | Cada contacto que se tiene con el cliente, sin importar el canal (WhatsApp, correo, llamada, asistente virtual o agente humano) o el motivo (KYC, biometría, atención, cobranza), queda registrado para mantener trazabilidad completa de toda la atención brindada. |
| **Precondiciones** | Se produce un contacto con el cliente por cualquier canal soportado. |
| **Flujo principal** | 1. Se produce un contacto con el cliente (por WhatsApp, correo, llamada, asistente virtual o agente humano).<br>2. El sistema o el agente registra canal, motivo, resultado y fecha del contacto.<br>3. El registro queda disponible en el historial general de atención del cliente, independientemente de si el contacto está o no relacionado con cobranza. |
| **Flujos alternativos / excepciones** | A1. El contacto es de cobranza: además de este registro general, se guarda en el módulo específico de notas de cobranza (ver [CU-012](../4. Cobranza/CU-012 Gestionar y registrar cartera y cobranza.md)).. |
| **Postcondiciones** | El cliente cuenta con un historial de atención completo y trazable, sin importar el canal o el motivo del contacto. |
| **Reglas de negocio** | El registro debe cubrir todos los canales y motivos de contacto, no solo la gestión de cobranza. |
| **Historias de usuario relacionadas** | HU-030 ([HU-030](../../Historias De Usuario/6. Servicio al Cliente/HU-030 Registrar cada contacto con el cliente.md)) (Registrar cada contacto con el cliente)<br>*relacionada con:*<br>[HU-006](../../Historias De Usuario/1. Onboarding/HU-006%20Completar%20la%20validaci%C3%B3n%20biom%C3%A9trica%20%28KYC%29.md)<br>[HU-007](../../Historias De Usuario/2. KYC/HU-007 Cargar soportes bancarios.md)<br>[HU-016](../../Historias De Usuario/6. Servicio al Cliente/HU-016 Atencion inicial por asistente virtual con IA.md)<br>[HU-017](../../Historias De Usuario/6. Servicio al Cliente/HU-017 Escalar a agente humano cuando la IA no resuelve el caso.md)<br>[HU-025](../../Historias De Usuario/4. Cobranza/HU-025 Registrar cada interacci�n de cobranza.md)<br>[HU-028](../../Historias De Usuario/6. Servicio al Cliente/HU-028 Recibir el caso escalado con contexto completo.md)<br>[HU-029](../../Historias De Usuario/6. Servicio al Cliente/HU-029 Validar identidad en casos cr�ticos.md)|
| **Estado en plataforma** | Ya existe un registro de notas de cobranza (`collection-notes.ts`, ver HU-025), pero no se encontró un registro general de contacto que cubra todos los flujos (KYC, biometría, atención por IA, atención humana, etc.). Pendiente de verificar en código. |
| **Referencias** | Fuente: ficha ([HU-030](../../Historias De Usuario/6. Servicio al Cliente/HU-030 Registrar cada contacto con el cliente.md))— *Historias de Usuario — Fliipa*, carpeta "5. Servicio al Cliente" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
