### CU-013: Recibir alivios ante dificultades de pago

![Diagrama de caso de uso CU-013](imagenes/diagrama_CU-013.svg)

| Campo | Detalle |
|:---:|:---:|
| **Actores** | Cliente empresarial; Comité de Cartera |
| **Descripción** | El cliente accede a alivios (abono parcial, congelamiento de intereses o condonación) cuando tiene dificultades temporales de pago, según las condiciones y topes definidos por bucket de mora, y estas decisiones se apoyan en el tablero semanal del Comité de Cartera (ver CU-012). |
| **Precondiciones** | El cliente presenta mora o dificultades temporales de pago, ubicadas dentro de un bucket con alivio definido. |
| **Flujo principal** | 1. El cliente manifiesta dificultades de pago o el sistema identifica su situación de mora. 2. El sistema (o el Comité de Cartera) evalúa las condiciones y topes definidos para el bucket de mora del cliente. 3. Se aplica el alivio correspondiente: abono parcial, congelamiento de intereses o condonación. 4. El cliente conserva su cupo y su historial. |
| **Flujos alternativos / excepciones** | A1. El cliente no cumple las condiciones del bucket para ningún alivio: el caso continúa el flujo estándar de cobranza (ver CU-012) o escala a jurídico (ver CU-021). |
| **Postcondiciones** | El cliente recibe el alivio aplicable sin perder su cupo ni su historial de crédito. |
| **Reglas de negocio** | Los alivios (abono parcial, congelamiento de intereses, condonación) están sujetos a condiciones y topes definidos por bucket de mora. |
| **Historias de usuario relacionadas** | HU-015 (Recibir alivios ante dificultades de pago), HU-026 (Tablero semanal de priorización del Comité de Cartera) |
| **Estado en plataforma** | No se encontró ningún módulo de alivios, condonación ni lógica de "bucket de mora" en el código revisado. Funcionalidad aparentemente no implementada en el código fuente entregado, o soportada por un sistema externo/manual; se recomienda confirmar con negocio. |
| **Referencias** | Fuente: fichas HU-015 y HU-026 — *Historias de Usuario — Fliipa*, carpeta "4. Cobranza" (repositorio `documentacion_fliipa`, María Fernanda Herazo). |
