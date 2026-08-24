### CU-005: Revisar manualmente casos de biometría en revisión

![Diagrama de caso de uso CU-005](imagenes/diagrama_CU-005.svg)



| Campo | Detalle |
|---|---|
| **Actores** | Analista de riesgo |
| **Descripción** | El analista de riesgo revisaría manualmente los casos de biometría marcados "en revisión" para decidir si el cliente puede continuar el proceso de solicitud. |
| **Precondiciones** | (Diseño) Existiría al menos un caso con resultado biométrico "en revisión" (ver CU-004, hoy pendiente/no disponible). |
| **Flujo principal** | 1. El analista consultaría el listado de casos "en revisión".<br>2. El analista revisaría la información biométrica del caso.<br>3. El analista registraría su decisión: continuar o rechazar.<br>4. El sistema actualizaría el estado de la solicitud según la decisión registrada. |
| **Flujos alternativos / excepciones** | A1. (Diseño, no verificado en código) Si el analista no contara con información suficiente, podría dejar el caso pendiente hasta obtener más contexto. |
| **Postcondiciones** | (Diseño) El caso biométrico dejaría de estar "en revisión" y quedaría con una decisión explícita (continuar o rechazar). Hoy no aplica: no existe el estado "en revisión" en la plataforma. |
| **Reglas de negocio** | (Diseño) Todo caso "en revisión" requeriría una decisión manual explícita del analista antes de continuar el flujo del cliente. No exigible hoy porque el CU no está operativo. |
| **Historias de usuario relacionadas** | [HU-022](../../Historias%20De%20Usuario/2.%20KYC/HU-022%20Revisi%C3%B3n%20Biometria.md) (Resolver manualmente casos de biometría en revisión) (Resolver manualmente casos de biometría en revisión) |
| **Estado en plataforma** | No se encontró en el código ningún estado de "en revisión" para biometría, ni cola o pantalla de revisión manual (búsqueda de "en_revision", "manual_review", "under_review" sin coincidencias). Sin respaldo verificable en el código fuente entregado. |
| **Referencias** | Fuente: ficha [HU-022](../../Historias%20De%20Usuario/2.%20KYC/HU-022%20Revisi%C3%B3n%20Biometria.md) (Resolver manualmente casos de biometría en revisión) — *Historias de Usuario — Fliipa*, carpeta "2. KYC" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
