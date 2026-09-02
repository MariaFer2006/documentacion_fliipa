### CU-021: Escalar casos a cobro jurídico

![Diagrama de caso de uso CU-021](imagenes/diagrama_CU-021.svg)



| Campo | Detalle |
|---|---|
| **Actores** | Analista jurídico / abogado; Sistema (Fliipa) |
| **Descripción** | *(Pendiente, no automático vigente hoy.)* Diseño previsto: los casos que alcancen el bucket de escalamiento jurídico se enrutarían automáticamente al analista jurídico, para iniciar el proceso de cobro legal sin depender de un traspaso manual. Este CU depende de los buckets de mora de CU-012, que hoy tampoco están implementados. |
| **Precondiciones** | (Diseño) Un caso de cartera alcanzaría el bucket de escalamiento jurídico definido en las reglas de gestión y escalamiento (ver [CU-012](CU-012 Gestionar y registrar cartera y cobranza.md), buckets pendientes). |
| **Flujo principal** | *(Flujo de diseño, no vigente hoy)* 1. El sistema identificaría que un caso alcanzó el bucket de escalamiento jurídico.<br>2. El sistema enrutaría automáticamente el caso al analista jurídico.<br>3. El analista jurídico recibiría el caso e iniciaría el proceso de cobro jurídico. |
| **Flujos alternativos / excepciones** | A1. (Diseño, no verificado en código) Si el caso saliera del bucket de escalamiento antes de ser tomado (por ejemplo, por un pago o alivio aplicado, ver [CU-013](CU-013 Recibir alivios ante dificultades de pago.md)), el enrutamiento automático no debería continuar. |
| **Postcondiciones** | El caso quedaría asignado al analista jurídico y se iniciaría el proceso de cobro legal correspondiente. Hoy no aplica: el CU está pendiente. |
| **Reglas de negocio** | El enrutamiento al analista jurídico debería ser automático, sin depender de un traspaso manual entre áreas; no exigible hoy porque el CU no está operativo. |
| **Historias de usuario relacionadas** | HU-027 (Recibir casos de escalamiento jurídico automáticamente) — *sin ficha propia en este repositorio; ver nota de organización arriba.* |
| **Estado en plataforma** | Sin respaldo en el código revisado, consistente con la ausencia general de lógica de buckets de mora (ver CU-012). Depende de resolver primero la discrepancia de plazos de escalamiento documentada en los requerimientos no funcionales (RNF-017). |
| **Referencias** | Fuente: ficha HU-027 (Recibir casos de escalamiento jurídico automáticamente) — *Historias de Usuario — Fliipa*, carpeta "4. Cobranza" (repositorio `documentacion_fliipa`, María Fernanda Herazo). **Hallazgo:** no existe un archivo HU-027 en este repositorio (a diferencia de HU-007/HU-008, que sí existen aunque vacíos); se recomienda crear la ficha faltante para cerrar la trazabilidad. |
