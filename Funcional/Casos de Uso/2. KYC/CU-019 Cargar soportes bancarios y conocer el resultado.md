### CU-019: Cargar soportes bancarios y conocer el resultado

![Diagrama de caso de uso CU-019](imagenes/diagrama_CU-019.svg)

| Campo | Detalle |
|---|---|
| **Actores** | Cliente empresarial (carga); Administrador / operaciones (consulta) |
| **Descripción** | El cliente carga sus soportes bancarios (certificación y extractos) como parte del proceso de KYC, conoce el resultado de su solicitud en un plazo máximo definido, y el equipo de operaciones puede consultar y abrir esos soportes desde el panel administrativo. |
| **Precondiciones** | El cliente validó su identidad (CU-003) y, según el flujo, completó o está completando la validación biométrica (CU-004). |
| **Flujo principal** | 1. El cliente carga la certificación bancaria y los extractos (2 PDFs) en la plataforma.<br>2. El sistema confirma de inmediato la recepción y procesa la carga en segundo plano.<br>3. El cliente recibe el resultado de su solicitud dentro del plazo máximo definido (24 horas).<br>4. Desde el panel administrativo, el equipo de operaciones (con permiso) consulta si hay certificación y extractos cargados para el cliente y abre cada PDF. |
| **Flujos alternativos / excepciones** | A1. Falta alguno de los soportes: el panel administrativo lo indica explícitamente.<br>A2. El usuario del panel no tiene permiso: no puede ver los soportes. |
| **Postcondiciones** | Los soportes bancarios del cliente quedan cargados y disponibles para consulta en el panel, y el cliente conoce el resultado de su solicitud dentro del SLA definido. |
| **Reglas de negocio** | El SLA de resultado de la solicitud es de máximo 24 horas. Solo usuarios con permiso pueden ver los soportes bancarios en el panel. |
| **Historias de usuario relacionadas** | HU-007 (Cargar soportes bancarios)<br>HU-008 (Conocer el resultado en máximo 24 horas)<br>HU-037 (Ver y abrir soportes bancarios en el panel) |
| **Estado en plataforma** | HU-037 (consulta en panel): implementado (hecho). HU-007 (carga de soportes): implementado, según referencia `b2b/fliipa-back/src/controllers/clients/upload-document.ts`; el cliente carga certificación bancaria y extractos como dos PDF, y el sistema procesa el almacenamiento en segundo plano sin bloquear el flujo. HU-008 (SLA de resultado en 24 horas): la evaluación se apoya en el microservicio `evaluations` (Experian, Reconocer), pero no se encontró en el código un job o temporizador que garantice ese SLA de forma automática; parece ser un compromiso operativo, no una regla codificada. La numeración CU-019 (en vez de CU-006, que HU-008 declara en su ficha de origen) se mantiene porque CU-006 ya corresponde en este catálogo a un flujo de un actor distinto (Analista de riesgo, no Cliente empresarial); no se mezclaron por falta de contenido en HU-007 u HU-008. |
| **Referencias** | Fuente: fichas HU-007, HU-008 y HU-037 — *Historias de Usuario — Fliipa*, carpeta "2. KYC" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
