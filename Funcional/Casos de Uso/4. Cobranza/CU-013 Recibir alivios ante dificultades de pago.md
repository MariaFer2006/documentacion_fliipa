### CU-013: Recibir alivios ante dificultades de pago

![Diagrama de caso de uso CU-013](imagenes/diagrama_CU-013.svg)

| Campo | Detalle |
|---|---|
| **Actores** | Cliente empresarial; Comité de Cartera |
| **Descripción** |  El cliente accedería a alivios (abono parcial, congelamiento de intereses o condonación) cuando tiene dificultades temporales de pago, según las condiciones y topes definidos por bucket de mora, apoyado en el tablero semanal del Comité de Cartera (ver [CU-012](CU-012 Gestionar y registrar cartera y cobranza.md), también sin buckets/tablero implementados hoy). |
| **Precondiciones** | (Diseño) El cliente presentaría mora o dificultades temporales de pago, ubicadas dentro de un bucket con alivio definido. |
| **Flujo principal** |  1. El cliente manifestaría dificultades de pago o el sistema identificaría su situación de mora.<br>2. El Comité de Cartera evaluaría las condiciones y topes definidos para el bucket de mora del cliente.<br>3. Se aplicaría el alivio correspondiente: abono parcial, congelamiento de intereses o condonación.<br>4. El cliente conservaría su cupo y su historial. |
| **Flujos alternativos / excepciones** | A1.Si el cliente no cumpliera las condiciones del bucket para ningún alivio, el caso continuaría el flujo estándar de cobranza (ver [CU-012](CU-012 Gestionar y registrar cartera y cobranza.md)) o escalaría a jurídico (ver [CU-021](CU-021 Escalar casos a cobro juridico.md)). |
| **Postcondiciones** | El cliente recibiría el alivio aplicable sin perder su cupo ni su historial de crédito.  |
| **Reglas de negocio** |  Los alivios (abono parcial, congelamiento de intereses, condonación) estarían sujetos a condiciones y topes definidos por bucket de mora. |
| **Historias de usuario relacionadas** |[HU-015](../../Historias De Usuario/4. Cobranza/HU-015 Recibir alivios ante dificultades de pago.md) (Recibir alivios ante dificultades de pago) |
| **Estado en plataforma** | No se encontró ningún módulo de alivios, condonación ni lógica de "bucket de mora" en el código revisado. Funcionalidad aparentemente no implementada en el código fuente entregado, o soportada por un sistema externo/manual; se recomienda confirmar con negocio. |
| **Referencias** | Fuente: ficha [HU-015](../../Historias De Usuario/4. Cobranza/HU-015 Recibir alivios ante dificultades de pago.md) — *Historias de Usuario — Fliipa*, carpeta "4. Cobranza" (repositorio `documentacion_fliipa`, María Fernanda Herazo). El tablero semanal del Comité de Cartera (HU-026) corresponde a [CU-012](CU-012 Gestionar y registrar cartera y cobranza.md), no a este CU. |
