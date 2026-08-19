### CU-012: Gestionar y registrar cartera y cobranza

![Diagrama de caso de uso CU-012](imagenes/diagrama_CU-012.svg)

| Campo | Detalle |
|:---:|:---:|
| **Actores** | Analista de cartera; Comité de Cartera |
| **Descripción** | El analista de cartera consulta la cartera segmentada por bucket de mora, registra cada interacción de cobranza realizada, y el Comité de Cartera visualiza semanalmente un tablero con los casos priorizados. |
| **Precondiciones** | Existen créditos en distintos estados de mora dentro de la cartera. |
| **Flujo principal** | 1. El analista consulta la cartera agrupada en pago anticipado y buckets 1 a 5. 2. El analista prioriza su gestión de cobro diaria según esa segmentación. 3. El analista contacta al cliente y registra la interacción (canal, tipo de contacto, resultado, monto comprometido). 4. El registro queda disponible en el resumen de atención del cliente. 5. Semanalmente, el Comité de Cartera visualiza el tablero de casos priorizados (días de mora, flujo de caja, cuota vencida, historial y monto adeudado) para decidir alivios o escalamiento jurídico. |
| **Flujos alternativos / excepciones** | A1. El caso alcanza el bucket de escalamiento legal: se enruta automáticamente al analista jurídico (ver CU-021). |
| **Postcondiciones** | La cartera queda segmentada y priorizada, cada interacción de cobranza queda registrada y trazable, y el Comité de Cartera cuenta con información consolidada para decidir. |
| **Reglas de negocio** | Toda interacción de cobranza debe registrar canal, tipo de contacto, resultado y compromiso de pago. |
| **Historias de usuario relacionadas** | HU-024 (Ver cartera segmentada por bucket de mora), HU-025 (Registrar cada interacción de cobranza), HU-026 (Tablero semanal de priorización del Comité de Cartera) |
| **Estado en plataforma** | El registro de interacciones de cobranza está completamente implementado (`collection-notes.ts`, incluyendo resumen de atención). La segmentación por bucket de mora y el tablero de priorización **no** se encontraron en el código revisado; el motor de reglas existente (`rules-engine`) está enfocado en preaprobación, no en cobranza. |
| **Referencias** | Fuente: fichas HU-024, HU-025 y HU-026 — *Historias de Usuario — Fliipa*, carpeta "4. Cobranza" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
