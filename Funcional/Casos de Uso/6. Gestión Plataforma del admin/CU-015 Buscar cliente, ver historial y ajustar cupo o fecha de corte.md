### CU-015: Buscar cliente, ver historial auditado y ajustar cupo o fecha de corte

![Diagrama de caso de uso CU-015](imagenes/diagrama_CU-015.svg)

| Campo | Detalle |
|---|---|
| **Actores** | Administrador del producto |
| **Descripción** | El administrador busca un cliente por documento, consulta su historial completo de operaciones auditadas y, cuando negocio lo autoriza, ajusta el cupo o la fecha de corte de su línea de crédito para corregir casos excepcionales. |
| **Precondiciones** | El cliente existe en la plataforma y tiene operaciones registradas. |
| **Flujo principal** | 1. El administrador busca al cliente por número de documento.<br>2. El sistema muestra hasta 500 registros de auditoría del cliente (línea de crédito, desembolsos, pagos).<br>3. Si negocio autorizó un ajuste excepcional, el administrador modifica el cupo o el día de corte de la línea de crédito.<br>4. El sistema valida que el día de corte esté en el rango de 1 a<br>31. 5. El sistema registra la acción en auditoría. |
| **Flujos alternativos / excepciones** | A1. El día de corte ingresado está fuera del rango 1–31: el sistema rechaza el ajuste. |
| **Postcondiciones** | El administrador cuenta con el historial auditado del cliente y, si aplicó, el cupo o la fecha de corte quedan ajustados y registrados en auditoría. |
| **Reglas de negocio** | El día de corte debe estar dentro del rango válido de 1 a 31 (para negocio: admin y portal). Toda modificación de cupo o fecha de corte queda registrada en auditoría. |
| **Historias de usuario relacionadas** | HU-031 (Buscar cliente y ver historial auditado)<br>HU-032 (Ajustar cupo o fecha de corte) |
| **Estado en plataforma** | Implementado (`clients.controller.ts` — `getClientAuditedOperations`; `credit-lines.controller.ts`). Hallazgo técnico: a nivel interno, la API de administración aún admite el valor `0` para el día de corte, mientras que redemption exige 1–31; para negocio el rango válido es 1–31. |
| **Referencias** | Fuente: fichas HU-031 y HU-032 — *Historias de Usuario — Fliipa*, carpeta "6. Gestión Plataforma del admin" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
