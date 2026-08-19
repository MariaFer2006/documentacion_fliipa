### CU-023: Registrar cada contacto con el cliente

![Diagrama de caso de uso CU-023](imagenes/diagrama_CU-023.svg)

> **Nota:** HU-030 no traía un número de CU asignado; se asigna el consecutivo **CU-023**.

| Campo | Detalle |
|---|---|
| **Actores** | Agente de servicio al cliente; Sistema (Fliipa) |
| **Descripción** | Cada contacto que se tiene con el cliente, sin importar el canal (WhatsApp, correo, llamada, asistente virtual o agente humano) o el motivo (KYC, biometría, atención, cobranza), queda registrado para mantener trazabilidad completa de toda la atención brindada. |
| **Precondiciones** | Se produce un contacto con el cliente por cualquier canal soportado. |
| **Flujo principal** | 1. Se produce un contacto con el cliente (por WhatsApp, correo, llamada, asistente virtual o agente humano).<br>2. El sistema o el agente registra canal, motivo, resultado y fecha del contacto.<br>3. El registro queda disponible en el historial general de atención del cliente, independientemente de si el contacto está o no relacionado con cobranza. |
| **Flujos alternativos / excepciones** | A1. El contacto es de cobranza: además de este registro general, se guarda en el módulo específico de notas de cobranza (ver [CU-012](CU-012%20Gestionar%20y%20registrar%20cartera%20y%20cobranza.md)).. |
| **Postcondiciones** | El cliente cuenta con un historial de atención completo y trazable, sin importar el canal o el motivo del contacto. |
| **Reglas de negocio** | El registro debe cubrir todos los canales y motivos de contacto, no solo la gestión de cobranza. |
| **Historias de usuario relacionadas** | HU-030 ([HU-030](../../Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-030%20Registrar%20cada%20contacto%20con%20el%20cliente.md)) (Registrar cada contacto con el cliente)<br>*relacionada con:*<br>[HU-006](../../Historias%20De%20Usuario/2.%20KYC/HU-006%20Completar%20la%20validaci%C3%B3n%20biom%C3%A9trica%20(KYC).md)<br>[HU-007](../../Historias%20De%20Usuario/2.%20KYC/HU-007%20Cargar%20soportes%20bancarios.md)<br>[HU-016](../../Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-016%20Atencion%20inicial%20por%20asistente%20virtual%20con%20IA.md)<br>[HU-017](../../Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-017%20Escalar%20a%20agente%20humano%20cuando%20la%20IA%20no%20resuelve%20el%20caso.md)<br>[HU-025](../../Historias%20De%20Usuario/4.%20Cobranza/HU-025%20Registrar%20cada%20interacci%C3%B3n%20de%20cobranza.md)<br>[HU-028](../../Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-028%20Recibir%20el%20caso%20escalado%20con%20contexto%20completo.md)<br>[HU-029](../../Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-029%20Validar%20identidad%20en%20casos%20cr%C3%ADticos.md)|
| **Estado en plataforma** | Ya existe un registro de notas de cobranza (`collection-notes.ts`, ver HU-025), pero no se encontró un registro general de contacto que cubra todos los flujos (KYC, biometría, atención por IA, atención humana, etc.). Pendiente de verificar en código. |
| **Referencias** | Fuente: ficha ([HU-030](../../Historias%20De%20Usuario/6.%20Servicio%20al%20Cliente/HU-030%20Registrar%20cada%20contacto%20con%20el%20cliente.md))— *Historias de Usuario — Fliipa*, carpeta "5. Servicio al Cliente" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
