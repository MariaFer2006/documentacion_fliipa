### CU-002: Consultar y ver cupo preaprobado

![Diagrama de caso de uso CU-002](imagenes/diagrama_CU-002.svg)

| Campo | Detalle |
|:---:|:---:|
| **Actores** | Cliente empresarial |
| **Descripción** | El cliente ingresa su número de documento para saber si tiene un cupo preaprobado y, de tenerlo, consulta el valor de dicho cupo antes de completar el formulario de solicitud. |
| **Precondiciones** | Existe un archivo o base de clientes preaprobados cargada y procesada por el motor de riesgo. |
| **Flujo principal** | 1. El cliente ingresa su tipo y número de documento. 2. El sistema consulta si existe una preaprobación asociada al documento. 3. El sistema informa al cliente si puede continuar con el proceso. 4. Si existe preaprobación, el sistema muestra el valor del cupo preaprobado o sugerido. 5. El cliente decide si continúa con el resto del formulario de solicitud. |
| **Flujos alternativos / excepciones** | A1. El documento no tiene preaprobación asociada: el sistema informa al cliente que no puede continuar por esta vía (ver CU-009, mensaje de no disponibilidad). |
| **Postcondiciones** | El cliente conoce si cuenta con preaprobación y, si aplica, el valor de su cupo, antes de invertir tiempo en completar todo el formulario. |
| **Reglas de negocio** | El valor mostrado corresponde al cupo disponible según la información de preaprobación cargada y procesada por la plataforma. La consulta debe resolverse antes de exigir el formulario completo. |
| **Historias de usuario relacionadas** | HU-001 (Recibir enlace único), HU-002 (Consultar si tengo cupo preaprobado), HU-003 (Ver cupo preaprobado antes de completar el formulario) |
| **Estado en plataforma** | Implementado y operativo en el motor de riesgo (`b2b-base-preapproval.ts`, `get-suggested-credit.ts`). |
| **Referencias** | Fuente: fichas HU-001, HU-002 y HU-003 — *Historias de Usuario — Fliipa*, carpeta "1. Onboarding" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
