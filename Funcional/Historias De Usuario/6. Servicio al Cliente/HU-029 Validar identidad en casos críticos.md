#### HU-029: Validar identidad en casos críticos

| Campo | Detalle |
|:---:|:---:|
| **Actor** | Agente de servicio al cliente |
| **Historia** | Como agente de servicio al cliente, quiero validar la identidad del cliente antes de aprobar un caso crítico (suplantación, uso indebido del cupo), para evitar fraude. |
| **Prioridad** | Alta |
| **Criterios de aceptación** | Los casos críticos requieren un proceso obligatorio de validación de identidad mediante **dos filtros de verificación**, antes de que el agente brinde información al cliente o proceda con su solicitud. Si el cliente pasa al menos uno de los dos filtros, el agente continúa atendiendo el caso. Si no pasa ninguno de los dos, la cuenta del cliente se bloquea por **24 horas**. |
| **Relaciones** | Casos de uso: [CU-014](../../Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md). Requerimiento: [RF-029](../../Requerimientos/Requerimientos%20Funcionales.md). |
| **Referencias** |[Atención al cliente](../../../Operaciones/Procesos/06%20Servicio%20Cliente.md); |
 **Autor** | María Fernanda Herazo |
| **Fecha** | 18/08/2026 |
| **Versión** | V.1.8 |
| **Comentarios** | Sin código de respaldo encontrado; es consistente con la ausencia general de un módulo de servicio al cliente/IA en el repositorio. **Corrección v1.8 (Acta Check-in de Producto, 27/08/2026):** se reemplaza "aprobación manual explícita" por el mecanismo concreto acordado: dos filtros de verificación de identidad, con bloqueo de cuenta por 24 horas si el cliente no pasa ninguno. Queda pendiente crear el documento de definición de "casos críticos" (asignado a María Fernanda Herazo) al que hace referencia [CU-014](../../Casos%20de%20Uso/5.%20Servicio%20al%20Cliente/CU-014%20Atender%20al%20cliente%20por%20IA%20y%20escalar%20a%20agente%20humano.md). |