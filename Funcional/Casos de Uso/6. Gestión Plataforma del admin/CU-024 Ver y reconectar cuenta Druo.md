### CU-024: Ver y reconectar la cuenta Druo del cliente

![Diagrama de caso de uso CU-024](imagenes/diagrama_CU-024.svg)

> **Nota:** HU-040 no traía un número de CU asignado; se asigna el consecutivo **CU-024**.

| Campo | Detalle |
|:---:|:---:|
| **Actores** | Administrador / operaciones |
| **Descripción** | El administrador consulta el estado de la cuenta Druo (conexión bancaria) de un cliente y solicita la reconexión si hace falta, para desbloquear el onboarding o los cobros asociados. |
| **Precondiciones** | El cliente tiene o tuvo una cuenta bancaria conectada mediante Druo. |
| **Flujo principal** | 1. El administrador abre la ficha del cliente. 2. El sistema muestra el estado actual de la cuenta Druo. 3. Si la conexión está caída o vencida, el administrador inicia el proceso de conexión/reconexión. 4. El sistema ejecuta el proceso real con Druo y refleja el resultado obtenido. |
| **Flujos alternativos / excepciones** | A1. El proceso de reconexión falla: el sistema no simula un éxito falso; refleja el resultado real de Druo. |
| **Postcondiciones** | El administrador conoce el estado real de la cuenta Druo del cliente y, si aplicó, la reconexión queda reflejada según el resultado real del proceso. |
| **Reglas de negocio** | El resultado de la reconexión depende del proceso real con Druo; no debe simularse un éxito falso. |
| **Historias de usuario relacionadas** | HU-040 (Ver y reconectar la cuenta Druo del cliente); relacionada con HU-014 (débito automático, aún pendiente de punta a punta) |
| **Estado en plataforma** | Sin estado de implementación explícito registrado en la ficha de origen; requiere confirmación en código. |
| **Referencias** | Fuente: ficha HU-040 — *Historias de Usuario — Fliipa*, carpeta "6. Gestión Plataforma del admin" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
