#### HU-028: Recibir el caso escalado con contexto completo

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero recibir el caso escalado por la IA con el contexto completo de la conversación, para no pedirle al cliente que repita su problema. |
| **Prioridad** | Baja|
| **Criterios de aceptación** | Cuando la IA escala un caso, el agente humano ve el historial completo de la conversación antes de responder. |
| **Relaciones** | Casos de uso: [CU-014](../../Casos de Uso/5. Servicio al Cliente/CU-014 Atender al cliente por IA y escalar a agente humano.md). Requerimiento: [RF-028](../../Requerimientos/Requerimientos Funcionales.md). Historia relacionada: [HU-017](../6. Servicio al Cliente/HU-017 Escalar a agente humano cuando la IA no resuelve el caso.md).  |
| **Referencias** | [Atención al cliente](../../../Operaciones/Procesos/06 Servicio Cliente.md); |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | Se confirma la separación entre el flujo de atención por IA (HU-016) y el de escalamiento/gestión humana (esta historia y HU-017): son procesos distintos y deben documentarse por separado. Confirmado (ver HU-016/HU-017): no existe módulo de IA conversacional ni de escalamiento en el código de `communications` ni en ningún otro servicio revisado. |
