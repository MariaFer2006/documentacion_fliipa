#### HU-028: Recibir el caso escalado con contexto completo

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero recibir el caso escalado por la IA con el contexto completo de la conversación, para no pedirle al cliente que repita su problema. |
| **Prioridad** | Baja|
| **Criterios de aceptación** | Cuando la IA escala un caso, el agente humano ve el historial completo de la conversación antes de responder. |
| **Relaciones** | Casos de uso: [CU-014](../../Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atenci%C3%B3n%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md). Requerimiento: [RF-028](../../Requerimientos/Requerimientos%20Funcionales.md). Historia relacionada: [HU-017](../6.%20Servicio%20al%20Cliente/HU-017%20Escalar%20a%20agente%20humano%20cuando%20la%20IA%20no%20resuelve%20el%20caso.md).  |
| **Referencias** | [Atención al cliente](../../../Operaciones/Procesos/06%20Servicio%20Cliente.md); |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.7 |
| **Comentarios** | Se confirma la separación entre el flujo de atención por IA (HU-016) y el de escalamiento/gestión humana (esta historia y HU-017): son procesos distintos y deben documentarse por separado. Confirmado (ver HU-016/HU-017): no existe módulo de IA conversacional ni de escalamiento en el código de `communications` ni en ningún otro servicio revisado. |
