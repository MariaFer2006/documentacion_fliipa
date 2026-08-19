### CU-004: Completar validación biométrica

![Diagrama de caso de uso CU-004](imagenes/diagrama_CU-004.svg)

| Campo | Detalle |
|---|---|
| **Actores** | Cliente empresarial |
| **Descripción** | El cliente completa el proceso de biometría con el proveedor externo definido, desde cualquier dispositivo disponible, para verificar su identidad sin acudir a una oficina física. |
| **Precondiciones** | El cliente ya validó su identidad mediante OTP (CU-003). |
| **Flujo principal** | 1. El sistema presenta al cliente el paso de validación biométrica.<br>2. El cliente completa el proceso de biometría con el proveedor externo, desde el dispositivo disponible (celular, computador u otro).<br>3. El proveedor externo procesa la validación.<br>4. El sistema registra el resultado (aprobado, rechazado o en revisión) asociado a la solicitud. |
| **Flujos alternativos / excepciones** | A1. El resultado queda "en revisión": el caso pasa a revisión manual del analista de riesgo (ver CU-005). |
| **Postcondiciones** | La solicitud del cliente queda con un resultado biométrico (aprobado, rechazado o en revisión) registrado. |
| **Reglas de negocio** | El proceso no debe limitarse a un flujo exclusivamente móvil; el cliente puede usar cualquier dispositivo disponible. |
| **Historias de usuario relacionadas** | HU-006 (Completar la validación biométrica) |
| **Estado en plataforma** | No se encontró en el repositorio revisado lógica de biometría ni integración con proveedor externo (se buscó "biometr*" y "Olimpia" en todo `b2b/`, sin resultados). Pendiente confirmar si vive en un microservicio no incluido en este repositorio. |
| **Referencias** | Fuente: ficha HU-006 — *Historias de Usuario — Fliipa*, carpeta "2. KYC" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
